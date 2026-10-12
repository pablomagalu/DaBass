---
name: agregar-ejercicio
description: Usar cuando el usuario pide agregar un ejercicio nuevo a la app DaBass. Guía cómo construir una entrada del array EXERCISES en index.html, con sus segmentos, offsets en semitonos y stepShift, respetando la regla de solo agregar al final.
---

Sos un asistente que agrega ejercicios a DaBass, un practicador de escalas para bajo de archivo único (index.html).

## Regla de oro
Los ejercicios SIEMPRE se agregan al FINAL del array EXERCISES. Nunca reemplaces, reordenes ni borres entradas existentes. Ya hubo una regresión por pisar entradas: no repitas ese error.

## Estructura de un ejercicio
Cada entrada define un patrón que el motor transporta por el mástil. Campos:

- `id`: identificador único en snake_case (no puede repetir uno existente).
- `name`: nombre descriptivo que se muestra en el selector.
- `description`: explicación musical del ejercicio.
- `segments`: uno o más segmentos `{ rootOffset, pattern }`. `rootOffset` es en cuántos semitonos arranca el segmento respecto de la raíz del paso; `pattern` es la lista de offsets en semitonos desde la raíz del propio segmento. Cada segmento se muestra como un paso separado, navegable de forma individual (no se fusionan).
- `stepShift`: cuántos semitonos sube la raíz en cada ciclo, para transportar el ejercicio por distintas tonalidades.
- `totalSteps`: cantidad de ciclos. Los pasos navegables son `totalSteps × segments.length`.
- `describeStep(segRootPC, segIdx)`: devuelve el texto de cada paso; usá `pcName(segRootPC)` para el nombre de la nota, en `<b>`.

Ejemplo real (copiá esta forma):

```js
  {
    id: 'augmented_dominant_maj7_resolution',
    name: 'Dominante Aumentada → Resolución Maj7',
    description: '...',
    segments: [
      { rootOffset: 0, pattern: [0,4,8,12,8,0] }, // tríada aumentada: R-3-5-R(8va)-5-R
      { rootOffset: 5, pattern: [0,4,7,11] },      // resuelve una 4ta arriba: maj7 = R-3-5-7
    ],
    stepShift: 1,
    totalSteps: 12,
    describeStep(segRootPC, segIdx){
      return segIdx===0
        ? `Arpegio aumentado de <b>${pcName(segRootPC)}</b> (dominante)`
        : `Resuelve a <b>${pcName(segRootPC)}</b> mayor7`;
    },
  },
```

## Cómo traducir una consigna musical a offsets
Convertí cada grado o nota del patrón a su distancia en semitonos desde la raíz. Ejemplos ya presentes en la app:

- "Tríadas Mayores - Salto 5ta": tríada mayor R-3-5-3-R = `[0,4,7,4,0]`, `stepShift: 7` (sube de a una quinta), `totalSteps: 12`.
- "Dominante Aumentada → Resolución Maj7": tríada aumentada R-3-5-R8-5-R = `[0,4,8,12,8,0]` que resuelve una cuarta arriba (`rootOffset: 5`) a un arpegio maj7 1-3-5-7 = `[0,4,7,11]`; `stepShift: 1`, `totalSteps: 12` (24 pasos navegables, porque cada segmento es su propio paso).
- "Escala Jónica Mayor - Ascenso y Regreso": grados 1-2-3-4-5-6-7-8-6-7-5-6-4-5-3-4-2-3-1 = `[0,2,4,5,7,9,11,12,9,11,7,9,5,7,4,5,2,4,0]`, `stepShift: 1`, `totalSteps: 12` (las 12 tonalidades).

## Procedimiento
1. Pedí o confirmá la consigna musical: qué grados o notas, en qué orden, y cómo transporta.
2. Traducí el patrón a offsets en semitonos desde la raíz.
3. Si hay más de una figura (por ejemplo una que resuelve en otra), separala en segmentos con su `rootOffset`.
4. Definí `stepShift` y `totalSteps`.
5. Agregá la entrada al final del array EXERCISES, sin tocar las anteriores.
6. Antes de commitear, pasale el `git diff` de index.html al agente `revisor-ejercicios`.
7. Entregá el index.html completo actualizado.
