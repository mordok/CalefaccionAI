📋 PRÓXIMOS PASOS PARA IMPLEMENTAR:
PASO 1: COPIAR EL CÓDIGO 📝
Copia TODO el código del artefacto y:
Opción A - Archivo único:
bash# Pega todo en configuration.yaml
# Reinicia Home Assistant

Opción B - Archivos separados (RECOMENDADO):
yaml# En configuration.yaml añade:
sensor: !include sensors.yaml
automation: !include automations.yaml
script: !include scripts.yaml
input_number: !include input_numbers.yaml
input_select: !include input_selects.yaml
input_datetime: !include input_datetimes.yaml
input_boolean: !include input_booleans.yaml
binary_sensor: !include binary_sensors.yaml
Luego crea los archivos correspondientes con las secciones del código.

PASO 2: VERIFICAR ENTIDADES ✅
Antes de reiniciar, verifica que existen estas entidades en tu HA:
CRÍTICAS (deben existir):
yaml# Aerotermia
sensor.circuito_2  ✓
switch.contactor_caldera  ✓

# Termostatos
climate.temostatov_sala  ✓
climate.temostatov_banos  ✓
climate.termostato_dormitorio  ✓
climate.temostatov_cocina  ✓
climate.temostatov_entrada  ✓
climate.temostatov_hab_peq  ✓

# Fronius
sensor.solarnet_energia_fotovoltaica  ✓
sensor.solarnet_carga_de_energia_consumida  ✓

# Forecast.Solar
sensor.power_production_now  ✓
sensor.energy_production_today_remaining  ✓
sensor.power_highest_peak_time_today  ✓

# Met.no
weather.forecast_casa  ✓
Si alguna NO existe, busca en Herramientas Desarrollador → Estados el nombre correcto y cámbialo en el código.

PASO 3: AJUSTAR TEMPERATURAS BASE 🌡️
Personaliza según tus preferencias en la sección input_number:
yamltemp_base_sala: 21°C        # Tu preferencia sala
temp_base_banos: 22°C       # Baños más calientes
temp_base_dormitorio: 20°C  # Dormitorio más fresco
temp_base_cocina: 19°C      # Cocina uso puntual
temp_base_entrada: 18°C     # Entrada zona paso
temp_base_hab_peq: 19°C     # Habitación pequeña

# Inercia térmica
sobrecalentamiento_inercia_max: 2.5°C  # Cuánto sobrecalentar
horas_inercia_objetivo: 5h             # Horas autonomía objetivo

PASO 4: CONFIGURAR HORARIOS ⏰
Ajusta según tus costumbres:
yamlhora_precalentamiento_inicio: "08:30"  # Cuando empieza precalentar
hora_precalentamiento_fin: "14:30"     # Cuando termina ventana
Y en las automatizaciones:
yamlafter: "08:00:00"   # Hora mínima activar calefacción
before: "18:00:00"  # Hora máxima desactivar automático
after: "21:00:00"   # Inicio modo nocturno
before: "08:00:00"  # Fin modo nocturno

PASO 5: REINICIAR Y PROBAR 🚀

Verificar configuración:

Herramientas Desarrollador → Comprobar configuración
Si hay errores → Revisar línea indicada


Reiniciar Home Assistant
Verificar que se crearon las entidades:

yaml   sensor.exceso_solar_disponible
   sensor.geniaair_cop_real
   sensor.temperatura_sala_fiable
   binary_sensor.geniaair_activa
   binary_sensor.es_hora_pico_solar
   # etc...

Activar el sistema:

Ve a input_select.modo_calefaccion_solar
Selecciona: "Auto Solar Inteligente"







🚀 MEJORAS FUTURAS OPCIONALES:
Una vez funcione perfectamente, puedes añadir:
1. Integración con Precios PVPC (si cambias a tarifa indexada)
yaml# Añadir sensor precio eléctrico
# Evitar calefacción en horas pico precio
2. Control ACS Inteligente
yaml# Coordinar ACS con calefacción
# Priorizar uno según exceso solar
3. Machine Learning Avanzado
yaml# Predicción consumo basado en históricos
# Aprendizaje patrones uso familiar
# Optimización COP automática
4. Integración con Batería (si añades batería)
yaml# Usar batería para calefacción nocturna
# Cargar batería en hora pico solar

