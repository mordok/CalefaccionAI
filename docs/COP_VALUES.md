# 📊 Tabla de Valores COP - GeniaAir 8kW

## ¿Qué es el COP?

**COP** (Coefficient of Performance) = Coeficiente de Rendimiento

Es la relación entre la **energía térmica producida** y la **energía eléctrica consumida**.
COP = Energía Térmica Generada / Energía Eléctrica Consumida

**Ejemplo**: COP = 4.0 significa:
- Por cada 1 kWh de electricidad consumida
- Se generan 4 kWh de calor
- **Eficiencia**: 400%

---

## Tabla COP Saunier Duval GeniaAir 8kW

### COP Base según Temperatura Exterior

| Temperatura Exterior | COP Base | Potencia Térmica @ 2000W eléctricos |
|---------------------|----------|-------------------------------------|
| ≥ 20°C              | 5.2      | 10,400 W (10.4 kW)                 |
| 15 - 20°C           | 4.8      | 9,600 W (9.6 kW)                   |
| 10 - 15°C           | 4.2      | 8,400 W (8.4 kW)                   |
| 7 - 10°C            | 3.8      | 7,600 W (7.6 kW)                   |
| 2 - 7°C             | 3.2      | 6,400 W (6.4 kW)                   |
| -7 - 2°C            | 2.6      | 5,200 W (5.2 kW)                   |
| < -7°C              | 2.1      | 4,200 W (4.2 kW)                   |

**Fuente**: Ficha técnica Saunier Duval GeniaAir + mediciones reales

---

## Factores que Afectan al COP

### 1. Temperatura de Impulsión (Agua)

| Temp Impulsión | Factor Corrección | COP Real si base=4.0 |
|----------------|-------------------|----------------------|
| < 40°C         | 1.00              | 4.0                  |
| 40 - 45°C      | 0.95              | 3.8                  |
| > 45°C         | 0.90              | 3.6                  |

**Recomendación**: Mantener curva climática ≤ 0.5 para máxima eficiencia

### 2. Ciclos ON/OFF

- **Funcionamiento continuo**: COP óptimo
- **Ciclos cortos frecuentes**: -10% a -15% COP
- **Arranque en frío**: -20% durante primeros 10 min

### 3. Desescarchado (Defrost)

Cuando temp exterior < 5°C y humedad alta:
- Ciclos defrost cada 45-90 min
- Duración: 5-10 min
- Impacto: -5% a -10% COP medio

---

## Cálculo COP en CalefaccionAI
```yaml
sensor:
  - platform: template
    sensors:
      geniaair_cop_real:
        value_template: >
          {% set temp_exterior = state_attr('weather.forecast_casa', 'temperature') | float(20) %}
          {% set temp_impulsion = states('sensor.micasa_circuit_0_current_flow_temperature') | float(22) %}
          
          {# COP base según temperatura exterior #}
          {% if temp_exterior >= 20 %}
            {% set cop_base = 5.2 %}
          {% elif temp_exterior >= 15 %}
            {% set cop_base = 4.8 %}
          {% elif temp_exterior >= 10 %}
            {% set cop_base = 4.2 %}
          {% elif temp_exterior >= 7 %}
            {% set cop_base = 3.8 %}
          {% elif temp_exterior >= 2 %}
            {% set cop_base = 3.2 %}
          {% elif temp_exterior >= -7 %}
            {% set cop_base = 2.6 %}
          {% else %}
            {% set cop_base = 2.1 %}
          {% endif %}
          
          {# Factor corrección por temperatura impulsión #}
          {% if temp_impulsion > 45 %}
            {% set factor = 0.90 %}
          {% elif temp_impulsion > 40 %}
            {% set factor = 0.95 %}
          {% else %}
            {% set factor = 1.0 %}
          {% endif %}
          
          {{ (cop_base * factor) | round(2) }}
```
## Optimización del COP
✅ Para Maximizar COP

1. Temperatura impulsión baja

- Usar curva climática 0.3 - 0.5
- Evitar >45°C


2. Evitar ciclos cortos

- Funcionamiento continuo preferible
- Usar inercia térmica (acumulación)


3. Aprovechar temperaturas altas

- Precalentamiento cuando >15°C exterior
- Acumulación máxima cuando >20°C


4. Mantener circulación

- Bombas circulación siempre activas
- Evitar estancamiento agua



## ⚠️ Cuándo NO usar aerotermia
|     Condición   |  COP       |         Recomendación               |
|-----------------|------------|-------------------------------------|
| Exterior < -5°C |  < 2.5     |   Considerar apoyo eléctrico        |
| Impulsión > 50°C| < 2.0      |   Reducir demanda o cambiar sistema |
| Sin aislamiento | Variable   |  Mejorar envolvente antes           |

Comparativa Eficiencia
Aerotermia vs Otros Sistemas (Manacor)
SistemaCOP / RendimientoCoste por kWh térmicoEmisiones CO₂Aerotermia (COP 4.0)400%0.038 €⭐⭐⭐⭐⭐ BajoCaldera gas condensación95%0.084 €⭐⭐ MedioRadiador eléctrico100%0.153 €⭐ AltoCaldera gasoil85%0.095 €⭐ Muy alto
Ahorro aerotermia vs eléctrico directo: ~75%

Ejemplos Reales 
Escenario 1: Día Soleado (Febrero)

Temp exterior: 18°C
COP real: 4.7

ReintentarEsta respuesta se pausó porque Claude alcanzó la longitud máxima del mensaje. Presiona continuar para que Claude siga.Continuar
