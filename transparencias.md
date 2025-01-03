---
marp: true
title: Memorias de TFG en LaTeX
theme: default
paginate: true
size: 4:3
math: mathjax
style: |
   img[alt~="center"] {
      display: block;
      margin: 0 auto;
   }
   .columns {
      display: grid;
      grid-template-columns: repeat(2, minmax(0, 1fr));
      gap: 1rem;
   }
---


<!-- _paginate: skip -->
![bg contain opacity:.15](img/gul_logo.svg)
# Memorias de TFG en $\LaTeX$
Por Luis Daniel Casais Mezquida


<br>

_Grupo de Usuarios de Linux_
[@guluc3m](https://twitter.com/guluc3m) | [gul.uc3m.es](https://gul.uc3m.es)

---

## Transparencias
![w:400 center](img/qrcode.svg)
<center>
<a href="https://github.com/rajayonin/latex-thesis">github.com/rajayonin/latex-thesis</a>
</center>



---
## $\LaTeX$
<!-- header: '' -->
Herramienta y lenguaje de programación ($\TeX$) para la creación de documentos de alta calidad.
- Uso de archivos de texto plano.
- Permite el uso de **plantillas** y _macros_ para simplificar y estandarizar el proceso.
- Extremadamente útil para $e - c \cdot u^a = c_i \sqrt{o} + \frac{n}{e^s}$ y bibliografía.
- Numeración automática de capítulos, figuras, tablas, referencias bibliográficas... 
- Generación automática de índices y glosarios


---
<!-- header: '$\LaTeX$' -->
### Cómo usar $\LaTeX$
- Online: [Overleaf](https://overleaf.com/)
- Linux: Instala `texlive-full` (para Arch, todos los paquetes `texlive-*`)
- Windows: Instala [MiKTeX](https://miktex.org/download#win) y [Strawberry Perl](https://strawberryperl.com/)
   ```powershell
   winget install MiKTeX.MiKTeX StrawberryPerl.StrawberryPerl
   ```
- MacOS: Instala [MacTeX](https://www.tug.org/mactex/mactex-download.html)
  ```zsh
  brew install --cask mactex
  sudo tlmgr install latexmk
  ```

Para usar SVGs en local es necesario instalar [Inkscape](https://inkscape.org/) y añadirlo al PATH.

---

#### Extensiones VS Code
- [LaTeX Workshop](https://marketplace.visualstudio.com/items?itemName=James-Yu.latex-workshop)
   - Recuerda añadir el parámetro `-shell-escape` (ver [LaTeX Workshop FAQ](https://github.com/James-Yu/LaTeX-Workshop/wiki/FAQ#how-to-pass--shell-escape-to-latexmk))
   -  Puedes habilitar el conteo de palabras estableciendo `latex-workshop.wordcount` a `onSave` en los ajustes.  
   Más información [en la Wiki](https://github.com/James-Yu/LaTeX-Workshop/wiki/ExtraFeatures#counting-words)

- [LTeX+](https://marketplace.visualstudio.com/items?itemName=ltex-plus.vscode-ltex-plus): Corrector ortográfico.
   - Puedes cambiar el idioma a través de la configuración parámetro `ltex.language`

---
## Plantilla tesis UC3M
<!-- header: '' -->
[github.com/ldcas-uc3m/thesis-template](https://github.com/ldcas-uc3m/thesis-template)
- Hecha por mí, para vosotros ~~jugadores~~
- Basada en la [guía de la biblioteca de la UC3M](https://uc3m.libguides.com/en/thesis/writing) para las tesis, y en [su propia plantilla](https://www.overleaf.com/latex/templates/bachelor-thesis-template-uc3m-ieee-style/rtmtnzvxjnwt)
- Bonita y fácil de usar


---
<!-- header: '**Plantilla tesis UC3M**' -->

![center](img/overview.svg)


---
### Uso
Comenzamos el archivo principal (`report.tex`) de la siguiente forma:
```tex
% plantilla
\documentclass[es]{uc3mthesisIEEE}  % [en] para inglés
```
```tex
% Es recomendable importar los paquetes utilizados
% en este punto
\usepackage{import}
```


```tex
\addbibresource{references.bib}  % bibliografía
\import{glossary.tex}  % glosario
```


---
Especificamos la carpeta de imágenes:
```tex
\graphicspath{{img/}}
```


Ahora configuramos las propiedades para la portada:
```tex
\degree{Grado en Ingeniería de Caminos}
\title{Análisis, diseño, e implementación de un camino}
\shorttitle{A.D.I de un camino}
\author{Perico de los Palotes}
\advisors{
   Segismundo de la Fuente
   % \\ Eugenio García
}
\place{Leganés, Madrid, Spain}
\date{Junio 2024}
```


---

Y empezamos el documento:

```tex
\begin{document}

  % [...]

\end{document}
```

<br>

Dentro de este _entorno_ `document` es donde se escribirá el documento en sí.

---

La plantilla viene con varios _comandos_ y _entornos_ para simplificar el proceso:

```tex
\makecover         % portada
```
```tex
% epígrafe
\makeepigraph
  {                % cita
    La vida es una aplastante derrota tras otra
    hasta que acabas deseando que se muera Flanders.
  }
  {Homer Simpson}  % autor
  {La Biblia}      % fuente (opcional)
```

---

```tex
% agradecimientos
\begin{acknowledgements}
  Quiero dar las gracias a mi papá, a mi mamá,
  a mi perro Pepe...
\end{acknowledgements}
```
```tex
% abstracto
\begin{abstract}
  En éste trabajo se desarrolla cómo hacer un camino,
  teniendo en cuenta las últimas tejnologías y...

  \keywords{Camino \sep piedra \sep cambio climático}
\end{abstract}
```


```tex
% índices
\tableofcontents  % contenidos
\listoffigures    % figuras
\listoftables     % tablas
```


---
También cuenta con un entorno `thesis`, en el cual es donde se debe escribir la tesis en sí.

Es recomendable separar los capítulos en archivos, e importarlos aquí.

```tex
\begin{thesis}

  \includefrom{parts/}{introduction.tex}
  \includefrom{parts/}{state_of_the_art.tex}
  % [...]
  \includefrom{parts/}{conclusions.tex}

\end{thesis}
```


---
Por último añadimos las partes finales:
```tex
% bibliografía
\cleardoublepage
\label{bibliography}
\printbibliography[heading=bibintoc]
```
```tex
% glosario
\cleardoublepage
\label{glossary}
\printglossaries
```
```tex
% apéndices
\begin{appendices}
  
  % [...]

\end{appendices}
```


---
### Compilación (local, en terminal)
Para compilar la memoria, usa:
```
latexmk -cd -shell-escape -pdf report.tex
```

Para compilar el glosario es necesario (después de compilar la primera vez), usar el comando:
```
makeglossaries report
```

Y luego volver a compilar.


---
<!-- header: '' -->
## How to $\LaTeX$
Nociones generales:
- Comentarios con `%`
- Los caracteres especiales deben ser escapados:
   - `#`, `$`, `%`, `&`, `_`, `{`, `}` se escapan con `\`, e.g. `\_`
   - `\`, `^`, `~` requieren un comando específico: `\textbackslash`, `\textasciicircum`, `\textasciitilde`

---
<!-- header: '**How to $\LaTeX$**' -->
### Formato de texto
- **Negrita**: `\textbf{...}`
- *Cursiva*: `\textit{...}`
- <ins>Subrayado</ins>: `\underline{...}`
- `Verbatim`: `\texttt{...}`
- [URLs](https://noot.space/):
   - `\href{https://test.com}{...}`
   - `\url{https://test.com}`
- Notas a pie de página: `\footnote{...}`

---
### Saltos de línea y párrafos
Los saltos de línea son automáticos.
- Un salto de línea en el archivo fuente no rompe una línea
- Para saltar de línea, se usa `\\`

<div class="columns">
<div>

```tex
Esta línea
no se rompe
```

</div>
<div>

```tex
Esta\\
sí
```

</div>
</div>

---

Para saltar de párrafo, se deja una, o más, líneas en blanco
- Para evitar la sangría (indentación) de la primera línea de un párrafo, se usa `\noindent`

<div class="columns">
<div>

```tex
y este es el final
de mi párrafo.

Hola, párrafo nuevo.
```

</div>
<div>

```tex
y este es el final
de mi párrafo.

\noindent
Hola, párrafo nuevo sin
sangría.
```

</div>
</div>



---
### Listas

Pueden ser enumeradas o no enumeradas

<div class="columns">
<div>

```latex
\begin{enumerate}
  \item Primero
  \item Segundo
\end{enumerate}
```

</div>
<div>

1. Primero
2. Segundo

</div>
</div>

<div class="columns">
<div>

```latex
\begin{itemize}
  \item Uno
  \item Otro
\end{itemize}
```

</div>
<div>

- Uno
- Otro

</div>
</div>


---
También puedes anidar las listas.

<div class="columns">
<div>

```latex
\begin{enumerate}
  \item Primero
  \begin{itemize}
    \item Primero A
    \item Primero B
  \end{itemize}
  \item Segundo
\end{enumerate}
```

</div>
<div>

1. Primero
   - Primero A
   - Primero B
2. Segundo

</div>
</div>



---
### Estructura del documento
- `\chapter{...}`: Capítulo; e.g. `1.`
- `\section{...}`: Sección; e.g. `1.1`
- `\subsection{...}`: Subsección, o apartado; e.g. `1.1.1`
- `\subsubsection{...}`: Subapartado; e.g. `1.1.1.1`

Usa `*` para que no quede enumerado, e.g. `\subsubsection*{...}`.

En esta plantilla, los capítulos empiezan en una página impar nueva.


---
### Referencias
Crea una marca con `\label{<id>}`, y la puedes referenciar con:
- `\ref{<id>}`: Pone el número de la sección/figura/etc. a la que se refiere.
- `\nameref{<id>}`: Pone el nombre de la sección/figura/etc. a la que se refiere.
- `\pageref{<id>}`: Pone el número de página de la sección/figura/etc. a la que se refiere.


---
### Figuras
Es necesario incrustarlas de la siguiente forma:
```tex
\begin{figure}[htb]
  \ffigbox[\FBwidth]
  {%
    \caption{...}
    \label{fig:<id>}
  }
  {
    % imagen
  }
\end{figure}
```

Puedes cambiar `htb` por `H` para obligar a que la figura quede en este punto exacto del texto.

---

#### Imágenes
La imagen será incrustada de distintas formas, dependiendo de su formato:
- Si es _raster_ (e.g. PNG):
  ```tex
  \includegraphics[width=.X\textwidth]{<imagen>}
  ```
- Si es vectorial (e.g. SVG):
  ```tex
  \includesvg
    [inkscapelatex=false,width=.X\textwidth]
    {<imagen>}
  ```

Donde `.X` es el porcentaje del ancho de la imagen con respecto al ancho de la página, e.g. `.7` (70%).




---
### Tablas

Similar a las figuras, es necesario incrustarlas de la siguiente forma:
```tex
\begin{table}[htb]
  \ttabbox[\FBwidth]
    {\caption{...}}
    {%
      \begin{tabular}{...}
        % [...]
      \end{tabular}
    }
\end{table}
```

También puedes usar `H`.

Para generar las tablas (entorno `tabular`), recomiendo usar un [generador de tablas](https://www.tablesgenerator.com/latex_tables).



---
### Comandos
Pequeñas macros con argumentos que permiten automatizar y simplificar el trabajo.
```latex
\newcommand{\helloworld}{Hello, world!}
\helloworld  % Hello, world!
```
```latex
\newcommand{\hello}[2]{Hello, #1 and #2!}
\hello{Jose}{Pepe}  % Hello, Jose and Pepe!
```
```latex
\newcommand{\hello}[3][Hello]{#1, #2 and #3!}
\hello{Jose}{Pepe}  % Hello, Jose and Pepe!
\hello[Hola]{Jose}{Pepe}  % Hola, Jose and Pepe!
```

---

Extremadamente útil meterlas en un archivo `mymacros.sty`:
```tex
\ProvidesPackage{mymacros}[Auxiliary helper macros]
% [...]
```
e importarlo en `report.tex` con:
```tex
\usepackage{mymacros}
```

<br>

Os dejo para que investiguéis:
- [Commands - Overleaf](https://www.overleaf.com/learn/latex/Commands)
- [Mis macros del TFG](https://github.com/ldcas-uc3m/TFG/blob/main/report/mymacros.sty)

---

```tex
% \graphicfigure[width]{filename}{caption}
\newcommand{\graphicfigure}[3][.7] {
  \begin{figure}[htb]
    \ffigbox[\FBwidth]
      {%
        \caption{#3}
        \label{fig:#2}
      }%
      {\includegraphics[width=#1\textwidth]{#2}}
  \end{figure}
}
```
```tex
Observamos un perrito en la Figura \ref{fig:perro}.
\graphicfigure[.5]{perro}{Un perrito}
```

---

```tex
% \svgfigure[width]{filename}{caption}
\newcommand{\svgfigure}[3][.7] {
  \begin{figure}[htb]
    \ffigbox[\FBwidth]
      {%
        \caption{#3}
        \label{fig:#2}
      }%
      {
        \includesvg
          [inkscapelatex=false,width=#1\textwidth]
          {#2.svg}
      }
  \end{figure}
}
```
```tex
La arquitectura del sistema queda reflejada
en la Figura \ref{fig:arquitectura}.
\svgfigure[.7]{arquitectura}{Arquitectura del sistema}
```


---
### Ecuaciones
$\LaTeX$ contiene el lenguaje más usado para definir expresiones matemáticas en texto plano.

Puedes incrustar expresiones _inline_ con `$`:

<div class="columns">
<div>

```latex
$e^{i\pi} + 1 = 0$
```

</div>
<div>

$e^{i\pi} + 1 = 0$

</div>
</div>

Y crear ecuaciones (numeradas) con el entorno `equation`:
```tex
\begin{equation}
  e^{i\pi} + 1 = 0
\end{equation}
```

---
La mayoría de símbolos usados se escriben con un comando:
- `+`, `=`, `<`, `>` o `-` se usan tal cual
- `·` es `\cdot`
- `≠` es `\ne`, `≤` es `\le`, `≥` es `\ge`
- `α` es `\alpha`, `β` es `\beta`, `γ` es `\gamma`...
- `Γ` es `\Gamma`, `Δ` es `\Delta`, `Θ` es `\Theta`...

[Detexify](https://detexify.kirelabs.org/classify.html) es una herramienta online que te permite dibujar el símbolo y te dice el comando.

También hay herramientas para facilitar la creación de fórmulas, como [CodeCogs](https://editor.codecogs.com).




---
### Bibliografía
Las bibliografías se gestionan con [BibteX](https://www.bibtex.org/).

- Todas las referencias van guardadas en `references.bib`, con un ID asociado.
- También puedes usar un gestor de referencias como [Zotero](https://www.zotero.org/)
- Para hacer que se respeten las mayúsculas, rodéalas de `{}`, e.g. `{Mi {C}arro}`
- Es recomendable añadir el [DOI](https://www.doi.org/the-identifier/what-is-a-doi/) siempre que se pueda

En el texto, se cita con `\cite{<id>}`. Si quieres incluír el texto en tu cita, usa `\textcquote{<id>}{...}`

---
#### Tipos de bibliografía
Hay diferentes tipos de bibliografía, dependiendo del recurso al que hagas referencia. Aquí dejo algunos ejemplos:

```bibtex
@book{lamport1986latex,
  title     = {{LATEX}: A Document Preparation System},
  author    = {Lamport, Leslie},
  year      = {1986},
  publisher = {Addison-Wesley}
  edition   = {},
  series    = {},
  url       = {},
}

```
---
```bibtex
@article{Gardner1970fantastic,
  title   = {{The fantastic combinations of John
             Conway's new solitaire game ``life''}},
  author  = {Gardner, Martin},
  journal = {Scientific American},
  volume  = {223},
  pages   = {120--123},
  year    = {1970},
  number  = {},
  doi     = {10.1038/scientificamerican1070-120},
}
```

```bibtex
@online{mal,
  title   = {{Make-A-Lisp}},
  author  = {Martin, Joel},
  year    = {2015},
  url     = {https://github.com/kanaka/mal},
  urldate = {2023-10-05}
}
```

---

```tex
@techreport{ISOcpp23,
  title       = {{Programming Languages -- C++}},
  number      = {ISO/IEC PRF 14882},
  type        = {International Standard Draft},
  year        = {2023},
  institution = {International Organization for Standardization}
}
```
```tex
@techreport{IEEE830-1984,
  title       = {{IEEE Guide for Software
                 Requirements Specifications}},
  type        = {IEEE Std.},
  number      = {830-1984},
  year        = {1984},
  institution = {Institute of Electrical and
                 Electronics Engineers},
  doi         = {10.1109/IEEESTD.1984.119205}
}
```

---
```tex
@conference{creatorZenodo,
  title        = {{CREATOR: Simulador didáctico y genérico para
                  la programación en ensamblador}},
  author       = {Camarmas Alonso, Diego and García Carballeira,
                  Felix and Del Pozo Puñal, Elías and Calderón
                  Mateos, Alejandro},
  year         = 2021,
  publisher    = {Zenodo},
  booktitle    = {XXXI Jornadas de Paralelismo},
  organization = {Sociedad de Arquitectura y Tecnología
                  de Computadores},
  address      = {Málaga, Spain},
  month        = jul,
  doi          = {10.5281/zenodo.5130302}
}
```


---
### Glosario

Las definiciones se guardan en `glossary.tex`:
```tex
% definición
\newglossaryentry{<id>} {
  name        = {...},
  description = {...}
}
```

```tex
% acrónimo
\newacronym{mcd}{MCD}{Máximo Común Divisor}
```

```tex
% definición con acrónimo
\newglossaryentrywithacronym{MCD}
  {Máximo común divisor}
  {El mayor número entero que divide a otros dos}
```

---

Para anotarlo en el texto:
- `\gls{<id>}`: referencia al término
- `\Gls{<id>}`: término con la primera letra en mayúscula
- `\glspl{<id>}`: término en plural
- `\Glspl{<id>}`: término en plural y la primera mayúscula
- `\glsdisp{<id>}{...}`: referencia con texto personalizado


---
### Paquetes útiles
- [`pdflscape`](https://ctan.org/pkg/pdflscape): Páginas horizontales. [_Ejemplo_](https://github.com/ldcas-uc3m/TFG/blob/main/report/parts/plan.tex#L36).
- [`pgfgantt`](https://ctan.org/pkg/pgfgantt): Diagramas de Gantt. [_Ejemplo_](https://github.com/ldcas-uc3m/TFG/blob/main/report/parts/plan.tex#L44-L99).
- [`dirtree`](https://ctan.org/pkg/dirtree): Árboles de directorios. [_Ejemplo_](https://github.com/ldcas-uc3m/TFG/blob/main/report/parts/implementation.tex#L22-L47).
- [`syntax`](https://ctan.org/pkg/syntax): Definición de lenguajes en _Backus-Naur Form_. [_Ejemplo_](https://github.com/ldcas-uc3m/TFG/blob/main/report/parts/design.tex#L211-L282).
- [`rajayonin/srs-latex`](https://github.com/rajayonin/srs-latex): Requisitos de software. [_Ejemplo_](https://github.com/ldcas-uc3m/TFG/blob/main/report/parts/analysis.tex#L36-L416).
- [`algpseudocode`](https://ctan.org/pkg/algpseudocode): Definición de algoritmos. [_Guía_](https://es.overleaf.com/learn/latex/Algorithms#The_algpseudocode_and_algorithm_packages).





---
<!-- header: '' -->
## Más información
- [guluc3m/report-template](https://github.com/guluc3m/report-template)
- [Overleaf knowledge base](https://www.overleaf.com/learn)
- [LaTeX - Wikibooks](https://en.wikibooks.org/wiki/LaTeX)
- [LaTeX Stack Exchange](https://tex.stackexchange.com/)
- [CTAN (Comprehensive TeX Archive Network)](https://ctan.org/)
- [ldcas-uc3m/TFG](https://github.com/ldcas-uc3m/TFG)
- [L. Prieto - Generación de documentos en LaTeX](https://youtu.be/cFieGJljKog) (2021)


---

<!-- _paginate: skip -->
![bg contain opacity:.15](img/gul_logo.svg)
# ¡Ánimo!


<br>
<br>

_Grupo de Usuarios de Linux_
[@guluc3m](https://twitter.com/guluc3m) | [gul.uc3m.es](https://gul.uc3m.es)