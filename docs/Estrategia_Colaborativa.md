# 🤝 Estrategia de Colaboración – Proyecto EduIA

Este documento describe la estrategia de trabajo colaborativo entre **Uziel Isaí Luján López** y **Diego Paniagua Molina** para el desarrollo del proyecto *EduIA*.

---

## 🎯 Objetivo de la estrategia
Asegurar que **ambos integrantes** aprendan y trabajen en **texto e imágenes**, evitando una división rígida de módulos que limite el aprendizaje individual.

La idea central es avanzar **paralelo y por etapas**, trabajando juntos en cada componente.

---

## 🔹 Fases de trabajo

### **Fase 1: Texto (QA generativo)**
- **Uzi**: experimenta con **FLAN-T5-XL** → prompts, evaluación con BLEU/ROUGE.
- **Diego**: experimenta con **BLOOMZ-3B** → prompts, inferencia en español, evaluación.
- **Ambos**:
  - Documentar diferencias de desempeño.
  - Diseñar un *wrapper* común en `text_module/model.py` para soportar ambos modelos.
  - Integrar resultados en `integration/pipeline.py`.

✅ Resultado esperado: módulo de texto funcional con dos backends evaluados.

---

### **Fase 2: Imagen**
- **Uzi**: enfoque en **programmatic** (Graphviz, Matplotlib).
- **Diego**: enfoque en **Stable Diffusion** (prompt → ilustración).
- **Ambos**:
  - Definir reglas de decisión para seleccionar el tipo de visualización.
  - Integrar ambos enfoques en `image_module/`.

✅ Resultado esperado: módulo de imagen híbrido y flexible.

---

### **Fase 3: Integración y Web**
- Ambos colaboran directamente en:
  - `integration/pipeline.py` → Ensamblaje del flujo texto + imagen.
  - `web_app/app.py` → Interfaz web (Gradio/Streamlit).
- Tareas divididas dinámicamente (uno en backend, otro en frontend).

✅ Resultado esperado: demo funcional con interfaz amigable.

---

## 🔹 Colaboración en GitHub
- Se trabajará con **ramas por tarea/experimento** en lugar de por módulo.  
Ejemplos de ramas:
  - `texto/flan-t5-uziel`
  - `texto/bloomz-diego`
  - `imagenes/stable-diffusion-diego`
  - `imagenes/programmatic-uziel`

- Una vez validado un experimento, se hará **merge a main** mediante *pull request*, revisado por ambos.

---

## ✅ Beneficios
- Ambos integrantes dominarán texto e imágenes.
- El código tendrá validación doble (dos implementaciones comparadas).
- Se asegura aprendizaje balanceado y colaboración real.
