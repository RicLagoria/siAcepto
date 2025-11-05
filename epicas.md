# 📋 Backlog para Jira (Historias de Usuario)
## Aplicación de Organización de Casamientos

---

## Épica 1: Autenticación y Acceso

**HU-1:** Como invitado, quiero autenticarme en la aplicación con mis credenciales para acceder a los módulos disponibles según mi perfil.

**Criterios de aceptación:**
- Validación de credenciales contra la lista de invitados
- Respuesta JWT válida con información del rol (Invitado/Organizador)
- Mensaje de error claro si las credenciales son inválidas
- Redirección automática según permisos del usuario

**HU-2:** Como invitado, quiero que el sistema valide si soy soltero para determinar si puedo acceder al módulo Tinder.

**Criterios de aceptación:**
- Consulta automática al endpoint de Lista de Invitados
- Bandera "soltero" determina visibilidad del módulo Tinder
- Si no soy soltero, el módulo Tinder no aparece en mi menú
- La validación se ejecuta en cada inicio de sesión

---

## Épica 2: Galería de Fotos - Gestión Básica

**HU-3:** Como invitado, quiero subir fotos desde la galería de mi dispositivo para compartirlas con otros invitados.

**Criterios de aceptación:**
- Permite seleccionar una o múltiples fotos (hasta el límite de rate)
- Formatos soportados: JPG, JPEG, PNG, HEIC
- Validación de tamaño máximo 12 MB por foto
- Validación de resolución máxima 36 MP
- Muestra barra de progreso durante la subida
- Mensaje de confirmación al completar la subida exitosa
- Mensaje de error claro si se excede tamaño, resolución o cupo
- Al alcanzar el cupo (80 fotos), bloquea subida y sugiere eliminar fotos propias

**HU-4:** Como invitado, quiero ver todas las fotos subidas en una galería para disfrutar de los recuerdos del evento.

**Criterios de aceptación:**
- Vista de galería muestra miniaturas (thumbnails) en grid responsive
- Ordenadas por fecha, más recientes primero
- Carga inicial muestra primeras 50 fotos en menos de 2 segundos
- Scroll infinito carga más fotos automáticamente
- Indicador de carga mientras se obtienen más fotos
- Mensaje "No hay fotos aún" si la galería está vacía

**HU-5:** Como invitado, quiero ver una foto en detalle con navegación para apreciarla mejor.

**Criterios de aceptación:**
- Al hacer click en una miniatura, abre la foto en vista de detalle
- Muestra versión display de la foto (máx 2048px, ~1.5MB)
- Botones de navegación anterior/siguiente a los costados
- Swipe izquierda/derecha para cambiar de foto (móvil)
- Botón de cerrar para volver a la galería
- Muestra badges con etiquetas de personas

**HU-6:** Como invitado, quiero descargar fotos a mi dispositivo para guardarlas personalmente.

**Criterios de aceptación:**
- Botón "Descargar" visible en vista de detalle
- Descarga la versión display (no thumbnail)
- Mensaje de confirmación al completar descarga
- Funciona en móvil y desktop

**HU-7:** Como invitado, quiero compartir fotos mediante un link para enviarlas a otras personas.

**Criterios de aceptación:**
- Botón "Compartir" visible en vista de detalle
- Genera link público temporal a la foto específica
- El link abre la foto en vista de detalle
- Funciona en móvil y desktop (integración con share nativo si está disponible)

**HU-8:** Como invitado, quiero eliminar mis propias fotos si cambio de opinión o necesito liberar cupo.

**Criterios de aceptación:**
- Botón "Eliminar" solo visible en fotos del usuario actual
- Solicita confirmación antes de eliminar
- Al confirmar, elimina permanentemente la foto
- Libera el cupo del usuario (contador se decrementa)
- Muestra mensaje de confirmación de eliminación

**HU-9:** Como invitado, quiero ver detalles técnicos de una foto (metadata) para conocer su información.

**Criterios de aceptación:**
- Botón de 3 puntos en vista de detalle
- Muestra overlay transparente con: nombre de archivo, tamaño, fecha de subida, autor
- Se puede cerrar haciendo click fuera del overlay

---

## Épica 3: Galería de Fotos - Etiquetado y Filtros

**HU-10:** Como invitado, quiero etiquetar personas en las fotos para identificar quién aparece en ellas.

