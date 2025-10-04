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
