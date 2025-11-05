# Especificación de Requisitos de Software (SRS)
## Aplicación de Organización de Casamientos
### Módulos: Galería de Fotos y Tinder de Invitados

---

## 1. Introducción

### 1.1 Propósito
Este documento especifica los requisitos funcionales y no funcionales de la aplicación de organización de casamientos, enfocándose en dos módulos principales: **Galería de Fotos** y **Tinder de Invitados**. El propósito es alinear a todos los stakeholders (novios, organizadores, equipo de diseño y desarrollo) sobre el alcance y comportamiento esperado del sistema.

### 1.2 Alcance

**Módulos incluidos:**
- Galería de fotos compartida
- Tinder de Invitados (perfil, exploración con likes/matches, chat)
- Integración con Lista de Invitados
- Integración con Eventos/Actividades

**Usuarios del sistema:**
- **Invitado**: Usuario estándar que puede subir fotos, etiquetar, ver contenido y, si está marcado como soltero, usar el módulo Tinder
- **Organizador**: Novios o wedding planner con permisos adicionales de moderación sobre la galería

**Exclusiones:**
- No existe rol "Administrador" del sistema
- No existe acción "dislike" en Tinder (solo like y saltar)
- No se incluyen otros módulos mencionados en requisitos iniciales (playlist Spotify, lista de regalos, configuración de mesas, etc.)

### 1.3 Definiciones, Acrónimos y Abreviaturas

- **Organizador**: Novios o wedding planner con permisos de moderación
- **Match**: Like recíproco entre dos perfiles de Tinder
- **Cupo**: Límite de cantidad de fotos que puede subir un usuario
- **Colección**: Categoría o álbum asociado a un evento/actividad específica
- **Etiqueta**: Identificación de una persona en una foto mediante su nombre de la lista de invitados
- **RF**: Requisito Funcional
- **RNF**: Requisito No Funcional
- **RBAC**: Control de Acceso Basado en Roles

### 1.4 Referencias
- Requisitos del proyecto proporcionados por el cliente
- IEEE 29148/830 - Guía de especificación de requisitos de software
- Documentación de integración con módulo de Lista de Invitados
- Documentación de integración con módulo de Eventos/Actividades

---

## 2. Vista General del Producto

### 2.1 Perspectiva del Sistema
La aplicación es un sistema móvil y web ligero, centrado en el evento del casamiento. Los módulos (Galería y Tinder) son independientes a nivel de interfaz de usuario pero comparten la autenticación básica de invitados y servicios comunes de backend.

### 2.2 Usuarios y Perfiles

| Rol | Descripción | Permisos |
|-----|-------------|----------|
| **Invitado** | Usuario estándar | Subir fotos, ver, descargar, compartir, etiquetar fotos. Usar Tinder si está marcado como soltero |
| **Organizador** | Novios o wedding planner | Todos los permisos de Invitado + moderar contenido de galería (ocultar, eliminar, ver reportes) |

### 2.3 Supuestos y Dependencias

**Supuestos:**
- Los usuarios tendrán conectividad a internet durante el evento
- Los dispositivos móviles cuentan con cámara funcional (requerido para Tinder)
- Existe una lista oficial de invitados disponible para validaciones y autocompletado

**Dependencias:**
- Endpoint del módulo "Lista de Invitados" para consultar datos de usuarios y bandera de soltería
- Endpoint del módulo "Eventos/Actividades" para obtener colecciones disponibles
- Servicio de almacenamiento externo (ej: Google Drive) para imágenes
- Servicio de notificaciones (WhatsApp para notificaciones push)

---

## 3. Requisitos Funcionales

### 3.1 Galería de Fotos

#### RF-GAL-1: Subir fotos [Prioridad: MUST]
El sistema **debe** permitir a invitados y organizadores subir fotos desde la galería de su dispositivo.

**Criterios de aceptación:**
- Soporta formatos JPG, JPEG, PNG, HEIC
- Tamaño máximo por foto: 12 MB
- Resolución máxima: 36 MP (megapíxeles)
- Permite subida múltiple (selección de varias fotos)
- Muestra progreso de subida
- Al completar, la foto aparece en la galería con identificación del autor y fecha
- PNG y HEIC se convierten automáticamente a JPG en el backend

