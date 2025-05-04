# DeepRL para Planificación en Acuicultura con MaskablePPO

Este repositorio contiene la implementación de un entorno personalizado de acuicultura, junto con un agente de *Deep Reinforcement Learning* entrenado mediante el algoritmo **Maskable PPO** (Stable-Baselines3 + sb3-contrib). El objetivo es aprender una política óptima de planificación de siembras de peces en jaulas flotantes, maximizando el beneficio económico bajo condiciones ambientales variables.

---

## Estructura del repositorio

```
RL-Acuicultura/
├── PPO_TFM.ipynb             # Notebook principal con entorno, entrenamiento y evaluación
├── temperatures.csv          # Dataset de temperaturas semanales del mar
├── sale_prices.csv           # Dataset de precios de venta del pescado 
├── feed_rates.csv            # Tabla técnica de tasas de crecimiento, alimentación y mortalidad del alimento utilizado
├── feed_prices.csv           # Dataset de precios semanales del alimento
├── modelo_ppo_masked.zip     # Modelo entrenado  
├── README.md                 # Este archivo
└── requirements.txt          # Librerías necesarias
```

---

## Objetivo del proyecto

Aprender una política óptima para decidir **cuántas semanas sembrar un lote de peces** dadas condiciones como:

- Semana del año
- Temperatura del agua
- Precios futuros del pescado
- Costes del alimento

El entorno está formulado como un problema de planificación secuencial con horizonte variable. Se emplea una red neuronal entrenada mediante *Proximal Policy Optimization* (PPO) con enmascaramiento de acciones inválidas.

---

## Algoritmo utilizado

- `MaskablePPO` (versión extendida de PPO que evita acciones inválidas)
- Implementación basada en `sb3-contrib` y `stable-baselines3`
- Optimización bayesiana de hiperparámetros usando `Optuna`

---

## Requisitos

Instala los siguientes paquetes en un entorno virtual:

```bash
pip install -r requirements.txt
```

**Contenido de `requirements.txt`:**

```
pandas
numpy
matplotlib
gymnasium
optuna
stable-baselines3
sb3-contrib
```

---

## Entrenamiento

Puedes entrenar el modelo desde cero ejecutando las celdas del notebook:

Acuicultura_RL.ipynb

Durante el entrenamiento:
- Se optimizan los hiperparámetros con `Optuna`
- Se entrena el agente PPO en un entorno vectorizado
- Se registran las recompensas y acciones por episodio

El modelo entrenado se guarda como `modelo_ppo_masked.zip`.

---

## Evaluación y simulación

Después de entrenar el modelo, puedes:

### 1. **Evaluar el agente**
Ejecutar el agente en modo determinista sobre todas las semanas iniciales del año, definiendo el horizonte de planificación que consideres.

### 2. **Visualizar las políticas**
Se genera un heatmap de decisiones por semana:

- Eje Y: semana de inicio del año (1–52)
- Eje X: pasos del episodio
- Color: duración del lote sembrado

### 3. **Simular el ciclo productivo completo**
Cada lote se simula semana a semana para visualizar:

- Peso del pez
- Población
- Alimento usado
- Costes e ingresos
- Recompensa por lote

Los resultados se exportan a `simulacion_modelo.csv` y se grafican automáticamente.

## Notas importantes

- El entorno utiliza enmascaramiento de acciones para asegurar la validez de las decisiones.
- La observación incluye codificación temporal, temperaturas futuras y precios proyectados.
- Se puede ajustar la duración del entrenamiento, episodios o el rango de semanas fácilmente.

## Autor

Proyecto desarrollado por **Pelayo González Fernández** como parte del Trabajo Fin de Máster (TFM) 2024-2025.

Máster en Ciencia de Datos.

Universidad de Cantabria

Supervisores: Manuel Luna García y Rodrigo García Manzanas 
