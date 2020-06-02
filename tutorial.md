pandoc .docx -s --wrap=none --atx -s -f docx+empty_paragraphs+styles -t markdown -o mioCid.md

pandoc 01mio_cid_final_intro.docx 02mio_cid_final.docx -s --wrap=none --atx -f docx+empty_paragraphs

`::: \{custom-style="\[Párrafo básico\]"\}\r?\n?(.*|)\r?\n?:::`

`::: \{custom-style="\[Párrafo básico\]"\}[\s\S]*?:::`

## 1. Intro

Lo que sigue es un objeto anfibio: mitad tutorial, mitad propuesta. La parte propuesta tiene que ver con una constatación: los flujos de trabajo editoriales en España (y en la mayoría de los países hispanos) adolecen de una ineficiencia alarmante, que proviene, sobre todo, del desface de una industria que trabaja como si lo digital no fuese una capa de la realidad, sino un añadido algo molesto que ha venido a exigir mejoras en un flujo de trabajo que se mantuvo inalterable (al menos conceptualmente, durante muchos, demasiados años). Al menos hasta donde se y veo, la adaptación a lo digital ha resultado más cosmética que real, y al menos en lo que respecta a la producción, atañe más al tipo de herramientas y de software que se utiliza más que (como sería deseable) a la idea que fundamenta la producción.
La parte tutorial propone un caso de estudio real. Lo que me propongo es realizar un experimento y proponer un flujo de trabajo orientado a la eficiencia y a la automatización, a la integración de herramientas, con la esperanza que esto de una idea de las posibilidades desaprovechadas que la transformación digital ofrece a los editores.
Aquí hablo además de un contexto muy particular: de cómo un pequeño editor podría resolver un proceso de producción de la forma más eficiente posible.

### 1.1 Fundamentos

### 1.2 Requisitos

Alguna familiaridad con la línea de comandos.
Conocimientos básicos de HTML y CSS. Conocimientos de InDesign a nivel de diseño editorial.
Una mente abierta (lo anterior se puede reemplazar con una aplicada búsqueda en Google, esto último no).

### 1.3 Herramientas & software

Para los efectos de este tutorial necesitaremos tener instalado en nuestro sistema:

- Editor de texto plano (no procesador de texto): yo utilizaré Atom, pero hay una serie de editores de texto igualmente útiles y libres (Visual Studio Code, Sublime Text, Vim, etc...)
- Línea de comandos (en Windows, el PowerShell, en Linux el terminal o uno cualquiera de sus emuladores; en Mac, la terminal).
- Pandoc
- InDesign
- Git y el cliente de escritorio de GitHub
- MS Word
- Jeckyll

### El problema

Supongamos que hará unos diez años editamos y publicamos un libro, que ahora queremos o necesitamos reeditar (es el caso, de hecho). Los archivos siguen almacenados en un disco duro, de modo que todo estaría en recuperarlos, abrirlos, hacer las correcciones y ajustes que hicieran falta, y volver a imprimir.

Pero resulta que esta vez también necesitamos crear (o recrear mejor dicho) un libro electrónico (que en su momento conseguimos utilizando una herramienta de conversión y que ahora, probando el archivo, resulta que funciona en el kindle, funciona a medias en la tablet, y se desarregla en el móvil como el pulcro invitado a una boda a las seis de la mañana después de muchas visitas al buffet de bebidas). Bien, esto todavía no es un problema, por que podemos exportarlo tranquilamente desde InDesign. Pero también sabemos que convendría hacer el libro electrónico lo más accesible posible, y que tal vez sería una buena idea poder disponer también de una maqueta alternativa para una versión en _print on demand_. Sin hablar de los metadatos, pero hace diez años ¿sabíamos que eran los metadatos? En fin, muchas preguntas.

Ah, lo olvidaba: por la razón que sea, tenemos un fin de semana para acabar el proyecto.


## Naturalmente, un manuscrito

Pongamos manos a la obra.

En la carpeta "tripa" efectivamente hay un archivo InDesign. Perfecto. El problema es que mi versión de InDesign decide que no es un archivo con quién quiera tener algún tipo de trato.

![InDesign no puede abrir el archivo](imgs/noSePuedeAbrirElArchivoInDesign.png)

El mensaje no sólo es desalentador, también es totalmente críptico. ¿Por qué no se puede abrir? ¿El archivo está corrupto? ¿Tiene que ver con la versión de InDesign que estoy usando? Ninguna pista, ninguna idea. Podría probar utilizando la versión de InDesign con la que cree el archivo, pero, demonios, hace diez años de eso, ¿Cuál podría haber sido? Sin contar con que tendría que descargarla e instalarla y sin ninguna garantía de que el asunto funcionase.

