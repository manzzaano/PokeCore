<div align="center">
  <img src="public/pokecore-logo.png" alt="PokeCore" width="360" />

  ![React](https://img.shields.io/badge/React-19-61DAFB?logo=react)
  ![Vite](https://img.shields.io/badge/Vite-6-646CFF?logo=vite)
  ![Tailwind](https://img.shields.io/badge/Tailwind_CSS-4-06B6D4?logo=tailwindcss)
  ![TanStack Query](https://img.shields.io/badge/TanStack_Query-5-FF4154?logo=reactquery)
  ![Zustand](https://img.shields.io/badge/Zustand-5-8B5CF6)

  **Pokédex de los 1025 Pokémon, en español y con carga instantánea.**
  En producción en **[manzzaano.github.io/PokeCore](https://manzzaano.github.io/PokeCore/)**.
</div>

---

## Qué hace

- **Regiones:** de Kanto a Paldea, con los tres iniciales de cada generación como portada.
- **Búsqueda** por nombre o número mientras escribes, y **filtro por los 18 tipos**.
- **Ficha completa:** estadísticas, debilidades, habilidades (también las ocultas), peso y altura, género, descripción por versión del juego, cadena evolutiva, variantes, versión shiny y unos 600 movimientos en español.
- **Favoritos** guardados en el navegador, sin cuentas ni servidor.
- **Diseño adaptado a móvil:** barra lateral plegable y cuadrícula de 2 a 4 columnas.

## Cómo consigue ir rápida

La PokéAPI no está pensada para pedirlo todo a la vez, así que cada dato se pide una sola vez y en el momento útil:

- **La lista de nombres se pide una vez** y TanStack Query la guarda una hora; la búsqueda filtra esa lista en el navegador, sin esperar a la red.
- **El filtro por tipo** consulta la API la primera vez y guarda la respuesta 24 horas, porque los tipos no cambian.
- **La ficha se pide antes del clic:** empieza a cargarse al pasar el ratón por la tarjeta y queda guardada media hora.
- **Imágenes por fases:** `SpriteImg` muestra primero el sprite pequeño y lo cambia por la ilustración oficial cuando carga (si no existe, prueba con la de HOME).
- **Todo en español sin peticiones extra:** tablas propias de movimientos, habilidades y efectividad de tipos.
- **Favoritos sin frenar la interfaz:** se guardan en `localStorage` cuando el navegador está libre, con `requestIdleCallback`.

Las decisiones están contadas en el caso de estudio: [leosoftware.dev/sistemas/pokecore](https://leosoftware.dev/sistemas/pokecore).

## Stack

| | |
|---|---|
| Interfaz | React 19, Tailwind CSS 4, Framer Motion, Lucide |
| Datos | TanStack Query 5 sobre la [PokéAPI](https://pokeapi.co) |
| Estado | Zustand (búsqueda, tipo y región elegidos) |
| Build | Vite 6 |
| Despliegue | GitHub Pages |

## En local

```bash
git clone https://github.com/manzzaano/PokeCore.git
cd PokeCore
npm install
npm run dev
npm run lint     # ESLint
```

## Despliegue

```bash
npm run deploy   # compila y publica dist/ en la rama gh-pages
```

GitHub Pages sirve la rama `gh-pages` desde la raíz.

## Estructura

```
src/
├── App.jsx                      # barra de favoritos, cabecera, cuadrícula y ficha
├── components/
│   ├── HomeScreen.jsx           # selector de región
│   ├── TypeFilter.jsx           # filtro de los 18 tipos
│   ├── ErrorBoundary.jsx        # recupera la interfaz si un componente falla
│   └── ui/                      # tarjeta, SpriteImg, barras de stats, badges, skeleton...
├── features/detail/             # ficha: detalle, evoluciones y descripciones por versión
├── hooks/                       # usePokemons, usePokemonDetail, useTypes, useFavorites
├── services/pokeApi.js          # cliente de la PokéAPI
├── store/usePokedexStore.js     # estado global con Zustand
└── data/                        # tabla de tipos y traducciones de movimientos y habilidades
```

---

<div align="center">
  <sub>Hecho por <a href="https://leosoftware.dev">Ismael Manzano León</a> · proyecto propio durante 1.º de DAM (2024-25)</sub>
</div>
