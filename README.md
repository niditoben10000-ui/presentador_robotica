# Presentación Interactiva FLL - Guía Completa

## Estructura del Proyecto

```
presentacion-fll/
├── interactivo-imagen.html   ← OPCIÓN RECOMENDADA (imagen con hotspots)
├── interactivo-3d.html       ← Opción avanzada (modelo 3D rotable)
├── assets/                   ← Aquí van tus fotos y modelo 3D
│   ├── robot.jpg             ← Foto del robot (tú la pones)
│   └── robot.glb             ← Modelo 3D del robot (opcional)
└── README.md                 ← Este archivo
```

---

## Opción A: Imagen Interactiva (RECOMENDADA)

**Archivo:** `interactivo-imagen.html`

### Paso 1 — Preparar la foto del robot

1. Toma una foto de tu robot con buena iluminación, fondo limpio (una cartulina blanca sirve)
2. Resolución mínima recomendada: **1920×1080 px**
3. Formato: **JPG** o **PNG**
4. Guárdala como `assets/robot.jpg`

### Paso 2 — Editar la configuración

Abre `interactivo-imagen.html` en cualquier editor de texto (Notepad, VS Code, etc.).

Busca la sección `CONFIG` al inicio del `<script>` y modifica:

```javascript
const CONFIG = {
  equipo: {
    nombre: 'TU EQUIPO AQUÍ',          // Nombre del equipo
    iniciales: 'TE',                    // 1-2 letras para el ícono
    temporada: 'SUBMERGED 2025-2026',   // Temporada actual
    nombreRobot: 'NOMBRE DEL ROBOT',    // Nombre de tu robot
  },

  imagenRobot: 'assets/robot.jpg',      // Ruta a la foto

  cloudinaryBase: 'https://res.cloudinary.com/TU_CLOUD_NAME/video/upload/',
  // ↑ Reemplaza TU_CLOUD_NAME con tu nombre de Cloudinary
};
```

### Paso 3 — Posicionar los hotspots

Cada componente tiene coordenadas `x` (horizontal) e `y` (vertical) en porcentaje:
- `x: 0` = borde izquierdo, `x: 100` = borde derecho
- `y: 0` = borde superior, `y: 100` = borde inferior

**Truco para encontrar las coordenadas:**
1. Abre la foto en cualquier editor de imágenes (Paint, Preview, etc.)
2. Pasa el cursor sobre el componente y anota la posición en píxeles
3. Divide la posición X entre el ancho total de la imagen y multiplica por 100
4. Divide la posición Y entre el alto total de la imagen y multiplica por 100

Ejemplo: si tu imagen es 1920×1080 y el Hub está en el píxel (960, 324):
- `x = (960 / 1920) × 100 = 50`
- `y = (324 / 1080) × 100 = 30`

### Paso 4 — Subir videos a Cloudinary