**Criterios de aceptación:**
- Botón "Etiquetar" en vista de detalle
- Al hacer click sobre la foto, permite agregar etiqueta en ese punto
- Campo de búsqueda con autocompletado de nombres de la lista de invitados
- Solo acepta nombres que existen en la lista oficial (no texto libre)
- Máximo 10 etiquetas por foto
- Muestra badges con los nombres etiquetados sobre o debajo de la foto
- Mensaje de error si se intenta agregar más de 10 etiquetas
- Guarda las etiquetas al confirmar

**HU-11:** Como invitado, quiero filtrar fotos por personas etiquetadas para encontrar fotos específicas.

**Criterios de aceptación:**
- Botón flotante de "Filtros" en vista de galería
- Pestaña "Etiquetas" muestra lista de personas que han sido etiquetadas
- Permite seleccionar una o múltiples personas
- Al aplicar, la galería muestra solo fotos con las personas seleccionadas
- Se puede combinar con filtros de colecciones
- Botón para limpiar filtros y volver a ver todas las fotos
- Muestra contador de fotos filtradas

---

## Épica 4: Galería de Fotos - Colecciones

**HU-12:** Como invitado, quiero agregar mis fotos a colecciones de eventos/actividades para organizarlas mejor.

**Criterios de aceptación:**
- Al subir una foto, opción "Agregar a colección" disponible
- Lista de colecciones proviene del módulo de Eventos/Actividades
- Colección "General" existe por defecto
- Permite seleccionar una colección al subir
- Por defecto, las fotos van a "General" si no se especifica
- Confirmación visual de la colección asignada

**HU-13:** Como invitado, quiero cambiar la colección de mis fotos para corregir la categorización.

**Criterios de aceptación:**
- En vista de detalle de mi foto, opción "Cambiar colección"
- Muestra lista de colecciones disponibles
- Permite cambiar a cualquier colección
- Guarda el cambio inmediatamente
- Mensaje de confirmación del cambio

**HU-14:** Como invitado, quiero agregar fotos de otros usuarios a colecciones adicionales para sugerir mejor categorización.

**Criterios de aceptación:**
- En vista de detalle de foto de otro usuario, opción "Agregar a colección"
- La foto puede pertenecer a múltiples colecciones
- Al agregar, el autor original recibe notificación
- El autor puede aceptar o rechazar la sugerencia
- Si acepta, la foto aparece en ambas colecciones

**HU-15:** Como invitado, quiero filtrar fotos por colecciones para ver fotos de eventos/actividades específicas.

**Criterios de aceptación:**
- Botón flotante de "Filtros" en vista de galería
- Pestaña "Colecciones" muestra lista de colecciones disponibles
- Permite seleccionar una o múltiples colecciones
- Se puede combinar con filtros de etiquetas de personas
- Al aplicar, la galería muestra solo fotos de las colecciones seleccionadas
- Botón para limpiar filtros

---

## Épica 5: Galería de Fotos - Moderación

**HU-16:** Como organizador, quiero moderar el contenido de la galería para mantener un ambiente apropiado.

**Criterios de aceptación:**
- Panel de moderación accesible solo para Organizador
- Opción de ocultar/mostrar fotos (no elimina, solo oculta de vista pública)
- Opción de eliminar permanentemente fotos inapropiadas
- Cada acción solicita confirmación
- Registro de auditoría de todas las acciones (quién, qué, cuándo)
- Fotos ocultas solo visibles para Organizador

**HU-17:** Como organizador, quiero ver reportes de actividad de la galería para monitorear el uso.

**Criterios de aceptación:**
- Dashboard muestra: total de fotos, top 5 usuarios que más subieron, fotos ocultas
- Filtros por fecha
- Exportación de reporte básico
- Actualización en tiempo real

---

## Épica 6: Tinder - Gestión de Perfil

**HU-18:** Como invitado soltero, quiero crear mi perfil de Tinder con fotos de cámara para participar en el módulo.

**Criterios de aceptación:**
- Módulo Tinder solo accesible desde la hora de inicio del casamiento
- Pantalla de captura con cámara en vivo
- Botón de captura de foto
- Botón para alternar entre cámara frontal y trasera
- Permite capturar entre 1 y 6 fotos
- No permite subir fotos de la galería del dispositivo
- Botón para revisar fotos capturadas en carrusel interno
- Mensaje de error si se intenta acceder sin permiso de cámara

**HU-19:** Como invitado soltero, quiero completar mi perfil con información personal y preferencias para que otros me conozcan.