#### RF-GAL-2: Ver y navegar fotos [Prioridad: MUST]
El sistema **debe** mostrar todas las fotos en una vista de galería (grid de miniaturas) y permitir ver fotos individuales en detalle.

**Criterios de aceptación:**
- Vista de galería muestra miniaturas ordenadas por fecha (más recientes primero)
- Al seleccionar una foto, se abre en vista de detalle
- En vista de detalle se pueden navegar fotos con botones anterior/siguiente o swipe

#### RF-GAL-3: Descargar y compartir fotos [Prioridad: MUST]
El sistema **debe** permitir a todos los usuarios descargar fotos a su dispositivo y compartir fotos mediante link.

**Criterios de aceptación:**
- Botón de descarga descarga la versión display de la foto (no thumbnail)
- Botón de compartir genera un link público temporal a la foto
- Las acciones están disponibles en la vista de detalle de foto

#### RF-GAL-4: Etiquetar personas en fotos [Prioridad: MUST]
El sistema **debe** permitir etiquetar personas en las fotos usando únicamente nombres de la lista oficial de invitados.

**Criterios de aceptación:**
- Al hacer clic sobre una foto, se puede agregar una etiqueta sobre una cara/persona
- El campo de búsqueda de nombre autocompletará solo con nombres de la lista oficial de invitados
- No se permiten etiquetas de texto libre
- Máximo 10 etiquetas por foto
- Las etiquetas se visualizan como badges sobre la foto o debajo de ella

#### RF-GAL-5: Filtrar fotos por personas etiquetadas [Prioridad: MUST]
El sistema **debe** permitir filtrar la galería por las personas etiquetadas en las fotos.

**Criterios de aceptación:**
- Botón de filtro muestra lista de personas que han sido etiquetadas
- Se pueden seleccionar una o múltiples personas para filtrar
- La galería muestra solo las fotos que contienen a las personas seleccionadas
- Se puede combinar con filtro de colecciones

#### RF-GAL-6: Eliminar fotos propias [Prioridad: SHOULD]
El sistema **debe** permitir que solo el autor de una foto pueda eliminarla.

**Criterios de aceptación:**
- El botón "Eliminar" solo aparece en fotos del usuario actual
- Al eliminar, se solicita confirmación
- La foto se elimina permanentemente y se libera el cupo del usuario

#### RF-GAL-7: Agregar fotos a colecciones [Prioridad: SHOULD]
El sistema **debe** permitir categorizar fotos en colecciones basadas en eventos/actividades.

**Criterios de aceptación:**
- Al subir una foto, se puede seleccionar a qué colección pertenece
- Las colecciones disponibles provienen del endpoint de Eventos/Actividades
- Existe una colección "General" por defecto
- El autor puede cambiar la colección de su foto en cualquier momento
- Un usuario puede agregar una foto de otro usuario a una colección adicional (la foto puede pertenecer a múltiples colecciones)
- Si un tercero agrega una foto a una colección, el autor recibe notificación y puede aceptar o rechazar

#### RF-GAL-8: Filtrar fotos por colecciones [Prioridad: SHOULD]
El sistema **debe** permitir filtrar la galería por colecciones de eventos/actividades.

**Criterios de aceptación:**
- Los filtros se organizan en dos pestañas: "Etiquetas" y "Colecciones"
- Se pueden seleccionar múltiples colecciones
- Los filtros de etiquetas y colecciones son combinables

#### RF-GAL-9: Ver detalles de foto [Prioridad: SHOULD]
El sistema **debe** mostrar metadata de la foto mediante un botón de opciones (3 puntos).

**Criterios de aceptación:**
- Muestra: nombre del archivo, tamaño, fecha de subida, autor
- Se visualiza como overlay transparente sobre la foto

### 3.2 Tinder de Invitados

#### RF-TDR-1: Crear y editar perfil [Prioridad: MUST]
El sistema **debe** permitir a invitados marcados como solteros crear un perfil con fotos tomadas con la cámara, datos personales y preferencias.

