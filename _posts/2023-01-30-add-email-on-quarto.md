---
title: How to add an email address on a pdf file rendered with Quarto
subtitle: customizing quarto document with a title.tex file
layout: default
date: 2023-01-30
keywords: quarto
summary: customizing quarto document with a title.tex file
published: true
---
#### tags: `miscellaneous`

By default, Quarto ignores a newline operator for an author name. So
instead of adding an email address in the author variable, you need to customize
the title part of the document as follows.

Configure the required information at the top of the jupyter notebook in a markdown format. The `title.tex` under the `template-partials` is the tex file that we'll use for the title box of our document. The `title.tex` can be replaced with the path of the tex file, for instance `../path_to_title/title.tex`.

```
---
title: "Title of the Document"
subtitle: "Subtitle of the Document"
author: "Your Name"
email: "yourid@email.com"
date: today
date-format: long
output: pdf_document
format:
  pdf:
    template-partials:
      - title.tex
---
```

Create a `title.tex` file as follows,

```tex
$if(title)$
\title{$title$$if(thanks)$\thanks{$thanks$}$endif$}
$endif$
$if(subtitle)$
$if(beamer)$
$else$
\usepackage{etoolbox}
\makeatletter
\providecommand{\subtitle}[1]{ % add subtitle to \maketitle
\apptocmd{\@title}{\par {\large #1 \par}}{}{}
}
\makeatother
$endif$
\subtitle{$subtitle$}
$endif$
\author{$author$ \\ \small{$email$}}
\date{$date$}
```

You can further customize the `title.tex` for any other information you want to include. After the rendering to pdf, the result should look like this.

<img width="735" alt="Pasted image 20230130183748" src="https://user-images.githubusercontent.com/48481523/215650669-aee1d71e-b00e-492f-98cc-4c155397edd4.png">

# References
[https://quarto.org/docs/authoring/title-blocks.html](https://quarto.org/docs/authoring/title-blocks.html)
[https://quarto.org/docs/journals/templates.html#template-partials](https://quarto.org/docs/journals/templates.html#template-partials)

