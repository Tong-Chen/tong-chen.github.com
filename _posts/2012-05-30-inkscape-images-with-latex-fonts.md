---
title: Inkscape images with LaTeX fonts
author: 悟道
layout: post
permalink: /?p=2126
categories:
  - tex
---
<table>
  <tr cellpadding=0><td>
    热度:
  </td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td></tr>
</table>

With the release of <a href="http://inkscape.org/" target="_blank">Inkscape 0.48</a>, it is now possible to match the font of the text in your images with the font used in your LaTeX document. This includes math environments and references. Hence that this is a very powerful tool that will make your LaTeX documents even prettier! Previously, this integration was also possible, but it was a bit of a pain. In this post I’ll show you how to get LaTeX typesetting in your Inkscape pictures.

## Creating the image

For this example, I’m going to create a double pendulum. I’m not going to show you how to draw this, because it isn’t that hard and not in the scope of this blog. The result can be viewed <a href="http://www.howtotex.com/images/inkscape-dpen-screen-1.png" target="_blank">here</a> (Note: the .pdf image can be downloaded below).

## Inserting text

This is the easy part, where it was before rather difficult. To insert text you don’t have to bother about the fonts you’re using. In my pendulum example, I want text next to the rods and the masses. I also want to indicate two angles. What I do is just pick the text tool in Inkscape and insert `$m_1$` next to the first mass. The same is done for the second mass and in Inkscape it looks like <a href="http://www.howtotex.com/images/inkscape-dpen-screen-2.png" target="_blank">this</a>. This doesn’t look okay at all! But remember what I said before, don’t worry about the font.

After I put the rest of the text in my image, I’d like to export it as a .pdf file. To do so, go to File > Save As… > Choose Portable Document Format (*.pdf). Now, a small window pops up. Choose the settings as shown <a href="http://www.howtotex.com/images/inkscape-dpen-screen-3.png" target="_blank">here</a>. After you save, Inkscape had created to files: the .pdf image and an .pdf_tex file. The last one contains the text information.

## Setting up your document

Open your LaTeX editor and create a document as. I used:

<div>
  <div>
    <pre>\documentclass[]{article}
\usepackage{graphicx}
\usepackage{color}
\usepackage{transparent}
\begin{document}
\begin{figure}[htb]
  \centering
  \def\svgwidth{200pt}
  \input{drawing.pdf_tex}
  \caption{Double pendulum}
\end{figure}
\end{document}</pre>
  </div>
</div>

Let’s explain this a bit. The `graphicx` package is needed because we’re inserting an image. The `<a href="http://www.ctan.org/tex-archive/macros/latex/contrib/xcolor/" target="_blank">color</a>` package and `<a href="ftp://ftp.tex.ac.uk/tex-archive/macros/latex/contrib/oberdiek/transparent.pdf" target="_blank">transparant</a>` package are needed if you use colors and/or transparency in you image. I’ve used grey once, which is treated as a color.  
Inside the `figure` environment you see the `svgwidth` line. This line defines the width of your image, since this is not yet done in the .pdf_tex file created by Inkscape. The next line inputs the image with the text.

Done! Render your document and you’ll see that the text in your images perfectly fits the font you use in your document.

## Making adjustments to the picture

In my example, I used a rather large font in Inkscape. This way, it’s pretty hard to place the text on the exact right spot (as can be seen in the compiled PDF, downloadable below). It’s wise to use a small font, for instance Arial size 6. Using a smaller font will make it a lot easier to place the text in the right place, especially if you have a lot of text to insert.

If you find the result compiled by LaTeX not satisfying and you want to adjust the position of some text elements, there are a few ways to do this. The first, of course, would be to adjust the whole image in Inkscape. But another way is to open the .pdf_tex file in your LaTeX editor. Scroll down to see the `picture` environment and notice the `\put` commands. These can be interpreted as follows:

<div>
  <div>
    <pre>\put(x,y)</pre>
  </div>
</div>

There is more code following this command, but by changing the x and/or y components of the command you can shift the picture horizontally and/or vertically. This is a nice solutions to make small adjustments.

## Download

You can download the content of this post in a [zip file][1]. In here, the image files are included. Also I used the `<a href="http://www.ctan.org/tex-archive/macros/latex/contrib/blindtext/" target="_blank">blindtext</a>` package to create dummy text. In the .tex file, the used commands are commented.

&nbsp;

<http://www.howtotex.com/tips-tricks/inkscape-images-with-latex-fonts/>

 [1]: http://www.howtotex.com/download/inkscape-howtotex.zip