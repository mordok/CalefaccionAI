💡 CONSEJOS DE USO:
PRIMEROS DÍAS:

Deja que aprenda (3-5 días observando)
No cambies temperaturas base aún
Observa las notificaciones Telegram
Revisa el histórico cada día

AJUSTE FINO (después 1 semana):

Si hace frío por la noche → Sube sobrecalentamiento_inercia_max a 3°C
Si hace demasiado calor mediodía → Baja a 2°C
Si alguna zona siempre fría → Sube su temp_base_XXX
Si consume mucho de red → Sube margen_seguridad_solar a 500W

OPTIMIZACIÓN (después 1 mes):

Analiza sensor.geniaair_cop_medio_7_dias
Si COP <3.5 → Revisa curva climática
Si ahorro <70% → Ajusta horarios precalentamiento
Revisa sensores redundantes que más fallan


⚠️ POSIBLES PROBLEMAS Y SOLUCIONES:
PROBLEMA 1: "No se activa nunca"
yamlCausas:
- Modo no en "Auto Solar Inteligente"
- Exceso solar nunca >2000W
- Ningún termostato demanda calor

Solución:
- Verifica input_select.modo_calefaccion_solar
- Baja umbral a 1500W en automatización
- Verifica termostatos en modo "heat"
PROBLEMA 2: "Consume de red con sol"
yamlCausas:
- margen_seguridad_solar muy alto
- Cálculo exceso solar incorrecto
- Demanda de 6 zonas excede producción

Solución:
- Baja margen_seguridad_solar a 300W
- Verifica sensores Fronius
- Sistema reducirá zonas automáticamente
PROBLEMA 3: "Sensor temperatura 'unavailable'"
yamlCausas:
- Sensor primario caído
- Batería baja Fibaro

Solución:
- Sistema usa automáticamente sensor secundario
- Revisa sensores en HA
- Cambia batería si necesario
PROBLEMA 4: "No llegan notificaciones"
yamlCausas:
- Servicio Telegram mal configurado
- Bot sin permisos

Solución:
- Prueba manualmente: notify.telegram_bot_7730409640_4634486477
- Verifica configuración Telegram en HA
