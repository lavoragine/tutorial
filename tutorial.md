## 1. El problema

Supongamos que hará unos diez años editamos y publicamos un libro, que ahora necesitamos reeditar. Los archivos siguen almacenados en un disco duro, de modo que todo estaría en recuperarlos, abrirlos en InDesign, hacer las correcciones y ajustes que hagan falta, y volver a imprimir.

En el disco duro encontramos la carpeta con el proyecto y dentro de esta carpeta, una subcarpeta llamada "tripa" donde efectivamente hay un archivo InDesign. Perfecto. El problema es que mi versión de InDesign decide que no es un archivo con quién quiera tener algún tipo de trato.

![InDesign no puede abrir el archivo](imgs/noSePuedeAbrirElArchivoInDesign.png)

El mensaje no solo es desalentador, también es totalmente opaco. ¿Por qué no se puede abrir? ¿El archivo está corrupto? ¿Tiene que ver con la versión de InDesign que estoy usando? Ninguna pista. Podría probar utilizando la versión de InDesign con la que cree el archivo, pero, demonios, hace diez años de eso, ¿cuál podría haber sido? Sin contar con que tendría que descargarla e instalarla y sin ninguna garantía de que el asunto funcionase.

Vamos, pues, al plan B. Que no es otro que localizar la última versión del manuscrito en MS en Word y rehacer la maqueta.

El manuscrito en cuestión se produjo después de un laborioso escaneo: nada extraño considerando que la última edición del libro en cuestión era de hace unos treinta o cuarenta años atrás. Cualquiera que halla escaneado un libro sabe que los resultados distan mucho de definir la palabra prolijidad. El resultado: la corrección tomó un buen tiempo, primero utilizando herramientas automatizadas (grep, fundamentalmente, pero ya hablaremos de eso), y un trabajo denodado de nuestro corrector. Por tanto, el ir y venir de borradores por correo electrónico fue profuso.

Considerando lo anterior, resulta natural (preocupante, pero natural) que cuando miramos en la carpeta que contiene los borradores, encontremos no uno sino una serie de archivos (versión2, versiónfinal, versión definitiva... espera, ¿"versiondefinitiva" es más final que "final" ¿o es al revés?). Siempre podemos buscar sencillamente la última versión del documento en MS Word y trabajar con esa. Pero, ¿es realmente la última o la corrección final fue hecha en InDesign? De ser así, posiblemente podríamos recuperar el log del control de cambios en InDesign... solo que no podemos. ¿O tal vez la revisión más reciente incluía cosas que descartamos en la versión final del libro? Es una posibilidad. De paso y ya que estamos, convendría también revisar los correos electrónicos con el corrector.

Al final escogemos un archivo, y lo abrimos. Naturalmente, los encabezaos brillan por su ausencia y después de echar un vistazo en el panel de estilos, sabemos que mapear esto e importarlo de alguna manera indolora en InDesign va a ser la más utópica de las proezas.

Llegado a este punto, habrán pasado un par de horas y estaremos sentados frente al ordenador con deseos de tirarlo por la ventana y correr a ahogarnos de chupitos en algún antro infame.


### 2.1

Cosas como estas pasan todo el tiempo. Sean estos los problemas, u otros distintos, o una combinación variable de problemas conocidos y otros totalmente novedosos, la combinación MS Word + InDesign rara vez es indolora, sobre todo si consideramos documentos enviados por correctores o traductores o escritores: pueden lucir muy bien, pero rara vez están bien estructurados. Y la tentación del diseño (que es una especie de enfermedad que se apodera tarde o temprano de los usuarios de Word) termina por crear monstruos, para mayor horror de diseñadores y editores. Discutiremos esto en otro lugar, pero sí podemos mencionar rápidamente los problemas de word:
- es poco sostenible
- nada transparente (messy)
-

Y sin embargo, word es el estándar, lo cual no deja de resultar misterioso. ¿No hay otra manera de hacer las cosas? En efecto la hay. Pero aunque es más eficiente, indolora, fluida y también nos abre numerosas posibilidades, por alguna razón nadie o casi nadie la utiliza.















### 1.1 Fundamentos

la idea es trabajar pensando en digital y asumiendo los principios del *Single Source Publishing* (un único documento para múltiples formatos de salida)

### 1.2 Requisitos

Para seguir este tutorial, es aconsejable:

- Alguna familiaridad con la línea de comandos.
- Tener conocimientos básicos de HTML y CSS.
- Un conocimientos de InDesign a nivel de diseño editorial.
- Una mente abierta (todo lo anterior se puede reemplazar con una aplicada búsqueda en Google, esto último no).

### 1.3 Herramientas & software

Para los efectos de este tutorial necesitaremos tener instalado en nuestro sistema:

- Un editor de texto plano (no procesador de texto): yo utilizaré Atom, pero hay una serie de editores de texto igualmente útiles y libres (Visual Studio Code, Sublime Text, Vim, etc...)
- Línea de comandos (en Windows, el PowerShell, en Linux el terminal o uno cualquiera de sus emuladores; en Mac, la terminal).
- Pandoc
- InDesign
- Git y el cliente de escritorio de GitHub
- MS Word
- Jeckyll




### Primer paso: formatear

Dado que de lo que se trata es de probar algo distinto (no se puede esperar un resultado diferente si hacemos lo mismo), vamos a cambiar totalmente nuestro flujo de trabajo. Y lo primero que haremos será convertir nuestro archivo (el que hemos decidido utilizar como archivo base) a Markdown

Lo que hace pandoc es mantener local formatting (italic y bold) y suprimir toda la información extra (que de hecho no necesitamos)

### Markdown



eso dice Alber Grenning, justificando un error en su paper sobremmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmm
