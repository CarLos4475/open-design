# Prompt de diseño — EcoRecicla Web Magazine

## Contexto del proyecto

Crea un sitio web completo para **EcoRecicla**, una plataforma ciudadana de reciclaje con sistema de recompensas. La app original fue desarrollada en Swift para iOS. A continuación se describe su arquitectura funcional y el modelo de datos para replicar correctamente todas las secciones.

---

## Modelo de datos y lógica de la aplicación

### Entidades principales

**Usuario**
- `id`, `nombre`, `apellido`, `email`, `password`
- `delegacion` (zona de CDMX: Del Valle, Coyoacán, Polanco, Xochimilco, Tlalpan, Iztapalapa, etc.)
- `ecopuntos` (entero, acumulable)
- `kg_reciclados` (decimal)
- `co2_evitado` (calculado: kg reciclados × factor por material)
- `rol`: `usuario` | `operador` | `administrador`
- `fecha_registro`, `activo` (bool)

**Material reciclable**
- `tipo`: `plastico` | `vidrio` | `papel` | `metal` | `organico` | `electronico`
- `puntos_por_100g` (o por pieza para electrónicos):
  - Plástico → 5 pts / 100g
  - Vidrio → 4 pts / 100g
  - Papel/Cartón → 3 pts / 100g
  - Metal → 8 pts / 100g
  - Orgánicos → 2 pts / 100g
  - Electrónicos (RAEE) → 20 pts / pieza
- `descripcion`, `instrucciones_deposito`, `aceptado_en` (lista de puntos verdes)

**Entrega de reciclaje**
- `id`, `usuario_id`, `punto_verde_id`
- `material_tipo`, `cantidad` (gramos o piezas)
- `puntos_otorgados` (calculado)
- `fecha`, `estado`: `pendiente` | `acreditado` | `rechazado`
- `operador_id` (quién registró la entrega)

**Punto verde (centro de acopio)**
- `id`, `nombre`, `direccion`, `delegacion`
- `latitud`, `longitud`
- `horario` (ej: "Lun–Sáb 8–18h")
- `materiales_aceptados` (array de tipos)
- `acepta_electronicos` (bool)
- `estado`: `activo` | `mantenimiento` | `cerrado`

**Recompensa / canje**
- `id`, `nombre` (ej: "Café gratis"), `descripcion`
- `costo_puntos` (ej: 50)
- `categoria`: `alimentos` | `descuento` | `transporte` | `ambiental`
- `fecha_expiracion`, `activo` (bool)

**Transacción de canje**
- `id`, `usuario_id`, `recompensa_id`
- `puntos_usados`, `fecha`, `codigo_canje`

**Promoción / novedad**
- `id`, `titulo`, `descripcion`, `tipo`: `promocion` | `evento` | `novedad`
- `fecha_inicio`, `fecha_fin`, `activo`

---

## Funcionalidades requeridas (todas deben estar presentes)

1. **Mostrar información general** — Hero, estadísticas globales, sección "¿Cómo funciona?", guía de materiales
2. **Consultas** — Consultar puntos y historial por email/cuenta
3. **Gestión de datos** — Registrar entregas, canjear recompensas, actualizar perfil
4. **Panel de administrador** — CRUD completo de usuarios, puntos verdes y entregas; exportar CSV; métricas del sistema
5. **Esquema de navegación claro** — Menú sticky con secciones bien definidas
6. **Acceso directo a funciones frecuentes** — Bloque de accesos rápidos visible desde el inicio
7. **Novedades y promociones** — Ticker de noticias, tarjetas de promociones activas
8. **Herramienta de búsqueda** — Búsqueda global con resultados inteligentes
9. **Nombre y logo** — "EcoRecicla" con ícono de reciclaje SVG
10. **Autogestionable** — Admin puede gestionar contenido sin código
11. **Responsive / Mobile-first** — Adaptable a móvil con menú hamburguesa

---

## Paleta de colores

```
Verde primario:   #639922  (--green-400)
Verde oscuro:     #3B6D11  (--green-600)
Verde muy oscuro: #27500A  (--green-800)
Verde claro fill: #EAF3DE  (--green-50)
Verde claro 100:  #C0DD97  (--green-100)

Teal acento:      #1D9E75  (--teal-400)
Teal oscuro:      #0F6E56  (--teal-600)
Teal fill:        #E1F5EE  (--teal-50)

Ámbar/acento:     #EF9F27  (--amber-200)
Ámbar oscuro:     #BA7517  (--amber-400)
Ámbar fill:       #FAEEDA  (--amber-50)

Grises:           #F1EFE8 / #D3D1C7 / #888780 / #5F5E5A / #2C2C2A
Blanco:           #FFFFFF
```

---

## Estilo visual — Diseño tipo MAGAZINE

Inspirado en revistas editoriales de moda y lifestyle (referencia: MAGZY UI Kit). El sitio debe sentirse como una **revista digital de alto impacto**, no como un dashboard de gobierno.

