# Manual Técnico - Plataforma Digital BVI

## Índice
1. [Arquitectura del Sistema](#arquitectura-del-sistema)
2. [Stack Tecnológico](#stack-tecnológico)
3. [Estructura del Proyecto](#estructura-del-proyecto)
4. [Configuración del Entorno](#configuración-del-entorno)
5. [Base de Datos](#base-de-datos)
6. [Componentes Principales](#componentes-principales)
7. [Rutas y Navegación](#rutas-y-navegación)
8. [Autenticación y Seguridad](#autenticación-y-seguridad)
9. [Despliegue](#despliegue)
10. [API y Servicios](#api-y-servicios)
11. [Mantenimiento](#mantenimiento)

---

## Arquitectura del Sistema

### Diagrama de Arquitectura

```
┌─────────────────────────────────────────────────────────────┐
│                        FRONTEND (React)                      │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────────────┐ │
│  │   Pages     │  │ Components  │  │   Library/Utils     │ │
│  │             │  │             │  │                     │ │
│  │ - Home      │  │ - PillNav   │  │ - supabase.js       │ │
│  │ - Admin     │  │ - Protected │  │ - utils.js          │ │
│  │ - Login     │  │ - UI Comps  │  │                     │ │
│  │ - Boletines │  │             │  │                     │ │
│  │ - Fotogal.  │  │             │  │                     │ │
│  └─────────────┘  └─────────────┘  └─────────────────────┘ │
└──────────────────────────┬──────────────────────────────────┘
                           │
                           │ HTTPS/API Calls
                           │
┌──────────────────────────▼──────────────────────────────────┐
│                   SUPABASE (Backend)                         │
│  ┌──────────────────────────────────────────────────────┐  │
│  │              PostgreSQL Database                      │  │
│  │  - boletines_mensuales                               │  │
│  │  - informativos_mensuales                            │  │
│  │  - boletines_anuales                                 │  │
│  │  - fotogaleria_anuales                               │  │
│  │  - fotogaleria_semestrales                           │  │
│  └──────────────────────────────────────────────────────┘  │
│  ┌──────────────────────────────────────────────────────┐  │
│  │              Authentication Service                   │  │
│  │  - Email/Password Auth                               │  │
│  │  - Session Management                                │  │
│  │  - RLS Policies                                      │  │
│  └──────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────┘
```

### Flujo de Datos

```
Usuario → Interfaz React → Supabase Client → API Supabase → PostgreSQL
                ↓                                    ↓
          React Router                         Row Level Security
                ↓                                    ↓
        Componentes UI ← JSON Response ← Query Results
```

---

## Stack Tecnológico

### Frontend
| Tecnología | Versión | Propósito |
|------------|---------|-----------|
| **React** | 18.3.1 | Framework UI principal |
| **Vite** | 7.1.12 | Build tool y dev server |
| **React Router DOM** | 7.1.1 | Enrutamiento SPA |
| **Tailwind CSS** | 3.4.17 | Framework CSS utility-first |
| **Framer Motion** | 11.15.0 | Animaciones y transiciones |

### Backend y Servicios
| Servicio | Propósito |
|----------|-----------|
| **Supabase** | BaaS (Backend as a Service) |
| **PostgreSQL** | Base de datos relacional |
| **Supabase Auth** | Autenticación de usuarios |
| **Supabase Storage** | (Opcional) Almacenamiento de archivos |

### Desarrollo y Build
| Tool | Versión | Propósito |
|------|---------|-----------|
| **ESLint** | 9.18.0 | Linting de código |
| **PostCSS** | 8.4.49 | Procesamiento CSS |
| **Autoprefixer** | 10.4.20 | Prefijos CSS automáticos |

### Despliegue
| Plataforma | Propósito |
|------------|-----------|
| **Vercel** | Hosting y CI/CD |
| **GitHub** | Control de versiones |

---

## Estructura del Proyecto

```
lading/
├── public/                          # Archivos estáticos
│   ├── logo_bvi-2021.png
│   ├── boletinesmensuales.jpg
│   ├── InformativosMensuales.jpg
│   ├── Boletinesanuales.jpg
│   ├── fotosemestral.png
│   └── fotoanual.png
│
├── src/
│   ├── assets/                      # Recursos de la aplicación
│   │
│   ├── components/                  # Componentes reutilizables
│   │   ├── PillNav.jsx             # Navegación por pestañas
│   │   ├── ProtectedRoute.jsx      # HOC para rutas protegidas
│   │   └── ui/                     # Componentes UI
│   │       └── shadcn-io/          # Componentes UI avanzados
│   │           ├── background-beams-with-collision/
│   │           └── background-paths/
│   │
│   ├── lib/                        # Utilidades y configuración
│   │   ├── supabase.js            # Cliente Supabase
│   │   └── utils.js               # Funciones helper
│   │
│   ├── pages/                      # Páginas de la aplicación
│   │   ├── Home.jsx               # Página principal
│   │   ├── Login.jsx              # Página de login
│   │   ├── Admin.jsx              # Panel administrativo
│   │   │
│   │   ├── BoletinesMensuales.jsx         # Lista de años
│   │   ├── BoletinesMensualesYear.jsx     # Boletines por año
│   │   ├── InformativosMensuales.jsx      # Lista de años
│   │   ├── InformativosMensualesYear.jsx  # Informativos por año
│   │   ├── BoletinesAnuales.jsx           # Boletines anuales
│   │   │
│   │   ├── FotogaleriaAnuales.jsx         # Galerías anuales
│   │   └── FotogaleriaSemestrales.jsx     # Galerías semestrales
│   │
│   ├── App.jsx                     # Configuración de rutas
│   ├── main.jsx                    # Punto de entrada
│   └── index.css                   # Estilos globales
│
├── .env                            # Variables de entorno (no versionado)
├── .gitignore                      # Archivos ignorados por Git
├── components.json                 # Configuración shadcn/ui
├── eslint.config.js               # Configuración ESLint
├── index.html                      # HTML principal
├── jsconfig.json                  # Configuración JavaScript
├── package.json                    # Dependencias y scripts
├── postcss.config.js              # Configuración PostCSS
├── tailwind.config.js             # Configuración Tailwind
├── vercel.json                     # Configuración Vercel
├── vite.config.js                 # Configuración Vite
├── MANUAL_USUARIO.md              # Manual de usuario
└── MANUAL_TECNICO.md              # Este documento
```

---

## Configuración del Entorno

### Requisitos Previos

- **Node.js:** ≥ 18.0.0
- **npm:** ≥ 9.0.0
- **Git:** Para control de versiones
- **Cuenta Supabase:** Para backend y base de datos

### Instalación

#### 1. Clonar el Repositorio

```bash
git clone https://github.com/Gabrieldla/lading.git
cd lading
```

#### 2. Instalar Dependencias

```bash
npm install
```

#### 3. Configurar Variables de Entorno

Crear archivo `.env` en la raíz:

```env
VITE_SUPABASE_URL=https://tu-proyecto.supabase.co
VITE_SUPABASE_ANON_KEY=tu-anon-key-aqui
```

**Obtener credenciales:**
1. Acceder a [Supabase Dashboard](https://app.supabase.com)
2. Ir a Settings → API
3. Copiar URL y anon/public key

#### 4. Iniciar Servidor de Desarrollo

```bash
npm run dev
```

Servidor disponible en: `http://localhost:5173`

#### 5. Build para Producción

```bash
npm run build
```

Archivos generados en `dist/`

---

## Base de Datos

### Configuración de Supabase

#### 1. Crear Proyecto en Supabase

1. Acceder a [app.supabase.com](https://app.supabase.com)
2. Crear nuevo proyecto
3. Anotar URL y API keys

#### 2. Ejecutar Migraciones SQL

**Script completo para crear todas las tablas:**

```sql
-- ============================================
-- TABLA: boletines_mensuales
-- ============================================
CREATE TABLE IF NOT EXISTS boletines_mensuales (
  id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
  titulo TEXT NOT NULL,
  descripcion TEXT,
  pdf_url TEXT NOT NULL,
  imagen_url TEXT NOT NULL,
  año INTEGER NOT NULL CHECK (año >= 2004 AND año <= 2099),
  mes INTEGER NOT NULL CHECK (mes >= 1 AND mes <= 12),
  created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);

-- Índices para optimización
CREATE INDEX idx_boletines_mensuales_year ON boletines_mensuales(año);
CREATE INDEX idx_boletines_mensuales_month ON boletines_mensuales(mes);

-- ============================================
-- TABLA: informativos_mensuales
-- ============================================
CREATE TABLE IF NOT EXISTS informativos_mensuales (
  id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
  titulo TEXT NOT NULL,
  descripcion TEXT,
  pdf_url TEXT NOT NULL,
  imagen_url TEXT NOT NULL,
  año INTEGER NOT NULL CHECK (año >= 2004 AND año <= 2099),
  mes INTEGER NOT NULL CHECK (mes >= 1 AND mes <= 12),
  created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);

-- Índices
CREATE INDEX idx_informativos_mensuales_year ON informativos_mensuales(año);
CREATE INDEX idx_informativos_mensuales_month ON informativos_mensuales(mes);

-- ============================================
-- TABLA: boletines_anuales
-- ============================================
CREATE TABLE IF NOT EXISTS boletines_anuales (
  id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
  titulo TEXT NOT NULL,
  descripcion TEXT,
  pdf_url TEXT NOT NULL,
  imagen_url TEXT NOT NULL,
  año INTEGER NOT NULL CHECK (año >= 2004 AND año <= 2099),
  created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);

-- Índice
CREATE INDEX idx_boletines_anuales_year ON boletines_anuales(año);

-- ============================================
-- TABLA: fotogaleria_anuales
-- ============================================
CREATE TABLE IF NOT EXISTS fotogaleria_anuales (
  id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
  titulo TEXT NOT NULL,
  descripcion TEXT,
  imagen_url TEXT NOT NULL,
  link TEXT NOT NULL,
  año INTEGER NOT NULL CHECK (año >= 2004 AND año <= 2099),
  created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);

-- Índice
CREATE INDEX idx_fotogaleria_anuales_year ON fotogaleria_anuales(año);

-- ============================================
-- TABLA: fotogaleria_semestrales
-- ============================================
CREATE TABLE IF NOT EXISTS fotogaleria_semestrales (
  id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
  titulo TEXT NOT NULL,
  descripcion TEXT,
  imagen_url TEXT NOT NULL,
  link TEXT NOT NULL,
  año INTEGER NOT NULL CHECK (año >= 2004 AND año <= 2099),
  semestre INTEGER NOT NULL CHECK (semestre IN (1, 2)),
  created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);

-- Índices
CREATE INDEX idx_fotogaleria_semestrales_year ON fotogaleria_semestrales(año);
CREATE INDEX idx_fotogaleria_semestrales_semester ON fotogaleria_semestrales(semestre);
```

#### 3. Configurar Row Level Security (RLS)

**Habilitar RLS en todas las tablas:**

```sql
-- Habilitar RLS
ALTER TABLE boletines_mensuales ENABLE ROW LEVEL SECURITY;
ALTER TABLE informativos_mensuales ENABLE ROW LEVEL SECURITY;
ALTER TABLE boletines_anuales ENABLE ROW LEVEL SECURITY;
ALTER TABLE fotogaleria_anuales ENABLE ROW LEVEL SECURITY;
ALTER TABLE fotogaleria_semestrales ENABLE ROW LEVEL SECURITY;
```

**Políticas de lectura pública:**

```sql
-- Permitir lectura pública (SELECT)
CREATE POLICY "Public read access" ON boletines_mensuales
  FOR SELECT USING (true);

CREATE POLICY "Public read access" ON informativos_mensuales
  FOR SELECT USING (true);

CREATE POLICY "Public read access" ON boletines_anuales
  FOR SELECT USING (true);

CREATE POLICY "Public read access" ON fotogaleria_anuales
  FOR SELECT USING (true);

CREATE POLICY "Public read access" ON fotogaleria_semestrales
  FOR SELECT USING (true);
```

**Políticas de escritura solo para usuarios autenticados:**

```sql
-- Permitir INSERT/UPDATE/DELETE solo a usuarios autenticados
CREATE POLICY "Authenticated users can insert" ON boletines_mensuales
  FOR INSERT TO authenticated USING (true);

CREATE POLICY "Authenticated users can update" ON boletines_mensuales
  FOR UPDATE TO authenticated USING (true);

CREATE POLICY "Authenticated users can delete" ON boletines_mensuales
  FOR DELETE TO authenticated USING (true);

-- Repetir para todas las tablas...
-- (informativos_mensuales, boletines_anuales, fotogaleria_anuales, fotogaleria_semestrales)
```

#### 4. Crear Usuario Administrador

```sql
-- Desde el dashboard de Supabase:
-- Authentication → Users → Add User

-- O mediante SQL (requiere permisos admin):
INSERT INTO auth.users (email, encrypted_password, email_confirmed_at)
VALUES ('admin@bvi.urp.edu.pe', crypt('tu-password-segura', gen_salt('bf')), NOW());
```

---

## Componentes Principales

### 1. Cliente Supabase (`src/lib/supabase.js`)

```javascript
import { createClient } from '@supabase/supabase-js'

const supabaseUrl = import.meta.env.VITE_SUPABASE_URL
const supabaseAnonKey = import.meta.env.VITE_SUPABASE_ANON_KEY

export const supabase = createClient(supabaseUrl, supabaseAnonKey)
```

**Uso:**
```javascript
import { supabase } from '@/lib/supabase'

// Consulta
const { data, error } = await supabase
  .from('boletines_mensuales')
  .select('*')
  .order('año', { ascending: false })

// Inserción
const { error } = await supabase
  .from('boletines_mensuales')
  .insert([{ titulo: 'Ejemplo', año: 2024, mes: 12 }])
```

### 2. ProtectedRoute (`src/components/ProtectedRoute.jsx`)

```javascript
import { useEffect, useState } from 'react'
import { Navigate } from 'react-router-dom'
import { supabase } from '@/lib/supabase'

function ProtectedRoute({ children }) {
  const [session, setSession] = useState(null)
  const [loading, setLoading] = useState(true)

  useEffect(() => {
    supabase.auth.getSession().then(({ data: { session } }) => {
      setSession(session)
      setLoading(false)
    })

    const { data: { subscription } } = supabase.auth.onAuthStateChange((_event, session) => {
      setSession(session)
    })

    return () => subscription.unsubscribe()
  }, [])

  if (loading) return <div>Cargando...</div>
  if (!session) return <Navigate to="/login" replace />
  
  return children
}

export default ProtectedRoute
```

**Propósito:** Proteger rutas que requieren autenticación (como `/admin`)

### 3. PillNav (`src/components/PillNav.jsx`)

```javascript
function PillNav({ tabs, activeTab, setActiveTab }) {
  return (
    <div className="flex gap-2 overflow-x-auto pb-2">
      {tabs.map((tab) => (
        <button
          key={tab.id}
          onClick={() => setActiveTab(tab.id)}
          className={`px-6 py-3 rounded-full font-semibold transition-all ${
            activeTab === tab.id
              ? 'bg-gradient-to-r from-orange-600 to-amber-600 text-white'
              : 'bg-gray-200 text-gray-700 hover:bg-gray-300'
          }`}
        >
          {tab.label}
        </button>
      ))}
    </div>
  )
}
```

**Propósito:** Navegación por pestañas en el panel de administración

---

## Rutas y Navegación

### Configuración de Rutas (`src/App.jsx`)

```javascript
import { BrowserRouter as Router, Routes, Route } from 'react-router-dom'

function App() {
  return (
    <Router>
      <Routes>
        {/* Rutas públicas */}
        <Route path="/" element={<Home />} />
        <Route path="/login" element={<Login />} />
        
        {/* Boletines */}
        <Route path="/boletines-mensuales" element={<BoletinesMensuales />} />
        <Route path="/boletines-mensuales/:year" element={<BoletinesMensualesYear />} />
        <Route path="/informativos-mensuales" element={<InformativosMensuales />} />
        <Route path="/informativos-mensuales/:year" element={<InformativosMensualesYear />} />
        <Route path="/boletines-anuales" element={<BoletinesAnuales />} />
        
        {/* Fotogalerías */}
        <Route path="/fotogaleria-anuales" element={<FotogaleriaAnuales />} />
        <Route path="/fotogaleria-semestrales" element={<FotogaleriaSemestrales />} />
        
        {/* Ruta protegida */}
        <Route path="/admin" element={
          <ProtectedRoute>
            <Admin />
          </ProtectedRoute>
        } />
      </Routes>
    </Router>
  )
}
```

### Tabla de Rutas

| Ruta | Componente | Tipo | Descripción |
|------|------------|------|-------------|
| `/` | Home | Pública | Página principal |
| `/login` | Login | Pública | Inicio de sesión |
| `/boletines-mensuales` | BoletinesMensuales | Pública | Lista de años |
| `/boletines-mensuales/:year` | BoletinesMensualesYear | Pública | Boletines de un año |
| `/informativos-mensuales` | InformativosMensuales | Pública | Lista de años |
| `/informativos-mensuales/:year` | InformativosMensualesYear | Pública | Informativos de un año |
| `/boletines-anuales` | BoletinesAnuales | Pública | Boletines anuales |
| `/fotogaleria-anuales` | FotogaleriaAnuales | Pública | Galerías anuales |
| `/fotogaleria-semestrales` | FotogaleriaSemestrales | Pública | Galerías semestrales |
| `/admin` | Admin | Protegida | Panel administrativo |

---

## Autenticación y Seguridad

### Flujo de Autenticación

```
1. Usuario accede a /login
2. Ingresa email y password
3. supabase.auth.signInWithPassword()
4. Supabase valida credenciales
5. Si válido: Genera session token
6. React guarda session en localStorage
7. Redirección a /admin
8. ProtectedRoute valida session
9. Si válida: Muestra Admin
10. Si inválida: Redirección a /login
```

### Implementación de Login

```javascript
// src/pages/Login.jsx
const handleSubmit = async (e) => {
  e.preventDefault()
  setLoading(true)
  setError('')

  const { error } = await supabase.auth.signInWithPassword({
    email,
    password,
  })

  if (error) {
    setError(error.message)
  } else {
    navigate('/admin')
  }
  
  setLoading(false)
}
```

### Implementación de Logout

```javascript
// src/pages/Admin.jsx
const handleLogout = async () => {
  await supabase.auth.signOut()
  navigate('/login')
}
```

### Seguridad de Datos

1. **Row Level Security (RLS):**
   - Lectura pública para todas las tablas
   - Escritura solo para usuarios autenticados

2. **Variables de entorno:**
   - Claves API en `.env` (no versionado)
   - Acceso mediante `import.meta.env.VITE_*`

3. **HTTPS:**
   - Todas las comunicaciones encriptadas
   - Certificado SSL automático en Vercel

---

## Despliegue

### Despliegue en Vercel

#### 1. Configuración Inicial

```bash
# Instalar Vercel CLI
npm i -g vercel

# Login
vercel login

# Deploy
vercel
```

#### 2. Variables de Entorno en Vercel

1. Acceder a Vercel Dashboard
2. Ir a Settings → Environment Variables
3. Agregar:
   - `VITE_SUPABASE_URL`
   - `VITE_SUPABASE_ANON_KEY`

#### 3. Configuración `vercel.json`

```json
{
  "rewrites": [
    {
      "source": "/(.*)",
      "destination": "/index.html"
    }
  ]
}
```

**Propósito:** Habilitar SPA routing (todas las rutas → index.html)

#### 4. Despliegue Automático

- **Push a `main`:** Despliega automáticamente a producción
- **Push a otras ramas:** Crea preview deployments
- **Pull Requests:** Genera preview URLs

---

## API y Servicios

### Operaciones CRUD

#### SELECT (Read)

```javascript
// Obtener todos los registros
const { data, error } = await supabase
  .from('boletines_mensuales')
  .select('*')

// Filtrar por año
const { data, error } = await supabase
  .from('boletines_mensuales')
  .select('*')
  .eq('año', 2024)

// Ordenar
const { data, error } = await supabase
  .from('boletines_mensuales')
  .select('*')
  .order('año', { ascending: false })
  .order('mes', { ascending: false })

// Obtener años únicos
const { data, error } = await supabase
  .from('boletines_mensuales')
  .select('año')
  .order('año', { ascending: false })
```

#### INSERT (Create)

```javascript
const { data, error } = await supabase
  .from('boletines_mensuales')
  .insert([{
    titulo: 'Boletín Enero 2024',
    descripcion: 'Primer boletín del año',
    pdf_url: 'https://example.com/boletin.pdf',
    imagen_url: 'https://example.com/portada.jpg',
    año: 2024,
    mes: 1
  }])
  .select()
```

#### UPDATE

```javascript
const { data, error } = await supabase
  .from('boletines_mensuales')
  .update({ 
    titulo: 'Nuevo título',
    descripcion: 'Nueva descripción'
  })
  .eq('id', 'uuid-del-registro')
  .select()
```

#### DELETE

```javascript
const { error } = await supabase
  .from('boletines_mensuales')
  .delete()
  .eq('id', 'uuid-del-registro')
```

### Manejo de Errores

```javascript
const fetchData = async () => {
  try {
    const { data, error } = await supabase
      .from('boletines_mensuales')
      .select('*')
    
    if (error) throw error
    
    setData(data)
  } catch (error) {
    console.error('Error fetching data:', error.message)
    setError(error.message)
  } finally {
    setLoading(false)
  }
}
```

---

## Mantenimiento

### Actualizaciones de Dependencias

```bash
# Verificar paquetes desactualizados
npm outdated

# Actualizar todos los paquetes
npm update

# Actualizar paquete específico
npm install react@latest
```

### Monitoreo

#### Logs de Vercel
- Acceder a Vercel Dashboard
- Ir a Deployments → [deployment] → Logs

#### Logs de Supabase
- Supabase Dashboard → Logs
- Monitorear queries lentas
- Detectar errores de autenticación

### Backup de Base de Datos

```bash
# Desde Supabase Dashboard:
# Database → Backups → Download

# O mediante CLI:
pg_dump -h db.your-project.supabase.co \
  -U postgres \
  -d postgres \
  -F c \
  -f backup_$(date +%Y%m%d).dump
```

### Optimización

#### 1. Caché de Imágenes
```javascript
// En vite.config.js
export default defineConfig({
  build: {
    rollupOptions: {
      output: {
        assetFileNames: 'assets/[name].[hash][extname]'
      }
    }
  }
})
```

#### 2. Code Splitting
```javascript
// Lazy loading de rutas
const Admin = lazy(() => import('./pages/Admin'))

<Suspense fallback={<div>Cargando...</div>}>
  <Admin />
</Suspense>
```

#### 3. Índices de Base de Datos
```sql
-- Verificar uso de índices
EXPLAIN ANALYZE 
SELECT * FROM boletines_mensuales WHERE año = 2024;

-- Crear índice compuesto
CREATE INDEX idx_boletines_year_month 
ON boletines_mensuales(año, mes);
```

---

## Scripts de Package.json

```json
{
  "scripts": {
    "dev": "vite",                    // Servidor de desarrollo
    "build": "vite build",            // Build para producción
    "preview": "vite preview",        // Preview del build
    "lint": "eslint ."                // Verificar código
  }
}
```

### Comandos Útiles

```bash
# Desarrollo
npm run dev

# Build
npm run build

# Preview local del build
npm run preview

# Lint
npm run lint

# Lint con auto-fix
npm run lint -- --fix
```

---

## Solución de Problemas Técnicos

### Error: "Failed to fetch"

**Causa:** Problemas de CORS o red

**Solución:**
```javascript
// Verificar configuración de Supabase
const supabase = createClient(
  process.env.VITE_SUPABASE_URL,
  process.env.VITE_SUPABASE_ANON_KEY,
  {
    auth: {
      persistSession: true,
      autoRefreshToken: true,
    }
  }
)
```

### Error: "RLS Policy Violation"

**Causa:** Políticas RLS restrictivas

**Solución:**
```sql
-- Verificar políticas
SELECT * FROM pg_policies WHERE tablename = 'boletines_mensuales';

-- Recrear política
DROP POLICY IF EXISTS "Public read access" ON boletines_mensuales;
CREATE POLICY "Public read access" ON boletines_mensuales
  FOR SELECT USING (true);
```

### Error: Build falla en Vercel

**Causa:** Variables de entorno faltantes

**Solución:**
1. Verificar `.env` local
2. Agregar en Vercel Dashboard
3. Redeploy

---

## Diagramas Técnicos

### Flujo de Datos en Admin

```
┌─────────────┐
│   Usuario   │
│   (Admin)   │
└──────┬──────┘
       │
       │ 1. Completa formulario
       ▼
┌─────────────────┐
│  Admin.jsx      │
│  handleAdd()    │
└──────┬──────────┘
       │
       │ 2. supabase.from().insert()
       ▼
┌─────────────────┐
│ Supabase Client │
└──────┬──────────┘
       │
       │ 3. HTTP POST
       ▼
┌─────────────────┐
│  Supabase API   │
└──────┬──────────┘
       │
       │ 4. Valida RLS Policy
       ▼
┌─────────────────┐
│   PostgreSQL    │
│   INSERT INTO   │
└──────┬──────────┘
       │
       │ 5. Retorna { data, error }
       ▼
┌─────────────────┐
│  Admin.jsx      │
│  loadData()     │
└──────┬──────────┘
       │
       │ 6. Actualiza UI
       ▼
┌─────────────────┐
│  Lista          │
│  Actualizada    │
└─────────────────┘
```

---

## Contacto Técnico

**Desarrollador Principal:** [Tu nombre]
**Email:** [tu-email]@urp.edu.pe
**GitHub:** https://github.com/Gabrieldla/lading
**Documentación Supabase:** https://supabase.com/docs

---

## Changelog Técnico

### v1.0.0 (Diciembre 2025)
- ✅ Implementación inicial con React 18 + Vite
- ✅ Integración completa con Supabase
- ✅ Sistema de autenticación con email/password
- ✅ CRUD completo para 5 entidades
- ✅ RLS policies configuradas
- ✅ Despliegue en Vercel con CI/CD
- ✅ Diseño responsive con Tailwind CSS
- ✅ Animaciones con Framer Motion

---

**Última actualización:** 10 de Diciembre de 2025  
**Versión del documento:** 1.0.0
