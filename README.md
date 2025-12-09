# Impacto del Dwell Time en Recomendación Secuencial  
**Autores:** Tomás Goas, Leopoldo Farr  
**Institución:** Pontificia Universidad Católica de Chile  

---

## Descripción general

Este repositorio contiene el código, experimentos y modelos utilizados para evaluar el **impacto del dwell time** en sistemas de **recomendación secuencial**.  
El dwell time se incorpora repitiendo cada ítem un número de veces proporcional al tiempo que el usuario lo visualiza, convirtiendo una señal implícita en una señal explícita dentro de la secuencia.

El objetivo principal es comparar distintas arquitecturas **con y sin dwell**, analizando cómo cada una responde a esta modificación estructural en las sesiones.

---

## Estructura del repositorio

```
├── GRU4Rec/                # Código + modelos finales entrenados
├── NARM/                   # Código + modelos finales entrenados
├── SASRec/                 # Código + modelos finales entrenados
├── BERT4Rec/               # Código + modelos finales entrenados
├── NextItNet/              # Código + modelos finales entrenados
├── Resultados antiguos/    # Experimentos previos (opcional)
└── README.md               # Este archivo
```

**En cada carpeta con el nombre del modelo encontrarás los modelos finales ya entrenados** (estructurados para poder correrlos nuevamente), junto con los scripts de entrenamiento correspondientes.

---

## Modelos evaluados

- **GRU4Rec:** RNN basada en GRUs, captura dependencias de corto plazo.  
- **NARM:** GRU con un mecanismo de atención global; arquitectura especialmente sensible al refuerzo introducido por dwell.  
- **SASRec:** Modelo *self-attention* unidireccional (causal).  
- **BERT4Rec:** Transformer bidireccional entrenado con *masked item prediction*.  
- **NextItNet:** Arquitectura convolucional profunda basada en convoluciones dilatadas.

Cada modelo fue evaluado en dos variantes:  
**(1) sesiones originales** y **(2) sesiones extendidas mediante dwell time**.

---

## Resultados generales

- El efecto del dwell time depende fuertemente de la arquitectura.  
- Modelos **causales** como GRU4Rec, NARM y SASRec muestran mejoras significativas.  
- Modelos **bidireccionales** (BERT4Rec) ven degradado su rendimiento debido al ruido contextual introducido por la repetición.  
- **NARM** obtiene las mayores ganancias al utilizar dwell.  
- El dwell aumenta la longitud de las sesiones y, con ello, los tiempos de entrenamiento.  
- En pruebas sobre el dataset de noviembre, el entrenamiento **sin dwell** resultó ~20% más lento, probablemente asociado a mayor variabilidad de longitudes y menos eficiencia en batching.

---

## Datasets

Los experimentos utilizan datos públicos del proyecto **Open CDP (Rees46 Technologies)**:

- **Octubre 2019**  
- **Noviembre 2019**

Los eventos incluyen: *product views*, *cart additions* y *purchases*, junto con el tiempo exacto del evento, necesario para calcular dwell time.

---

## Reproducibilidad

Para **reproducir los experimentos de cada arquitectura**:

1. **Requisitos previos**  
   - Python 3.7+  
   - Instalar las dependencias indicadas en cada carpeta de modelo (es para casi todos lo mismo, porque siguen el mismo pipeline).

2. **Ejecuta los scripts desde la carpeta del modelo**  
   - Cada carpeta (`GRU4Rec/`, `NARM/`, `SASRec/`, `BERT4Rec/`, `NextItNet/`) contiene:
     - Scripts de entrenamiento y evaluación.
     - Modelos finales ya entrenados (listos para ser evaluados nuevamente).

   - Repita el proceso análogo en cada carpeta de modelo.

3. **Entrenamiento y evaluación**
   - Puedes entrenar desde cero usando los scripts de cada modelo, o evaluar directamente los modelos pre-entrenados.
   - Para evaluar variantes **con** o **sin** dwell time, selecciona el dataset o configuración correspondiente.
   - Para probar partes mas pequeñas del dataset que tomen menos tiempo, esta comentado "df_small" para usarlo.

4. **Notas**
   - Todos los modelos están organizados en carpetas separadas.
   - Los scripts son autónomos por carpeta: no es necesario moverse fuera del directorio del modelo para ejecutar los experimentos.
   - Ante dudas sobre la ejecución específica para un modelo, consulta el README adicional o script de ayuda de esa carpeta/modelo.

---

## Contacto y Créditos

- Tomás Goas - [tgoas@uc.cl](mailto:tgoas@uc.cl)
- Leopoldo Farr - [lfarr@uc.cl](mailto:lfarr@uc.cl)

---