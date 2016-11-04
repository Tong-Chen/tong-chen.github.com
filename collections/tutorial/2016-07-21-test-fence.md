---
layout: post
title: Code Blocks in Lists or Nested Lists
---

(Source: [gist.github.com/clintel/1155906](https://gist.github.com/clintel/1155906))

For discussion, see [issue #1](https://github.com/planetjekyll/sandbox-syntax-highlighter/issues/1).  Thanks to Thomas Leitner for clearing up the syntax.

## Fenced code blocks inside ordered and unordered lists (V8)

**How it works**

The gist is that the indentation for the code block in lists is determined
by the column number of the first non-space character after the list item marker.

Examples (edit: I replaced the leading spaces with dots e.g. `·` so it looks correct):


**Bulleted List**

```
*·some text     =>  use 2 spaces indentation
*···some text   =>  use 4 spaces indentation
```

**Numbered List**

```
1.·some text    =>  use 3 spaces indentation
```

**==> If you line up the fenced code block with the "natural" list indentation, it will work.**


## Github fenced code blocks - It works, no magic.

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


## More Examples - Numbered Lists

1. This is a numbered list.
2. I'm going to include a fenced code block as part of this bullet:

   ```
   Code
   More Code
   ```

3. We can put fenced code blocks inside nested bullets, too.
   1. Like this:

      ```c
      printf("Hello, World!");
      ```

   2. The key is to indent your fenced code block lined up with the list item.
   3. Also need to put a separating newline above and below the fenced block.


## More Examples - Bulleted Lists

* This is a bulleted list.
* I'm going to include a fenced code block as part of this bullet:

  ```
  Code
  More Code
  ```

* We can put fenced code blocks inside nested bullets, too.
  * Like this:

    ```c
    printf("Hello, World!");
    printf("Hello, World!");
    printf("Hello, World!");
    printf("Hello, World!");
    printf("Hello, World!");
    printf("Hello, World!");
    printf("Hello, World!");
    ```

 * The key is to indent your fenced code block lined up with the list item.
 * Also need to put a separating newline above and below the fenced block.

