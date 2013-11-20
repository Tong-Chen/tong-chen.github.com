---
title: WordPress Blog to Print Book – A Case Study
author: 悟道
layout: post
permalink: /?p=2923
categories:
  - tool
---
<table>
  <tr cellpadding=0><td>
    热度:
  </td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td></tr>
</table>

# [A Sourceful of Secrets][1]

<div id="bubble">
  <p>
    Andrew E. Bruno
  </p>
</div>

<div id="content">
  <div>
    <h2 id="post-257">
      WordPress Blog to Print Book – A Case Study
    </h2>
    
    <p>
      <a href="http://left.subtree.org/2011/04/09/wordpress-blog-to-print-book-a-case-study/#comments">with 4 comments</a>
    </p>
    
    <div>
      <p>
        In this post I discuss my experience converting a WordPress blog into a print book. This is by no means a generic how-to guide but more along the lines of a case study. There’s a number of ways one could tackle this problem however I wasn’t able to find any existing methods that fit my needs. Specifically, I wanted to convert the content of a WordPress blog into a high quality print ready PDF book (complete with chapters, sections, table of contents, images, figures, page numbering, index, etc.) which could then be sent to various <a href="http://en.wikipedia.org/wiki/Print_on_demand">POD</a> publishers such as <a href="http://www.lulu.com/">Lulu</a> for printing. I wanted to streamline as much of the process as possible to allow for regenerating the PDF book as new posts are made. Ideally there would be a WordPress plugin for this but to make such a plugin generic enough would be tricky and require many assumptions to be made regarding the structure of your blog (i.e. what constitutes a chapter or a section?, etc.). In this post I describe how I ended up creating a PDF book from WordPress and discuss a few challenges I encountered along the way. A brief disclaimer: this post is intended for folks who are familiar with *nix command line and enjoy mucking around in code (and don’t mind slinging around some XML here and there). It’s not for the faint of heart but hopefully it will be useful to others interested in a similar outcome.
      </p>
      
      <p>
        If you’d rather skip this epic post and dive right into the code you can browse it all over on <a href="https://github.com/aebruno/wp2print">github</a>. There’s a <a href="https://github.com/aebruno/wp2print/blob/master/README">README</a> file and a <a href="https://github.com/aebruno/wp2print/blob/master/Makefile">Makefile</a> which details how to run wp2print and includes a simple example.
      </p>
      
      <p>
        <strong>Background and Assumptions</strong>
      </p>
      
      <p>
        The idea for this project came about as my family has been writing a private blog that I want to be able to share with my children some day. I’ve often thought about giving them a copy of the blog when their much older and wondered what would be the best way to preserve the content ensuring it’s viewable years down the road. I thought by creating a physical copy of the blog I could have something tangible to pass down through the generations. Using the services provided by companies like Lulu and Blurb printing a book is as simple as uploading a PDF and designing a cover. Having <a href="http://oreilly.com/">worked</a> in the publishing industry in a former life I had some experience generating PDF books so I looked forward to the challenge.
      </p>
      
      <p>
        As my goal was to create a book I needed to convert the content of the blog into an intermediate format which represented the book and could then be used to generate a PDF file. As I had a good amount of experience slinging around <a href="http://www.docbook.org/">DocBook</a>, my general idea was to export the content from WordPress and convert it into DocBook. Then converting DocBook into a PDF is fairly straightforward using the wonderful <a href="http://docbook.sourceforge.net/">DocBook stylesheets</a> and <a href="http://xmlgraphics.apache.org/fop/">Apache FOP</a>.
      </p>
      
      <p>
        The first obvious challenge when converting a blog into a book is deciding how to go about organizing the blog posts into chapters and sections. Our family blog was authored in such a way that each post had only one tag (category) and most importantly all posts were tagged chronologically. Meaning that all posts in a given category were sequential. For example, posts 0-5 are all tagged with “tag1″, posts 6-10 are all tagged with “tag2″, and so on. You can probably see where this is going. Having authored the blog in this format allowed me to easily use each tag as a Chapter and each post appeared as a section within that chapter. If your unable to make these assumptions about your blog (and most likely you won’t be able to) just keep this in mind as we delve into the code later on. You would need to modify the script I wrote and add in the appropriate logic to slice your blog posts up into chapters/sections or however you’d like to structure your DocBook file. I experimented with just making each post a chapter (and even a series of DocBook <a href="http://www.docbook.org/tdg5/en/html/article.html">articles</a>) which isn’t a bad option however depending on the number of posts you may want to consider omitting the table of contents.
      </p>
      
      <p>
        A few other assumptions I made:
      </p>
      
      <ul>
        <li>
          All posts were written by the same author so I omitted displaying any author information. Easy enough to add in if needed
        </li>
        <li>
          All comments were excluded from the book. Comments are an important part of any blog but in this case my blog didn’t have very many comments. I was most interested in the content of the post only and decided to omit any and all comments. These could certainly be added in but some thought would be needed on which DocBook element to use for structuring them within the book.
        </li>
        <li>
          There was one page (not a post) with the title “About” that I used as the preface for the book. This can be any post/page or omitted completely if desired.
        </li>
        <li>
          Access to the WordPress code that runs the blog. This won’t work if your blog is hosted for example at WordPress.com. You’ll need to export your blog and run it on your own server.
        </li>
      </ul>
      
      <p>
        Here’s a brief outline of the entire process. I’ll go over each step in detail in the next section.
      </p>
      
      <ol>
        <li>
          Convert WordPress content to DocBook – using PHP and some XSLT
        </li>
        <li>
          Convert DocBook to <a href="https://secure.wikimedia.org/wikipedia/en/wiki/XSL_Formatting_Objects">XSL-FO</a> – using DocBook stylesheets
        </li>
        <li>
          Convert XSL-FO to PDF – using Apache FOP
        </li>
        <li>
          Upload PDF file to Lulu and order print book
        </li>
      </ol>
      
      <p>
        <strong>Convert WordPress content to DocBook</strong>
      </p>
      
      <p>
        First step was to convert the blog into DocBook. This was by far the most challenging step. My first attempt was to use the <a href="https://en.support.wordpress.com/export/">Export</a> feature in WordPress which dumps the entire contents of your blog in XML format (WordPress eXtended RSS) and write an XSLT to convert into DocBook. This turned out to be slightly harder than I anticipated because of how the content of each post was formatted in the WordPress XML dump. It appeared to be in the native format WordPress uses to store the post in the database and I didn’t want to have to write a custom WordPress post renderer for DocBook. I decided to instead write a fairly simple PHP script which used the WordPress API to render each post in HTML just like it normally would if someone visited the site, then convert the HTML to DocBook. I found converting the HTML to DocBook was slightly easier than having to parse the native WordPress format. I did this in two steps, first I wrote a PHP script to generate a quasi-DocBook file which uses the WordPress API to embed the HTML content of each post within a <code>&lt;section/&gt;</code>. Then I wrote an XSLT which transforms the quasi-DocBook and embedded HTML into a final valid DocBook file. The main PHP code is <a href="https://github.com/aebruno/wp2print/blob/master/lib/export-docbook.php">here</a>. You’ll need to change the include paths in <a href="https://github.com/aebruno/wp2print/blob/master/lib/config.php">config.php</a> to point to your WordPress installation (see the <a href="https://github.com/aebruno/wp2print/blob/master/Makefile">Makefile</a> for a complete example). The XSLT is <a href="https://github.com/aebruno/wp2print/blob/master/wp-html2docbook.xsl">here</a>. It looks for various HTML tags that appear in my blog and converts those to valid DocBook elements. I built up the XSLT by trial and error. I first just rendered the quasi-DocBook generated from the PHP script as PDF. The DocBook stylesheets have a nice feature in that any invalid DocBook elements it encounters are highlighted in red in the resulting PDF. By iterating through the invalid elements I was able to add the correct templates to my XSLT to account for all HTML tags found in my blog posts. You’ll most certainly need to modify this XSLT file to suite your specific needs but should serve as a decent starting point. Here’s an example of the HTML generated by WordPress for an image included in a blog post:
      </p>
      
      <p>
        &nbsp;
      </p>
      
      <div id="highlighter_977195">
        <div>
          <div>
            <table>
              <tr>
                <td>
                  <code>1</code>
                </td>
                
                <td>
                  <code>&lt;</code><code>div</code> <code>id</code><code>=</code><code>"attachment_155"</code> <code>class</code><code>=</code><code>"wp-caption aligncenter"</code> <code>style</code><code>=</code><code>"width: 310px"</code><code>&gt;</code>
                </td>
              </tr>
            </table>
          </div>
          
          <div>
            <table>
              <tr>
                <td>
                  <code>2</code>
                </td>
                
                <td>
                  <code>  </code><code>&lt;</code><code>a</code> <code>href</code><code>=</code><code>"/wp-content/media/2008/11/image.jpg"</code><code>&gt;</code>
                </td>
              </tr>
            </table>
          </div>
          
          <div>
            <table>
              <tr>
                <td>
                  <code>3</code>
                </td>
                
                <td>
                  <code>        </code><code>&lt;</code><code>img</code> <code>class</code><code>=</code><code>"size-medium wp-image-155"</code> <code>title</code><code>=</code><code>"image title"</code> <code>src</code><code>=</code><code>"/wp-content/media/2008/11/image-300x218.jpg"</code> <code>alt</code><code>=</code><code>"image alt"</code> <code>width</code><code>=</code><code>"300"</code> <code>height</code><code>=</code><code>"218"</code><code>/&gt;</code>
                </td>
              </tr>
            </table>
          </div>
          
          <div>
            <table>
              <tr>
                <td>
                  <code>4</code>
                </td>
                
                <td>
                  <code>  </code><code>&lt;/</code><code>a</code><code>&gt;</code>
                </td>
              </tr>
            </table>
          </div>
          
          <div>
            <table>
              <tr>
                <td>
                  <code>5</code>
                </td>
                
                <td>
                  <code>  </code><code>&lt;</code><code>p</code> <code>class</code><code>=</code><code>"wp-caption-text"</code><code>&gt;This is a description of the image&lt;/</code><code>p</code><code>&gt;</code>
                </td>
              </tr>
            </table>
          </div>
          
          <div>
            <table>
              <tr>
                <td>
                  <code>6</code>
                </td>
                
                <td>
                  <code>&lt;/</code><code>div</code><code>&gt;</code>
                </td>
              </tr>
            </table>
          </div>
        </div>
      </div>
      
      <p>
        &nbsp;
      </p>
      
      <p>
        Which then gets converted to a DocBook <a href="http://www.docbook.org/tdg5/en/html/mediaobject.html">mediaobject</a> element:
      </p>
      
      <p>
        &nbsp;
      </p>
      
      <div id="highlighter_865389">
        <div>
          <div>
            <table>
              <tr>
                <td>
                  <code>1</code>
                </td>
                
                <td>
                  <code>&lt;</code><code>para</code><code>&gt;</code>
                </td>
              </tr>
            </table>
          </div>
          
          <div>
            <table>
              <tr>
                <td>
                  <code>2</code>
                </td>
                
                <td>
                  <code>  </code><code>&lt;</code><code>mediaobject</code><code>&gt;</code>
                </td>
              </tr>
            </table>
          </div>
          
          <div>
            <table>
              <tr>
                <td>
                  <code>3</code>
                </td>
                
                <td>
                  <code>    </code><code>&lt;</code><code>imageobject</code><code>&gt;</code>
                </td>
              </tr>
            </table>
          </div>
          
          <div>
            <table>
              <tr>
                <td>
                  <code>4</code>
                </td>
                
                <td>
                  <code>       </code><code>&lt;</code><code>imagedata</code> <code>align</code><code>=</code><code>"center"</code> <code>fileref</code><code>=</code><code>"images/2008/11/image.jpg"</code> <code>width</code><code>=</code><code>"4.0in"</code> <code>depth</code><code>=</code><code>"3.0in"</code> <code>scalefit</code><code>=</code><code>"1"</code> <code>format</code><code>=</code><code>"JPG"</code><code>/&gt;</code>
                </td>
              </tr>
            </table>
          </div>
          
          <div>
            <table>
              <tr>
                <td>
                  <code>5</code>
                </td>
                
                <td>
                  <code>    </code><code>&lt;/</code><code>imageobject</code><code>&gt;</code>
                </td>
              </tr>
            </table>
          </div>
          
          <div>
            <table>
              <tr>
                <td>
                  <code>6</code>
                </td>
                
                <td>
                  <code>    </code><code>&lt;</code><code>caption</code><code>&gt;&lt;</code><code>para</code><code>&gt;This is a description of the image&lt;/</code><code>para</code><code>&gt;&lt;/</code><code>caption</code><code>&gt;</code>
                </td>
              </tr>
            </table>
          </div>
          
          <div>
            <table>
              <tr>
                <td>
                  <code>7</code>
                </td>
                
                <td>
                  <code>  </code><code>&lt;/</code><code>mediaobject</code><code>&gt;</code>
                </td>
              </tr>
            </table>
          </div>
          
          <div>
            <table>
              <tr>
                <td>
                  <code>8</code>
                </td>
                
                <td>
                  <code>&lt;/</code><code>para</code><code>&gt;</code>
                </td>
              </tr>
            </table>
          </div>
        </div>
      </div>
      
      <p>
        &nbsp;
      </p>
      
      <p>
        <strong>A note about images…</strong>
      </p>
      
      <p>
        Care must be taken to ensure any images you want included in the book are print ready. I ended up having quite a few images in my blog that I wanted to include in the final PDF which required some extra work to get them ready for printing. For best results you’ll want make to be sure the resolution of your images are at least 300ppi (<a href="https://secure.wikimedia.org/wikipedia/en/wiki/Dots_per_inch#DPI_or_PPI_in_digital_image_files">pixels per inch</a>). See <a href="http://connect.lulu.com/t5/Interior-Formatting/What-resolution-DPI-should-my-images-have-to-achieve-optimum/ta-p/31434">this post on Lulu</a>. For example, if your image is 600x600px and you set the resolution to be 300ppi, the printed image will be roughly 2x2in. In my case I was printing a 6×9 book and after factoring in margins/spine/bleed etc. I calculated the maximum print size I wanted each image was 4x3in (as defined in the DocBook XML element <code>&lt;imagedata width="4.0in" height="3.0in"/&gt;</code> in the above example). As most of the images were pictures, this print size ended up being large enough so the photo was still viewable but small enough to allow for 2 images per page. This meant that the minimum size (in pixels) each image had to be was 1200x900px. The problem was when we uploaded pictures to our blog we had WordPress resize them to 500x400px (from their original size of 2816x2112px from the camera). Fortunately, I still had the original image files which I collected and used in the final PDF. Something to keep in mind if you have images (especially photographs) in your blog that you want printed. I ran into another edge case with the images which required a little bit of <a href="http://www.imagemagick.org/">imagemagick</a>. I had a few important pictures that were taken with photo booth on a mac in which the original size image was a mere 640x480px. I knew the print version of the images would look dreadful so my only option was to resample them to a higher resolution. This can easily be accomplished using imagemagick’s <a href="http://www.imagemagick.org/script/command-line-options.php#resample">convert command</a>:
      </p>
      
      <p>
        &nbsp;
      </p>
      
      <div id="highlighter_664011">
        <div>
          <div>
            <table>
              <tr>
                <td>
                  <code>1</code>
                </td>
                
                <td>
                  <code>$ convert -resample 300x orig.jpg hires.jpg</code>
                </td>
              </tr>
            </table>
          </div>
        </div>
      </div>
      
      <p>
        &nbsp;
      </p>
      
      <p>
        In summary, be sure your images are high enough resolution for printing. It’s definitely worth the extra work. I had roughly 100 images in my blog and all of them turned out really nice in the final print book. I was quite impressed with the quality of Lulu’s printers.
      </p>
      
      <p>
        <strong>DocBook –> XSL-FO –> PDF</strong>
      </p>
      
      <p>
        Converting DocBook to PDF was fairly straightforward using two excellent projects <a href="http://docbook.sourceforge.net/">DocBook stylesheets</a> and <a href="http://xmlgraphics.apache.org/fop/">Apache FOP</a>. I won’t cover how to install them on your platform and refer you to the excellent INSTALL guides at the <a href="http://docbook.sourceforge.net/release/xsl/current/INSTALL">respective</a> <a href="http://xmlgraphics.apache.org/fop/quickstartguide.html">sites</a>. If you happen to be running Ubuntu using the stock packages should work fine. Simply run <code>aptitude install fop docbook-xsl</code> and you should be all set. The basic goal for this step was to use the DocBook XSL FO stylesheets to convert the DocBook created from the previous step into XSL-FO which can be fed into Apache FOP for conversion into PDF. This step required that an XSLT processor be installed such as xsltproc (libXML), Saxon, Xalan, etc. I used xsltproc and can easily be installed on Ubuntu <code>aptitude install xsltproc</code>. After running xsltproc I passed the resulting XSL-FO output into Apache FOP to generate the final PDF. For more details see the <a href="https://github.com/aebruno/wp2print/blob/master/Makefile">Makefile</a>. Here’s the basic commands:
      </p>
      
      <p>
        &nbsp;
      </p>
      
      <div id="highlighter_705196">
        <div>
          <div>
            <table>
              <tr>
                <td>
                  <code>1</code>
                </td>
                
                <td>
                  <code>$ xsltproc /path/to/docbook-xsl/fo/docbook.xsl docbook-final.xml &gt; book.fo</code>
                </td>
              </tr>
            </table>
          </div>
          
          <div>
            <table>
              <tr>
                <td>
                  <code>2</code>
                </td>
                
                <td>
                  <code>$ fop book.fo book.pdf</code>
                </td>
              </tr>
            </table>
          </div>
        </div>
      </div>
      
      <p>
        &nbsp;
      </p>
      
      <p>
        The DocBook XSL FO stylesheets provide a <a href="http://docbook.sourceforge.net/release/xsl/current/doc/fo/index.html">generous number of parameters</a> for customizing the resulting FO. The default parameter settings produce a very nice looking PDF but if you like to tweak things there’s no shortage of knobs to turn. As I ended up printing my book with Lulu there were a few specific customizations that were required. First I was interested in printing a US Trade 6×9 inch hard cover book so the default page <a href="http://docbook.sourceforge.net/release/xsl/current/doc/fo/page.width.html">width</a>/<a href="http://docbook.sourceforge.net/release/xsl/current/doc/fo/page.height.html">height</a> needed to be set accordingly. Some other tweaks I made included adjusting the <a href="http://docbook.sourceforge.net/release/xsl/current/doc/fo/page.margin.inner.html">margins</a> slightly to provide some extra room on the <a href="http://connect.lulu.com/t5/Interior-Formatting/How-big-should-my-margins-be/ta-p/31404">spine edge</a> of the book, customizing the <a href="http://docbook.sourceforge.net/release/xsl/current/doc/fo/generate.toc.html">table of contents</a> to only include the chapter/sections, and <a href="http://docbook.sourceforge.net/release/xsl/current/doc/fo/body.start.indent.html">customizing the indentation</a> of chapters and sections (in this case I didn’t want any indentation). Here’s the resulting xsltproc command with the custom parameter settings:
      </p>
      
      <p>
        &nbsp;
      </p>
      
      <div id="highlighter_653142">
        <div>
          <div>
            <table>
              <tr>
                <td>
                  <code>01</code>
                </td>
                
                <td>
                  <code>xsltproc \</code>
                </td>
              </tr>
            </table>
          </div>
          
          <div>
            <table>
              <tr>
                <td>
                  <code>02</code>
                </td>
                
                <td>
                  <code>--stringparam page.width 6in \</code>
                </td>
              </tr>
            </table>
          </div>
          
          <div>
            <table>
              <tr>
                <td>
                  <code>03</code>
                </td>
                
                <td>
                  <code>--stringparam page.height 9in \</code>
                </td>
              </tr>
            </table>
          </div>
          
          <div>
            <table>
              <tr>
                <td>
                  <code>04</code>
                </td>
                
                <td>
                  <code>--stringparam page.margin.inner 1.0in \</code>
                </td>
              </tr>
            </table>
          </div>
          
          <div>
            <table>
              <tr>
                <td>
                  <code>05</code>
                </td>
                
                <td>
                  <code>--stringparam page.margin.outer 0.8in \</code>
                </td>
              </tr>
            </table>
          </div>
          
          <div>
            <table>
              <tr>
                <td>
                  <code>06</code>
                </td>
                
                <td>
                  <code>--stringparam body.start.indent 0pt \</code>
                </td>
              </tr>
            </table>
          </div>
          
          <div>
            <table>
              <tr>
                <td>
                  <code>07</code>
                </td>
                
                <td>
                  <code>--stringparam body.font.family  Times \</code>
                </td>
              </tr>
            </table>
          </div>
          
          <div>
            <table>
              <tr>
                <td>
                  <code>08</code>
                </td>
                
                <td>
                  <code>--stringparam title.font.family Times \</code>
                </td>
              </tr>
            </table>
          </div>
          
          <div>
            <table>
              <tr>
                <td>
                  <code>09</code>
                </td>
                
                <td>
                  <code>--stringparam dingbat.font.family Times \</code>
                </td>
              </tr>
            </table>
          </div>
          
          <div>
            <table>
              <tr>
                <td>
                  <code>10</code>
                </td>
                
                <td>
                  <code>--stringparam generate.toc 'book toc title' \</code>
                </td>
              </tr>
            </table>
          </div>
          
          <div>
            <table>
              <tr>
                <td>
                  <code>11</code>
                </td>
                
                <td>
                  <code>--stringparam hyphenate false \</code>
                </td>
              </tr>
            </table>
          </div>
          
          <div>
            <table>
              <tr>
                <td>
                  <code>12</code>
                </td>
                
                <td>
                  <code>/path/to/docbook-xsl/fo/docbook.xsl \</code>
                </td>
              </tr>
            </table>
          </div>
          
          <div>
            <table>
              <tr>
                <td>
                  <code>13</code>
                </td>
                
                <td>
                  <code>docbook-final.xml &gt; book.fo</code>
                </td>
              </tr>
            </table>
          </div>
        </div>
      </div>
      
      <p>
        &nbsp;
      </p>
      
      <p>
        <strong>A note about Fonts..</strong>
      </p>
      
      <p>
        The last and most important configuration I made was with fonts. Lulu requires fonts to be fully <a href="https://secure.wikimedia.org/wikipedia/en/wiki/Portable_Document_Format#Fonts">embedded</a> which means any font you use in your PDF <a href="http://www.lulu.com/help/embed_fonts">must be embedded</a> (the font files are included directly in the PDF file) or else they will reject the PDF. Embedding fonts is supported by Apache FOP but requires some custom configuration. First I had to decide which font to use. Fonts can be really tricky and I didn’t want to get too fancy. Using a single font for the entire book was fine with me and I decided to stick with a traditional Times New Roman font. I ended up using the FreeSerif TrueType font from <a href="http://www.gnu.org/software/freefont/">GNU FreeFont</a>. It was already installed on my Ubuntu machine and very easy to embed with Apache FOP. By default these fonts are installed in <code>/usr/share/fonts/truetype/freefont/</code>.There’s lots of other free fonts out there that you could use including the <a href="https://fedorahosted.org/liberation-fonts/">Liberation Fonts</a> and even the <a href="http://packages.ubuntu.com/lucid/ttf-mscorefonts-installer">Micro$oft True Type Core Fonts</a> which can be installed on Ubuntu by running <code>aptitude install msttcorefonts</code>. To configure Apache FOP to use GNU Free Fonts and embed them into the final PDF I created a file called <code>userconf.xconf</code> with the following lines:
      </p>
      
      <p>
        &nbsp;
      </p>
      
      <div id="highlighter_435813">
        <div>
          <div>
            <table>
              <tr>
                <td>
                  <code>01</code>
                </td>
                
                <td>
                  <code>&lt;?</code><code>xml</code> <code>version</code><code>=</code><code>"1.0"</code><code>?&gt;</code>
                </td>
              </tr>
            </table>
          </div>
          
          <div>
            <table>
              <tr>
                <td>
                  <code>02</code>
                </td>
                
                <td>
                  <code>&lt;</code><code>fop</code> <code>version</code><code>=</code><code>"1.0"</code><code>&gt;</code>
                </td>
              </tr>
            </table>
          </div>
          
          <div>
            <table>
              <tr>
                <td>
                  <code>03</code>
                </td>
                
                <td>
                  <code>&lt;</code><code>renderers</code><code>&gt;</code>
                </td>
              </tr>
            </table>
          </div>
          
          <div>
            <table>
              <tr>
                <td>
                  <code>04</code>
                </td>
                
                <td>
                  <code>   </code><code>&lt;</code><code>renderer</code> <code>mime</code><code>=</code><code>"application/pdf"</code><code>&gt;</code>
                </td>
              </tr>
            </table>
          </div>
          
          <div>
            <table>
              <tr>
                <td>
                  <code>05</code>
                </td>
                
                <td>
                  <code>      </code><code>&lt;!-- Full path to truetype fonts to be embedded in PDF file --&gt;</code>
                </td>
              </tr>
            </table>
          </div>
          
          <div>
            <table>
              <tr>
                <td>
                  <code>06</code>
                </td>
                
                <td>
                  <code>      </code><code>&lt;</code><code>fonts</code><code>&gt;</code>
                </td>
              </tr>
            </table>
          </div>
          
          <div>
            <table>
              <tr>
                <td>
                  <code>07</code>
                </td>
                
                <td>
                  <code>        </code><code>&lt;</code><code>font</code> <code>embed-url</code><code>=</code><code>"&lt;a href="file:///usr/share/fonts/truetype/freefont/FreeSerif.ttf">file:///usr/share/fonts/truetype/freefont/FreeSerif.ttf&lt;/a>"</code><code>&gt;</code>
                </td>
              </tr>
            </table>
          </div>
          
          <div>
            <table>
              <tr>
                <td>
                  <code>08</code>
                </td>
                
                <td>
                  <code>          </code><code>&lt;</code><code>font-triplet</code> <code>name</code><code>=</code><code>"Times"</code> <code>style</code><code>=</code><code>"normal"</code> <code>weight</code><code>=</code><code>"normal"</code><code>/&gt;</code>
                </td>
              </tr>
            </table>
          </div>
          
          <div>
            <table>
              <tr>
                <td>
                  <code>09</code>
                </td>
                
                <td>
                  <code>        </code><code>&lt;/</code><code>font</code><code>&gt;</code>
                </td>
              </tr>
            </table>
          </div>
          
          <div>
            <table>
              <tr>
                <td>
                  <code>10</code>
                </td>
                
                <td>
                  <code>        </code><code>&lt;</code><code>font</code> <code>embed-url</code><code>=</code><code>"&lt;a href="file:///usr/share/fonts/truetype/freefont/FreeSerifBold.ttf">file:///usr/share/fonts/truetype/freefont/FreeSerifBold.ttf&lt;/a>"</code><code>&gt;</code>
                </td>
              </tr>
            </table>
          </div>
          
          <div>
            <table>
              <tr>
                <td>
                  <code>11</code>
                </td>
                
                <td>
                  <code>          </code><code>&lt;</code><code>font-triplet</code> <code>name</code><code>=</code><code>"Times"</code> <code>style</code><code>=</code><code>"normal"</code> <code>weight</code><code>=</code><code>"bold"</code><code>/&gt;</code>
                </td>
              </tr>
            </table>
          </div>
          
          <div>
            <table>
              <tr>
                <td>
                  <code>12</code>
                </td>
                
                <td>
                  <code>        </code><code>&lt;/</code><code>font</code><code>&gt;</code>
                </td>
              </tr>
            </table>
          </div>
          
          <div>
            <table>
              <tr>
                <td>
                  <code>13</code>
                </td>
                
                <td>
                  <code>        </code><code>&lt;</code><code>font</code> <code>embed-url</code><code>=</code><code>"&lt;a href="file:///usr/share/fonts/truetype/freefont/FreeSerifItalic.ttf">file:///usr/share/fonts/truetype/freefont/FreeSerifItalic.ttf&lt;/a>"</code><code>&gt;</code>
                </td>
              </tr>
            </table>
          </div>
          
          <div>
            <table>
              <tr>
                <td>
                  <code>14</code>
                </td>
                
                <td>
                  <code>          </code><code>&lt;</code><code>font-triplet</code> <code>name</code><code>=</code><code>"Times"</code> <code>style</code><code>=</code><code>"italic"</code> <code>weight</code><code>=</code><code>"normal"</code><code>/&gt;</code>
                </td>
              </tr>
            </table>
          </div>
          
          <div>
            <table>
              <tr>
                <td>
                  <code>15</code>
                </td>
                
                <td>
                  <code>        </code><code>&lt;/</code><code>font</code><code>&gt;</code>
                </td>
              </tr>
            </table>
          </div>
          
          <div>
            <table>
              <tr>
                <td>
                  <code>16</code>
                </td>
                
                <td>
                  <code>        </code><code>&lt;</code><code>font</code> <code>embed-url</code><code>=</code><code>"&lt;a href="file:///usr/share/fonts/truetype/freefont/FreeSerifBoldItalic.ttf">file:///usr/share/fonts/truetype/freefont/FreeSerifBoldItalic.ttf&lt;/a>"</code><code>&gt;</code>
                </td>
              </tr>
            </table>
          </div>
          
          <div>
            <table>
              <tr>
                <td>
                  <code>17</code>
                </td>
                
                <td>
                  <code>          </code><code>&lt;</code><code>font-triplet</code> <code>name</code><code>=</code><code>"Times"</code> <code>style</code><code>=</code><code>"italic"</code> <code>weight</code><code>=</code><code>"bold"</code><code>/&gt;</code>
                </td>
              </tr>
            </table>
          </div>
          
          <div>
            <table>
              <tr>
                <td>
                  <code>18</code>
                </td>
                
                <td>
                  <code>        </code><code>&lt;/</code><code>font</code><code>&gt;</code>
                </td>
              </tr>
            </table>
          </div>
          
          <div>
            <table>
              <tr>
                <td>
                  <code>19</code>
                </td>
                
                <td>
                  <code>      </code><code>&lt;/</code><code>fonts</code><code>&gt;</code>
                </td>
              </tr>
            </table>
          </div>
          
          <div>
            <table>
              <tr>
                <td>
                  <code>20</code>
                </td>
                
                <td>
                  <code>   </code><code>&lt;/</code><code>renderer</code><code>&gt;</code>
                </td>
              </tr>
            </table>
          </div>
          
          <div>
            <table>
              <tr>
                <td>
                  <code>21</code>
                </td>
                
                <td>
                  <code>&lt;/</code><code>renderers</code><code>&gt;</code>
                </td>
              </tr>
            </table>
          </div>
          
          <div>
            <table>
              <tr>
                <td>
                  <code>22</code>
                </td>
                
                <td>
                  <code>&lt;/</code><code>fop</code><code>&gt;</code>
                </td>
              </tr>
            </table>
          </div>
        </div>
      </div>
      
      <p>
        &nbsp;
      </p>
      
      <p>
        Then ran fop passing the -f option like so: <code>fop -f userconf.xconf book.fo book.pdf</code>. Note the <code>&lt;font-triplet &lt;strong>name="Times"&lt;/strong> /&gt;</code> attribute must match the <code>body.font.family Times</code> XSLT parameter passed to xsltproc command.
      </p>
      
      <p>
        <strong>Simple Example</strong>
      </p>
      
      <p>
        All the code described in this post is available on <a href="https://github.com/aebruno/wp2print">github</a>. I also include a simple example to demonstrate the entire conversion process and provide some sample PDFs to see how final book renders. I created a simple test blog consisting of Shakespeare’s Sonnets I thru X and exported the content in WordPress eXtended RSS so you can then import into a fresh install of WordPress. I tested using the latest version of WordPress at the time of this writing (v3.1). To try it out yourself download the code for wp2print and read thru the <a href="https://github.com/aebruno/wp2print/blob/master/README">README</a> file which outlines all the gory details. The <a href="https://github.com/aebruno/wp2print/blob/master/Makefile">Makefile</a> outlines the general process and should provide a good starting point for experimenting. Here’s some sample PDFs that were rendered from the example Shakespeare blog:
      </p>
      
      <ul>
        <li>
          <a href="http://qnot.files.wordpress.com/2011/04/book-with-chapters.pdf">Book with Chapters and Sections</a>
        </li>
        <li>
          <a href="http://qnot.files.wordpress.com/2011/04/book-with-articles.pdf">Book with all posts as DocBook Articles</a>
        </li>
        <li>
          <a href="https://github.com/aebruno/wp2print/blob/master/sample/sample-docbook.xml">Raw DocBook output</a>
        </li>
      </ul>
      
      <p>
        <strong>Conclusion</strong>
      </p>
      
      <p>
        With the help of a few simple scripts it’s possible to create a high quality print ready PDF book from a WordPress blog. Depending on the content of the blog you’ll most certainly need to tailor these scripts to suite your specific requirements. The main challenges are figuring out how you want to organize your blog posts into the framework of a book and then modifying the XSLT templates to convert the WordPress html markup of your blog into valid DocBook elements. The services offered by print on demand publishers such as Lulu provide an easy way to turn the resulting PDF into a high quality paper book.
      </p>
      
      <p>
        &nbsp;
      </p>
      
      <p>
        SOURCE：<a href="http://left.subtree.org/2011/04/09/wordpress-blog-to-print-book-a-case-study/">http://left.subtree.org/2011/04/09/wordpress-blog-to-print-book-a-case-study/</a>
      </p>
    </div>
  </div>
</div>

 [1]: http://left.subtree.org/