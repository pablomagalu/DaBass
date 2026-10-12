\# CLAUDE.md — DaBass (practicador de escalas para bajo)



\## Qué es este proyecto

App de práctica de bajo de archivo único: un solo `index.html` autocontenido, sin build, sin dependencias externas. UI en español, nombres de notas en inglés (A–G). Tres secciones reordenables: Escalas, Ejercicios y Notas.



\## Reglas al modificar

\- Todos los cambios van dentro del único `index.html`. No agregar build system ni dependencias externas.

\- Los ejercicios SIEMPRE se agregan al final del array `EXERCISES`. Nunca reemplazar ni pisar entradas existentes (ya hubo una regresión por sobrescribir entradas).

\- Al entregar cambios, devolver el archivo completo actualizado.



\## Constantes del motor (tocar con cuidado)

\- `MAX\_STRETCH = 3`: span máximo de 3 trastes por cuerda (caja real de 4 dedos).

\- Las cuerdas al aire se evitan solo si una alternativa pisada se mantiene dentro del span cómodo; la primera nota de una secuencia/posición queda exenta.

\- El fingering sube de forma monótona y no retrocede (`bestPatternAnchor` + `minFret` acumulado).

\- Las notas repetidas dentro de un patrón reutilizan la misma cuerda/traste de su primera aparición (`seenAbs` en `assignFrets`).



\## Deploy

\- Hosteado en Vercel desde el repo de GitHub `pablomagu/DaBass`.

\- El archivo principal se llama `index.html` por compatibilidad con Vercel.

\- Es una PWA: incluye `manifest.json` y `service-worker.js`.

\- Identidad git: usuario PML, email pablo.magalu@gmail.com.



