---
title: Markdown tips
author: ct
layout: page
---


### 记录无法归类的小问题及解决方法

5. Markdown中给图片增加标题

   [如下代码]{http://stackoverflow.com/questions/19331362/using-an-image-caption-in-markdown-jekyll}

   ```markdown
   ![](path_to_image)
   *image_caption*
   ```
   
   ```html
   <p>
       <img src="path_to_image" alt>
   	<em>image_caption</em>
   </p>
   ```

6. Markdown table
 
   |---
   | Default aligned | Left aligned | Center aligned | Right aligned
   |-|:-|:-:|-:
   | First body part | Second cell | Third cell | fourth cell
   | Second line |foo | **strong** | baz
   | Third line |quux | baz | bar
   |---
   | Second body
   | 2 line
   |===
   | Footer row
   
   ```
   |---
   | Default aligned | Left aligned | Center aligned | Right aligned
   |-|:-|:-:|-:
   | First body part | Second cell | Third cell | fourth cell
   | Second line |foo | **strong** | baz
   | Third line |quux | baz | bar
   |---
   | Second body
   | 2 line
   |===
   | Footer row
   ```

7. Fence codes

   1. Do step 1.
   2. Now do this:
       
      ```ruby
      def print_hi(name)
        puts "Hi, #{name}"
      end
      print_hi('Tom')
      #=> prints 'Hi, Tom' to STDOUT.
      ```
           
   3. Now you can do this.
   
    * The key is to indent your fenced code block lined up with the list item.
    * Also need to put a separating newline above and below the fenced block.

