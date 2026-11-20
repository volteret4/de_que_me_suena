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

## Ajustes

- **Partida**: por rondas o contrarreloj, número de rondas o tiempo total, tiempo por canción.
- **Dificultad**: canciones en juego, distractores al azar o del mismo artista, carátulas en las opciones, inicio del trozo.
- **Puntos**: penalización por fallo y premio según popularidad.
- **Fondo**: bandas de frecuencia u osciloscopio.

## Probar en local

```bash
python3 -m http.server 8000
```
