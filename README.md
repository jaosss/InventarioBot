# InventarioBot

**InventarioBot** es un chatbot interactivo para consola diseñado para gestionar y consultar inventarios de componentes electrónicos de forma rápida e inteligente. Utiliza la potencia del modelo de lenguaje de **Groq (`qwen/qwen3.8-27b`)** combinado con el análisis de datos de **Pandas** para ofrecer respuestas precisas sobre existencias, precios y estadísticas sin saturar los límites de la API.

##  Características principales

* **Consultas en lenguaje natural:** Pregúntale al bot de forma abierta sobre qué productos quedan, cuáles están agotados o qué componentes específicos necesitas.
* **Análisis de datos híbrido:** Integra **Pandas** en el backend para pre-procesar y responder de forma analítica e inmediata consultas complejas (como detectar el producto más caro, el más barato o artículos con stock crítico).
* **Manejo de streaming:** Respuestas fluidas en tiempo real directamente en la terminal a medida que el modelo las genera.
* **Consumo óptimo de Tokens:** Evita los errores de saturación de contexto (`Error 413 / 429`) gracias a una ventana de historial inteligente y a un filtro previo que solo envía a la API las filas relevantes del inventario.
* **Diseñado para tu negocio:** Mapeado específicamente para procesar las columnas exactas de tu archivo local `componentes_electronicos.cvs` (*ID Artículo, Categoría, Descripción, Precio Unitario, Existencias Actuales, Merma, Próximas Existencias y Estado*).

##  Requisitos del sistema

Antes de ejecutar el script, asegúrate de tener instalado Python 3.11 o superior y las siguientes dependencias:

1. **Instalación de Librerías:**
   Instala los paquetes necesarios ejecutando el siguiente comando en tu terminal:
   ```bash
   pip install pandas gradio groq
   ```

2. **Clave de la API de Groq:**
   Debes contar con una clave de API válida de Groq configurada en tu entorno o inicializada correctamente en tu cliente de Python (`cliente = Groq(api_key="TU_API_KEY")`).

3. **Archivo de Inventario:**
   El programa requiere un archivo llamado obligatoriamente `componentes_electronicos.cvs` ubicado en la misma carpeta raíz del script. Este archivo debe respetar la siguiente estructura de columnas:
   ```text
   ID Artículo,Categoría,Descripción,Precio Unitario (\$),Existencias Actuales,Merma (Unidades),Próximas Existencias (En camino),Estado
   ```

##  Instrucciones

1. **Preparar el entorno:** Coloca el script de Python y tu archivo `componentes_electronicos.cvs` en el mismo directorio.
2. **Ejecutar el programa:** Abre tu terminal y ejecuta el script con el comando:
   ```bash
   python nombre_de_tu_archivo.py
   ```
3. **Interactuar con el Bot:** El programa abrirá un ciclo continuo en la consola donde podrás realizar consultas directamente en lenguaje natural.

### Preguntas que puedes realizar:
* *¿Cuál es el producto más caro del inventario?*
* *¿Qué artículos tienen menos stock o están en estado crítico?*
* *¿Cuántos productos distintos hay registrados en total?*
* *¿Qué componentes vienen en camino o tienen próximas existencias?*
* *¿Tienes resistencias o capacitores disponibles?*

4. **Pare cerrar el programa:** Para salir del chat y terminar el ciclo, escribe la palabra `terminar`.

# Guía para generar un Token de API en Groq

Para poder utilizar los modelos de lenguaje de Groq en tus aplicaciones o scripts, necesitas generar una clave de API (**API Key**). Sigue estos sencillos pasos:

## Pasos para obtener tu API Key

1. **Inicia sesión o regístrate:**
   * Ve al sitio web oficial de [Groq Console](https://groq.com).
   * Introduce tus credenciales o crea una cuenta nueva si aún no la tienes.

2. **Accede a la sección de API Keys:**
   * En el menú lateral izquierdo, busca y haz clic en la opción **"API Keys"**.

3. **Crea una nueva clave:**
   * Haz clic en el botón que dice **"Create API Key"** (Crear clave de API).
   * *(Opcional)* Asigna un nombre a tu clave para identificarla fácilmente (por ejemplo, *'Proyecto-Test'*).

4. **Guarda tu Token:**
   * Se abrirá una ventana emergente mostrando tu nueva clave.
   * **Copia la clave inmediatamente** haciendo clic en el botón de copiar.
   * *Nota: Por motivos de seguridad, no podrás volver a ver esta clave una vez que cierres la ventana.*

## ⚠️ Recomendaciones de Seguridad

* **No compartas tu clave:** Nunca subas tu API Key a repositorios públicos como GitHub.
* **Usa variables de entorno:** Es una buena práctica guardar tu token en un archivo `.env` de la siguiente manera:
  ```env
  GROQ_API_KEY=tu_token_aqui_xxxxx
  ```