**Criterios de aceptación:**
- Formulario incluye: nombre (predeterminado de lista, editable), edad, género, orientación, descripción (máx 280 caracteres)
- Configuración de preferencias: rango de edad (18-80), género preferido, orientación preferida
- Validación de edad en rango válido
- Validación de descripción máximo 280 caracteres
- No permite guardar si faltan campos obligatorios o si tiene menos de 1 foto
- Botón "Guardar perfil" publica el perfil y redirige al feed

**HU-20:** Como invitado soltero, quiero editar mi perfil y preferencias para actualizar mi información.

**Criterios de aceptación:**
- Opción "Editar perfil" accesible desde el menú de Tinder
- Permite cambiar fotos (capturando nuevas con la cámara)
- Permite editar todos los campos del perfil
- Permite ajustar preferencias de búsqueda
- Al guardar, actualiza inmediatamente
- El feed se actualiza con los nuevos filtros de preferencias

---

## Épica 7: Tinder - Exploración y Matching

**HU-21:** Como invitado soltero, quiero ver perfiles de otros usuarios según mis preferencias para conocer personas.

**Criterios de aceptación:**
- Feed muestra perfiles filtrados por: edad, género, orientación (según preferencias configuradas)
- Cada perfil muestra: foto principal (carrusel si hay varias), nombre, edad, descripción
- Los perfiles aparecen de forma aleatoria
- No se repiten perfiles ya vistos (likeados o saltados) en la misma sesión
- Si no hay más perfiles, mensaje "No hay más perfiles según tus preferencias"
- Scroll horizontal o botones para ver múltiples fotos del perfil

**HU-22:** Como invitado soltero, quiero dar like a perfiles que me interesan para indicar mi interés.

**Criterios de aceptación:**
- Botón "Like" visible y accesible en cada perfil
- Al hacer like, se registra la acción
- El perfil desaparece y muestra el siguiente
- Rate limit: máximo 200 likes por hora
- Si se alcanza el rate limit, muestra mensaje temporal con tiempo de espera
- Animación visual al dar like

**HU-23:** Como invitado soltero, quiero saltar perfiles que no me interesan sin penalizarlos.

**Criterios de aceptación:**
- Botón "Saltar" visible en cada perfil
- Al saltar, no se registra acción negativa (no hay dislike)
- El perfil desaparece y muestra el siguiente
- No afecta al otro usuario de ninguna forma

**HU-24:** Como invitado soltero, quiero recibir notificación cuando hago match con alguien para saber que hay interés mutuo.

**Criterios de aceptación:**
- Match se produce cuando ambos usuarios se dieron like mutuamente
- Notificación pop-up aparece inmediatamente al producirse el match
- La notificación muestra el nombre del otro usuario
- Incluye botón para ver el perfil completo del match
- Si se cierra la notificación, el match aparece en la lista de chats

**HU-25:** Como invitado soltero, quiero ver el perfil completo de mis matches para conocerlos mejor.

**Criterios de aceptación:**
- Al hacer click en notificación o en la lista de chats, abre perfil del match
- Muestra carrusel con todas las fotos del perfil
- Muestra datos: nombre, edad, descripción
- Botón "Iniciar chat" visible
- Navegación entre fotos con botones o swipe

---

## Épica 8: Tinder - Chat

**HU-26:** Como invitado soltero, quiero chatear con mis matches para conocerlos mejor.

**Criterios de aceptación:**
- Botón "Iniciar chat" desde el perfil del match abre la vista de chat
- Vista de chat muestra mensajes como burbujas de diálogo
- Mensajes propios alineados a la derecha con color primario
- Mensajes del otro alineados a la izquierda con color secundario
- Campo de texto para escribir mensaje
- Botón "Enviar" con ícono
- Envío también con tecla Enter (desktop)
- Scroll automático al último mensaje

**HU-27:** Como invitado soltero, quiero ver la lista de todos mis chats para acceder a conversaciones previas.

**Criterios de aceptación:**
- Pestaña "CHATS" muestra lista de todos los matches
- Cada item muestra: foto principal del otro, nombre, fragmento del último mensaje
- Ordenados por actividad reciente (último mensaje primero)
- Al hacer click en un chat, abre la conversación
- Badge con número de mensajes no leídos (opcional)

**HU-28:** Como invitado soltero, quiero que mis chats persistan después del evento para mantener el contacto.

**Criterios de aceptación:**
- Los chats no tienen fecha de expiración
- Los mensajes se mantienen indefinidamente
- Se puede acceder a chats días/semanas después del casamiento
- Historial completo de conversación disponible

