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
```

📘 Ver Guía Completa de Instalación

⚙️ Configuración
Modos de Funcionamiento
ModoDescripciónAuto Solar InteligenteGestión automática completa ⭐Manual CompletoControl manual de termostatosSolo EmergenciaSolo protección anti-fríoMantenimientoSistema pausadoVacacionesModo ahorro máximo
Prioridades de Zonas

🏆 Sala (21°C)
🚿 Baños (22°C)
🛏️ Dormitorio (20°C)
🍳 Cocina (19°C)
🚪 Entrada (18°C)
🛋️ Habitación pequeña (19°C)


📖 Documentación

📘 Instalación Completa
⚙️ Configuración Avanzada
🔧 Troubleshooting
📊 Valores COP
📝 Changelog


💡 Estructura del Proyecto
CalefaccionAI/
├── packages/CalefaccionIA/
│   ├── inputs.yaml          # Configuración usuario
│   ├── sensors.yaml         # Sensores template
│   ├── binary_sensors.yaml  # Estados binarios
│   ├── automations.yaml     # Automatizaciones
│   ├── scripts.yaml         # Scripts modulares
│   └── dashboard.md         # Dashboard Lovelace
├── docs/                    # Documentación
├── secrets.yaml.example     # Plantilla secretos
└── README.md               # Este archivo

🤝 Contribuir
¡Las contribuciones son bienvenidas!

Fork el proyecto
Crea tu rama (git checkout -b feature/MejoraCOP)
Commit cambios (git commit -m 'feat: Mejora cálculo COP')
Push (git push origin feature/MejoraCOP)
Abre un Pull Request


📊 Estadísticas

Automatizaciones: 7 principales
Scripts: 12 modulares
Sensores: 25+
Zonas: 6 con priorización
Ahorro estimado: 40-60%


📄 Licencia
MIT License - ver LICENSE

🙏 Agradecimientos

Comunidad Home Assistant
Saunier Duval API MiCasa
Fronius Solar API
Forecast.Solar


Hecho con ❤️ en Manacor, Mallorca | Última actualización: 2025-10-04
