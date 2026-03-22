# Guía de Diseño — Template Skilling Center Tecmilenio

Extraído del archivo `TEMPLATE INSTRUCTORES.pptx`.
Usar estos elementos para todas las presentaciones del curso de ciberseguridad INDEX.

---

## Paleta de colores

### Colores primarios de marca

| Nombre | Hex | Uso |
|--------|-----|-----|
| **Verde teal oscuro** | `#00534C` | Logo, títulos principales, barras de énfasis |
| **Verde teal medio** | `#017564` | Encabezados secundarios, bordes |
| **Teal corporativo** | `#00879B` | Fondos de sección, íconos activos |
| **Teal profundo** | `#0B8078` | Variante de botones y badges |

### Colores de acento

| Nombre | Hex | Uso |
|--------|-----|-----|
| **Turquesa brillante** | `#40C6BD` | Íconos, puntos de proceso, highlights |
| **Menta clara** | `#6BCABA` | Fondos de cuadros informativos |
| **Menta muy clara** | `#B1DFDC` | Fondos de tablas, áreas sombreadas |
| **Turquesa oscuro** | `#27879B` | Texto sobre fondos claros |

### Colores neutros

| Nombre | Hex | Uso |
|--------|-----|-----|
| **Blanco** | `#FFFFFF` | Fondo principal de diapositivas |
| **Gris muy claro** | `#E7E6E6` | Fondos alternativos, líneas divisorias |
| **Gris azulado** | `#A5A5A5` | Texto secundario, subtítulos |
| **Azul marino** | `#44546A` | Texto de cuerpo, tablas |
| **Negro** | `#000000` | Texto de alto contraste |

### Paleta completa CSS

```css
:root {
  /* Primarios */
  --teal-dark:     #00534C;
  --teal-medium:   #017564;
  --teal-corp:     #00879B;
  --teal-deep:     #0B8078;

  /* Acentos */
  --turquoise:     #40C6BD;
  --mint:          #6BCABA;
  --mint-light:    #B1DFDC;
  --turquoise-mid: #27879B;

  /* Neutros */
  --white:         #FFFFFF;
  --gray-light:    #E7E6E6;
  --gray-mid:      #A5A5A5;
  --navy:          #44546A;
  --black:         #000000;
}
```

---

## Tipografía

| Uso | Fuente | Peso |
|-----|--------|------|
| Títulos principales | Calibri Light | Regular (300) |
| Subtítulos y encabezados | Calibri | Bold (700) |
| Cuerpo de texto | Calibri | Regular (400) |
| Datos / tablas | Calibri | Regular (400) |

---

## Layouts de diapositiva

### 1. Portada / Diapositiva de título
- **Fondo:** Fotografía de personas a pantalla completa (~60% izquierda)
- **Panel de título:** Rectángulo teal (`#00879B`) en zona derecha (~40%)
- **Texto:** Blanco, Calibri Light, centrado en panel teal
- **Logo:** Skilling Center Tecmilenio en esquina superior izquierda sobre la foto

**Imagen sugerida para portada del curso:** `image1.jpeg` (equipo, puños unidos)

### 2. Diapositiva de contenido
- **Fondo:** Blanco `#FFFFFF`
- **Barra vertical izquierda:** `#00879B` o `#00534C`, 8–12px de ancho
- **Logo Tecmilenio:** Esquina superior derecha
- **Título de sección:** Verde teal `#00534C`, Calibri Bold
- **Cuerpo:** `#44546A`, Calibri Regular

### 3. Diapositiva de sección / divisor
- Misma estructura que portada pero con imagen diferente
- Panel teal contiene el número y nombre del bloque (ej. "Bloque 1 — Amenazas con IA")

### 4. Diapositiva infográfica
- **Fondo:** Blanco
- **Barra superior:** Franja teal `#40C6BD` de ~20px
- **Elementos:** Hexágonos o círculos con gradiente de `#40C6BD` a `#00534C`
- Íconos blancos dentro de figuras teal

---

## Imágenes disponibles en el template

Todas están en `source/template_assets/`

| Archivo | Descripción | Diapositiva sugerida |
|---------|-------------|----------------------|
| `image1.jpeg` | Equipo haciendo fist bump — colaboración grupal | Portada general del curso |
| `image3.jpeg` | Joven estudiante con laptop, sonriendo | Portada Día 1 (accesible, tecnología) |
| `image5.png` | Persona trabajando en laptop con café | Portada Día 3 (trabajo híbrido) |
| `image6.jpeg` | Mujer profesional en oficina moderna | Portada Día 2 (identidad, profesionalismo) |
| `image9.jpeg` | Equipo uniendo manos sobre un puzzle | Portada Día 4 (respuesta, trabajo en equipo) |
| `image10.jpeg` | Agenda con notas coloridas y laptop | Planeación, estructura del curso |
| `image11.jpeg` | Hombre en videollamada tomando notas | Día 1 (deepfakes, videollamadas sospechosas) |

### Imágenes de fondo adicional (archivo externo)
`Back Skilling Center.jpeg` — Imagen de fondo institucional Tecmilenio

---

## Logos disponibles

| Archivo | Descripción | Uso |
|---------|-------------|-----|
| `image2.png` | Logo "Kick Off — Skilling Center Tecmilenio" horizontal, fondo blanco | Portadas de arranque |
| `image4.png` | Logo "TECMILENIO" texto, verde oscuro, fondo blanco | Diapositivas de contenido |
| `image12.png` | Logo "Skilling Center Tecmilenio" árbol + texto teal y verde | Logo principal en todos los slides |

---

## Elementos infográficos del template

### Diagrama de proceso circular (image7 slide)
- Círculo central con foto
- 5 puntos satélite con círculos `#40C6BD` → `#00534C` (gradiente por tamaño)
- Líneas punteadas de conexión en `#6BCABA`
- Barra lateral izquierda `#00879B` con título vertical

**Uso en curso:** Fases de NIST CSF, pasos de respuesta a incidentes, etapas de un ataque.

### Diagrama de hexágonos (image8 slide)
- 5 hexágonos en cadena horizontal
- Color: `#B1DFDC` relleno con borde negro grueso
- Íconos teal en esquinas de cada hexágono
- Franja superior `#40C6BD`

**Uso en curso:** Comparar 5 tipos de MFA, 5 controles CIS, 5 señales de phishing.

---

## Reglas de aplicación para el curso

1. **Fondo predeterminado:** Siempre blanco `#FFFFFF`. Reservar fondos teal para portadas y divisores de sección.
2. **Jerarquía de color:** Verde oscuro `#00534C` para títulos, turquesa `#40C6BD` para highlights y puntos de lista.
3. **Tablas:** Encabezado `#00534C` con texto blanco; filas alternadas `#B1DFDC` y `#FFFFFF`.
4. **Alertas / advertencias:** Usar `#ED7D31` (naranja del tema) para elementos de riesgo alto.
5. **Consistencia tipográfica:** Calibri Light para títulos, Calibri regular para cuerpo.
6. **Logo:** Siempre presente en esquina superior derecha en diapositivas de contenido.
