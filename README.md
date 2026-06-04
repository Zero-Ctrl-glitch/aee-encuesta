# AEE — Encuesta de Evaluación Docente
## Guía completa para subir a GitHub y conectar con Google Sheets

---

## Resumen de archivos

```
aee-encuesta/
├── index.html   ← Formulario para estudiantes (página pública)
├── admin.html   ← Panel de resultados (acceso con contraseña)
├── Code.gs      ← Código para Google Apps Script (backend)
└── README.md    ← Este archivo
```

---

## PASO 1 — Crear la hoja de Google Sheets

1. Ve a **sheets.google.com** e inicia sesión
2. Crea una nueva hoja en blanco
3. Nómbrala como quieras, por ejemplo: `AEE Encuesta 2024`
4. Copia el **ID de la hoja** de la URL del navegador:
   ```
   https://docs.google.com/spreadsheets/d/  ESTE_ES_EL_ID  /edit
   ```
5. Guarda ese ID, lo necesitarás más adelante

---

## PASO 2 — Crear el Google Apps Script

1. Dentro de tu hoja de Google Sheets, ve al menú:
   **Extensiones → Apps Script**
2. Se abrirá el editor de código
3. Borra todo el código que aparece por defecto
4. Abre el archivo `Code.gs` de este proyecto y **copia todo su contenido**
5. Pégalo en el editor de Apps Script
6. Haz clic en **Guardar** (ícono de disquete o Ctrl+S)
7. Ponle un nombre al proyecto, por ejemplo: `AEE Backend`

---

## PASO 3 — Publicar el Apps Script como Web App

1. En el editor de Apps Script, haz clic en **"Implementar" → "Nueva implementación"**
2. Haz clic en el ícono de engranaje ⚙️ junto a "Tipo" y elige **"Aplicación web"**
3. Configura así:
   - **Descripción:** `AEE Encuesta v1`
   - **Ejecutar como:** `Yo (tu correo)`
   - **Quién tiene acceso:** **Cualquier usuario** ← ⚠️ importante
4. Haz clic en **"Implementar"**
5. Google te pedirá que **autorices los permisos** — acepta todo
6. Copia la **URL de la aplicación web** que aparece al final
   (se ve así: `https://script.google.com/macros/s/XXXXXX/exec`)
7. Guarda esa URL

---

## PASO 4 — Configurar los archivos HTML

Abre `index.html` con VS Code y busca esta línea:
```javascript
APPS_SCRIPT_URL: 'PEGA_AQUI_TU_URL_DE_APPS_SCRIPT'
```
Reemplázala con la URL que copiaste en el Paso 3:
```javascript
APPS_SCRIPT_URL: 'https://script.google.com/macros/s/TU_ID/exec'
```

Abre `admin.html` con VS Code y busca estas líneas:
```javascript
APPS_SCRIPT_URL: 'PEGA_AQUI_TU_URL_DE_APPS_SCRIPT',
SHEET_ID:        'PEGA_AQUI_TU_SHEET_ID',
ADMIN_PASSWORD:  'aee2024admin'
```
Reemplaza con tus valores reales:
```javascript
APPS_SCRIPT_URL: 'https://script.google.com/macros/s/TU_ID/exec',
SHEET_ID:        'TU_ID_DE_GOOGLE_SHEETS',
ADMIN_PASSWORD:  'tu-contraseña-segura'
```

---

## PASO 5 — Subir a GitHub Pages

### 5a. Crear el repositorio en GitHub
1. Ve a **github.com** e inicia sesión
2. Haz clic en **"New repository"** (botón verde)
3. Nómbralo: `aee-encuesta` (o como quieras)
4. Marca **"Public"** ← necesario para GitHub Pages gratis
5. Haz clic en **"Create repository"**

### 5b. Subir los archivos
En la página del repositorio vacío, haz clic en **"uploading an existing file"**:
1. Arrastra y suelta estos 3 archivos:
   - `index.html`
   - `admin.html`
   - `README.md`
   (NO subas `Code.gs`, ese ya lo usaste en Apps Script)
2. Escribe un mensaje de commit, por ejemplo: `Primera versión`
3. Haz clic en **"Commit changes"**

### 5c. Activar GitHub Pages
1. En tu repositorio, ve a **Settings** (pestaña de configuración)
2. En el menú izquierdo, haz clic en **"Pages"**
3. En "Branch", selecciona **`main`** y carpeta **`/ (root)`**
4. Haz clic en **"Save"**
5. Espera 1-2 minutos y recarga la página
6. Aparecerá tu URL pública:
   ```
   https://TU-USUARIO.github.io/aee-encuesta/
   ```

---

## PASO 6 — Probar todo

| Página | URL |
|---|---|
| Formulario (estudiantes) | `https://TU-USUARIO.github.io/aee-encuesta/` |
| Panel admin | `https://TU-USUARIO.github.io/aee-encuesta/admin.html` |

1. Abre el formulario en tu celular y llena una respuesta de prueba
2. Abre el panel admin en tu laptop
3. Ingresa tu contraseña
4. Haz clic en **"🔄 Actualizar"**
5. Deberías ver la respuesta que enviaste desde el celular ✅
6. También puedes abrir tu Google Sheet y ver los datos ahí directamente

---

## Actualizar el sitio después de cambios

Si necesitas modificar algo en los archivos HTML:
1. Edítalos en VS Code
2. Ve a tu repositorio en GitHub
3. Haz clic en el archivo → ícono de lápiz ✏️ → edita → "Commit changes"
   **O** simplemente arrastra el archivo nuevo encima del repositorio

---

## ¿Cómo ven los datos los estudiantes vs. tú?

| | Estudiante | Tú (admin) |
|---|---|---|
| URL | `/index.html` | `/admin.html` |
| Necesita contraseña | No | Sí |
| Ve los resultados | No | Sí |
| Puede exportar PDF | No | Sí |

---

## Solución de problemas frecuentes

**"No se pudo conectar con la base de datos"**
→ La URL del Apps Script en `admin.html` está incorrecta o el script no está publicado con acceso "Cualquier usuario"

**"El formulario no envía"**
→ La URL del Apps Script en `index.html` está incorrecta

**"Los datos no aparecen en el admin"**
→ Haz clic en "🔄 Actualizar" — el panel no se actualiza automáticamente

**"GitHub Pages no muestra el sitio"**
→ Espera 5 minutos y recarga. Si sigue sin funcionar, verifica que el repositorio sea público

---

*Asociación de Estudiantes de Ingeniería Electrónica (AEE)*