**Criterios de aceptación:**
- Acceso exclusivo desde la hora de inicio del casamiento
- Solo disponible para usuarios con bandera "soltero" activa
- Captura de fotos usando la cámara del dispositivo (no permite galería)
- Permite tomar entre 1 y 6 fotos
- Botón para alternar entre cámara frontal y trasera
- Formulario incluye: nombre (predeterminado de lista de invitados, editable), edad, género, orientación sexual, descripción (máx 280 caracteres)
- Configuración de preferencias: rango de edad (18-80), género preferido, orientación preferida
- Las preferencias determinan qué perfiles aparecerán en el feed

#### RF-TDR-2: Explorar perfiles y dar like [Prioridad: MUST]
El sistema **debe** mostrar perfiles de otros usuarios según las preferencias configuradas y permitir dar like.

**Criterios de aceptación:**
- Feed muestra perfiles de forma aleatoria filtrados por preferencias
- Cada perfil muestra: foto principal (carrusel si hay varias), nombre, edad, descripción
- Botones: Like y Saltar
- No existe acción "dislike" (saltar no registra acción negativa)
- No se repiten perfiles ya likeados o saltados recientemente
- Rate limit: máximo 200 likes por hora

#### RF-TDR-3: Notificación y visualización de match [Prioridad: MUST]
El sistema **debe** notificar cuando dos usuarios se dan like mutuamente y permitir acceso al perfil del match.

**Criterios de aceptación:**
- Al producirse match (like recíproco), aparece notificación pop-up inmediata
- La notificación muestra el nombre del otro usuario
- Al hacer click en la notificación se abre el perfil completo del match
- El perfil muestra carrusel de fotos, datos (nombre, edad, descripción)
- Incluye botón para iniciar chat

#### RF-TDR-4: Chat entre matches [Prioridad: SHOULD]
El sistema **debe** permitir conversación mediante chat entre usuarios que han hecho match.

**Criterios de aceptación:**
- Vista de chat muestra mensajes como burbujas de diálogo
- Mensajes propios alineados a la derecha (color primario)
- Mensajes del otro alineados a la izquierda (color secundario)
- Campo de texto para escribir mensaje e ícono de enviar
- Los chats persisten fuera del horario del casamiento
- Lista de chats muestra: foto del otro, nombre, fragmento del último mensaje

#### RF-TDR-5: Navegación entre Tinder y Chats [Prioridad: SHOULD]
El sistema **debe** permitir navegar entre la vista de exploración de perfiles y la lista de chats mediante pestañas.

**Criterios de aceptación:**
- Dos pestañas visibles: "TINDER" y "CHATS"
- Pestaña TINDER muestra el feed de perfiles
- Pestaña CHATS muestra lista de todos los matches con los que se puede chatear
- Las pestañas están disponibles en todas las vistas excepto en configuración inicial de perfil

#### RF-TDR-6: Editar preferencias [Prioridad: SHOULD]
El sistema **debe** permitir editar las preferencias de búsqueda desde la vista de Tinder.

**Criterios de aceptación:**
- Botón de configuración en vista de feed
- Permite editar rango de edad, género preferido, orientación preferida
- Al guardar, el feed se actualiza con los nuevos filtros

### 3.3 Integraciones

#### RF-INT-1: Integración con Lista de Invitados [Prioridad: MUST]
El sistema **debe** obtener información de usuarios desde el módulo de Lista de Invitados.

**Criterios de aceptación:**
- Consulta endpoint de Lista de Invitados para obtener: nombre, edad, bandera de soltería
- La bandera de soltería determina si el módulo Tinder está habilitado para ese usuario
- Los nombres de la lista se usan para autocompletar etiquetas en fotos
- El acceso al módulo Tinder se valida en cada carga consultando el endpoint

#### RF-INT-2: Integración con Eventos/Actividades [Prioridad: SHOULD]
El sistema **debe** obtener la lista de eventos/actividades para crear colecciones de fotos.

**Criterios de aceptación:**
- Consulta endpoint de Eventos/Actividades para obtener lista de eventos
- Cada evento se convierte en una colección disponible para categorizar fotos
- La colección "General" existe por defecto aunque no venga del endpoint
- Las colecciones se actualizan dinámicamente si cambia la lista de eventos

