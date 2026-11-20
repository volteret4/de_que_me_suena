# ¿De qué me suena?

Juego web: suena un trozo de una canción y hay que acertar cuál es entre 4 opciones. Cuanto antes aciertes, más puntos.

- **Canciones** (no hace falta cuenta salvo en la primera):
  - *Mis escuchas*: `user.getTopTracks` de Last.fm (semana, mes, 3/6/12 meses o todas) o `user.getWeeklyTrackChart` entre dos fechas.
  - *Estilos*: `tag.getTopTracks` de una o varias etiquetas, mezcladas a partes iguales; si una etiqueta tiene pocas canciones, se completa con lo más escuchado de sus artistas principales (`tag.getTopArtists`).
  - *Un país*: `geo.getTopTracks`.
  - *Artistas*: `artist.getTopTracks` de uno o varios artistas, mezclados.
  - *Éxitos*: `chart.getTopTracks`, lo más escuchado en todo Last.fm.
  - *Lista de Deezer*: cualquier lista pública por su enlace; trae los fragmentos incluidos.
- **Audio**: fragmentos de 30 s de Deezer (JSONP) y, si no hay, de iTunes.
- **Fondo**: bandas de frecuencia (por defecto) u osciloscopio con lo que suena (Web Audio `AnalyserNode` + canvas; Deezer e iTunes sirven los fragmentos con CORS).
- **Guardado**: ajustes, récords (uno por fuente) y canciones sin fragmento en `localStorage`.
- **Enlaces**: la dirección guarda la fuente para compartirla: `?user=…&period=…`, `?tag=80s,synthpop`, `?country=spain`, `?artist=Radiohead,Queen`, `?chart=1`, `?playlist=<id>`.

Es una página estática para GitHub Pages, sin servidor ni ficheros que subir.

## Retos

Al acabar, «Retar a alguien» copia un enlace `?reto=…` con la partida entera comprimida: canciones, opciones, punto de inicio de cada trozo, ajustes y tu resultado en cada ronda. Quien lo abre juega exactamente lo mismo y al final ve la comparación. No necesita base de datos.

## Ranking (opcional, con Firebase)

Si `FIREBASE_CONFIG` en `index.html` es `null`, el ranking no aparece y no se carga nada de Firebase. Para activarlo:

1. Crea un proyecto en <https://console.firebase.google.com> (el plan gratuito Spark basta).
2. *Authentication* → *Sign-in method*: activa **Google**. En *Settings → Authorized domains* añade `volteret4.github.io`.
3. *Firestore Database*: créala en modo producción y pega en *Rules* el contenido de [`firestore.rules`](firestore.rules).
4. *Configuración del proyecto* → *Tus apps* → añade una app web y copia el objeto `firebaseConfig` en `FIREBASE_CONFIG`.

Funcionamiento:

- Cada persona entra con Google y elige si sus partidas son **privadas** (por defecto: no se publica nada) o **públicas**. Al pasar a privadas se borran sus puntuaciones publicadas.
- Se guarda solo la mejor puntuación de cada persona en cada tabla. Una tabla es una fuente más los ajustes que cambian la puntuación; cada reto tiene su propia tabla.
- «Mis escuchas» no tiene ranking (cada cual juega con sus canciones), pero un reto hecho con ellas sí.
- Las reglas solo dejan escribir lo propio y rechazan puntuaciones imposibles (más de 2000 por acierto). Como la puntuación se calcula en el navegador, alguien con maña podría inflarla dentro de ese límite.

## Ajustes

- **Partida**: por rondas o contrarreloj, número de rondas o tiempo total, tiempo por canción.
- **Dificultad**: canciones en juego, distractores al azar o del mismo artista, carátulas en las opciones, inicio del trozo.
- **Puntos**: penalización por fallo y premio según popularidad.
- **Fondo**: bandas de frecuencia u osciloscopio.

## Probar en local

```bash
python3 -m http.server 8000
```
