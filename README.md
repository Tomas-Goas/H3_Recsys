# Impacto del Dwell Time en Recomendación Secuencial  
**Autores:** Tomás Goas, Leopoldo Farr  
**Institución:** Pontificia Universidad Católica de Chile  

---

## Resumen del estudio

Este repositorio contiene los experimentos, modelos y código utilizados para analizar el **impacto del dwell time** en el rendimiento de distintos algoritmos de **recomendación secuencial**.

El *dwell time* se incorpora repitiendo un ítem dentro de la secuencia un número de veces proporcional al tiempo que el usuario lo visualiza. Esto convierte el interés del usuario en una señal explícita dentro del modelo, pero al mismo tiempo **alarga artificialmente las sesiones**, lo que incrementa los tiempos de entrenamiento y modifica la distribución de secuencias.

El estudio compara modelos **con** y **sin** dwell, evaluando cómo la arquitectura influye en su capacidad para aprovechar esta señal.

---

## 📊 Modelos evaluados

### **GRU4Rec**
Modelo recurrente basado en GRUs que captura dependencias de corto plazo a través de un estado oculto.  
El dwell actúa como una forma natural de refuerzo dentro de la dinámica recurrente.

### **BERT4Rec**
Transformer bidireccional entrenado mediante *masked item prediction*.  
La repetición producida por dwell introduce ruido contextual y degrada el rendimiento en forma consistente.

### **SASRec**
Modelo Transformer **causal/unidireccional**.  
Aprovecha la atención como BERT, pero sin romper la direccionalidad. El dwell se incorpora como una señal temporal válida.

### **NARM (Neural Attentive Session Model)**
Modelo híbrido que combina GRU + atención sobre el contexto.  
Es el que **más se beneficia** del dwell: la atención amplifica señales repetidas interpretándolas como evidencia explícita de interés.

---

## 📈 Principales resultados

- El dwell time **no es universalmente beneficioso**: depende fuertemente de la arquitectura.  
- Modelos **causales** (GRU4Rec, SASRec, NARM) mejoran significativamente.  
- Modelos **bidireccionales** (BERT4Rec) se degradan por ruido contextual.  
- **NARM** presenta las mejoras más grandes entre todos los modelos.  
- El dwell genera **sesiones más largas**, mayor costo computacional y diferencias en tiempos de entrenamiento.  
  - En noviembre, curiosamente, el entrenamiento **sin dwell fue ~20% más lento**, posiblemente por mayor variabilidad en longitudes, batching menos eficiente o mayor dispersión en las sesiones.

---

## ⚙️ Datasets

Los experimentos usan datasets públicos del proyecto **Open CDP (Rees46 Technologies)**, correspondientes a:

- Octubre 2019  
- Noviembre 2019  

Cada registro representa un evento asociado a un producto en un e-commerce multicategoría (views, cart, purchase).