---

## 4. Requisitos No Funcionales

### 4.1 Seguridad y Control de Acceso (RNF-SEC)

#### RNF-SEC-1: Control de acceso basado en roles (RBAC) [Prioridad: MUST]
El sistema **debe** implementar control de acceso basado en roles para restringir funcionalidades según el tipo de usuario.

**Criterios:**
- Solo Organizador puede: ocultar/mostrar fotos, eliminar fotos de otros, ver reportes de moderación
- Invitados solo pueden eliminar sus propias fotos
- El acceso a Tinder se valida contra la bandera de soltería del usuario

#### RNF-SEC-2: Auditoría de acciones de moderación [Prioridad: MUST]
El sistema **debe** registrar todas las acciones de moderación en un log inmutable y trazable.

**Criterios:**
- Cada acción de moderación registra: quién (usuario), qué (acción), cuándo (timestamp), sobre qué (recurso afectado)
- El log es de solo lectura y no se puede modificar retroactivamente

### 4.2 Capacidad y Límites (RNF-CAP)

#### RNF-CAP-1: Límites de tamaño de fotos [Prioridad: MUST]
El sistema **debe** procesar fotos con los siguientes límites de tamaño:

| Versión | Tamaño máximo lado mayor | Peso máximo | Formato |
|---------|-------------------------|-------------|---------|
| **Subida** | N/A | 12 MB | JPG, JPEG, PNG, HEIC |
| **Original almacenado** | 36 MP de resolución | Variable | JPG |
| **Display** | 2048 px | 1.5 MB | JPG |
| **Thumbnail** | 400 px | 100 KB | JPG |

**Criterios:**
- PNG y HEIC se convierten a JPG automáticamente en el backend
- Si la foto excede 12 MB en subida, se rechaza con mensaje claro
- Si la foto excede 36 MP de resolución, se rechaza con mensaje explicativo
- El backend genera automáticamente versiones display y thumbnail

#### RNF-CAP-2: Cupos de fotos por usuario [Prioridad: MUST]
El sistema **debe** implementar los siguientes cupos de fotos:

| Tipo de usuario | Cupo |
|----------------|------|
| Invitado | 80 fotos |
| Organizador | 500 fotos |
| Evento (total) | 20,000 fotos |

**Criterios:**
- Al alcanzar el cupo, el sistema bloquea nuevas subidas
- Mensaje claro indica que se alcanzó el cupo y sugiere eliminar fotos propias para liberar espacio
- El contador de cupo se actualiza en tiempo real

#### RNF-CAP-3: Límite de etiquetas por foto [Prioridad: MUST]
El sistema **debe** permitir máximo 10 etiquetas de personas por foto.

#### RNF-CAP-4: Mensajería clara de errores [Prioridad: MUST]
El sistema **debe** proporcionar mensajes claros y accionables ante rechazos o errores.

**Criterios:**
- Cada error explica la causa específica
- Sugiere acción correctiva cuando sea posible
- Ejemplos: "La foto excede el tamaño máximo de 12 MB. Por favor, selecciona una foto más pequeña" o "Has alcanzado tu cupo de 80 fotos. Elimina algunas fotos para subir nuevas"

#### RNF-CAP-5: Rate limits [Prioridad: SHOULD]
El sistema **debe** implementar límites de tasa para prevenir abuso:

| Acción | Límite |
|--------|--------|
| Subida de fotos | 10 fotos / 5 minutos |
| Subida de fotos | 60 fotos / hora |
| Likes en Tinder | 200 likes / hora |

**Criterios:**
- Al exceder el límite, se muestra mensaje temporal indicando cuándo podrá volver a realizar la acción
- Los límites se resetean automáticamente según el período establecido

### 4.3 Usabilidad (RNF-UX)

#### RNF-UX-1: Paleta de colores pastel [Prioridad: MUST]
El sistema **debe** usar una paleta de colores pastel consistente en toda la aplicación y sus módulos.

#### RNF-UX-2: Diseño responsive [Prioridad: MUST]
El sistema **debe** ser completamente responsive, adaptándose a dispositivos móviles y de escritorio.