Pasamos al plan B entonces, que consiste en buscar la última versión del manuscrito en MS en Word y rehacer la maqueta.

El manuscrito en cuestión se produjo después de un laborioso escaneo: nada extraño considerando que la última edición del libro en cuestión era de hace unos treinta o cuarenta años atrás. Cualquiera que halla escaneado un libro sabe que los resultados distan mucho de definir la palabra prolijidad. El resultado: la corrección tomó un buen tiempo, primero utilizando herramientas automatizadas (Grep, fundamentalmente, pero ya hablaremos de eso), y un trabajo denodado de nuestro corrector. Por tanto, el ir y venir de borradores por correo electrónico fue constante.

Considerando lo anterior, resulta natural que cuando miremos en la carpeta que contiene los borradores, encontremos no uno sino una serie de archivos (versión2, versiónfinal, versión definitiva... espera, ¿"versiondefinitiva" es más final que "final" ¿o es al revés?). Siempre podemos buscar sencillamente la última versión del documento en MS Word y trabajar con esa. Pero, ¿Es realmente la última o la corrección final fue hecha en InDesign? De ser así, posiblemente podríamos recuperar el log del control de cambios en InDesign... solo que no podemos. ¿O tal vez la revisión más reciente incluía cosas que descartamos en la versión final del libro? Es una posibilidad. De paso y ya que estamos, convendría revisar mis intercambios de mail con el corrector del libro.

A todo esto, han pasado un par de horas y estamos sentados frente al ordenador con deseos de tirarlo por la ventana y correr a ahogarnos de chupitos en algún antro infame.

Todos estos problemas, o un subconjunto de ellos, o algún otro que no hemos listado aquí han podido ocurrir. Se sabe, los sistemas documentales son azarosos y dependen de seres humanos que toman decisiones y esas decisiones pueden o no ser consistentes, sin hablar que si no se deja registro de por qué las tomamos, no hay forma de que podamos saberlo, eso si fuimos nosotros quienes tomamos la decisión y no alguien más, otro editor u otro diseñador.


Demasiados problemas. Pero lo cierto es que hay maneras de hacer todo esto muchísimo más sostenible, eficiente, agradable y de paso, aumentando el valor del libro final de una manera evidente. Se trata simplemente de pensar en digital. Ok, depende de cambiar algunos hábitos por otros, deshacernos de prejuicios, y también exige un aprendizaje, pero qué clase de editores seríamos si tuviéramos algo en contra del aprendizaje.

Necsitamos, eso sí, software en que podamos confiar, lo que equivale a decir que necesitamos herramientas que cumplan los siguientes requisitos:

1. Que sean sostenibles (o sea: que no cambien con el tiempo o no tengan problemas de compatibilidad reversa)
2. Que nos permitan añadir estructura al contenido
3. Y separar el contenido de la presentación
4. Hagan posible un control de versiones eficaz y colaborativo
5. Una automatización eficiente de nuestro flujo de trabajo (o sea: herramientas que se comuniquen bien entre ellas)

### Markdown

MS Word es un software estupendo, pero si lo consideramos bien, no cumple ninguno de estos requisitos: cada versión hace algo más complicado trabajar con la anterior (sin contar con que en los últimos años ha reescrito un par de veces su código y cambiado su interfaz), su manera de añadir estructura a los documentos es mas bien esotérica, su sistema de control de cambios es desesperante, y por último, pese a que se ha trabajado bastante la integración con otros softwares (digamos InDesign), el tipo de código que añade al texto transforma todo el proceso en una invitación al error. Lo que haría casi cualquier diseñador sería trabajar con word la estructura (añadiendo encabezados) y exportar intentando mapear los estilos de word con indesign de la manera más exacta posible. Pero esto, sin duda, añade un tedioso proceso para el cual por otra parte, no tenemos tiempo... ¿Qué hacer?


### Primer paso: formatear

Si revisamos el archivo que vamos a adoptar como punto de partida, podemos darnos cuenta de alguna cosas:

1. No hay estructura.

Los estilos no están asociados a encabezados, de manera que no hay un _outline_ que utilizar para estructurar nuestro texto. Esto se puede reparar de varias maneras.

- Crear la estructura en MS Word
- convertir el archivo a Markdown y formatearlo con un editor de texto
