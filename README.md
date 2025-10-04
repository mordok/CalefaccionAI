# 🏠 CalefaccionAI - Sistema Inteligente de Climatización Solar

[![Home Assistant](https://img.shields.io/badge/Home%20Assistant-2024.1+-41BDF5.svg?style=flat-square&logo=homeassistant)](https://www.home-assistant.io/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Maintenance](https://img.shields.io/badge/Maintained%3F-yes-green.svg)](https://github.com/mordok/CalefaccionAI/graphs/commit-activity)

> Sistema de gestión inteligente para aerotermia Saunier Duval GeniaAir 8kW con optimización solar fotovoltaica y control predictivo por zonas.

---

## ✨ Características Principales

🌞 **Gestión Solar Inteligente**
- Integración Fronius para monitorización en tiempo real
- Predicciones solares con Forecast.Solar
- Acumulación térmica durante picos solares
- 5 niveles de optimización según energía disponible

🏠 **Control Multi-Zona (6 Zonas)**
- Priorización inteligente por importancia
- Sensores redundantes para máxima fiabilidad
- Gestión de inercia térmica para uso nocturno
- Ajuste dinámico según condiciones

📊 **Monitorización Avanzada**
- Cálculo COP real basado en temperatura exterior
- Métricas económicas: ahorro diario y eficiencia
- Medición consumo real con LEGRAND EMDX³
- Históricos de 90 días para análisis

🤖 **Automatizaciones**
- Activación solar inteligente
- Precalentamiento predictivo matinal
- Acumulación máxima en hora pico
- Control reactivo anti-exportación
- Protección nocturna anti-frío

---

## 📦 Requisitos

### Hardware
- Aerotermia Saunier Duval GeniaAir 8kW
- Inversor solar Fronius con API
- Medidor LEGRAND EMDX³ (Modbus TCP)
- Gateway Saunier Duval MiLink
- Mínimo 6 sensores temperatura

### Software
- Home Assistant 2024.1+
- Integraciones: `saunierduval`, `fronius`, `forecast_solar`, `met`, `modbus`, `telegram_bot`

---

## 🚀 Instalación Rápida
```bash
# 1. Clonar repositorio
cd /config
git clone https://github.com/mordok/CalefaccionAI.git

# 2. Configurar secretos
cd CalefaccionAI
cp secrets.yaml.example secrets.yaml
nano secrets.yaml

# 3. Copiar package
cp -r packages/CalefaccionIA /config/packages/

# 4. Añadir a configuration.yaml
homeassistant:
  packages: !include_dir_named packages/

# 5. Reiniciar Home Assistant