**HU-29:** Como invitado soltero, quiero navegar entre el feed de Tinder y mis chats fácilmente.

**Criterios de aceptación:**
- Dos pestañas visibles en la parte superior: "TINDER" y "CHATS"
- Pestaña "TINDER" muestra el feed de exploración de perfiles
- Pestaña "CHATS" muestra la lista de conversaciones
- Cambio instantáneo entre pestañas
- Las pestañas están disponibles en todas las vistas excepto en configuración inicial de perfil

---

## Épica 9: Integraciones

**HU-30:** Como sistema, necesito consultar la lista de invitados para obtener información de usuarios y validar acceso a módulos.

**Criterios de aceptación:**
- Endpoint `GET /api/invitados/{id}` retorna: id, nombre, edad, esSoltero
- Endpoint `GET /api/invitados` retorna lista completa para autocompletado
- La consulta se realiza al iniciar sesión
- La bandera "esSoltero" determina visibilidad del módulo Tinder
- Los nombres se usan para autocompletar etiquetas en fotos
- Caché de lista de invitados con refresco periódico
- Manejo de errores si el endpoint no responde

**HU-31:** Como sistema, necesito consultar eventos y actividades para crear colecciones de fotos.

**Criterios de aceptación:**
- Endpoint `GET /api/eventos` retorna lista de eventos: [{ id, nombre, fecha, hora }]
- Cada evento se convierte en una colección disponible
- La colección "General" existe por defecto siempre
- Las colecciones se actualizan si cambia la lista de eventos
- Caché de colecciones con refresco cada hora
- Manejo de errores si el endpoint no responde (mantiene colecciones en caché)

---

## Épica 10: Requerimientos No Funcionales

### Tareas Técnicas: Seguridad

**TT-1:** Implementar control de acceso basado en roles (RBAC) para diferenciar permisos de Invitado y Organizador.

**Criterios de aceptación:**
- Middleware de autorización valida rol en cada endpoint
- Endpoints de moderación solo accesibles por Organizador
- Token JWT incluye información del rol
- Respuesta 403 Forbidden si el rol no tiene permiso

**TT-2:** Implementar sistema de auditoría para acciones de moderación.

**Criterios de aceptación:**
- Log inmutable registra: usuario, acción, timestamp, recurso afectado
- Tabla de auditoría en base de datos separada
- No se permite modificación retroactiva de logs
- Dashboard de auditoría para Organizador

**TT-3:** Configurar HTTPS en el servidor para comunicación segura.

**Criterios de aceptación:**
- Certificado SSL/TLS configurado
- Redirección automática de HTTP a HTTPS
- Headers de seguridad configurados (HSTS, CSP)

**TT-4:** Implementar encriptación de datos sensibles en base de datos.

**Criterios de aceptación:**
- Contraseñas hasheadas con bcrypt o algoritmo similar
- Datos personales encriptados en reposo
- Conexión a base de datos con SSL

### Tareas Técnicas: Capacidad y Rendimiento

**TT-5:** Implementar validaciones de tamaño y formato de imágenes.

**Criterios de aceptación:**
- Validación en frontend: máx 12 MB, formatos JPG/JPEG/PNG/HEIC
- Validación en backend: máx 36 MP de resolución
- Conversión automática de PNG/HEIC a JPG
- Generación de versión display (≤2048px, ~1.5MB) y thumbnail (≤400px, ~100KB)
- Respuesta clara de error si no cumple requisitos

**TT-6:** Implementar sistema de cupos por usuario y por evento.

**Criterios de aceptación:**
- Contador de fotos por usuario en base de datos
- Validación antes de permitir subida
- Cupos: Invitado 80, Organizador 500, Evento 20,000
- Bloqueo de subida al alcanzar cupo con mensaje explicativo
- Decremento de contador al eliminar foto

**TT-7:** Implementar rate limiting para prevenir abuso.

**Criterios de aceptación:**
- Rate limit subida: 10 fotos / 5 min, 60 fotos / hora por usuario
- Rate limit likes: 200 / hora por usuario
- Respuesta 429 Too Many Requests con tiempo de espera
- Mensaje en frontend indicando cuándo puede volver a intentar
- Redis o similar para mantener contadores de rate limit

**TT-8:** Optimizar carga de galería con lazy loading y paginación.