**Criterios:**
- Diseño mobile-first
- Breakpoints para tablet y desktop
- Elementos táctiles con tamaño mínimo de 44x44 px

#### RNF-UX-3: Estados de carga [Prioridad: SHOULD]
El sistema **debe** mostrar indicadores de carga durante operaciones asíncronas (subida de fotos, consultas a API).

### 4.4 Disponibilidad (RNF-AVA)

#### RNF-AVA-1: Período de disponibilidad de Galería [Prioridad: MUST]
El sistema **debe** permitir acceso a la galería desde 2 días antes del casamiento, sin fecha de fin por defecto.

**Criterios:**
- El período es configurable por evento
- Por defecto: inicio 2 días antes, sin límite de fin

#### RNF-AVA-2: Período de disponibilidad de Tinder [Prioridad: MUST]
El sistema **debe** habilitar el módulo Tinder desde la hora de inicio del casamiento.

**Criterios:**
- Antes de la hora de inicio, el módulo no es accesible
- Los chats persisten indefinidamente después del evento

### 4.5 Rendimiento (RNF-REN)

#### RNF-REN-1: Tiempo de carga de galería [Prioridad: SHOULD]
El sistema **debe** cargar la vista inicial de galería (primeros 50 thumbnails) en menos de 2 segundos bajo condiciones normales de red.

#### RNF-REN-2: Tiempo de procesamiento de fotos [Prioridad: SHOULD]
El sistema **debe** procesar una foto (validación + conversión + generación de thumbnails) en menos de 5 segundos.

### 4.6 Almacenamiento (RNF-ALM)

#### RNF-ALM-1: Almacenamiento de imágenes [Prioridad: MUST]
Las imágenes **deben** almacenarse en Google Drive (configurado por los novios).

#### RNF-ALM-2: Base de datos [Prioridad: MUST]
Los datos estructurados **deben** almacenarse en servidores propios (base de datos relacional o NoSQL según diseño técnico).

---

## 5. Reglas de Negocio

### RN-1: Etiquetas solo de lista oficial
Las etiquetas de personas en fotos **solo** pueden contener nombres que existan en la lista oficial de invitados. No se permiten etiquetas de texto libre.

### RN-2: Participación en Tinder por bandera
Solo usuarios con la bandera "soltero" activa en la lista de invitados pueden acceder al módulo Tinder.

### RN-3: Fotos de perfil Tinder exclusivas de cámara
Las fotos del perfil de Tinder **solo** pueden ser capturadas con la cámara de la aplicación. No se permite subir fotos de la galería del dispositivo.

### RN-4: Feed filtrado por preferencias
El feed de Tinder muestra únicamente perfiles que coincidan con las preferencias de edad, género y orientación configuradas por el usuario.

### RN-5: Colecciones desde Eventos/Actividades
Las colecciones de fotos disponibles se obtienen exclusivamente del módulo de Eventos/Actividades, excepto la colección "General" que existe por defecto.

### RN-6: Match requiere like recíproco
Un match solo se produce cuando dos usuarios se han dado like mutuamente. No hay match unilateral.

### RN-7: Propiedad de foto
Solo el usuario que subió una foto puede eliminarla, excepto el Organizador que puede eliminar cualquier foto por motivos de moderación.

---

## 6. Requisitos de Interfaces Externas

### 6.1 Interfaz de Usuario

#### Galería de Fotos
- **Vista de galería (grid)**: Miniaturas en cuadrícula, botón flotante "+" para agregar fotos, botón flotante de filtro
- **Vista de detalle de foto**: Foto grande, botones anterior/siguiente, barra inferior con acciones (Compartir, Descargar, Etiquetar, Eliminar si es autor), botón de opciones (3 puntos) para ver detalles
- **Modal de etiquetado**: Click sobre la foto para agregar etiqueta, campo de búsqueda con autocompletado
- **Modal de filtros**: Dos pestañas (Etiquetas / Colecciones), checkboxes múltiples, botón aplicar
- **Panel de moderación** (solo Organizador): Lista de fotos reportadas, botones ocultar/mostrar, eliminar