1. Ve a [cloudinary.com](https://cloudinary.com) e inicia sesión
2. Sube cada video de componente (máx 30-60 segundos cada uno)
3. **Formato recomendado:** MP4, códec H.264, resolución 720p (1280×720)
4. **Tamaño máximo recomendado:** 15 MB por video
5. Copia el nombre del archivo (ej: `hub-spike-prime.mp4`)
6. Ponlo en el campo `video:` de cada componente en la configuración

Si quieres usar la URL completa en vez del nombre, también funciona:

```javascript
video: 'https://res.cloudinary.com/miequipo/video/upload/v1234/hub-spike.mp4',
```

### Paso 5 — Probar en la tablet

**Opción más fácil — abrir archivo directamente:**
1. Copia toda la carpeta `presentacion-fll/` a la tablet (cable USB o Google Drive)
2. Abre Chrome en la tablet
3. En la barra de direcciones escribe: `file:///sdcard/Download/presentacion-fll/interactivo-imagen.html`
   (ajusta la ruta según dónde copiaste los archivos)

**Opción alternativa — servidor local (mejor rendimiento):**
1. Instala "Simple HTTP Server" desde Google Play Store
2. Apunta el servidor a la carpeta `presentacion-fll/`
3. Abre Chrome e ingresa la dirección que muestra la app (ej: `http://localhost:8080`)

**Opción con internet — GitHub Pages (gratis):**
1. Crea una cuenta en [github.com](https://github.com) si no tienes una
2. Crea un repositorio nuevo llamado `presentacion-robot`
3. Sube los archivos
4. Ve a Settings → Pages → selecciona la rama `main`
5. Tu presentación estará en: `https://tu-usuario.github.io/presentacion-robot/interactivo-imagen.html`

---

## Opción B: Modelo 3D Interactivo (AVANZADA)

**Archivo:** `interactivo-3d.html`

### Formatos soportados (DIRECTO desde BrickLink Studio)

El visor 3D acepta estos formatos **sin necesidad de conversión ni Blender**:
- **.dae** (Collada) — **RECOMENDADO**, exporta directo desde BrickLink Studio
- **.obj** (Wavefront OBJ) — exporta directo desde BrickLink Studio
- **.glb** (GL Binary) — si conviertes con herramienta online
- **.gltf** (GL Transmission Format)

### Exportar desde BrickLink Studio (3 minutos)

**Opción recomendada — Collada (.dae):**
1. En BrickLink Studio: **File → Export As → Export as Collada...**
2. Guarda el archivo como `robot.dae`
3. Copia el archivo a la carpeta `assets/`
4. En CONFIG, cambia: `modeloRobot: 'assets/robot.dae'`

**Opción alternativa — OBJ:**
1. En BrickLink Studio: **File → Export As → Export as OBJ...**
2. Guarda como `robot.obj`
3. Copia a `assets/` y actualiza CONFIG

### Si quieres convertir a GLB (OPCIONAL, ya no es necesario)

Herramientas online gratuitas (NO necesitas Blender):

1. **GLTFTools** — [gltftools.com/converter/dae-to-glb](https://www.gltftools.com/converter/dae-to-glb)
   Arrastra tu `.dae`, convierte, descarga `.glb`. Todo en el navegador.

2. **Three.js Editor** — [threejs.org/editor](https://threejs.org/editor/)
   File → Import → tu `.dae` → File → Export → GLTF

3. **Sketchfab** (integrado en BrickLink Studio):
   File → Export to Sketchfab → descarga como GLB desde tu cuenta

### Posicionar los hotspots del modelo 3D

La versión 3D incluye un **Modo Editor** integrado:

1. Carga tu modelo 3D (configura `modeloRobot` en CONFIG)
2. Haz clic en el botón **"Modo Editor"** arriba a la derecha
3. Haz clic en cualquier componente del modelo 3D
4. Abajo aparecen las coordenadas exactas (`posicion`)
5. Copia esos valores al campo correspondiente en CONFIG

```javascript
{
  id: 'hub',
  nombre: 'Hub SPIKE Prime',
  posicion: '0.0012 0.1523 -0.0034',  // ← Coordenadas del Modo Editor
  video: 'hub-spike-prime.mp4',
},
```

### IMPORTANTE: Servidor local necesario para 3D

Los modelos 3D no cargan con `file://` en Chrome. Necesitas:

**En computadora:** `python3 -m http.server 8000` → abre `http://localhost:8000`
**En tablet:** Instala "Simple HTTP Server" de Google Play
**Online (gratis):** Sube a GitHub Pages o Netlify

### Optimización del modelo 3D para tablet

Para que funcione bien en la Lenovo M11:
- **Tamaño máximo del archivo:** 30 MB (ideal < 15 MB)
- **Polígonos:** máximo 100,000 (ideal < 50,000)
- Si el modelo es pesado, exporta con menos detalle desde Studio

---

## Especificaciones de Videos para Cloudinary

| Aspecto | Recomendación |
|---|---|
| Formato | MP4 (códec H.264) |
| Resolución | 1280×720 (720p) |
| Duración | 30-60 segundos máximo |
| Tamaño por video | < 15 MB |
| Audio | Sí, con sonido claro |
| FPS | 30 fps |
| Orientación | Horizontal (landscape) |

### Tips para grabar buenos videos

1. Graba en un lugar silencioso con buena iluminación
2. El estudiante debe hablar mirando a cámara, claro y con energía
3. Si es posible, muestra el componente real del robot mientras explicas
4. Duración ideal: 30-45 segundos por componente
5. Usa un trípode o apoya el celular para evitar temblores

---

## Requisitos de la Lenovo M11

| Requisito | Especificación |
|---|---|
| Sistema Operativo | Android 12+ |
| Navegador | Chrome (última versión) |
| RAM mínima | 4 GB |
| Almacenamiento libre | 500 MB (para archivos locales) |
| Conexión internet | Necesaria para videos de Cloudinary |
| Pantalla | Funciona en cualquier resolución |

---

## Plan B — Si Algo Falla

### Si los videos no cargan desde Cloudinary:
- Descarga los videos MP4 y ponlos en la carpeta `assets/`
- Cambia las URLs en CONFIG para apuntar a archivos locales:
  ```javascript
  video: 'assets/hub-spike-prime.mp4',  // Ruta local
  ```

### Si no alcanza el tiempo para el modelo 3D:
- Usa la versión de imagen (`interactivo-imagen.html`) — funciona perfectamente

### Si la foto del robot no se ve bien con los hotspots:
- Toma la foto desde arriba (vista superior) para que todos los componentes sean visibles
- O usa varias fotos y crea una versión por cada ángulo (duplica componentes en CONFIG)

### Si la tablet no tiene internet el día de la presentación:
- Descarga los videos y usa rutas locales (ver arriba)
- Lleva un hotspot móvil como respaldo

### Si nada funciona:
- Abre los videos directamente desde la galería de la tablet
- Ordénalos numéricamente (01-hub.mp4, 02-motor-izq.mp4, etc.)
- Muéstralos manualmente mientras señalas los componentes del robot real

---

## Tiempo Estimado de Implementación

| Tarea | Imagen (Opción A) | 3D (Opción B) |
|---|---|---|
| Tomar/preparar foto del robot | 30 min | — |
| Crear modelo 3D en Studio 2.0 | — | 8-15 horas |
| Grabar videos de componentes | 2-3 horas | 2-3 horas |
| Editar y subir videos a Cloudinary | 1-2 horas | 1-2 horas |
| Configurar hotspots y datos | 1 hora | 1-2 horas |
| Probar y ajustar en tablet | 1 hora | 2 horas |
| **TOTAL** | **5-7 horas** | **15-25 horas** |
