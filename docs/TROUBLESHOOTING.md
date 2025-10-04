# 🔧 Guía de Solución de Problemas

## Problemas Comunes

### ❌ GeniaAir no se enciende automáticamente

**Síntomas**: La aerotermia no arranca aunque hay exceso solar.

**Verificaciones**:

1. **Comprobar modo sistema**
   - Ir a: Configuración → Helpers
   - Buscar: `input_select.modo_calefaccion_solar`
   - Debe estar en: **"Auto Solar Inteligente"**

2. **Verificar exceso solar**
   - Sensor: `sensor.potencia_disponible_calefaccion`
   - Debe ser: **> 1500W**

3. **Comprobar demanda**
   - Al menos 1 termostato debe estar en modo **'heat'**
   - Sensor: `sensor.zonas_demandando_calor` >= 1

4. **Verificar switch contactor**
   - Probar manualmente: `switch.contactor_caldera`
   - Si no funciona: problema cableado físico

**Solución**:
- Si falla el switch → revisar cableado contactor
- Si no hay demanda → activar manualmente un termostato
- Si no hay exceso → esperar mejor producción solar

---

### ❌ Sensores de temperatura muestran "unknown"

**Causas posibles**:
- Sensor sin batería
- Fuera de rango Zigbee/Z-Wave
- Sensor no emparejado correctamente

**Diagnóstico**:
1. Ir a **States** (Herramientas de desarrollo)
2. Buscar: `sensor.temperatura_sala_fiable`
3. Si muestra "unknown" → problema en sensor primario

**Solución**:
1. Reemplazar batería sensor
2. Añadir repetidor Zigbee/Z-Wave si está lejos
3. Re-emparejar sensor
4. ✅ El sistema usará sensor secundario automáticamente (fallback)

---

### ❌ Notificaciones Telegram no llegan

**Verificar configuración**:

1. **Revisar secrets.yaml**:
```yaml
   telegram_bot_api_key: "CORRECTO"
   telegram_chat_id: "CORRECTO"

Obtener chat_id correcto:

Abrir Telegram
Buscar: @userinfobot
Enviar: /start
Copiar el número que devuelve


Test manual:

yaml   service: notify.telegram_bot_7730409640_4634486477
   data:
     message: "Test CalefaccionAI"

⚠️ COP calculado parece incorrecto
Verificar datos entrada:
El sensor sensor.geniaair_cop_real depende de:

Temperatura exterior: weather.forecast_casa
Temperatura impulsión: sensor.micasa_circuit_0_current_flow_temperature

Valores esperados:
Temp ExteriorCOP Esperado20°C4.8 - 5.215°C4.2 - 4.810°C3.8 - 4.27°C3.2 - 3.82°C2.6 - 3.2
Si difiere mucho → consultar COP_VALUES.md

❌ Consumo excede exceso solar disponible
Síntoma:
sensor.geniaair_consumo_actual > sensor.potencia_disponible_calefaccion
Causas:

Demanda térmica mayor que energía disponible
Muchas zonas activas simultáneamente
Temperatura exterior muy baja (COP bajo)

Solución automática:
El sistema ejecuta automáticamente:
yamlAutomatización: ⚡ Control Reactivo Consumo LEGRAND
Script: reducir_demanda_termostatos_prioritario
Reduce zonas en orden: 6→5→4 (menos prioritarias primero)
Solución manual:

Reducir temperatura objetivo zonas no críticas
Desactivar zonas secundarias temporalmente
Aumentar input_number.margen_seguridad_solar


❌ Aerotermia se apaga inesperadamente
Verificar condiciones apagado:
Automatización: 🌙 Apagar GeniaAir Sin Solar Suficiente
Condiciones para apagar:

sensor.potencia_disponible_calefaccion < 1000W durante 10 min
Hora > 18:00
Todas las temperaturas > 18.5°C

Si NO debería apagarse:

Desactivar automatización temporalmente
Ajustar umbral potencia mínima
Activar: input_boolean.permitir_calefaccion_noche


⚠️ Protección anti-frío se activa mucho
Causa: Inercia térmica insuficiente durante el día.
Solución a largo plazo:

Aumentar sobrecalentamiento:

input_number.sobrecalentamiento_inercia_max
De 2.5°C → 3.0°C o 3.5°C


Ampliar objetivo inercia:

input_number.horas_inercia_objetivo
De 5h → 6h o 7h


Adelantar precalentamiento:

input_datetime.hora_precalentamiento_inicio
De 08:30 → 08:00


Mejorar aislamiento vivienda

Solución inmediata:
yamlActivar: input_boolean.permitir_calefaccion_noche = ON
⚠️ Esto consumirá energía de red eléctrica

Comandos de Diagnóstico
Ver estado completo sistema

Ir a: Herramientas de desarrollo → States
Filtrar por:

geniaair → Ver todos los sensores GeniaAir
exceso_solar → Ver energía disponible
zona → Ver estado termostatos



Ver por qué NO se ejecutó automatización

Ir a: Configuración → Automatizaciones
Buscar: 🌞 Activación Solar GeniaAir
Click en "Traza" (icono tres puntos)
Ver condiciones que fallaron

Probar scripts manualmente
En Herramientas de desarrollo → Servicios:
yaml# Activar precalentamiento manual
service: script.precalentamiento_inercia_6_zonas

# Acumulación máxima manual
service: script.acumulacion_maxima_inercia_6_zonas

# Modo emergencia
service: script.calentamiento_emergencia_zonas_criticas

Herramientas de Depuración
Template Tool
Herramientas de desarrollo → Template
Probar cálculos en vivo:
jinja2{{ states('sensor.exceso_solar_disponible') | float }}
{{ states('sensor.geniaair_cop_real') | float }}
{{ states('sensor.zonas_demandando_calor') | int }}

{# Test condición activación #}
{% set exceso = states('sensor.potencia_disponible_calefaccion') | float %}
{% set demanda = states('sensor.zonas_demandando_calor') | int %}
{{ exceso > 1500 and demanda >= 1 }}
Activar logs detallados
Editar configuration.yaml:
yamllogger:
  default: info
  logs:
    homeassistant.components.automation: debug
    homeassistant.components.script: debug
    homeassistant.components.template: debug
Luego reiniciar HA y ver: Configuración → Logs

Tabla de Diagnóstico Rápido
SíntomaCausa ProbableSoluciónNo enciende aerotermiaModo incorrecto / Sin demandaVerificar modo "Auto Solar" y termostatosSensor unknownBatería / Fuera rangoCambiar batería / Añadir repetidorTelegram no funcionaToken/ChatID incorrectosRevisar secrets.yamlCOP bajoTemperatura exterior bajaNormal, verificar tabla COPSe apaga rápidoPoco exceso solarAumentar sobrecalentamiento inerciaImporta mucho de redDemanda > Solar disponibleReducir zonas activas

Contacto Soporte
Si el problema persiste:

GitHub Issues: Crear issue
Incluir:

Versión Home Assistant
Logs relevantes (copiar desde UI)
Configuración (SIN secretos)
Descripción detallada paso a paso
