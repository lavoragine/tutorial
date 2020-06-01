


pandoc .docx -s --wrap=none --atx -s -f docx+empty_paragraphs+styles -t markdown -o mioCid.md

pandoc 01mio_cid_final_intro.docx 02mio_cid_final.docx -s --wrap=none --atx -f docx+empty_paragraphs



``::: \{custom-style="\[Párrafo básico\]"\}\r?\n?(.*|)\r?\n?:::``

``::: \{custom-style="\[Párrafo básico\]"\}[\s\S]*?:::``


## 1. Intro

Lo que sigue es un objeto anfibio: mitad tutorial, mitad propuesta. La parte propuesta tiene que ver con una constatación: los flujos de trabajo editoriales en España (y en la mayoría de los países hispanos) adolecen de una ineficiencia alarmante, que proviene, sobre todo, del desface de una industria que trabaja como si lo digital no fuese una capa de la realidad, sino un añadido algo molesto que ha venido a exigir mejoras en un flujo de trabajo que se mantuvo inalterable (al menos conceptualmente, durante muchos, demasiados años). Al menos hasta donde se y veo, la adaptación a lo digital ha resultado más cosmética que real, y al menos en lo respecta a la producción, atañe más al tipo de herramientas y de software que se utiliza más que (como sería deseable) a la idea que fundamenta la producción.
la parte tutorial propone un caso de estudio real. Lo que me propongo es realizar un experimento y proponer un flujo de trabajo orientado a la eficiencia y a la automatización, a la integración de herramientas, con la esperanza que esto de una idea de las posibilidades desaprovechadas que la transformación digital ofrece a los editores.
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

Supongamos que hará unos diez años editamos y publicamos un libro, que ahora queremos reeditar (ese es el caso, aunque esto también podría servir para un libro que estemos a punto de editar ahora). Los archivos siguen almacenados en un disco duro, de modo que todo estaría en recuperarlos, hacer las correcciones que hicieran falta hacer, y volver a imprimir... fácil, ¿no?
Pero resulta que esta vez deberíamos también crear un libro electrónico (que en su momento conseguimos utilizando una herramienta de conversión y que ahora, probando el archivo, resulta que funciona a medias en la tablet, funciona en el kindle, y se desarregla en el móvil como el pulcro invitado a una boda a las seis de la mañana después de muchas visitas al buffet de bebidas). Bien, esto todavía no es un problema, por que podemos exportarlo tranquilamente desde InDesign. Pero también sabemos (estos años no han pasado en vano) que convendría hacer el libro electrónico lo más accesible posible, y que tal vez sería una buena idea poder disponer también de una maqueta alternativa para una versión en print on demand. Sin hablar de los metadatos, pero hace diez años ¿sabíamos que eran los metadatos? En fin, muchas preguntas.
(todos estos problemas, o un subconjunto de ellos, o algún otro que no hemos listado aquí han podido ocurrir. Se sabe, los sistemas documentales son azarosos y dependen de seres humanos que toman decisiones y esas decisiones pueden o no ser consistentes, sin hablar que si no se deja registro de por qué las tomamos, no hay forma de que podamos saberlo, eso si fuimos nosotros quienes tomamos la decisión y no alguien más, otro editor u otro diseñador.)
Ah, lo olvidaba: tenemos un fin de semana para acabar el proyecto.

## 2. Configurando el espacio de trabajo


### 2.1 Herramientas & software
### 2.2 Árbol de archivos y repositorio


## Naturalmente, un manuscrito

Pongamos manos a la obra.


En la carpeta "tripa" efectivamente hay un archivo InDesign. Perfecto. El problema es que mi versión de InDesign decide que no es un archivo con quién quiera tener algún tipo de trato.

![InDesign no puede abrir el archivo](imgs/noSePuedeAbrirElArchivoInDesign.png)

El mensaje no sólo es desalentador, también es totalmente críptico. ¿Por qué no se puede abrir? ¿El archivo está corrupto? ¿Tiene que ver con la versión de InDesign que estoy usando? Ninguna pista, ninguna idea. Podría probar utilizando la versión de InDesign con la que cree el archivo, pero, demonios, hace diez años de eso, ¿Cuál podría haber sido? Sin contar con que tendría que descargarla e instalarla y sin ninguna garantía de que el asunto funcionase.

Pasamos al plan B entonces, que consiste en buscar la última versión de MS en Word y rehacer la maqueta.
Pero resulta que una vez hemos mirado en la carpeta, hemos encontrado una serie de archivos (versión2, versiónfinal, versión definitiva... espera, ¿"versiondefinitiva" es más final que "final" ¿o es al revés?). Siempre podemos buscar sencillamente la última versión del documento en word y trabajar con esa. Pero, ¿Es realmente la última o la corrección final fue hecha en InDesign? De ser así, posiblemente podríamos recuperar el log del control de cambios en InDesign... solo que no podemos.  ¿O tal vez la revisión más reciente incluía cosas que descartamos en la versión final del libro? es una posibilidad. ¿No sería bueno que tuviéramos un sistema de control de cambios externo, que no dependiera del software o de la versión del software que estamos utilizando? ¿Y no sería todavía mejor que este sistema de control de cambios pudiera recordar todo lo que ha ocurrido en el proyecto y además almacenarlo en un repositorio remoto dónde pudieran trabajar otros colaboradores sin estorbarse, sencillamente creando versiones alternativas del proyecto que cuando estuviesen listas, se integraran en el proyecto principal? Esto en efecto existe, se llama GitHub y es lo que utilizaremos para almacenar nuestro proyecto. Pero ya hablaremos de ello. Antes, necesitamos resolver qué hacemos con el manuscrito.

### Markdown

MS Word es un software estupendo para escribir cartas, pero es alarmantemente inadecuado para la producción editorial. Discutiré los problemas en otro sitio, pero de momento baste decir que como muchos softwares propietarios tiene una tendencia acusada a producir problemas de compatibilidad con sus versiones anteriores, un sistema de control de cambios cuyo usuario ideal padece de un insomnio ideal. Dicho esto, es curioso que esté tan extendido. gg
