PROYECTO: ARQUITECTURAS AGÉNTICAS PARA TEXT & WEB ANALYTICS
============================================================

Este proyecto implementa una arquitectura de agentes utilizando la librería 'crewai' para realizar un análisis web y de texto con un flujo de trabajo secuencial. El sistema está diseñado para tomar una consulta de usuario, rastrear la web para encontrar productos, analizarlos bajo un criterio específico y generar un informe final de recomendaciones.

-----------------------------------------------------------
1. REQUISITOS E INSTALACIÓN
-----------------------------------------------------------

1.1. Instalación de Dependencias

Ejecuta los siguientes comandos en tu terminal para instalar las librerías y dependencias necesarias:

pip install -U crewai "crewai[tools]" crewai_tools litellm
pip install -U google-genai langchain-google-genai
pip install spacy
python -m spacy download es_core_news_sm
pip install tavily-python

1.2. Configuración de Variables de Entorno

El proyecto requiere el uso de modelos de lenguaje (Gemini) y una herramienta de búsqueda web (Tavily). Debes configurar las siguientes variables de entorno.

Crea un archivo llamado '.env' en la raíz del proyecto para almacenar tus claves de forma segura, o expórtalas directamente en tu entorno:

| VARIABLE | DESCRIPCIÓN |
| :--- | :--- |
| GEMINI_API_KEY | Clave de acceso a la API de Gemini (Google GenAI). |
| TAVILY_API_KEY | Clave para la herramienta de búsqueda web (Tavily). |

Ejemplo de archivo .env:

GEMINI_API_KEY="TU_CLAVE_DE_GEMINI_AQUI"
TAVILY_API_KEY="TU_CLAVE_DE_TAVILY_AQUI"

NOTA: Las claves deben cargarse al inicio de un script o configurarse directamente en la celda inicial del Jupyter Notebook.

-----------------------------------------------------------
2. ESTRUCTURA Y EJECUCIÓN DEL CÓDIGO
-----------------------------------------------------------

El proyecto se ejecuta a través del script principal contenido en el archivo 'Proyecto_Text_&_Web_Analytics.ipynb'.

2.1. Agentes y Flujo de Trabajo

El flujo de trabajo es SECUENCIAL y está compuesto por cuatro agentes especializados que se pasan el contexto de manera ordenada:

1.  Orquestador de Tareas: Divide la consulta del usuario en Keyword y Cualidad de análisis.
2.  Agente Rastreador Web: Usa la TAVILY_API_KEY para buscar productos basándose en la Keyword.
3.  Agente Analizador: Evalúa los resultados del rastreador y asigna un Score (0-100) basándose en la Cualidad solicitada (ej. precio, rendimiento).
4.  Generador del Informe Final: Sintetiza el análisis y presenta el TOP 3 de productos recomendados.

2.2. Ejecución

Para ejecutar el sistema, abre el archivo 'Proyecto_Text_&_Web_Analytics.ipynb' en un entorno Jupyter (o Google Colab) y EJECUTA LAS CELDAS EN ORDEN.

Asegúrate de:
* Haber configurado las variables de entorno correctamente.
* Definir la consulta de usuario en la celda donde se instancia y se invoca el método 'crew.kickoff()'.

2.3. Ejemplo de Ejecución con Consulta

La consulta de ejemplo para el Crew es:

------------------------------------------------------------------------------

inputs_para_crew = {
    "user_query": "busca una bocina resitente al agua marca JBL en Colombia"
}

------------------------------------------------------------------------------

El resultado final será el informe generado por el Generador del Informe Final impreso en la última celda de ejecución del Notebook.

Gemini puede cometer errores, así que verifica las respuestas.

