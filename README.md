# 💍 siAcepto - Aplicación para Organización de Casamientos

Plataforma integral para la organización y gestión de casamientos, que permite a los novios y sus invitados compartir momentos especiales a través de una galería de fotos colaborativa y conectar con otros invitados mediante un módulo de interacción social.

![Estado del Proyecto](https://img.shields.io/badge/Estado-En%20Desarrollo-yellow)
![Documentación](https://img.shields.io/badge/Documentación-Completa-green)
![Licencia](https://img.shields.io/badge/Licencia-MIT-blue)

---

## 📋 Tabla de Contenidos

- [Descripción](#-descripción)
- [Características Principales](#-características-principales)
- [Módulos del Sistema](#-módulos-del-sistema)
- [Documentación](#-documentación)
- [Gestión del Proyecto](#-gestión-del-proyecto)
- [Arquitectura](#-arquitectura)
- [Tecnologías](#-tecnologías)
- [Instalación](#-instalación)
- [Roadmap](#-roadmap)
- [Contribución](#-contribución)
- [Licencia](#-licencia)

---

## 🎯 Descripción

**siAcepto** es una aplicación móvil y web diseñada para facilitar la organización de casamientos, permitiendo a las parejas y sus invitados:

- 📸 Compartir fotos del evento en tiempo real en una galería colaborativa
- 💕 Conectar con otros invitados solteros durante la celebración
- 🏷️ Etiquetar personas en fotos y organizarlas por eventos/actividades
- 💬 Chatear con matches dentro de la aplicación
- 🎨 Disfrutar de una experiencia visual con paleta de colores pastel

### Usuarios del Sistema

| Rol | Descripción | Funcionalidades |
|-----|-------------|----------------|
| **Invitado** | Usuario estándar | Subir fotos (hasta 80), ver/descargar/compartir, etiquetar personas, usar Tinder si es soltero |
| **Organizador** | Novios/Wedding Planner | Todo lo de Invitado + moderar contenido (hasta 500 fotos), eliminar fotos, ver reportes |

---

## ✨ Características Principales

### 📷 Galería de Fotos Compartida
- Subida múltiple de fotos desde dispositivo
- Procesamiento automático en 3 versiones (original, display, thumbnail)
- Etiquetado de personas usando lista oficial de invitados
- Filtros por personas y colecciones de eventos
- Compartir fotos mediante link
- Disponible desde 2 días antes del casamiento

### 💕 Tinder de Invitados
- Exclusivo para invitados marcados como solteros
- Creación de perfil con fotos capturadas en el momento
- Feed personalizado según preferencias (edad, género, orientación)
- Sistema de matching con notificaciones instantáneas
- Chat persistente con matches
- Disponible desde la hora de inicio del casamiento

### 🔐 Seguridad y Control
- Control de acceso basado en roles (RBAC)
- Cupos personalizados por usuario (80/500 fotos)
- Rate limiting para prevenir abuso
- Auditoría completa de acciones de moderación
- Almacenamiento seguro en Google Drive

---

## 🧩 Módulos del Sistema

```mermaid
graph LR
    A[👤 Usuario] --> B[🔐 Autenticación]
    B --> C[📷 Galería de Fotos]
    B --> D[💕 Tinder de Invitados]
    C --> E[☁️ Google Drive]
    D --> F[💬 Chat]
    C --> G[📋 Lista de Invitados]
    D --> G
    C --> H[🎉 Eventos/Actividades]
```

### Módulos Principales

1. **Galería de Fotos**
   - Subida y gestión de imágenes
   - Etiquetado colaborativo
   - Organización por colecciones
   - Moderación de contenido

2. **Tinder de Invitados**
   - Gestión de perfiles
   - Sistema de matching
   - Chat entre matches
   - Filtrado por preferencias

3. **Integraciones**
   - Lista de Invitados (fuente de verdad para usuarios)
   - Eventos/Actividades (colecciones de fotos)

---

## 📚 Documentación

Este proyecto cuenta con documentación técnica completa siguiendo estándares de ingeniería de software:

### 📄 Documentos Disponibles

| Documento | Descripción | Enlace |
|-----------|-------------|--------|
| **Requerimientos** | Especificación de Requisitos de Software (SRS) con RF y RNF | [📖 Ver](./requerimientos.md) |
| **Épicas** | 31 Historias de Usuario + 17 Tareas Técnicas para Jira | [📖 Ver](./epicas.md) |
| **Casos de Uso** | Diagramas y descripciones detalladas de casos de uso | [📖 Ver](./casos-de-uso.md) |
| **Diagrama de Clases** | Modelo de datos completo del sistema | [📖 Ver](./diagrama-clases.md) |
| **Diagramas de Secuencia** | 4 flujos principales con interacciones entre componentes | [📖 Ver](./diagrama-de-secuencias.md) |
| **Diagramas de Actividad** | 3 procesos críticos del negocio | [📖 Ver](./diagrama-de-actividad.md) |

### 🎨 Diagramas UML

Todos los diagramas están disponibles en formato **Mermaid** (se visualizan en GitHub) y **PlantUML** (para herramientas especializadas).

#### Casos de Uso Principales
- UC-GAL-1: Subir fotos
- UC-GAL-2: Ver/Descargar/Compartir
- UC-GAL-3: Etiquetar personas
- UC-GAL-4: Eliminar foto propia
- UC-TDR-1: Crear/Editar perfil
- UC-TDR-2: Explorar y dar like (+ match)

#### Diagramas de Secuencia
- Subida de fotos con validaciones
- Etiquetado de personas
- Creación de perfil de Tinder
- Proceso de matching

#### Diagramas de Actividad
- Flujo de subida de fotos
- Flujo de matching
- Flujo de creación de perfil

---

## 📊 Gestión del Proyecto

### Tablero Jira

El proyecto se gestiona utilizando Jira para el seguimiento de épicas, historias de usuario y tareas técnicas:

🔗 **[Tablero de Proyecto en Jira](https://santigodoy52.atlassian.net/jira/software/projects/GFTI/boards/1/backlog?atlOrigin=eyJpIjoiYzAwOTEzMDhhNzMwNGM0ZjgwM2VlYTBiYmEzNTU0OWYiLCJwIjoiaiJ9)**

### Organización del Backlog

El backlog está organizado en:
- **10 Épicas** principales
- **31 Historias de Usuario** (HU)
- **17 Tareas Técnicas** (TT)

Consulta el archivo [epicas.md](./epicas.md) para ver el detalle completo de todas las historias de usuario y tareas técnicas.

---

## 🏗️ Arquitectura

### Arquitectura General

```mermaid
graph TB
    subgraph "Frontend"
        A[📱 App Móvil<br/>React Native / Flutter]
        B[💻 App Web<br/>React / Next.js]
    end
    
    subgraph "Backend"
        C[🔧 API REST<br/>Node.js / NestJS]
        D[🔐 Autenticación<br/>JWT]
        E[⚙️ Procesador de Imágenes<br/>Sharp / ImageMagick]
    end
    
    subgraph "Almacenamiento"
        F[💾 Base de Datos<br/>PostgreSQL / MongoDB]
        G[☁️ Google Drive<br/>Imágenes]
    end
    
    subgraph "Servicios Externos"
        H[📋 API Lista de Invitados]
        I[🎉 API Eventos/Actividades]
        J[📲 Notificaciones<br/>WhatsApp / Push]
    end
    
    A --> C
    B --> C
    C --> D
    C --> E
    C --> F
    E --> G
    C --> H
    C --> I
    C --> J
```

### Componentes Clave

#### Backend
- **API REST**: Endpoints para todas las operaciones del sistema
- **Procesador de Imágenes**: Generación automática de versiones optimizadas
- **Motor de Matching**: Lógica de likes recíprocos y creación de matches
- **Sistema de Auditoría**: Logs inmutables de acciones de moderación

#### Almacenamiento
- **Base de datos relacional/NoSQL**: Metadata, usuarios, matches, mensajes
- **Google Drive**: Almacenamiento de imágenes (3 versiones por foto)
- **Redis** (opcional): Cache y rate limiting

#### Integraciones
- API de Lista de Invitados (validación de soltería, autocompletado)
- API de Eventos/Actividades (colecciones de fotos)
- Servicio de notificaciones (WhatsApp/Push)

---

## 🛠️ Tecnologías

### Stack Recomendado

#### Frontend
- **Móvil**: React Native o Flutter
- **Web**: React, Next.js, TypeScript
- **UI**: Tailwind CSS, Material-UI (paleta pastel)
- **Estado**: Redux Toolkit, Zustand

#### Backend
- **Framework**: Node.js con NestJS o Express
- **Base de Datos**: PostgreSQL (relacional) o MongoDB (NoSQL)
- **ORM**: Prisma, TypeORM, Mongoose
- **Autenticación**: JWT, Passport.js
- **Procesamiento de Imágenes**: Sharp, ImageMagick
- **Cola de Jobs**: Bull + Redis

#### Almacenamiento
- **Archivos**: Google Drive API
- **Cache**: Redis
- **CDN** (opcional): CloudFlare, AWS CloudFront

#### DevOps
- **Containerización**: Docker, Docker Compose
- **CI/CD**: GitHub Actions, GitLab CI
- **Hosting**: AWS, Google Cloud, Vercel (frontend)
- **Monitoreo**: Sentry, LogRocket

---

## 🚀 Instalación

### Prerrequisitos

- Node.js >= 18.x
- npm o yarn
- PostgreSQL/MongoDB
- Redis (opcional pero recomendado)
- Cuenta de Google Cloud (para Google Drive API)

### Clonar el Repositorio

```bash
git clone https://github.com/RicLagoria/siAcepto.git
cd siAcepto
```

### Configuración (cuando esté implementado)

```bash
# Backend
cd backend
npm install
cp .env.example .env
# Editar .env con tus credenciales

# Ejecutar migraciones
npm run migrate

# Iniciar servidor
npm run dev
```

```bash
# Frontend
cd frontend
npm install
cp .env.example .env
# Editar .env con la URL del backend

# Iniciar app
npm run dev
```

### Variables de Entorno

```env
# Backend
DATABASE_URL=postgresql://user:password@localhost:5432/siacepto
JWT_SECRET=tu_secreto_jwt
GOOGLE_DRIVE_CLIENT_ID=xxx
GOOGLE_DRIVE_CLIENT_SECRET=xxx
REDIS_URL=redis://localhost:6379

# Frontend
VITE_API_URL=http://localhost:3000
```

---

## 📈 Roadmap

### Fase 1: Fundamentos (Actual)
- [x] Documentación completa de requerimientos
- [x] Diseño de arquitectura y diagramas UML
- [x] Definición de épicas e historias de usuario
- [ ] Setup inicial del proyecto
- [ ] Configuración de base de datos

### Fase 2: Módulo Galería
- [ ] Backend: API de subida de fotos
- [ ] Backend: Procesamiento de imágenes
- [ ] Backend: Sistema de etiquetado
- [ ] Frontend: UI de galería
- [ ] Frontend: Filtros y búsqueda
- [ ] Integración con Google Drive

### Fase 3: Módulo Tinder
- [ ] Backend: Gestión de perfiles
- [ ] Backend: Motor de matching
- [ ] Backend: Sistema de chat
- [ ] Frontend: UI de perfil
- [ ] Frontend: Feed de exploración
- [ ] Frontend: Chat

### Fase 4: Integraciones
- [ ] Integración con Lista de Invitados
- [ ] Integración con Eventos/Actividades
- [ ] Sistema de notificaciones
- [ ] Moderación y auditoría

### Fase 5: Optimización y Lanzamiento
- [ ] Testing completo (unitario, integración, E2E)
- [ ] Optimización de rendimiento
- [ ] Pruebas de carga
- [ ] Deploy a producción
- [ ] Monitoreo y analytics

---

## 🎨 Diseño

### Paleta de Colores Pastel

La aplicación utiliza una paleta de colores pastel consistente en todos los módulos:

- **Primario**: Rosa pastel `#FFE1F0`
- **Secundario**: Azul pastel `#E1F0FF`
- **Acento**: Verde pastel `#E1FFE8`
- **Advertencia**: Amarillo pastel `#FFF4E1`
- **Error**: Rojo pastel `#FFE1E1`
- **Neutro**: Gris pastel `#F0F0F0`

### Responsive Design

- **Móvil**: < 768px (diseño mobile-first)
- **Tablet**: 768-1024px
- **Desktop**: > 1024px

Elementos táctiles mínimo 44x44px según guidelines de accesibilidad.

---

## 📊 Límites y Configuración

### Cupos de Fotos

| Tipo | Límite |
|------|--------|
| Invitado | 80 fotos |
| Organizador | 500 fotos |
| Evento (total) | 20,000 fotos |

### Límites de Imágenes

| Versión | Tamaño | Peso |
|---------|--------|------|
| Subida | - | ≤ 12 MB |
| Original | ≤ 36 MP | Variable |
| Display | ≤ 2048px | ~1.5 MB |
| Thumbnail | ≤ 400px | ~100 KB |

### Rate Limits

| Acción | Límite |
|--------|--------|
| Subida de fotos | 10 fotos / 5 min |
| Subida de fotos | 60 fotos / hora |
| Likes en Tinder | 200 / hora |

### Tinder - Configuración

| Parámetro | Valor |
|-----------|-------|
| Fotos de perfil | 1-6 |
| Bio | ≤ 280 caracteres |
| Rango de edad | 18-80 años |
| Etiquetas por foto | ≤ 10 |

---

## 🧪 Testing

### Estrategia de Testing

```bash
# Tests unitarios
npm run test

# Tests de integración
npm run test:integration

# Tests E2E
npm run test:e2e

# Coverage
npm run test:coverage
```

### Cobertura Mínima
- **Backend**: 70% de cobertura
- **Frontend**: 60% de cobertura
- **Tests críticos**: 100% (autenticación, matching, subida de fotos)

---

## 👥 Contribución

¡Las contribuciones son bienvenidas! Por favor sigue estos pasos:

1. **Fork** el proyecto
2. Crea una rama para tu feature (`git checkout -b feature/AmazingFeature`)
3. Commit tus cambios (`git commit -m 'Add some AmazingFeature'`)
4. Push a la rama (`git push origin feature/AmazingFeature`)
5. Abre un **Pull Request**

### Guías de Contribución

- Sigue los estándares de código del proyecto (ESLint, Prettier)
- Escribe tests para nuevas funcionalidades
- Actualiza la documentación según sea necesario
- Sigue los mensajes de commit convencionales (Conventional Commits)

---

## 📄 Licencia

Este proyecto está bajo la Licencia MIT - ver el archivo [LICENSE](LICENSE) para más detalles.

---

## 👨‍💻 Equipo

**Desarrolladores**: Santiago Godoy Cabrera, Jorge Iriarte Chamorro, Ricardo Augusto Lagoria, Mariano Zabala.  
**Email**: rlagoria@ubp.edu.ar  
**GitHub**: [@RicLagoria](https://github.com/RicLagoria)

---

## 🙏 Agradecimientos

- A todos los futuros usuarios de **siAcepto**
- A la comunidad open source por las herramientas utilizadas
- A los colaboradores que contribuyan al proyecto

---

## 📞 Soporte

¿Tienes preguntas o necesitas ayuda?

- 📧 Email: rlagoria@ubp.edu.ar
- 🐛 Issues: [GitHub Issues](https://github.com/RicLagoria/siAcepto/issues)
- 📖 Wiki: [Documentación completa](https://github.com/RicLagoria/siAcepto/wiki)

---

<div align="center">

**[⬆ Volver arriba](#-siacepto---aplicación-para-organización-de-casamientos)**

Hecho con ❤️ para parejas que quieren un casamiento memorable

</div>
