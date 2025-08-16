# Plan “EduIA” – Educador Multimodal Inteligente Académico

## 🎯 Objetivo

Desarrollar un sistema que reciba texto como pregunta y devuelva:

- **Explicación generativa en español.**
- **Imagen de apoyo visual** (diagrama, gráfico o ilustración simple).

Todo tratando de usar modelos open source y técnicas aprendidas en el curso.

---

## 1️⃣ Arquitectura general

```
Pregunta → Preprocesamiento → Modelo de texto (QA generativo)
       ↘                           ↙
        Generador de imagen (Stable Diffusion / programático)
                    ↓
       Respuesta final (texto + imagen)
```

---

## 2️⃣ Componentes y tecnologías

### Módulo de Texto

- **Base:** Experimentar con 2 modelos y evaluarlos, FLAN-T5-XL y BLOOMZ-3B (HuggingFace) – modelos multilingües con buen rendimiento en español.

- **Estrategia:**

    - Prompt engineering para forzarlos a devolver el formato: explicación clara + descripción breve y concreta de la sugerencia visual o imagen de apoyo.
    - Fine-tuning ligero opcional con dataset educativo en español (ej. adaptación de SQuAD-es o conjunto propio).
- **Framework:** Transformers de HuggingFace + PyTorch.

### Módulo de Imagen

- **Opción 1 (generativa):** Stable Diffusion ejecutado localmente con pesos open source, evitando el uso de servicios de pago → genera diagramas o ilustraciones simples según descripción.
- **Opción 2 (programática):** Matplotlib, NetworkX, Graphviz, o Mermaid → genera gráficos, diagramas de flujo, o esquemas automáticos a partir de datos estructurados.

- **Decisión dinámica:**
    - Si el tema es más abstracto (ej. “red neuronal”), usar Stable Diffusion.
    - Si es técnico-matemático, usar imagen programática.

---

## Integración

Script Python que:

1. Recibe pregunta.
2. Llama al modelo de texto para generar explicación y descripción de imagen.
3. Llama al generador de imágenes con esa descripción.
4. Devuelve ambos como respuesta integrada.

---

## 3️⃣ Flujo detallado

**1. Entrada:** Texto de pregunta.

**2. Preprocesamiento:**
    - Limpieza mínima (caracteres mal formateados).

**3. Modelo de texto:**

Prompt base:
```text
Responde a la siguiente pregunta de forma clara y detallada. Incluye también una breve descripción de un diagrama o imagen que ayudaría a entender la respuesta. Pregunta: {input}
```

**4. Postprocesamiento texto:**
- Separar la parte de explicación y la descripción de la imagen.

**5. Generación de imagen:**
- Stable Diffusion: usar descripción para crear ilustración.
- Programático: traducir descripción a código de diagrama.

**6. Salida combinada:**
- Mostrar explicación y renderizar imagen en interfaz web.




---

## 4️⃣ Extras para impresionar

- Explicaciones paso a paso: forzar modelo a numerar pasos.
- Interfaz web: Gradio o Streamlit para que cualquiera pruebe el prototipo.
- Métrica de evaluación: BLEU/ROUGE para medir calidad textual y un score de similaridad CLIP para evaluar relevancia imagen–texto.

---

## 5️⃣ Recursos recomendados

- HuggingFace Transformers para modelos NLP.
- Diffusers para Stable Diffusion local.
- Matplotlib / Graphviz para diagramas programáticos.
- **Datasets:**
- SQuAD-es, MLQA-es para QA.
- Colecciones propias para ejemplos visuales.



## 📡 Estrategia de Ejecución en Clúster – Flujo “Batch” Académico

Dado que el clúster Lab-SB (CIMAT) no está diseñado para servir interfaces web en tiempo real, el flujo de ejecución de *EduIA* se adaptará a un esquema **batch**. Esto permite aprovechar la potencia del supercómputo para generar todas las salidas (texto + imágenes) de forma masiva y luego presentarlas localmente simulando tiempo real.

### 🔹 Descripción del flujo

1. **Preparación local**
   - Descargar y almacenar modelos, tokenizers y datasets de HuggingFace en local.
   - Transferir al clúster mediante SFTP (`scp` o Bitvise) siguiendo la estructura:
     ```
     /EduIA/
     ├── models/         # Modelos locales (FLAN-T5-XL, BLOOMZ-3B)
     ├── data/           # Preguntas y prompts
     └── scripts/        # Código fuente + .sh de lanzamiento
     ```
   
2. **Ejecución en el clúster (SLURM)**
   - Usar scripts `.sh` con configuración de SLURM para lanzar la generación en modo batch.
   - Los scripts recibirán como entrada:
     - Ruta del modelo base.
     - Archivo de preguntas.
     - Directorio de salida.
   - El clúster procesará todas las preguntas, generando:
     - `resultados.json` → texto explicativo y descripción visual.
     - Carpeta `imagenes/` → imágenes generadas (Stable Diffusion o programáticas).
   
3. **Postprocesamiento y transferencia**
   - Descargar resultados (`resultados.json` + `imagenes/`) a la máquina local.
   - Guardar en `/EduIA/results/` para que la interfaz web pueda acceder a ellos.

4. **Visualización local**
   - La interfaz web (Gradio o Streamlit) leerá los resultados pre-generados y los mostrará como si fueran respuestas en tiempo real.
   - Posible opción de “reprocesar” una pregunta enviándola a una cola batch en el clúster para ejecución posterior.

### 🔹 Ventajas del enfoque
- Aprovecha el clúster para la parte más costosa: generación de texto e imagen.
- Evita latencias y cuellos de botella propios del tiempo real.
- Mantiene el carácter académico y reproducible del proyecto.
- Permite demos fluidas sin depender de la conexión al HPC.

### 🔹 Notas importantes
- Los modelos y datasets deben subirse completos al clúster (no hay internet en nodos de cómputo).
- La carpeta `logs/` será clave para depuración y trazabilidad de resultados.
- Mantener scripts `.sh` en la raíz del proyecto para simplificar rutas.
