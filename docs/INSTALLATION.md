# 📘 Guía de Instalación CalefaccionAI

## Requisitos Previos

### Hardware Necesario
- ✅ Aerotermia Saunier Duval GeniaAir 8kW (o compatible)
- ✅ Inversor solar Fronius con API habilitada
- ✅ Medidor LEGRAND EMDX³ con Modbus TCP
- ✅ Gateway Saunier Duval MiLink
- ✅ Contactor para control ON/OFF
- ✅ Mínimo 6 sensores de temperatura (Zigbee/Z-Wave)

### Software Necesario
- Home Assistant 2024.1 o superior
- Integraciones:
  - `saunierduval` (MiCasa Cloud)
  - `fronius` (Solar)
  - `forecast_solar`
  - `met` (Meteorología)
  - `modbus` (LEGRAND)
  - `telegram_bot`

## Instalación Paso a Paso

### 1. Clonar el Repositorio

Desde SSH en tu Home Assistant:
```bash
cd /config
git clone https://github.com/mordok/CalefaccionAI.git
```
### 2. Configurar Secretos
```bash
cd CalefaccionAI
cp secrets.yaml.example secrets.yaml
nano secrets.yaml
```
Rellenar con tus datos reales.

### 3. Configurar Packages

Editar tu `/config/configuration.yaml` principal:
```yamlhomeassistant:
packages: !include_dir_named packages/
```
### 4. Copiar Package
```bash
cp -r packages/CalefaccionIA /config/packages/
```
### 5. Ajustar Entidades

Editar `/config/packages/CalefaccionIA/inputs.yaml` con tus temperaturas preferidas.

### 6. Validar Configuración

Desde UI de Home Assistant:
- **Herramientas de desarrollo** → **Comprobar configuración**

O desde terminal:
```bash
hass --script check_config
```
### 7. Reiniciar Home Assistant

**Configuración** → **Sistema** → **Reiniciar**

### 8. Verificar

Después del reinicio, verifica que aparecen:
- Sensor `sensor.geniaair_cop_real`
- Sensor `sensor.exceso_solar_disponible`
- Automatización `🌞 Activación Solar GeniaAir`

## Configuración Inicial

### Ajustar Temperaturas Base

**Configuración** → **Helpers** → Buscar "Temperatura Base"

Zonas por prioridad:
1. Sala: 21°C
2. Baños: 22°C  
3. Dormitorio: 20°C
4. Cocina: 19°C
5. Entrada: 18°C
6. Habitación pequeña: 19°C

### Configurar Horarios

- **Inicio precalentamiento**: 08:30
- **Fin precalentamiento**: 14:30

### Calibrar Inercia

- **Sobrecalentamiento máximo**: 2.5°C (ajustar según aislamiento)
- **Horas inercia objetivo**: 5h

## Troubleshooting

### Error: "Entity not found"

**Causa**: Nombres de entidades diferentes.

**Solución**: Editar `secrets.yaml` con los nombres reales de tus sensores.

### GeniaAir no enciende

**Verificar**:
1. Switch `switch.contactor_caldera` funciona manualmente
2. Modo sistema: "Auto Solar Inteligente"
3. Hay demanda (algún termostato activo)
4. Hay exceso solar >1500W

### Notificaciones Telegram no funcionan

**Verificar**:
1. Bot creado en @BotFather
2. Chat ID correcto (usar @userinfobot)
3. Token correcto en `secrets.yaml`

## Próximos Pasos

- Consultar [CONFIGURATION.md](CONFIGURATION.md) para ajustes avanzados
- Ver [TROUBLESHOOTING.md](TROUBLESHOOTING.md) para problemas comunes
- Revisar [COP_VALUES.md](COP_VALUES.md) para entender cálculos
