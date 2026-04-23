# 🏀 NBA United States Map

Aplicación web interactiva que muestra el mapa de Estados Unidos con información en tiempo real de los equipos de la NBA — clasificaciones, jugadores, resultados recientes y próximos partidos.

![NBA Map Preview](https://cdn.nba.com/logos/nba/1610612747/global/L/logo.svg)

---

## 🗺️ ¿Qué es?

Una single-page application (SPA) sin frameworks ni build steps, que combina un mapa interactivo de EEUU con datos reales de la temporada NBA 2025-26. El usuario puede explorar equipos por estado, consultar la clasificación por conferencias y divisiones, y ver resultados y próximos partidos de cada equipo.

---

## ✨ Características

### Mapa Interactivo
- Mapa SVG de todos los estados de EEUU renderizado con D3.js + TopoJSON
- Los estados con equipo NBA se resaltan en verde
- Al seleccionar un estado se muestra la información de su(s) equipo(s)
- Selección tipo radio: al elegir un estado, el anterior se desmarca automáticamente

### Panel de Clasificación (izquierda)
- Clasificación real de la temporada 2025-26
- Organizada por **Conferencia Este / Oeste** y por **divisiones** (Atlantic, Central, Southeast, Northwest, Pacific, Southwest)
- Columnas: Posición, Equipo, Victorias, Derrotas, PPG (puntos anotados/partido), PCG (puntos recibidos/partido), % Victorias
- Indicadores visuales de corte de **Playoffs (top 6)** y **Play-in (7-10)**
- Botón **↻ Actualizar** que obtiene datos en tiempo real desde la API de ESPN

### Panel de Equipo (derecha)
- Logo, nombre, ciudad, conferencia y división
- Jugadores destacados con foto oficial de la NBA
- Últimos 5 partidos con resultado (victoria/derrota), marcador y rival
- **Próximo partido**: rival, fecha, hora y condición (local/visitante)

### Tema Claro / Oscuro
- Toggle animado en el header para cambiar entre tema claro y oscuro
- Implementado con **CSS Custom Properties** — el cambio es instantáneo y afecta a todos los elementos (mapa, tablas, tarjetas, textos)

### Versión Móvil
- Diseño completamente adaptado para pantallas pequeñas
- Navegación inferior con tres pestañas: 🏆 Clasificación · 🗺️ Mapa · 🏀 Equipo
- Al tocar un estado en el mapa, cambia automáticamente a la pestaña de Equipo
- Badge naranja en la pestaña Equipo cuando hay un estado seleccionado

---

## 🛠️ Tecnologías

| Tecnología | Uso |
|---|---|
| **HTML5** | Estructura, single file sin build step |
| **CSS3 + Custom Properties** | Temas claro/oscuro, layout responsive, animaciones |
| **Vanilla JavaScript (ES6+)** | Lógica de la aplicación, gestión de estado |
| **D3.js v7** | Renderizado del mapa SVG, proyección geográfica Albers USA |
| **TopoJSON v3** | Geometría vectorial de los estados de EEUU |
| **ESPN Public API** | Clasificaciones y partidos en tiempo real (sin API key) |
| **NBA CDN** | Logos oficiales de equipos y fotos de jugadores |
| **Google Fonts** | Tipografías Bebas Neue y DM Sans |

---

## 📡 APIs Utilizadas

### ESPN Public API (sin autenticación)
```
# Clasificaciones
GET https://site.api.espn.com/apis/v2/sports/basketball/nba/standings?season=2026

# Partidos del día (resultados + próximos)
GET https://site.api.espn.com/apis/site/v2/sports/basketball/nba/scoreboard
```

### NBA CDN (logos y fotos)
```
# Logo de equipo
https://cdn.nba.com/logos/nba/{teamId}/global/L/logo.svg

# Foto de jugador
https://cdn.nba.com/headshots/nba/latest/260x190/{playerId}.png
```

### Mapa TopoJSON
```
https://cdn.jsdelivr.net/npm/us-atlas@3/states-10m.json
```

---

## 🚀 Cómo usar

No requiere instalación, servidor ni dependencias. Es un único fichero HTML autocontenido:

```bash
# Simplemente abre el fichero en cualquier navegador moderno
open nba-map.html
```

O súbelo a cualquier hosting estático (GitHub Pages, Netlify, Vercel...) y funciona directamente.

---

## 📁 Estructura del fichero

```
nba-map.html
├── <style>
│   ├── CSS Custom Properties (temas claro/oscuro)
│   ├── Layout desktop (3 paneles)
│   └── Layout móvil (bottom nav + media queries)
│
└── <script>
    ├── Datos
    │   ├── GAMES          — Últimos partidos (historial)
    │   ├── NEXT_GAMES     — Próximos partidos por equipo
    │   ├── STANDINGS_RAW  — Clasificación temporada 2025-26
    │   └── TEAMS          — Info de los 30 equipos + plantillas
    │
    ├── Tema
    │   └── toggleTheme()  — Cambia entre claro/oscuro via CSS vars
    │
    ├── Clasificación
    │   ├── buildStandings() — Renderiza tabla con divisiones
    │   └── showConf()       — Filtra por conferencia
    │
    ├── Panel de equipo
    │   ├── buildPanel()   — Genera tarjetas con jugadores y partidos
    │   └── getGames()     — Filtra partidos de un equipo
    │
    ├── Mapa (D3.js)
    │   ├── buildMap()           — Renderiza SVG (desktop + mobile)
    │   ├── selectState()        — Selección radio de estados
    │   └── refreshAllMapFills() — Actualiza colores (tema/selección)
    │
    ├── Móvil
    │   ├── switchTab()      — Navegación entre pestañas
    │   └── buildPanelMobile() — Replica contenido en vista móvil
    │
    └── Actualización en tiempo real
        └── refreshData()  — Fetch a ESPN API → actualiza clasificación,
                             resultados y próximos partidos
```

---

## 📊 Datos incluidos (temporada 2025-26)

- **30 equipos** NBA con colores, logo, ciudad y conferencia
- **Clasificación completa** con estadísticas por partido (PPG, PCG, %V)
- **20 partidos** recientes (11-13 Abril 2026)
- **Próximos partidos** pre-cargados (25-26 Abril 2026), actualizables en tiempo real
- **Plantillas** con los jugadores más destacados de cada equipo

---

## 🌐 Compatibilidad

Probado y compatible con:
- Chrome / Edge (Chromium) 90+
- Firefox 88+
- Safari 14+
- Móvil: Chrome para Android, Safari para iOS

---

## 📝 Licencia

Proyecto de uso personal / educativo. Los logos, imágenes y datos de equipos son propiedad de la **NBA**. Los datos de partidos proceden de la API pública de **ESPN**.
