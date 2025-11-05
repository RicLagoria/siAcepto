# Diagramas de Actividad
## Aplicación de Organización de Casamientos
### Módulos: Galería de Fotos y Tinder de Invitados

---

## Índice de Diagramas

1. [Proceso de Subida de Fotos](#1-proceso-de-subida-de-fotos)
2. [Proceso de Matching en Tinder](#2-proceso-de-matching-en-tinder)
3. [Proceso de Creación de Perfil de Tinder](#3-proceso-de-creación-de-perfil-de-tinder)

---

## 1. Proceso de Subida de Fotos

### Descripción
Este diagrama muestra el flujo completo desde que un usuario selecciona fotos hasta que se publican en la galería compartida. Incluye todas las validaciones necesarias: cupo disponible, tamaño de archivo, formato, y resolución. El proceso permite subida múltiple con resultados parciales (algunas fotos pueden ser aceptadas y otras rechazadas).

### Actores
- **Usuario**: Invitado u Organizador que sube fotos

### Validaciones incluidas
- ✅ Verificación de cupo disponible (80 para Invitado, 500 para Organizador)
- ✅ Tamaño de archivo ≤ 12 MB
- ✅ Formato válido: JPG, JPEG, PNG, HEIC
- ✅ Resolución ≤ 36 MP

### Procesos automatizados
- Conversión de PNG/HEIC a JPG
- Generación de versión Display (≤2048px, ~1.5MB)
- Generación de versión Thumbnail (≤400px, ~100KB)

### Diagrama

```mermaid
flowchart TD
    Start([👤 Usuario: Agregar fotos]) --> Select[📱 Seleccionar 1..N fotos<br/>de la galería del dispositivo]
    Select --> ValidCupo{🔍 ¿Cupo disponible?}
    
    ValidCupo -->|❌ No| ErrorCupo[⚠️ Mostrar error:<br/>Cupo excedido<br/>Sugerir eliminar fotos propias]
    ErrorCupo --> End1([🔴 Fin - Operación cancelada])
    
    ValidCupo -->|✅ Sí| LoopStart{📋 ¿Hay más fotos<br/>por procesar?}
    
    LoopStart -->|No hay más| Summary[📊 Mostrar resumen:<br/>Exitosas / Fallidas]
    Summary --> UpdateFeed[🔄 Actualizar galería]
    UpdateFeed --> End2([🟢 Fin - Completado])
    
    LoopStart -->|Sí| NextPhoto[📷 Tomar siguiente foto]
    NextPhoto --> ValidSize{📏 ¿Tamaño ≤ 12MB?}
    
    ValidSize -->|❌ No| RejectSize[❌ Rechazar foto:<br/>Excede 12 MB]
    RejectSize --> LoopStart
    
    ValidSize -->|✅ Sí| ValidFormat{🎨 ¿Formato válido?<br/>JPG/PNG/HEIC}
    
    ValidFormat -->|❌ No| RejectFormat[❌ Rechazar foto:<br/>Formato no soportado]
    RejectFormat --> LoopStart
    
    ValidFormat -->|✅ Sí| ValidResolution{🖼️ ¿Resolución ≤ 36MP?}
    
    ValidResolution -->|❌ No| RejectResolution[❌ Rechazar foto:<br/>Excede 36 MP]
    RejectResolution --> LoopStart
    
    ValidResolution -->|✅ Sí| Upload[☁️ Subir a Storage/CDN<br/>Google Drive]
    Upload --> Convert[🔄 Convertir a JPG<br/>si es PNG/HEIC]
    Convert --> Generate[⚙️ Generar versiones:<br/>Display 2048px<br/>Thumbnail 400px]
    Generate --> SaveDB[💾 Guardar en BD:<br/>autor, fecha, URLs, estado]
    SaveDB --> Increment[➕ Incrementar contador<br/>de fotos del usuario]
    Increment --> LoopStart
    
    style Start fill:#e1f5e1
    style End1 fill:#ffe1e1
    style End2 fill:#e1f5e1
    style ErrorCupo fill:#ffcccc
    style RejectSize fill:#ffcccc
    style RejectFormat fill:#ffcccc
    style RejectResolution fill:#ffcccc
    style Summary fill:#cce5ff
    style Upload fill:#e1e8ff
    style Generate fill:#fff4e1
    style SaveDB fill:#e8f5e9
```

### Resultado esperado

Al finalizar el proceso, el usuario recibe un resumen:

**Ejemplo de resumen exitoso:**
```
✅ 5 de 5 fotos subidas correctamente
```

**Ejemplo de resumen parcial:**
```
✅ 3 de 5 fotos subidas correctamente
❌ 2 fotos rechazadas:
   • foto_beach.png - Excede 12 MB
   • foto_sunset.raw - Formato no soportado
```

**Ejemplo de rechazo total por cupo:**
```
❌ No se pueden subir fotos
Has alcanzado tu cupo de 80 fotos.
💡 Elimina algunas fotos para liberar espacio.
```

<details>
<summary>📄 Código PlantUML (click para expandir)</summary>

```plantuml
@startuml
title Proceso de Subida de Fotos

start
:Usuario: Tocar "Agregar fotos";
:Seleccionar 1..N archivos de la galería;

if (¿Cupo disponible?) then (No)
  :Mostrar error:
  **Cupo excedido**
  Sugerir eliminar fotos propias;
  stop
else (Sí)
  while (¿Hay más fotos por procesar?) is (Sí)
    :Tomar siguiente foto;
    
    if (¿Tamaño ≤ 12MB?) then (No)
      :Rechazar: Excede 12 MB;
    elseif (¿Formato válido JPG/PNG/HEIC?) then (No)
      :Rechazar: Formato no soportado;
    elseif (¿Resolución ≤ 36MP?) then (No)
      :Rechazar: Excede 36 MP;
    else (Todas las validaciones OK)
      :Subir original a Storage/CDN;
      :Convertir a JPG si es PNG/HEIC;
      :Generar versión Display (2048px);
      :Generar versión Thumbnail (400px);
      :Guardar registro en BD
      (autor, fecha, URLs, estado);
      :Incrementar contador de fotos;
    endif
  endwhile (No hay más)
  
  :Mostrar resumen:
  Exitosas / Fallidas;
  :Actualizar vista de galería;
  stop
endif

@enduml
```

</details>

### Casos de error comunes

| Error | Causa | Acción sugerida |
|-------|-------|----------------|
| Cupo excedido | Usuario alcanzó 80/500 fotos | Eliminar fotos propias para liberar cupo |
| Tamaño excedido | Foto > 12 MB | Comprimir imagen antes de subir |
| Formato inválido | Archivo .raw, .bmp, .tiff | Convertir a JPG/PNG antes de subir |
| Resolución excedida | Foto > 36 MP (ej: 8000x5000) | Reducir resolución de la imagen |
| Rate limit | >10 fotos en 5 min | Esperar unos minutos antes de continuar |

---

## 2. Proceso de Matching en Tinder

### Descripción
Este diagrama muestra el flujo de decisión cuando un usuario da "like" a otro perfil en el módulo Tinder. El sistema verifica si existe un like recíproco para crear un match, o simplemente registra el like si no hay reciprocidad aún.

### Actores
- **Usuario A**: Invitado soltero que da like
- **Usuario B**: Invitado soltero que recibe like (puede haber dado like previamente)

### Reglas de negocio
- ✅ Match se crea solo cuando hay like recíproco (A→B y B→A)
- ✅ No existe acción "dislike" negativa
- ✅ Al crear match, se notifica instantáneamente a ambos usuarios
- ✅ El match habilita automáticamente un chat entre ambos

### Diagrama

```mermaid
flowchart TD
    Start([💕 Usuario A: Like a perfil de B]) --> RegisterLike[💾 Registrar Like A→B<br/>en base de datos]
    RegisterLike --> CheckReciprocal{🔍 ¿Existe Like B→A<br/>previo?}
    
    CheckReciprocal -->|❌ No| NoMatch[📝 Solo registrar like<br/>Sin match aún]
    NoMatch --> WaitB[⏳ B verá perfil de A<br/>en su feed más adelante]
    WaitB --> NextProfile[➡️ Mostrar siguiente<br/>perfil a Usuario A]
    NextProfile --> End1([🔴 Fin - Sin match])
    
    CheckReciprocal -->|✅ Sí| CreateMatch[🎉 Crear Match A↔B<br/>¡Like recíproco!]
    CreateMatch --> CreateChat[💬 Crear Chat asociado<br/>al match]
    CreateChat --> NotifyA[🔔 Notificar a Usuario A:<br/>¡Es un match con B!]
    NotifyA --> NotifyB[🔔 Notificar a Usuario B:<br/>¡Es un match con A!]
    NotifyB --> ShowPopup[📱 Mostrar pop-up de match<br/>con foto y nombre del otro]
    ShowPopup --> EnableActions[✅ Habilitar acciones:<br/>Ver perfil completo<br/>Iniciar chat]
    EnableActions --> End2([🟢 Fin - Match creado])
    
    style Start fill:#ffe1f0
    style End1 fill:#e1e1e1
    style End2 fill:#e1ffe1
    style CreateMatch fill:#ffe1f0
    style NotifyA fill:#fff4e1
    style NotifyB fill:#fff4e1
    style ShowPopup fill:#ffe1f0
    style NoMatch fill:#f0f0f0
```

### Flujos posibles

#### Escenario 1: Like sin match (más común inicialmente)
1. Usuario A da like a Usuario B
2. Sistema registra like(A→B)
3. Sistema verifica: ¿existe like(B→A)? → **No**
4. Solo se guarda el like
5. Usuario A continúa viendo perfiles
6. **Resultado**: B eventualmente verá el perfil de A y podrá hacer match

#### Escenario 2: Like con match inmediato
1. Usuario A da like a Usuario B
2. Sistema registra like(A→B)
3. Sistema verifica: ¿existe like(B→A)? → **Sí** (B ya había dado like a A previamente)
4. Sistema crea Match(A↔B)
5. Sistema crea Chat asociado
6. **Ambos** reciben notificación push simultáneamente
7. Se muestra pop-up: "¡Es un match! 💕"
8. **Resultado**: Ambos pueden chatear inmediatamente

### Estructura de datos resultante

**Like registrado:**
```json
{
  "id": "like_abc123",
  "deUsuarioId": "usr_A",
  "paraUsuarioId": "usr_B",
  "timestamp": "2025-11-05T18:30:00Z"
}
```

**Match creado (cuando es recíproco):**
```json
{
  "id": "match_xyz789",
  "usuarioAId": "usr_A",
  "usuarioBId": "usr_B",
  "fechaMatch": "2025-11-05T18:30:00Z",
  "activo": true,
  "chatId": "chat_999"
}
```

<details>
<summary>📄 Código PlantUML (click para expandir)</summary>

```plantuml
@startuml
title Proceso de Matching en Tinder

start
:Usuario A: Like a perfil de Usuario B;
:Registrar Like(A→B) en BD;

if (¿Existe Like(B→A) previo?) then (No)
  :Solo registrar like;
  note right
    B verá el perfil de A
    en su feed más adelante
  end note
  :Mostrar siguiente perfil a A;
  stop
else (Sí - Like recíproco)
  :Crear Match(A↔B);
  :Crear Chat asociado al match;
  
  fork
    :Notificar a Usuario A;
    :Mostrar pop-up:
    "¡Es un match!"
    con foto de B;
  fork again
    :Notificar a Usuario B;
    :Mostrar pop-up:
    "¡Es un match!"
    con foto de A;
  end fork
  
  :Habilitar acciones:
  • Ver perfil completo
  • Iniciar chat;
  
  stop
endif

@enduml
```

</details>

### Notificaciones Push

Cuando se produce un match, ambos usuarios reciben:

**Título:** "¡Es un match! 💕"

**Contenido:** "A [Nombre del otro] le gustas"

**Acción al tocar:** Abre el perfil del match con opción de iniciar chat

---

## 3. Proceso de Creación de Perfil de Tinder

### Descripción
Este diagrama muestra el flujo completo para que un invitado soltero cree su perfil en el módulo Tinder. El proceso incluye la solicitud de permisos de cámara, captura de fotos, completado del formulario con datos personales y configuración de preferencias de búsqueda.

### Actores
- **Usuario**: Invitado soltero (con bandera `esSoltero = true`)
- **Cámara del dispositivo**: Hardware necesario para capturar fotos

### Precondiciones
- Usuario marcado como soltero en la lista de invitados
- Módulo Tinder disponible (desde hora de inicio del casamiento)
- Dispositivo con cámara funcional

### Restricciones importantes
- ⚠️ **Solo fotos de cámara**: No se permiten fotos de la galería del dispositivo
- 📸 **Rango de fotos**: Mínimo 1, máximo 6 fotos
- ✍️ **Bio limitada**: Máximo 280 caracteres
- 🎂 **Rango de edad**: 18-80 años

### Diagrama

```mermaid
flowchart TD
    Start([👤 Usuario: Abrir Tinder]) --> CheckSingle{🔍 ¿Usuario es soltero?}
    
    CheckSingle -->|❌ No| DenySingle[🚫 Módulo no disponible<br/>Solo para solteros]
    DenySingle --> End1([🔴 Fin - Acceso denegado])
    
    CheckSingle -->|✅ Sí| CheckTime{⏰ ¿Casamiento iniciado?}
    
    CheckTime -->|❌ No| DenyTime[🕐 Módulo no disponible aún<br/>Disponible desde hora de inicio]
    DenyTime --> End2([🔴 Fin - Muy temprano])
    
    CheckTime -->|✅ Sí| RequestCamera[📷 Solicitar permiso<br/>de cámara]
    RequestCamera --> CheckPermission{🔐 ¿Permiso concedido?}
    
    CheckPermission -->|❌ No| DenyCamera[⚠️ Mostrar instrucciones:<br/>Habilitar cámara en configuración]
    DenyCamera --> End3([🔴 Fin - Sin permiso])
    
    CheckPermission -->|✅ Sí| EnableCamera[✅ Habilitar cámara]
    EnableCamera --> PhotoLoop{📸 ¿Capturar foto?}
    
    PhotoLoop -->|Sí| CapturePhoto[📷 Capturar foto<br/>con cámara]
    CapturePhoto --> SaveTemp[💾 Guardar temporalmente]
    SaveTemp --> CountPhotos{🔢 ¿Cantidad de fotos?}
    
    CountPhotos -->|< 6 fotos| PhotoLoop
    CountPhotos -->|6 fotos| FormStart[📝 Ir a formulario]
    
    PhotoLoop -->|No, continuar| CheckMin{🔍 ¿Al menos 1 foto?}
    
    CheckMin -->|❌ No| ErrorMinPhotos[❌ Error: Mínimo 1 foto<br/>requerida para perfil]
    ErrorMinPhotos --> PhotoLoop
    
    CheckMin -->|✅ Sí| FormStart
    
    FormStart --> FillForm[✍️ Usuario completa:<br/>• Nombre<br/>• Edad<br/>• Género<br/>• Orientación<br/>• Bio máx 280 chars]
    FillForm --> ValidateBio{📏 ¿Bio ≤ 280 chars?}
    
    ValidateBio -->|❌ No| ErrorBio[❌ Error: Bio muy larga<br/>Máximo 280 caracteres]
    ErrorBio --> FillForm
    
    ValidateBio -->|✅ Sí| SetPreferences[⚙️ Configurar preferencias:<br/>• Rango edad 18-80<br/>• Géneros preferidos<br/>• Orientaciones preferidas]
    SetPreferences --> UploadPhotos[☁️ Subir fotos a Storage]
    UploadPhotos --> SaveProfile[💾 Guardar perfil en BD]
    SaveProfile --> ActivateProfile[✅ Activar perfil]
    ActivateProfile --> ShowConfirmation[🎉 Confirmar:<br/>Perfil creado exitosamente]
    ShowConfirmation --> RedirectFeed[➡️ Redirigir al Feed<br/>de exploración]
    RedirectFeed --> End4([🟢 Fin - Perfil activo])
    
    style Start fill:#ffe1f0
    style End1 fill:#ffe1e1
    style End2 fill:#ffe1e1
    style End3 fill:#ffe1e1
    style End4 fill:#e1ffe1
    style DenySingle fill:#ffcccc
    style DenyTime fill:#ffcccc
    style DenyCamera fill:#fff4cc
    style ErrorMinPhotos fill:#ffcccc
    style ErrorBio fill:#ffcccc
    style ShowConfirmation fill:#e1ffe1
    style ActivateProfile fill:#e1f5e1
```

### Validaciones del formulario

| Campo | Validación | Mensaje de error |
|-------|-----------|------------------|
| Fotos | 1-6 fotos | "Debes tener al menos 1 foto" o "Máximo 6 fotos" |
| Nombre | No vacío | "El nombre es obligatorio" |
| Edad | Número válido | "Ingresa una edad válida" |
| Género | Selección obligatoria | "Selecciona tu género" |
| Orientación | Selección obligatoria | "Selecciona tu orientación" |
| Bio | ≤ 280 caracteres | "La biografía no puede exceder 280 caracteres" |
| Pref. Edad | 18-80 años | "Rango de edad debe estar entre 18 y 80" |
| Pref. Género | Al menos 1 | "Selecciona al menos un género de interés" |
| Pref. Orientación | Al menos 1 | "Selecciona al menos una orientación" |

### Ejemplo de perfil completo

```json
{
  "id": "perfil_123",
  "usuarioId": "usr_456",
  "nombre": "María García",
  "edad": 28,
  "genero": "FEMENINO",
  "orientacion": "BISEXUAL",
  "biografia": "🍷 Sommelier amateur | 🏔️ Montañista los fines de semana | 📚 Siempre con un libro en la mochila. Me encanta viajar y conocer nuevas culturas.",
  "fotosUrls": [
    "https://cdn.example.com/perfil_123_foto1.jpg",
    "https://cdn.example.com/perfil_123_foto2.jpg",
    "https://cdn.example.com/perfil_123_foto3.jpg"
  ],
  "preferencias": {
    "edadMinima": 25,
    "edadMaxima": 35,
    "generosPreferidos": ["MASCULINO", "FEMENINO"],
    "orientacionesPreferidas": ["HETEROSEXUAL", "BISEXUAL", "HOMOSEXUAL"]
  },
  "fechaCreacion": "2025-11-05T10:00:00Z",
  "activo": true
}
```

<details>
<summary>📄 Código PlantUML (click para expandir)</summary>

```plantuml
@startuml
title Proceso de Creación de Perfil de Tinder

start

:Usuario: Abrir módulo Tinder;

if (¿Usuario es soltero?) then (No)
  :Mostrar: Módulo solo para solteros;
  stop
else (Sí)
  if (¿Casamiento iniciado?) then (No)
    :Mostrar: Disponible desde hora de inicio;
    stop
  else (Sí)
    :Solicitar permiso de cámara;
    
    if (¿Permiso concedido?) then (No)
      :Mostrar instrucciones:
      Habilitar cámara en configuración;
      stop
    else (Sí)
      :Habilitar cámara del dispositivo;
      
      while (¿Capturar más fotos? Y <6) is (Sí)
        :Usuario: Tomar foto con cámara;
        :Guardar foto temporalmente;
      endwhile (No)
      
      if (¿Al menos 1 foto?) then (No)
        :Error: Mínimo 1 foto requerida;
        stop
      else (Sí)
        :Usuario: Completar formulario
        • Nombre
        • Edad
        • Género
        • Orientación
        • Bio (≤280 chars);
        
        if (¿Bio ≤ 280 caracteres?) then (No)
          :Error: Bio muy larga;
          stop
        else (Sí)
          :Usuario: Configurar preferencias
          • Rango edad (18-80)
          • Géneros preferidos
          • Orientaciones preferidas;
          
          :Subir fotos a Storage/CDN;
          :Guardar perfil en BD;
          :Activar perfil;
          :Confirmación: Perfil creado;
          :Redirigir al Feed de exploración;
          stop
        endif
      endif
    endif
  endif
endif

@enduml
```

</details>

### Estados del perfil

Un perfil de Tinder puede tener los siguientes estados:

| Estado | Descripción | Visible en feed |
|--------|-------------|----------------|
| **Borrador** | Perfil incompleto, en proceso de creación | ❌ No |
| **Activo** | Perfil completo y publicado | ✅ Sí |
| **Pausado** | Usuario pausó temporalmente su perfil | ❌ No |
| **Inactivo** | Usuario desactivó su perfil | ❌ No |

### Edición de perfil

Una vez creado el perfil, el usuario puede:
- ✏️ Editar bio, edad, género, orientación
- 📸 Capturar nuevas fotos (reemplazando las anteriores)
- ⚙️ Modificar preferencias de búsqueda
- ⏸️ Pausar/reactivar perfil
- 🗑️ Eliminar perfil completamente

---

## Resumen de Diagramas

| Diagrama | Complejidad | Decisiones clave | Loops |
|----------|-------------|------------------|-------|
| **Subida de Fotos** | Alta | 4 validaciones (cupo, tamaño, formato, resolución) | Sí (por cada foto) |
| **Matching** | Media | 1 decisión (like recíproco) | No |
| **Creación de Perfil** | Alta | 5 validaciones (permisos, fotos, bio, edad, preferencias) | Sí (captura de fotos) |

---

## Convenciones utilizadas

### Símbolos
- 🔴 Fin con error/cancelación
- 🟢 Fin exitoso
- ⚠️ Advertencia
- ❌ Validación fallida
- ✅ Validación exitosa
- 🔍 Verificación/consulta
- 💾 Almacenamiento
- 📱 Interacción con UI
- 🔔 Notificación
- ⏳ Espera/proceso asíncrono

### Colores (en diagramas Mermaid)
- **Verde claro**: Inicio exitoso / Fin exitoso
- **Rojo claro**: Fin con error
- **Amarillo claro**: Advertencias / Notificaciones
- **Azul claro**: Resúmenes / Información
- **Gris claro**: Estados neutrales

---

**Documento generado para:** Aplicación de Organización de Casamientos  
**Versión:** 1.0  
**Fecha:** Noviembre 2025

