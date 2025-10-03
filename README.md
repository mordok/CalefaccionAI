# CalefaccionIA

Automatización avanzada para calefacción eficiente en Home Assistant con bomba de calor Saunier Duval GeniaAir 8kW, integración solar Fronius, Forecast.Solar y gestión inteligente por zonas. 

## Características

- Priorización de zonas por demanda y energía solar disponible.
- Precalentamiento predictivo según predicción solar y temperatura exterior.
- Protección anti-frío nocturna y automatización de apagado inteligente.
- Optimización de la curva climática según el COP real.
- Integración con sensores virtuales y físicos, notificaciones Telegram y dashboards Lovelace personalizados.

## Instalación

1. Copia la carpeta `packages/CalefaccionIA` dentro de tu directorio `/config/packages/` de Home Assistant.
2. Añade la siguiente línea en tu `configuration.yaml` principal (si no existe):

   ```yaml
   homeassistant:
     packages: !include_dir_named packages/
   ```

3. Reinicia Home Assistant.
4. Ajusta los parámetros de zonas y sensores a tu instalación.

## Estructura del package

- `inputs.yaml`: Parámetros ajustables (temperaturas, modos, horarios, etc.)
- `sensors.yaml`: Sensores template, integración solar, eficiencia, estados.
- `binary_sensors.yaml`: Sensores binarios (activación, demanda, hora pico, etc.)
- `automations.yaml`: Automatizaciones principales (activación solar, precalentamiento, apagado, etc.)
- `scripts.yaml`: Scripts de gestión de zonas y lógica avanzada.
- `dashboard.md`: Ejemplo de dashboard Lovelace.

## Requisitos

- Home Assistant, integración con Fronius, Forecast.Solar, sensores de temperatura y consumo compatibles.
- Entidades y nombres de sensores adaptados a tu instalación.
- Telegram configurado para notificaciones (opcional).

---

> Sugerencia: Personaliza las entidades y parámetros para tu vivienda antes de usar en producción.