### Tipografía
- **Display / Títulos:** fuente serif condensada o sans-serif bold editorial (ej: `Playfair Display`, `Cormorant Garamond`, o `Syne` en 800). Títulos grandes, dominantes, con mucho carácter.
- **Cuerpo:** `DM Sans` o `Inter` en weight 300–400 para texto largo, aireado.
- **Labels / Tags:** uppercase, letter-spacing amplio, 10–12px, peso 700.

### Layout editorial
- **Hero**: Fondo oscuro (verde muy oscuro o negro) con el nombre **ECORECICLA** en tipografía display gigante, estilo portada de revista. Subtítulo pequeño y CTA.
- **Grid asimétrico**: mezclar columnas de 1/3 y 2/3, cards de distintas alturas, imágenes que rompen la cuadrícula.
- **Sección de materiales**: estilo "artículos de revista" — cada material como una tarjeta editorial con su ícono, título grande y descripción breve.
- **Sección de noticias/novedades**: layout tipo periódico con artículo destacado grande + artículos secundarios menores.
- **Promociones**: cards con foto de fondo, overlay de color y texto encima, como portadas de revista.
- **Estadísticas**: números enormes en verde/teal sobre fondo oscuro, al estilo infográfico editorial.
- **Footer**: dark, denso, con columnas tipo directorio de revista.

### Detalles de estilo
- Usar líneas horizontales finas (`1px solid`) como separadores editoriales
- Etiquetas de categoría al estilo magazine: `[ PLÁSTICO ]`, `[ METAL ]`, `[ RECICLAJE ]`
- Números de artículo o íconos decorativos tipo "01 / 02 / 03"
- Animaciones sutiles de entrada (fade + translateY) al hacer scroll
- Hover en cards: ligero zoom en imagen + overlay de color con opacity
- Sin bordes redondeados agresivos — usar `border-radius: 0` o máximo `4px` para mantener el look editorial
- Mezcla de fondos: secciones alternadas entre blanco crudo (`#FAFAF8`), verde muy oscuro y un tono crema (`#F5F0E8`)

### Navegación
- Barra superior minimalista con logo a la izquierda, links en mayúsculas espaciadas, y botón "SUSCRIBIRSE / REGISTRARSE" en verde primario
- En mobile: menú slide-in lateral con fondo oscuro

### Componentes clave con estilo magazine

**Hero section**
```
[FONDO OSCURO — verde 900 o negro]
ECORECICLA          ← tipografía display, enorme, ocupa toda la pantalla
Recicla. Gana. Transforma.   ← serif italic, tamaño mediano
[ REGISTRAR ENTREGA ]  [ VER PUNTOS VERDES ]
—————————————————————
1,240 USUARIOS   |   8.4 T RECICLADAS   |   23 PUNTOS VERDES
```

**Sección materiales — estilo grid editorial**
```
┌─────────────────┬──────────────────────────────┐
│  01             │  PLÁSTICO                    │
│  ──             │  Botellas PET, envases...    │
│  PLÁSTICO       │  +5 pts / 100g               │
│                 │  [ Ver instrucciones → ]     │
└─────────────────┴──────────────────────────────┘
```

**Novedades — layout periódico**
```
┌──────────────────────────────┬────────┬────────┐
│  ARTÍCULO DESTACADO          │ Nota 2 │ Nota 3 │
│  (ocupa 2/3 del ancho)       │        │        │
│                              │ Nota 4 │ Nota 5 │
└──────────────────────────────┴────────┴────────┘
```

---

## Instrucciones adicionales para la IA generadora

- Todo el sitio debe ser **un solo archivo HTML** autocontenido (HTML + CSS + JS inline)
- El JavaScript debe ser funcional: los formularios calculan puntos reales, las tabs cambian contenido, el admin panel tiene CRUD real con DOM manipulation
- Usar **SVG inline** para el logo e íconos (sin dependencias externas excepto Google Fonts)
- La barra de búsqueda debe tener un índice interno con al menos 10 resultados relevantes
- El panel de admin se protege con usuario `admin` / contraseña `eco2024`
- Incluir notificaciones tipo toast al realizar acciones
- El ticker de novedades debe ser animado (CSS marquee o JS)
- Compatible con Chrome, Firefox, Safari y Edge
- **No usar frameworks CSS externos** (sin Bootstrap, Tailwind, etc.) — CSS puro con variables

---

## Secciones del sitio (en orden)

1. **Barra de novedades** — ticker animado con últimas noticias
2. **Navegación** — sticky, minimalista, magazine
3. **Hero** — portada editorial oscura con nombre gigante
4. **Acceso rápido** — 6 botones de acceso a funciones frecuentes
5. **Servicios / Información general** — grid editorial con los 6 servicios
6. **¿Cómo funciona?** — pasos numerados estilo 01/02/03
7. **Materiales reciclables** — grid asimétrico tipo artículos
8. **Consultas y gestión** — tabs: Registrar | Consultar | Historial | Canjear
9. **Puntos verdes** — placeholder de mapa + lista de ubicaciones
10. **Novedades y promociones** — layout periódico + 3 tarjetas de promo
11. **Panel de administración** — login protegido + CRUD + métricas
12. **Footer** — dark, estilo directorio de revista

---

*Generado para el proyecto EcoRecicla — Hackathon CDMX 2026*
