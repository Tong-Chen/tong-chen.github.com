---
title: Makefile tips
author: ct
layout: page
---


### 记录无法归类的小问题及解决方法

1. Makefile variable assignment [ref](http://stackoverflow.com/questions/448910/makefile-variable-assignment)

   * Lazy Set: Normal setting of a variable - values within it are recursively expanded when the variable is used,  not when it's declared.

     ```
     VARIABLE = value
     ```
    
	* Immediate Set: Setting of a variable with simple expansion of the values inside - values within it are expanded at declaration time.
      
	  ```
      VARIABLE := value
      ```

    * Set If Absent: Setting of a variable only if it doesn't have a value

	  ```
      VARIABLE ?= value
      ```

	* Append: Appending the supplied value to the existing value (or setting to that value if the variable didn't exist)

	  ```
      VARIABLE += value
	  ```

2.




