# Changelog

Todos los cambios notables de este proyecto serán documentados aquí.

El formato está basado en [Keep a Changelog](https://keepachangelog.com/es-ES/1.0.0/),
y este proyecto adhiere a [Semantic Versioning](https://semver.org/lang/es/).

## [2.0.0] - 2025-10-04

### 🎉 Reestructuración Completa

#### Añadido
- Estructura modular profesional del repositorio
- Sistema de packages para Home Assistant
- Documentación completa en carpeta `docs/`
- Archivo `.gitignore` para proteger secretos
- Plantilla `secrets.yaml.example`
- Dashboard Lovelace personalizado
- GitHub Actions para validación automática
- Ejemplos de configuración
- Sistema de issues templates

#### Mejorado
- Separación lógica de componentes (sensors, automations, scripts)
- Documentación técnica detallada
- README con badges y estructura clara
- Gestión de versiones semánticas

#### Seguridad
- Protección de credenciales con `.gitignore`
- Plantilla de secretos sin datos sensibles

---

## [1.0.0] - 2025-01-XX

### 🚀 Versión Inicial

#### Añadido
- Sistema base de control aerotermia GeniaAir 8kW
- Integración Fronius solar
- Integración Forecast.Solar
- Control multi-zona (6 zonas)
- Priorización inteligente de zonas
- Cálculo COP real
- Automatizaciones principales:
  - Activación solar inteligente
  - Precalentamiento predictivo
  - Acumulación hora pico
  - Control reactivo consumo
  - Apagado nocturno
  - Protección anti-frío
- Scripts gestión zonas
- Sensores eficiencia y ahorro
- Notificaciones Telegram

#### Integraciones
- Saunier Duval MiCasa Cloud
- Fronius Solar WebAPI
- LEGRAND EMDX³ Modbus
- Met.no Weather
- Forecast.Solar

---

## Tipos de Cambios

- **Añadido**: Nueva funcionalidad
- **Mejorado**: Mejora de funcionalidad existente
- **Corregido**: Corrección de bugs
- **Eliminado**: Funcionalidad eliminada
- **Seguridad**: Vulnerabilidades corregidas
- **Deprecated**: Funcionalidad que será eliminada
