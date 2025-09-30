📌 Generador de QRs con enlaces a manuales en Google Drive

Este proyecto genera etiquetas QR para equipos biomédicos a partir de un archivo Excel.
Cada QR enlaza directamente al manual del equipo almacenado en Google Drive.

Ideal para hospitales, clínicas o empresas de mantenimiento que necesitan identificar rápidamente la documentación técnica de cada dispositivo.

🚀 Requisitos

Python 3.9+
Cuenta de Google
Acceso a Google Cloud Console

📦 Instalación de dependencias

pip install pandas openpyxl pillow qrcode unidecode google-auth google-auth-oauthlib google-auth-httplib2 google-api-python-client

⚙️ Configuración de Google Drive API

1. Ve a Google Cloud Console.
2. Crea un proyecto (o usa uno existente).
  Habilita la Google Drive API:
3. API & Services > Enable APIs & Services > Google Drive API.
4. Crea credenciales:
  Tipo: OAuth client ID
    Aplicación de escritorio
Descarga el archivo credentials.json.
Coloca el archivo en la raíz del proyecto.
En la primera ejecución del script:
Se abrirá el navegador para loguearte en tu cuenta de Google.
Se generará automáticamente un archivo token.json (usado en ejecuciones futuras).

📂 Estructura esperada

.
├── generate_qr.py
├── credentials.json       # credenciales descargadas de Google Cloud
├── token.json             # se genera automáticamente tras la primera ejecución
├── equipos_soata.xlsx     # archivo Excel con equipos
├── etiquetas_qr/          # aquí se guardarán las imágenes generadas
├── errores.log            # listado de equipos sin PDF (generado automáticamente)

📑 Formato del Excel

El archivo debe contener exactamente estas columnas:

NOMBRE DEL EQUIPO
MARCA
MODELO

Ejemplo:

NOMBRE DEL EQUIPO	MARCA	MODELO
BÁSCULA DE PISO	DETECTO	BARRA123
DEA	MINDRAY	C1A
▶️ Ejecución
python generate_qr.py

Al finalizar:

Se generarán imágenes PNG en la carpeta etiquetas_qr/.
Se registrarán en errores.log los equipos que no encontraron PDF.

🔍 Lógica de búsqueda de PDFs

El script busca coincidencias en los nombres de los archivos PDF dentro de la carpeta de Google Drive configurada.

Orden de búsqueda (de más estricto a más flexible):

1. Nombre + Marca + Modelo
2. Nombre + Marca
3. Nombre + Modelo
4. Solo Nombre
5. Marca + Modelo

✨ Mejoras futuras

Log detallado en errores.log con fecha, hora y equipos sin coincidencias.
Exportar también en PDF con una lista consolidada de todos los equipos y su QR.
Interfaz gráfica (GUI) para cargar Excel y generar etiquetas sin usar la terminal.
Soporte multi-carpeta en Drive para organizar mejor los manuales.
Opciones de diseño (colores, logos institucionales, tamaños de etiquetas).

📝 Licencia

Este proyecto está bajo la licencia MIT.
Puedes usarlo, modificarlo y compartirlo libremente.
