# Casos de Prueba
## Aplicación de Organización de Casamientos
### Módulos: Galería de Fotos y Tinder de Invitados

---

## Índice de Casos de Prueba

1. [PR-UC-G1: Subir foto a la galería](#pr-uc-g1-subir-foto-a-la-galería)
2. [PR-UC-G2: Etiquetar personas en una foto](#pr-uc-g2-etiquetar-personas-en-una-foto)
3. [PR-UC-T1: Crear/editar perfil de Tinder](#pr-uc-t1-creareditar-perfil-de-tinder)
4. [PR-UC-T2: Explorar perfiles y dar like (con match)](#pr-uc-t2-explorar-perfiles-y-dar-like-con-match)

---

## PR-UC-G1: Subir foto a la galería

### Información General

| Campo | Valor |
|-------|-------|
| **Identificador de caso de uso** | UC-G1 |
| **Nombre de caso de uso** | Subir foto a la galería |
| **Identificador de la prueba** | PR-UC-G1 |
| **Descripción de la Prueba** | Verificar que el sistema permita subir una foto válida, generar las versiones necesarias (display/thumbnail), actualizar contador y registrar autor/fecha. |
| **Responsable** | |
| **Fecha de la Prueba** | |

### Prerrequisitos

- Que existan fotos en la galería del dispositivo para subir
- Usuario autenticado (rol: Invitado u Organizador)
- Galería habilitada
- Cupo no excedido
- Foto cumple con tamaño <12 MB, formato JPG/PNG y resolución ≤36 MP

### Entrada/s

- **Usuario:** usuario_invitado_01
- **Archivo:** 
  - imagen1.jpg (8 MB, 20 MP, formato JPG)
  - imagen2.jpg (8 MB, 20 MP, formato JPG)
  - imagen3.jpg (8 MB, 20 MP, formato JPG)
- **Acción del usuario:** seleccionar archivo y confirmar subida

### Detalle de la Prueba

1. Iniciar sesión en el sistema
2. Acceder a la sección "Galería"
3. Presionar "Agregar foto"
4. Seleccionar archivo imagen1.jpg
5. Confirmar la subida
6. Esperar confirmación del sistema
7. Acceder a la sección "Galería"
8. Presionar "Agregar foto"
9. Seleccionar los archivos: imagen1.jpg, imagen2.jpg, imagen3.jpg
10. Confirmar la subida de todos los archivos
11. Esperar confirmación del sistema

### Detalle de que se Prueba

- Solo una foto seleccionada
- Muchas fotos seleccionadas
- Ninguna Foto seleccionada
- Una Foto con formato no soportado
- Muchas fotos con formatos inválidos

### Resultado Esperado

| Escenario | Resultado Esperado |
|-----------|-------------------|
| Solo una foto seleccionada | La foto se carga correctamente y aparece en la galería con su miniatura |
| Muchas fotos seleccionadas | Las fotos se cargan correctamente y aparecen en la galería con su miniatura |
| Ninguna Foto seleccionada | No se carga ninguna imagen y se advierte que no se han seleccionado fotos |
| Una Foto con formato no soportado | No se carga ninguna imagen y se advierte que la foto tiene un formato no soportado |
| Muchas fotos con formatos inválidos | No se carga ninguna imagen y se advierte que al menos una foto tiene un formato no soportado |

### Resultado Obtenido

| Escenario | Funciona | No Funciona | Comentarios | Resultado |
|-----------|----------|-------------|-------------|-----------|
| Solo una foto seleccionada | | | | |
| Muchas fotos seleccionadas | | | | |
| Ninguna Foto seleccionada | | | | |
| Una Foto con formato no soportado | | Requiere mantenimiento perfectivo | | |
| Muchas fotos con formatos inválidos | | | | |

**Resultado Final:** ⬜ ACEPTADO &nbsp;&nbsp;&nbsp; ⬜ NO ACEPTADO

---

## PR-UC-G2: Etiquetar personas en una foto

### Información General

| Campo | Valor |
|-------|-------|
| **Identificador de caso de uso** | UC-G2 |
| **Nombre de caso de uso** | Etiquetar personas en una foto |
| **Identificador de la prueba** | PR-UC-G2 |
| **Descripción de la Prueba** | Verificar que el sistema permita etiquetar personas válidas en una foto, respetando el límite de 10 etiquetas y la lista oficial de invitados. |
| **Responsable** | |
| **Fecha de la Prueba** | |

### Prerrequisitos

- Foto visible en la galería
- Lista oficial de invitados cargada
- Usuario autenticado (rol Invitado u Organizador)

### Entrada/s

- **Foto:** foto_evento01.jpg
- **Invitados:** Ana López, Juan Pérez, María Gómez
- **Usuario:** organizador_01
- **Selección de nombres desde la lista oficial**

### Detalle de la Prueba

1. Abrir la galería y seleccionar una foto visible
2. Presionar "Etiquetar"
3. Escribir el nombre "Juan Pérez" en el campo de búsqueda
4. Seleccionar el nombre de la lista
5. Repetir hasta agregar varias etiquetas (≤10)
6. Presionar "Guardar"

### Detalle de que se Prueba

- **CA1:** el filtro por persona incluye la foto etiquetada
- **CA2:** no se aceptan nombres fuera de la lista oficial
- **CA3:** límite máximo de 10 etiquetas

### Resultado Esperado

| Escenario | Resultado Esperado |
|-----------|-------------------|
| Una Foto con una etiqueta creada | Se genera el filtro por la etiqueta, el filtro conduce a la foto, sin repetirse los filtros |
| Muchas fotos con una etiqueta creada | Se generan el filtro por las etiqueta, el filtro conduce a las fotos que corresponden a esa etiqueta, sin repetirse los filtros |
| Una Foto con muchas etiquetas | Se generan los filtros por todas las etiquetas creadas sin repetirse los filtros |
| Muchas fotos con muchas etiquetas | Se generan los filtros sin repetición y al seleccionar muchos filtros de etiquetas conducen a las fotos en las que aparecen todos juntos |
| Foto sin etiquetas creadas | La foto no es alcanzable por ningún filtro de etiqueta, sino solamente por la vista general |

### Resultado Obtenido

| Escenario | Funciona | No Funciona | Comentarios | Resultado |
|-----------|----------|-------------|-------------|-----------|
| Una Foto con una etiqueta creada | | | | |
| Muchas fotos con una etiqueta creada | | | | |
| Una Foto con muchas etiquetas | | | | |
| Muchas fotos con muchas etiquetas | | | | |
| Foto sin etiquetas creadas | | Requiere mantenimiento perfectivo | | NO ACEPTADO |

**Resultado Final:** ⬜ ACEPTADO &nbsp;&nbsp;&nbsp; ⬜ NO ACEPTADO

---

## PR-UC-T1: Crear/editar perfil de Tinder

### Información General

| Campo | Valor |
|-------|-------|
| **Identificador de caso de uso** | UC-T1 |
| **Nombre de caso de uso** | Crear/editar perfil de Tinder |
| **Identificador de la prueba** | PR-UC-T1 |
| **Descripción de la Prueba** | Validar que un usuario soltero pueda crear o editar su perfil con fotos, biografía y preferencias, cumpliendo restricciones establecidas. |
| **Responsable** | |
| **Fecha de la Prueba** | |

### Prerrequisitos

- Usuario autenticado y marcado como soltero
- Módulo Tinder habilitado

### Entrada/s

- **Usuario:** invitado_07
- **Fotos:** 3 imágenes tomadas con cámara (requerido)
- **Biografía:** "Amante de la música y los viajes." (120 caracteres)
- **Preferencias:** edad 25-35, género femenino, orientación heterosexual
- **Datos personales, fotos, texto de bio, rango de edad y género** (requerido)

### Detalle de la Prueba

1. Acceder al módulo Tinder
2. Seleccionar "Crear/Editar perfil"
3. Permitir acceso a la cámara y tomar 3 fotos
4. Completar la bio (≤280 caracteres)
5. Definir preferencias de edad, género y orientación
6. Guardar los cambios

### Detalle de que se Prueba

- **CA1:** con 1-6 fotos y bio ≤280 caracteres, el perfil se publica
- **CA2:** sin cámara no finaliza el proceso
- **CA3:** cambios guardados se reflejan en el feed

### Resultado Esperado

| Escenario | Resultado Esperado |
|-----------|-------------------|
| Sin foto tomada | No deja avanzar al formulario |
| Con una o más fotos tomadas | Avanza al formulario |
| Formulario con uno, algunos o todos los campos requeridos vacíos | No deja registrar el perfil |
| Formulario con todos los campos requeridos llenos | El perfil queda registrado y se puede avanzar a la vista de Tinder |
| Formulario con campos opcionales vacíos | El perfil queda registrado y se puede avanzar a la vista de Tinder |
| Formulario con campos opcionales llenos | El perfil queda registrado y se puede avanzar a la vista de Tinder |

### Resultado Obtenido

| Escenario | Funciona | No Funciona | Comentarios | Resultado |
|-----------|----------|-------------|-------------|-----------|
| Sin foto tomada | | | | |
| Con una o más fotos tomadas | | | | |
| Formulario con campos requeridos vacíos | | | | |
| Formulario con campos requeridos llenos | | | | |
| Formulario con campos opcionales vacíos | | Requiere mantenimiento perfectivo | | NO ACEPTADO |
| Formulario con campos opcionales llenos | | | | ACEPTADO |

**Resultado Final:** ⬜ ACEPTADO &nbsp;&nbsp;&nbsp; ⬜ NO ACEPTADO

---

## PR-UC-T2: Explorar perfiles y dar like (con match)

### Información General

| Campo | Valor |
|-------|-------|
| **Identificador de caso de uso** | UC-T2 |
| **Nombre de caso de uso** | Explorar perfiles y dar like (con match) |
| **Identificador de la prueba** | PR-UC-T2 |
| **Descripción de la Prueba** | Comprobar que el usuario pueda visualizar perfiles, registrar likes y recibir notificación de match cuando es recíproco. |
| **Responsable** | |
| **Fecha de la Prueba** | |

### Prerrequisitos

- Perfil activo creado mediante UC-T1
- Feed disponible

### Entrada/s

- **Usuario actual:** invitado_07
- **Candidato mostrado:** invitado_15 (ya dio like previo)
- **Interacción del usuario:** (Like o Saltar)

### Detalle de la Prueba

1. Ingresar al módulo Tinder
2. Abrir el feed de exploración
3. Visualizar un perfil sugerido
4. Presionar "Like"
5. Verificar respuesta del sistema

### Detalle de que se Prueba

- **CA1:** no se repiten inmediatamente perfiles ya likeados
- **CA2:** ante match se notifica y habilita chat
- **CA3:** comunica correctamente cuando no hay candidatos disponibles

### Resultado Esperado

| Escenario | Resultado Esperado |
|-----------|-------------------|
| Like sin match previo | Se registra el like, no hay notificación, se muestra siguiente perfil |
| Like con match (recíproco) | Se crea match, se notifica a ambos usuarios, se habilita chat |
| Saltar perfil | No se registra acción, se muestra siguiente perfil |
| Sin más perfiles disponibles | Se muestra mensaje "No hay más perfiles según tus preferencias" |

### Resultado Obtenido

| Escenario | Funciona | No Funciona | Comentarios | Resultado |
|-----------|----------|-------------|-------------|-----------|
| Like sin match previo | | | | |
| Like con match (recíproco) | | | | |
| Saltar perfil | | | | |
| Sin más perfiles disponibles | | | | |

**Resultado Final:** ⬜ ACEPTADO &nbsp;&nbsp;&nbsp; ⬜ NO ACEPTADO

---

## Resumen de Casos de Prueba

| ID Prueba | Caso de Uso | Estado | Resultado |
|-----------|-------------|--------|-----------|
| PR-UC-G1 | Subir foto a la galería | Pendiente | - |
| PR-UC-G2 | Etiquetar personas en una foto | Pendiente | - |
| PR-UC-T1 | Crear/editar perfil de Tinder | Pendiente | - |
| PR-UC-T2 | Explorar perfiles y dar like | Pendiente | - |

---

## Notas

### Criterios de Aceptación

Un caso de prueba se considera **ACEPTADO** cuando:
- Todos los escenarios críticos funcionan correctamente
- Los errores encontrados son menores y no bloquean la funcionalidad principal
- Las validaciones de seguridad y restricciones se cumplen

Un caso de prueba se considera **NO ACEPTADO** cuando:
- Hay errores críticos que impiden el uso de la funcionalidad
- No se cumplen los requisitos de seguridad
- Las validaciones principales fallan

### Tipos de Mantenimiento

- **Mantenimiento correctivo:** Corrección de errores/bugs
- **Mantenimiento perfectivo:** Mejoras de funcionalidad o usabilidad
- **Mantenimiento adaptativo:** Adaptación a cambios del entorno
- **Mantenimiento preventivo:** Prevención de futuros problemas

---

**Documento generado para:** Aplicación de Organización de Casamientos  
**Versión:** 1.0  
**Fecha:** Noviembre 2025  
**Total de casos de prueba:** 4