**Criterios de aceptación:**
- Primera carga muestra 50 thumbnails en <2 segundos
- Scroll infinito carga siguientes 50 automáticamente
- Thumbnails cargados bajo demanda (lazy loading)
- Indicador de carga mientras se obtienen más fotos

**TT-9:** Garantizar tiempo de procesamiento de fotos en <5 segundos.

**Criterios de aceptación:**
- Pipeline de procesamiento: validación → conversión → resize → upload
- Procesamiento asíncrono con cola (ej: Bull con Redis)
- Feedback en tiempo real del progreso
- Pruebas de carga con 100 usuarios simultáneos subiendo fotos

### Tareas Técnicas: Almacenamiento

**TT-10:** Configurar almacenamiento de imágenes en Google Drive.

**Criterios de aceptación:**
- Integración con Google Drive API
- Organización por evento (carpeta por casamiento)
- Subcarpetas: originals, display, thumbnails
- URLs públicas temporales para acceso desde la app
- Backup automático configurado

**TT-11:** Configurar base de datos en servidores propios.

**Criterios de aceptación:**
- Base de datos PostgreSQL o MongoDB según diseño
- Esquema de tablas/colecciones definido
- Índices en campos de búsqueda frecuente
- Backup automático diario
- Replicación para alta disponibilidad (opcional)

### Tareas Técnicas: Usabilidad

**TT-12:** Implementar diseño responsive con paleta de colores pastel.

**Criterios de aceptación:**
- Diseño mobile-first que se adapta a tablet y desktop
- Breakpoints definidos: móvil (<768px), tablet (768-1024px), desktop (>1024px)
- Paleta de colores pastel consistente en toda la app
- Elementos táctiles mínimo 44x44 px
- Pruebas en dispositivos iOS y Android

**TT-13:** Implementar estados de carga y mensajes de error claros.

**Criterios de aceptación:**
- Skeletons o spinners durante cargas
- Mensajes de error específicos y accionables
- Toasts o snackbars para confirmaciones
- Manejo graceful de errores de red
- Estados vacíos informativos ("No hay fotos aún")

### Tareas Técnicas: Disponibilidad

**TT-14:** Implementar configuración de períodos de disponibilidad por módulo.

**Criterios de aceptación:**
- Configuración a nivel evento: fecha inicio/fin de galería, hora inicio Tinder
- Validación de disponibilidad en cada acceso al módulo
- Mensaje informativo si se intenta acceder fuera del período
- Valores por defecto: Galería desde 2 días antes sin fin, Tinder desde hora inicio del evento

**TT-15:** Garantizar persistencia indefinida de chats de Tinder.

**Criterios de aceptación:**
- Mensajes sin fecha de expiración
- Acceso a chats disponible después del evento
- No hay límite temporal en el almacenamiento

### Tareas Técnicas: Testing

**TT-16:** Implementar pruebas unitarias y de integración.

**Criterios de aceptación:**
- Cobertura mínima 70% en backend
- Tests de endpoints críticos (subida, autenticación, match)
- Tests de validaciones (tamaño, cupos, rate limits)
- CI/CD ejecuta tests en cada commit

**TT-17:** Realizar pruebas de carga y rendimiento.

**Criterios de aceptación:**
- Simular 100 usuarios concurrentes subiendo fotos
- Simular 500 usuarios navegando galería simultáneamente
- Tiempo de respuesta promedio <3 segundos
- Identificar y resolver cuellos de botella

---

## Resumen de Épicas

| Épica | Historias de Usuario | Tareas Técnicas | Total |
|-------|---------------------|-----------------|-------|
| 1. Autenticación y Acceso | 2 | 0 | 2 |
| 2. Galería - Gestión Básica | 7 | 0 | 7 |
| 3. Galería - Etiquetado y Filtros | 2 | 0 | 2 |
| 4. Galería - Colecciones | 4 | 0 | 4 |
| 5. Galería - Moderación | 2 | 0 | 2 |
| 6. Tinder - Gestión de Perfil | 3 | 0 | 3 |
| 7. Tinder - Exploración y Matching | 5 | 0 | 5 |
| 8. Tinder - Chat | 4 | 0 | 4 |
| 9. Integraciones | 2 | 0 | 2 |
| 10. Requerimientos No Funcionales | 0 | 17 | 17 |
| **TOTAL** | **31** | **17** | **48** |

---

**Documento generado para:** Aplicación de Organización de Casamientos  
**Versión:** 1.0  
**Fecha:** Noviembre 2025  
**Total de items:** 48 (31 HU + 17 TT)

