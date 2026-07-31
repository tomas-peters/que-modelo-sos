[README.md](https://github.com/user-attachments/files/30595009/README.md)
# ¿Cuál es tu modelo experimental?

Test de personalidad tipo BuzzFeed / Sombrero Seleccionador para el seminario de becarios. Los participantes escanean un QR y responden preguntas absurdas (nada de ciencia de por medio) que arman un perfil de personalidad. Primero se revela un **arquetipo** (El Arquitecto ⚙️, El Explorador 🧭 o El Estratega 🛡️) y recién ahí el modelo experimental asociado: **Drosophila melanogaster** 🪰, **cultivo celular** 🧫 o **ratas y ratones de laboratorio** 🐭. Ningún modelo queda como "el mejor" — los tres tienen virtudes y defectos igual de simpáticos. Al final del seminario podés mostrar en el proyector el % del público que cayó en cada categoría.

Todo el juego es un único archivo (`index.html`), no necesita instalación ni servidor propio.

## Probarlo ahora mismo, antes de subir nada

Simplemente hacé doble clic en `index.html` y se abre en el navegador. Podés jugar una partida completa vos mismo para probarlo.

## Cómo editar las preguntas y los resultados

Abrí `index.html` con cualquier editor de texto (Bloc de notas, VS Code, etc.) y buscá la sección que dice:

```
CONFIGURACIÓN DEL JUEGO — esta es la parte que pueden editar a gusto
```

Ahí van a encontrar, en este orden:

- **`RESULTADOS`**: un bloque por cada una de las 3 categorías (`cultivo`, `drosophila`, `ratones`), con:
  - `arquetipo` / `arquetipoEmoji`: el nombre y emoji que se revela primero ("El Arquitecto ⚙️", etc.)
  - `organismo` / `organismoEmoji`: el modelo experimental que se revela al final.
  - `frase`: la frase corta que aparece debajo del arquetipo.
  - `virtudes` / `defectos`: las listas de rasgos que se muestran como "chips" de colores.
  - `descripcionArquetipo` / `descripcionOrganismo`: los dos párrafos largos (uno para cada pantalla de revelación).
- **`RESULTADOS_MIXTOS`**: el texto que se muestra si alguien empata entre dos categorías.
- **`PREGUNTAS`**: la lista de preguntas. Cada pregunta tiene un `texto` y 3 `opciones`, y cada opción tiene un `cat` (`drosophila`, `cultivo` o `ratones`) que indica a qué categoría suma esa respuesta. A propósito ninguna pregunta menciona laboratorio ni ciencia — la gracia es que no se note qué respuesta suma para cada perfil hasta el resultado final.

Para agregar o sacar una pregunta, simplemente copien/borren uno de los bloques `{ texto: ..., opciones: [...] }` del array `PREGUNTAS`. No hace falta tocar nada de lo que está más abajo en el archivo (esa parte es la lógica del juego).

**Importante:** no hace falta ningún programa especial para editar esto, ni saber programar — es simplemente texto entre comillas. Eso sí, tengan cuidado de no borrar comas, comillas o llaves `{ }` al editar.

## Cómo agregar fotos propias

Por ahora cada resultado muestra un emoji grande (🪰 🧫 🐭). Si más adelante quieren poner una foto real (por ejemplo, del propio labo):

1. Creen una carpeta llamada `images` al lado de `index.html`.
2. Guarden ahí tres fotos con estos nombres exactos:
   - `drosophila.jpg`
   - `cultivo.jpg`
   - `ratones.jpg`
3. Listo — el juego las va a mostrar automáticamente. Si en algún momento sacan la foto o el nombre no coincide, no pasa nada: vuelve a mostrarse el emoji.

## Cómo funciona el conteo de porcentajes en vivo

Cada vez que alguien termina el juego, se envía un "+1" a un contador público y gratuito ([abacus.jasoncameron.dev](https://abacus.jasoncameron.dev)) para su categoría. En la pantalla de inicio hay un link chiquito arriba a la derecha que dice **"📊 resultados en vivo"** — tóquenlo desde la notebook que están proyectando para mostrar los porcentajes acumulados de todo el público. Se actualiza solo cada 8 segundos, o pueden forzar la actualización con el botón "Actualizar ahora".

Si por algún motivo el wifi del auditorio falla, el juego sigue funcionando igual para cada participante — lo único que no se actualiza es el conteo grupal.

**Para reiniciar el contador en un futuro seminario** (para que no se sumen a los resultados de esta vez): busquen la línea

```js
const NAMESPACE = "leloir-seminario-becarios-2026";
```

y cámbienla por cualquier otro texto (por ejemplo, agregando la fecha nueva). Con eso alcanza para que el conteo arranque de cero.

## Cómo subirlo a GitHub y publicarlo con un link

Esto les va a dar una URL pública (tipo `https://usuario.github.io/nombre-repo/`) que pueden convertir en QR y proyectar.

### 1. Crear una cuenta de GitHub (si no tienen)

Entren a [github.com](https://github.com) y creen una cuenta gratuita.

### 2. Crear el repositorio

1. Arriba a la derecha, toquen el `+` → **New repository**.
2. Pónganle un nombre, por ejemplo `que-modelo-sos`.
3. Dejen la opción **Public**.
4. No marquen "Add a README" (ya tenemos uno).
5. Toquen **Create repository**.

### 3. Subir los archivos (sin usar la terminal)

En la página del repo recién creado va a aparecer un link que dice **"uploading an existing file"**.

1. Tóquenlo, y arrastren `index.html` (y la carpeta `images` si ya tienen fotos) a la ventana.
2. Abajo, escriban un mensaje como "primera versión del juego" y toquen **Commit changes**.

### 4. Activar GitHub Pages

1. En el repo, vayan a **Settings** (arriba).
2. En el menú de la izquierda, busquen **Pages**.
3. En "Branch", elijan `main` y la carpeta `/ (root)`, y toquen **Save**.
4. Esperen 1-2 minutos y refresquen la página. Va a aparecer un mensaje verde con el link público, algo como:

   `https://<usuario>.github.io/que-modelo-sos/`

Ese es el link que van a proyectar como QR.

### 5. Generar el QR para proyectar

No hace falta hacer nada especial: el propio juego genera el QR automáticamente en su pantalla de inicio, apuntando a la URL donde esté publicado. Así que simplemente abran ese link en la notebook que van a proyectar, y el QR que aparece ahí es el que la gente tiene que escanear.

### 6. Actualizar el juego más adelante

Cada vez que editen `index.html` con cambios (nuevas preguntas, fotos, etc.), vuelvan al repo en GitHub, toquen el archivo, luego el lápiz (✏️ Edit), peguen el contenido actualizado, y hagan **Commit changes**. GitHub Pages se actualiza solo, en general en menos de un minuto.

## Colaborar entre varios compañeros

Cualquiera con acceso de escritura al repositorio puede editar `index.html` directamente desde el navegador (botón ✏️ en GitHub) sin instalar nada. Para invitar compañeros: **Settings → Collaborators → Add people**.

## Resumen para el día del seminario

1. Abran el link de GitHub Pages en la notebook conectada al proyector.
2. Dejen esa pantalla (con el QR) proyectada mientras la gente escanea con el celular.
3. Cada uno juega en su propio teléfono.
4. Al final, en esa misma notebook, toquen "📊 resultados en vivo" para mostrar los porcentajes de todo el público.
