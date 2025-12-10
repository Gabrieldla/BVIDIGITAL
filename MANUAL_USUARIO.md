# Manual de Usuario - Plataforma Digital BVI

## Índice
1. [Introducción](#introducción)
2. [Acceso a la Plataforma](#acceso-a-la-plataforma)
3. [Navegación Principal](#navegación-principal)
4. [Secciones de Contenido](#secciones-de-contenido)
5. [Panel de Administración](#panel-de-administración)
6. [Guía Rápida para Administradores](#guía-rápida-para-administradores)

---

## Introducción

La Plataforma Digital BVI es un sistema web diseñado para gestionar y visualizar boletines mensuales, informativos y fotogalerías de la Biblioteca Virtual de Ingeniería. Esta plataforma permite a los usuarios consultar documentos históricos organizados por año y periodo, así como acceder a galerías fotográficas institucionales.

### Características Principales
- 📄 Boletines Mensuales organizados por año
- 📰 Informativos Mensuales con actualizaciones periódicas
- 📚 Boletines Anuales consolidados
- 📸 Fotogalerías Anuales y Semestrales
- 🔐 Panel de administración protegido
- 📱 Diseño responsive (móvil, tablet, desktop)

---

## Acceso a la Plataforma

### URL Principal
```
https://[tu-dominio].vercel.app
```

### Navegación del Menú Superior
El menú fijo en la parte superior contiene los siguientes enlaces:

| Enlace | Descripción |
|--------|-------------|
| **ExamURP** | Acceso a la plataforma de exámenes |
| **Estantería Virtual** | (Próximamente) |
| **Página Oficial URP** | Sitio web institucional de la universidad |
| **Semana Ingeniería** | Página del evento anual |
| **Login** | Acceso al panel de administración |

---

## Navegación Principal

### Página de Inicio (Home)

#### Sección Hero
- Título principal de la plataforma
- Botón "Explorar" para desplazarse al contenido

#### Botones de Navegación
- **Ir hacia abajo** (↓): Ubicado al final del hero, lleva a la primera sección
- **Volver arriba** (↑): Flotante en esquina inferior derecha, siempre visible

### Estructura de Secciones
1. **Boletines Mensuales** (Naranja)
2. **Informativos Mensuales** (Naranja)
3. **Boletines Anuales** (Naranja/Ámbar)
4. **Fotogalería Semestral** (Rosa/Naranja)
5. **Fotogalería Anual** (Púrpura/Rosa)

---

## Secciones de Contenido

### 1. Boletines Mensuales

**Paso 1:** Click en "Ver Boletines" desde la página principal

**Paso 2:** Selecciona un año de la lista disponible
- Los años se muestran en tarjetas organizadas cronológicamente
- Formato de tarjeta: Año + icono de navegación

**Paso 3:** Explora los boletines del año seleccionado
- Vista de cuadrícula con hasta 12 tarjetas (una por mes)
- Cada tarjeta muestra:
  - Imagen de portada
  - Título del boletín
  - Mes y año
  - Descripción breve

**Paso 4:** Click en cualquier tarjeta para abrir el PDF
- Se abre en nueva pestaña
- Permite descarga directa

---

### 2. Informativos Mensuales

**Funcionamiento:** Idéntico a Boletines Mensuales
- Misma estructura de navegación
- Diseño de tarjetas similar
- Contenido enfocado en comunicados oficiales

---

### 3. Boletines Anuales

**Acceso Directo:** Click en "Ver Boletines Anuales"

**Visualización:**
- Tarjetas con imagen de portada grande (256px altura)
- Badge con el año en esquina superior derecha
- Título y descripción
- Click directo al PDF sin página intermedia

**Características:**
- Grid responsive: 1 columna (móvil), 2 (tablet), 3 (desktop)
- Ordenados por año descendente
- Borde superior naranja distintivo

---

### 4. Fotogalería Semestral

**Paso 1:** Click en "Ver Fotos Semestrales"

**Paso 2:** Explora las galerías disponibles
- Tarjetas con imagen de portada
- Badges superiores:
  - **Azul:** 1er Semestre
  - **Naranja:** 2do Semestre
  - **Gris:** Año

**Paso 3:** Click en tarjeta
- Abre galería externa (Google Photos, etc.)
- Se abre en nueva pestaña

---

### 5. Fotogalería Anual

**Funcionamiento:** Similar a Fotogalería Semestral
- Tarjetas con imagen de portada
- Badge púrpura con el año
- Enlace a galería externa completa

---

## Panel de Administración

### Acceso al Admin

**Paso 1:** Click en "Login" en el menú superior

**Paso 2:** Ingresa credenciales
- Email registrado en Supabase
- Contraseña

**Paso 3:** Click en "Iniciar Sesión"

### Cerrar Sesión
- Botón "Cerrar Sesión" visible en la parte superior del panel

---

## Guía Rápida para Administradores

### Estructura del Panel

El panel tiene 5 pestañas principales:

#### 1️⃣ Boletines Mensuales

**Agregar Boletín:**
1. Completa el formulario:
   - **Título:** Nombre del boletín
   - **URL del PDF:** Link directo al documento
   - **URL de Imagen:** Link a la portada (recomendado: 800×512px)
   - **Descripción:** Texto breve descriptivo
   - **Año:** 2004-2099
   - **Mes:** Selector 1-12

2. Click en "Agregar Boletín"

**Editar Boletín:**
1. Click en "Editar" en la tarjeta deseada
2. Modifica los campos necesarios
3. Click en "Actualizar Boletín"

**Eliminar Boletín:**
1. Click en "Eliminar"
2. Confirma la acción en el diálogo

---

#### 2️⃣ Informativos Mensuales

**Funcionalidad:** Idéntica a Boletines Mensuales
- Mismo formulario
- Mismos campos
- Mismas operaciones CRUD

---

#### 3️⃣ Boletines Anuales

**Agregar Boletín Anual:**
1. Título
2. URL del PDF
3. URL de Imagen de Portada (800×512px)
4. Descripción
5. Año (2004-2099)

**Nota:** No requiere campo "mes"

---

#### 4️⃣ Fotogalería Anuales

**Agregar Galería Anual:**
1. **Título:** Ej. "Galería Anual 2024"
2. **URL de Imagen de Portada:** Imagen representativa (800×512px)
3. **Link de la Galería:** URL externa (Google Photos, Flickr, etc.)
4. **Descripción:** Breve descripción del contenido
5. **Año:** 2004-2099

**Importante:**
- `imagen_url`: Portada que se muestra en la tarjeta
- `link`: Enlace a la galería completa externa

---

#### 5️⃣ Fotogalería Semestrales

**Agregar Galería Semestral:**
1. **Título:** Ej. "Primer Semestre 2024"
2. **URL de Imagen de Portada:** Imagen representativa (800×512px)
3. **Link de la Galería:** URL externa
4. **Descripción:** Texto descriptivo
5. **Año:** 2004-2099
6. **Semestre:** 
   - 1 = Primer Semestre
   - 2 = Segundo Semestre

---

## Recomendaciones de Imágenes

### Portadas en Home (Secciones)
- **Formato:** 4:3
- **Resolución recomendada:** 800×600px o 1600×1200px
- **Archivos actuales:**
  - `/boletinesmensuales.jpg`
  - `/InformativosMensuales.jpg`
  - `/Boletinesanuales.jpg`
  - `/fotosemestral.png`
  - `/fotoanual.png`

### Tarjetas de Contenido
- **Formato:** 1.56:1 (aprox.)
- **Resolución recomendada:** 800×512px
- **Formato de archivo:** JPG, PNG, WebP
- **Peso máximo recomendado:** 200KB

---

## Base de Datos (Supabase)

### Tablas Utilizadas

#### `boletines_mensuales`
```sql
- id (uuid, PK)
- titulo (text)
- descripcion (text)
- pdf_url (text)
- imagen_url (text)
- año (integer)
- mes (integer)
- created_at (timestamp)
```

#### `informativos_mensuales`
```sql
- id (uuid, PK)
- titulo (text)
- descripcion (text)
- pdf_url (text)
- imagen_url (text)
- año (integer)
- mes (integer)
- created_at (timestamp)
```

#### `boletines_anuales`
```sql
- id (uuid, PK)
- titulo (text)
- descripcion (text)
- pdf_url (text)
- imagen_url (text)
- año (integer)
- created_at (timestamp)
```

#### `fotogaleria_anuales`
```sql
- id (uuid, PK)
- titulo (text)
- descripcion (text)
- imagen_url (text)
- link (text)
- año (integer)
- created_at (timestamp)
```

#### `fotogaleria_semestrales`
```sql
- id (uuid, PK)
- titulo (text)
- descripcion (text)
- imagen_url (text)
- link (text)
- año (integer)
- semestre (integer) -- CHECK: 1 o 2
- created_at (timestamp)
```

### SQL para Crear las Tablas de Fotogalería

```sql
-- Agregar columna 'link' a fotogaleria_anuales
ALTER TABLE fotogaleria_anuales
ADD COLUMN link TEXT NOT NULL DEFAULT '';

-- Agregar columna 'link' a fotogaleria_semestrales
ALTER TABLE fotogaleria_semestrales
ADD COLUMN link TEXT NOT NULL DEFAULT '';
```

---

## Resolución de Problemas

### Error: "No se pueden cargar los datos"
**Solución:**
1. Verifica conexión a internet
2. Revisa que las tablas existan en Supabase
3. Confirma que las políticas RLS permitan lectura pública

### Error: "No se puede subir contenido"
**Solución:**
1. Verifica estar logueado como administrador
2. Revisa permisos de escritura en Supabase
3. Confirma que todos los campos requeridos estén completos

### Imágenes no se muestran
**Solución:**
1. Verifica que las URLs sean accesibles públicamente
2. Usa URLs HTTPS (no HTTP)
3. Confirma que las imágenes existan en la ruta especificada

### PDFs no se abren
**Solución:**
1. Verifica que la URL del PDF sea válida
2. Asegúrate de que el archivo sea accesible sin autenticación
3. Usa servicios confiables (Google Drive en modo público, etc.)

---

## Contacto y Soporte

Para soporte técnico o reportar errores:
- **Email:** [tu-email]@urp.edu.pe
- **GitHub:** [repositorio del proyecto]

---

## Registro de Cambios

### Versión 1.0.0 (Diciembre 2025)
- ✅ Implementación inicial
- ✅ Boletines mensuales, informativos y anuales
- ✅ Sistema de fotogalerías (anual y semestral)
- ✅ Panel de administración con CRUD completo
- ✅ Diseño responsive
- ✅ Integración con Supabase

---

**Última actualización:** 10 de Diciembre de 2025