#### Tinder de Invitados
- **Pantalla de captura**: Vista de cámara en vivo, botón de captura, botón de alternancia de cámara, botón para ver fotos capturadas
- **Galería interna**: Carrusel de fotos capturadas, botones navegar, botones cancelar/aceptar
- **Formulario de perfil**: Campos de texto (nombre, edad, descripción), selects (género, orientación), sliders (rango de edad), botón guardar
- **Feed de perfiles**: Carta con foto/carrusel, nombre, edad, descripción, botones Like/Saltar
- **Notificación de match**: Pop-up con nombre del match, botón para ver perfil
- **Perfil de match**: Carrusel de fotos, datos textuales, botón "Iniciar chat"
- **Vista de chat**: Área de mensajes (burbujas), campo de texto, botón enviar
- **Lista de chats**: Items con foto, nombre, último mensaje
- **Pestañas de navegación**: TINDER / CHATS
- **Configuración de preferencias**: Modal con selects y sliders, botón guardar

### 6.2 Interfaces de Datos

#### Entidades principales:

**Usuario**
- id, nombre, rol (Invitado/Organizador), estadoSoltero (boolean)

**Foto**
- id, autorId, fecha, tamaño, urlOriginal, urlDisplay, urlThumb, estadoModeracion, colecciones[]

**Etiqueta**
- id, fotoId, invitadoId (referencia a lista de invitados)

**Coleccion**
- id, nombre, eventoId (referencia a Eventos/Actividades)

**PerfilTinder**
- id, usuarioId, bio, edad, genero, orientacion, fotos[], preferenciasEdad, preferenciasGenero, preferenciasOrientacion

**Like**
- id, deUsuarioId, paraUsuarioId, fecha

**Match**
- id, usuarioA_Id, usuarioB_Id, fecha

**Mensaje**
- id, matchId, deUsuarioId, texto, fecha, leido

#### Endpoints externos consumidos:

**Lista de Invitados**
- `GET /api/invitados/{id}` → Retorna: { id, nombre, edad, esSoltero }
- `GET /api/invitados` → Retorna lista completa para autocompletado de etiquetas

**Eventos/Actividades**
- `GET /api/eventos` → Retorna: [{ id, nombre, fecha, hora }]

---

## 7. Anexo: Parámetros Configurables

Todos los siguientes parámetros son configurables a nivel de evento:

| Parámetro | Valor por defecto |
|-----------|-------------------|
| Tamaño máximo de subida | 12 MB |
| Resolución máxima original | 36 MP |
| Tamaño lado mayor display | 2048 px |
| Peso máximo display | 1.5 MB |
| Tamaño lado mayor thumbnail | 400 px |
| Peso máximo thumbnail | 100 KB |
| Cupo Invitado | 80 fotos |
| Cupo Organizador | 500 fotos |
| Cupo total del evento | 20,000 fotos |
| Etiquetas máximas por foto | 10 |
| Rate limit subida (corto plazo) | 10 fotos / 5 minutos |
| Rate limit subida (largo plazo) | 60 fotos / hora |
| Rate limit likes | 200 / hora |
| Rango de edad mínimo Tinder | 18 años |
| Rango de edad máximo Tinder | 80 años |
| Fotos mínimas perfil Tinder | 1 |
| Fotos máximas perfil Tinder | 6 |
| Caracteres máximos bio Tinder | 280 |
| Inicio disponibilidad galería | 2 días antes del casamiento |
| Fin disponibilidad galería | Sin límite |
| Inicio disponibilidad Tinder | Hora de inicio del casamiento |
| Persistencia de chats | Indefinida |

---

## 8. Criterios de Aceptación General

Para considerar los módulos como completados, deben cumplirse todos los requisitos marcados como **MUST** (prioridad obligatoria) y al menos el 80% de los requisitos **SHOULD** (prioridad recomendada).

Los requisitos marcados como **COULD** son opcionales y pueden implementarse en fases posteriores.

---

**Documento generado para:** Aplicación de Organización de Casamientos  
**Versión:** 1.0  
**Fecha:** Noviembre 2025  
**Módulos:** Galería de Fotos, Tinder de Invitados

