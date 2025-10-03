```yaml
type: vertical-stack
title: "🏠 Sistema GeniaAir 8kW "
cards:
  - type: horizontal-stack
    cards:
      - type: entity
        entity: sensor.geniaair_estado_detallado
        name: "Estado GeniaAir"
      - type: entity
        entity: input_select.modo_calefaccion_solar
        name: "Modo Sistema"
      - type: entity
        entity: sensor.estado_sistema_optimo
        name: "Estado Óptimo"
  - type: horizontal-stack
    cards:
      - type: gauge
        entity: sensor.geniaair_consumo_actual
        name: "Consumo GeniaAir"
        unit: "W"
        min: 0
        max: 8000
        severity:
          green: 0
          yellow: 5000
          red: 7000
        needle: true
      - type: gauge
        entity: sensor.exceso_solar_disponible
        name: "Exceso Solar"
        unit: "W"
        min: 0
        max: 5000
        severity:
          red: 1000
          yellow: 2500
          green: 4000
        needle: true
      - type: gauge
        entity: sensor.geniaair_cop_real
        name: "COP Real"
        min: 2
        max: 5.5
        severity:
          red: 2.5
          yellow: 3.5
          green: 4.5
        needle: true
  - type: entities
    title: "💰 Eficiencia y Ahorro"
    entities:
      - entity: sensor.eficiencia_solar_actual
        name: "Eficiencia Solar"
        icon: mdi:solar-power
      - entity: sensor.ahorro_economico_hoy
        name: "Ahorro Hoy"
        icon: mdi:currency-eur
      - entity: sensor.geniaair_energia_consumida_hoy
        name: "Energía Consumida"
      - entity: sensor.geniaair_potencia_termica
        name: "Potencia Térmica"
  - type: entities
    title: "🌡️ Termostatos (Prioridad 1-6)"
    entities:
      - type: custom:fold-entity-row
        head:
          entity: climate.temostatov_sala
          name: "1️⃣ SALA (Prioritario)"
        entities:
          - sensor.temperatura_sala_fiable
          - input_number.temp_base_sala
      - type: custom:fold-entity-row
        head:
          entity: climate.temostatov_banos
          name: "2️⃣ BAÑOS"
        entities:
          - sensor.temperatura_bano_fibaro
          - input_number.temp_base_banos
      - type: custom:fold-entity-row
        head:
          entity: climate.termostato_dormitorio
          name: "3️⃣ DORMITORIO (Físico)"
        entities:
          - sensor.temperatura_dormitorio_fiable
          - input_number.temp_base_dormitorio
      - climate.temostatov_cocina
      - climate.temostatov_entrada
      - climate.temostatov_hab_peq
  - type: entities
    title: "☀️ Predicciones Solares (Manacor)"
    entities:
      - sensor.power_production_now
      - sensor.prediccion_solar_proximas_6h
      - sensor.energy_production_today_remaining
      - sensor.power_highest_peak_time_today
      - sensor.indice_precalentamiento
      - binary_sensor.es_hora_pico_solar
  - type: horizontal-stack
    cards:
      - type: entity
        entity: sensor.zonas_demandando_calor
        name: "Zonas Activas"
      - type: entity
        entity: sensor.demanda_termica_total
        name: "Demanda Total"
      - type: entity
        entity: binary_sensor.demanda_calefaccion_general
        name: "Demanda General"
  - type: entities
    title: "⚙️ Configuración Inercia Térmica"
    entities:
      - input_number.sobrecalentamiento_inercia_max
      - input_number.horas_inercia_objetivo
      - input_datetime.hora_precalentamiento_inicio
      - input_datetime.hora_precalentamiento_fin
      - input_boolean.permitir_calefaccion_noche
  - type: history-graph
    title: "📈 Histórico 24 horas"
    entities:
      - entity: sensor.geniaair_consumo_actual
        name: "Consumo"
      - entity: sensor.exceso_solar_disponible
        name: "Exceso Solar"
      - entity: sensor.geniaair_cop_real
        name: "COP"
      - entity: sensor.temperatura_sala_fiable
        name: "Temp Sala"
    hours_to_show: 24
    refresh_interval: 60
```
