---
description: Revisa los cambios de index.html y, si está todo en orden, los sube a GitHub.
---

Vas a publicar los cambios de la app DaBass siguiendo estos pasos en orden. Detenete y avisá al usuario si algún paso encuentra un problema; no subas nada si la revisión falla.

1. Mostrá un resumen de los cambios pendientes (git status y git diff) para que quede claro qué se va a subir. Si no hay nada pendiente, decilo y terminá acá.

2. Si index.html cambió, revisalo contra las reglas del proyecto delegando en el subagente revisor-ejercicios. Pasale en el pedido el `git diff` completo de index.html (el subagente no puede correr git por su cuenta). Tiene que verificar:
   - Que el array EXERCISES solo haya sumado entradas al final, sin pisar las existentes.
   - Que no se hayan agregado dependencias externas: todo autocontenido en index.html.
   - Que no se hayan tocado a la ligera las constantes del motor (MAX_STRETCH y la asignación de trastes).

3. Si la revisión encuentra un problema, o marca algo para revisión humana, detenete acá y explicá qué está mal. No sigas con la subida.

4. Si está todo en orden, hacé el commit con un mensaje descriptivo de lo que cambió y después el push a la rama main.

5. Confirmá al usuario que la subida se completó.
