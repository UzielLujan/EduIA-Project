 EduIA-Project/
 │
 ├── data/                     # Datos para entrenamiento y pruebas
 │   ├── raw/                  # Datos sin procesar
 │   ├── processed/            # Datos procesados y listos para uso
 │   └── prompts/              # Preguntas batch para ejecución en el clúster
 │
 ├── notebooks/                # Experimentos y análisis exploratorio
 │   ├── nlp_experiments.ipynb
 │   ├── image_experiments.ipynb
 │
 ├── src/                      # Código fuente principal
 │   ├── __init__.py
 │   ├── config.py              # Configuración general
 │   ├── main.py                # Script principal de ejecución
 │   ├── text_module/           # Lógica del módulo de texto
 │   │   ├── __init__.py
 │   │   ├── model.py
 │   │   ├── prompts.py
 │   │   └── utils.py
 │   ├── image_module/          # Lógica del módulo de imagen
 │   │   ├── __init__.py
 │   │   ├── stable_diffusion.py
 │   │   ├── programmatic.py
 │   │   └── utils.py
 │   ├── integration/           # Integración texto-imagen
 │   │   ├── __init__.py
 │   │   └── pipeline.py
 │   └── web_app/               # Interfaz web (Gradio/Streamlit)
 │       ├── __init__.py
 │       └── app.py
 │
 ├── models/                   # Modelos locales descargados (FLAN-T5, BLOOMZ, etc.)
 │   └── checkpoints/          # Checkpoints generados en entrenamiento/fine-tuning
 │
 ├── results/                  # Resultados generados en el clúster
 │   ├── outputs/              # Texto e imágenes generados (simulados en tiempo real)
 │   └── logs/                 # Logs de SLURM y del sistema
 │
 ├── hpc_scripts/              # Scripts auxiliares para HPC (descarga, preparación)
 │
 ├── tests/                    # Pruebas unitarias y de integración
 │   ├── test_text_module.py
 │   ├── test_image_module.py
 │   └── test_pipeline.py
 │
 ├── docs/                     # Documentación del proyecto
 │   ├── Plan_Proyecto_EduIA.md
 │   ├── Estructura_Carpetas.md
 │   ├── Stack_Tecnico.md
 │   └── README.md
 │
 ├── requirements.txt          # Dependencias del proyecto
 ├── README.md                 # Descripción general del repositorio
 ├── run_train.sh              # Script de entrenamiento para SLURM
 ├── run_inference.sh          # Script de inferencia batch para SLURM
 └── .gitignore                # Archivos/Carpetas a ignorar en Git
