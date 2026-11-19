# ¿De qué me suena?

Juego web: suena un trozo de una canción de tus escuchas de Last.fm y hay que acertar cuál es entre 4 opciones. Cuanto antes aciertes, más puntos.

- **Canciones**: `user.getTopTracks` de Last.fm (semana, mes, 3/6/12 meses o todas) o `user.getWeeklyTrackChart` entre dos fechas.
- **Audio**: fragmentos de 30 s de Deezer (JSONP) y, si no hay, de iTunes.
- **Fondo**: osciloscopio con la onda de lo que suena (Web Audio `AnalyserNode` + canvas; Deezer e iTunes sirven los fragmentos con CORS).
- **Guardado**: ajustes, récords y canciones sin fragmento en `localStorage`.

Es una página estática para GitHub Pages, sin servidor ni ficheros que subir.

## Ajustes

En la pantalla de inicio: canciones entre las que elegir, distractores al azar o del mismo artista, carátulas en las opciones, inicio del trozo, tiempo por canción, rondas o contrarreloj, penalización y premio según escuchas.

## Probar en local

```bash
python3 -m http.server 8000
```
