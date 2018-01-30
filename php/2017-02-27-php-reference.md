# PHP Reference
> :calendar: *February 27, 2017*

### [String Functions](http://php.net/manual/en/ref.strings.php)

[`implode`](http://php.net/manual/en/function.implode.php)

Returns a string containing a string representation of all the array elements in the same order, with the glue string between each element.

[`join`](http://php.net/manual/en/function.join.php)

Alias of implode.

[`explode`](http://php.net/manual/en/function.explode.php)

Returns an array of strings, each of which is a substring of string formed by splitting it on boundaries formed by the string delimiter.

[`strlen`](http://php.net/manual/en/function.strlen.php)

Returns the length of a given string.

[`substr`](http://php.net/manual/en/function.substr.php)

Returns the portion of a string specified by the start and length parameters. 

[`strpos`](http://php.net/manual/en/function.strrpos.php)

Find the numeric position of the last occurrence of needle in the haystack string. Returns the position where the needle exists relative to the beginning of the haystack string (independent of search direction or offset). Also note that string positions start at 0, and not 1. Returns `false` if the needle was not found.

[`strrev`](http://php.net/manual/en/function.strrev.php)

Reverses a string.

[`strtoupper`](http://php.net/manual/en/function.strtoupper.php)

Returns string with all alphabetic characters converted to uppercase.

[`strtolower`](http://php.net/manual/en/function.strtolower.php)

Returns string with all alphabetic characters converted to lowercase.

[`trim`](http://php.net/manual/en/function.trim.php)

Strip whitespace (or other characters, i.e, tabs, newlines, returns) from the beginning and end of a string.

[`ltrim`](http://php.net/manual/en/function.ltrim.php)

Strip whitespace from the beginning of a string.

[`rtrim`](http://php.net/manual/en/function.rtrim.php)

Strip whitespace from the end of a string.

### [Array Functions](http://php.net/manual/en/ref.array.php)

[`array`](http://php.net/manual/en/function.array.php)

Creates an array.

[`array_push`](http://php.net/manual/en/function.array-push.php)

Push one or more elements onto the end of array. `array_push()` treats an array as a stack, and pushes the passed variables onto the end of array. The length of array increases by the number of variables pushed.

[`count`](http://php.net/manual/en/function.count.php)

Count all elements in an array, or something in an object.

[`array_shift`](http://php.net/manual/en/function.array-shift.php)

Shifts the first value of the array off and returns it, shortening the array by one element and moving everything down. All numerical array keys will be modified to start counting from zero while literal keys won't be touched.

[`array_unshift`](http://php.net/manual/en/function.array-unshift.php)

Prepends passed elements to the front of the array. Note that the list of elements is prepended as a whole, so that the prepended elements stay in the same order. All numerical array keys will be modified to start counting from zero while literal keys won't be changed.

[`array_pop`](http://php.net/manual/en/function.array-pop.php)

Pops and returns the last value of the array, shortening the array by one element.

[`unset`](http://php.net/manual/en/function.unset.php)

Destroys the specified variables. The behavior of `unset()` inside of a function can vary depending on what type of variable you are attempting to destroy. If a globalized variable is `unset()` inside of a function, only the local variable is destroyed. The variable in the calling environment will retain the same value as before `unset()` was called.

[`array_splice`](http://php.net/manual/en/function.array-splice.php)

Removes a portion of the array and replace it with something else.

[`array_combine`](http://php.net/manual/en/function.array-combine.php)

Creates an array by using the values from the keys array as keys and the values from the values array as the corresponding values.

[`array_merge`](http://php.net/manual/en/function.array-merge.php)

Merges the elements of one or more arrays together so that the values of one are appended to the end of the previous one. It returns the resulting array.

[`extract`](http://php.net/manual/en/function.extract.php)

Imports variables from an array into the current symbol table. Checks each key to see whether it has a valid variable name. It also checks for collisions with existing variables in the symbol table.

[`sort`](http://php.net/manual/en/function.sort.php)

This function sorts an array. Elements will be arranged from lowest to highest when this function has completed.

[`rsort`](http://php.net/manual/en/function.rsort.php)

This function sorts an array in reverse order (highest to lowest).

[`asort`](http://php.net/manual/en/function.asort.php)

This function sorts an array such that array indices maintain their correlation with the array elements they are associated with. This is used mainly when sorting associative arrays where the actual element order is significant.

[`arsort`](http://php.net/manual/en/function.arsort.php)

This function sorts an array such that array indices maintain their correlation with the array elements they are associated with. This is used mainly when sorting associative arrays where the actual element order is significant.

[`ksort`](http://php.net/manual/en/function.ksort.php)

Sorts an array by key, maintaining key to data correlations. This is useful mainly for associative arrays.

[`krsort`](http://php.net/manual/en/function.krsort.php)

Sorts an array by key in reverse order, maintaining key to data correlations. This is useful mainly for associative arrays.

[`each`](http://php.net/manual/en/function.each.php)

Returns the current key and value pair from an array and advances the array cursor. After `each()` has executed, the array cursor will be left on the next element of the array, or past the last element if it hits the end of the array. You have to use `reset()` if you want to traverse the array again using each.

[`list`](http://php.net/manual/en/function.list.php)

Assigns variables as if they were an array. `list()` only works on numerical arrays and assumes the numerical indices start at 0. In PHP 5, `list()` assigns the values starting with the right-most parameter. In PHP 7, `list()` starts with the left-most parameter.

[`array_keys`](http://php.net/manual/en/function.array-keys.php)

Returns an array of all the keys in an array. 

[`array_walk`](http://php.net/manual/en/function.array-walk.php)

Applies a user-defined callback function on every element of an array.

[`in_array`](http://php.net/manual/en/function.in-array.php)

Checks if a value exists in an array. Seaches haystack for needle. Returns `true` if the needle is found, `false` otherwise.

### [Math Functions](http://php.net/manual/en/ref.math.php)

[`round`](http://php.net/manual/en/function.round.php)

Returns the rounded value of a float to specified precision (optional). 

[`ceil`](http://php.net/manual/en/function.ceil.php)

Rounds a float to the next highest integer.

[`floor`](http://php.net/manual/en/function.floor.php)

Rounds a float to the next lowest integer.

[`pi`](http://php.net/manual/en/function.pi.php)

Returns an approximation of pi. The returned float has a precision based on the precision directive in php.ini, which defaults to 14. Also, you can use the `M_PI` constant which yields identical results to `pi()`.

[`abs`](http://php.net/manual/en/function.abs.php)

Returns the absolute value of a given number.

[`sqrt`](http://php.net/manual/en/function.sqrt.php)

Returns the square root of a given number.

[`rand`](http://php.net/manual/en/function.rand.php)

Returns a random integer between a given min and max integer (inclusive).

### [Variable Functions](http://php.net/manual/en/ref.var.php)

[`isset`](http://php.net/manual/en/function.isset.php)

Determines if a variable is set and is not `NULL`. If a variable has been unset with `unset()`, it will no longer be set. `isset()` will return FALSE if testing a variable that has been set to `NULL`. Also note that a null character `\0` is not equivalent to the PHP `NULL` constant. If multiple parameters are supplied then `isset()` will return `true` only if all of the parameters are set. Evaluation goes from left to right and stops as soon as an unset variable is encountered.

### [Control Structures](http://php.net/manual/en/control-structures.intro.php)

[`if`](http://php.net/manual/en/control-structures.if.php)

The `if` construct is one of the most important features of many languages, PHP included. It allows for conditional execution of code fragments.

[`else`](http://php.net/manual/en/control-structures.else.php)

Often you'd want to execute a statement if a certain condition is met, and a different statement if the condition is not met. This is what `else` is for. `else` extends an `if` statement to execute a statement in case the expression in the `if` statement evaluates to `false`.

```php
if(true) {
  echo "True";
} else {
  echo "False";
}
```

[`elseif`](http://php.net/manual/en/control-structures.elseif.php)

`elseif`, as its name suggests, is a combination of `if` and `else`. Like `else`, it extends an `if` statement to execute a different statement in case the original `if` expression evaluates to `false`. However, unlike `else`, it will execute that alternative expression only if the `elseif` conditional expression evaluates to `true`.

[`switch`](http://php.net/manual/en/control-structures.switch.php)

 - A switch statement is useful for when you have multiple if/elseif/else statements with multiple expressions that depend on the same value.
 - You can add multiple cases without a break, which is called "falling through".
 - Alternatively, you can end your switch with endswitch, which would negate the need for curly braces (syntactic sugar).

```php
switch(1) {
  case 1:
    echo "One";
    break;
  case 2:
    echo "Two";
    break;
  case 3:
  case 4:
    echo "Three or Four";
    break;
  default:
    echo "Not one through Four";
}
```

[`while`](http://php.net/manual/en/control-structures.while.php)

 - A While loop will execute the code block as long as a condition remains true.
 - As always with While loops, you must include a way for the condition to eventually evaluate to false.
 - While loops can be written similarly to a Switch using while/endwhile.
 
```php
$condition = true;

while($condition):
  echo "true"
endwhile;
```

[`do while`](http://php.net/manual/en/control-structures.do.while.php)

Use a do/while loop to ensure the code in the do block executes at least once, even if the condition in the while block is false.

```php
$condition = false;

do {
  echo "true";
} while($condition)
```

[`for`](http://php.net/manual/en/control-structures.for.php)

`for` loops are the most complex loops in PHP. The first expression is evaluated (executed) once unconditionally at the beginning of the loop. In the beginning of each iteration, the second expression is evaluated. If it evaluates to `true`, the loop continues and the nested statements are executed. If it evaluates to `false`, the execution of the loop ends. At the end of each iteration, the third expression is evaluated (executed).

```php
for ($i = 1; $i <= 10; $i++) {
  echo $i;
}
```

[`foreach`]()

The `foreach` construct provides an easy way to iterate over arrays. `foreach` works only on arrays and objects, and will issue an error when you try to use it on a variable with a different data type or an uninitialized variable.

In PHP 5, when `foreach` first starts executing, the internal array pointer is automatically reset to the first element of the array. This means that you do not need to call `reset()` before a `foreach` loop. In PHP 7, `foreach` does not use the internal array pointer.

```php
$greeting = array("Hello", " ", "World");

foreach($greeting as $word) {
  echo $word;
}
```

```php
$myM3 = array(
'year' => 2013,
'color' => "Black",
'doors' => 2  
);

foreach($myM3 as $key => $value) {
  echo $key . ": " . $value;
}
```

### [Directory Functions](http://php.net/manual/en/ref.dir.php)

[`chdir`](http://php.net/manual/en/function.chdir.php)

Change directory.

[`chroot`](http://php.net/manual/en/function.chroot.php)

Change the root directory.

[`closedir`](http://php.net/manual/en/function.closedir.php)

Close directory handle.

[`dir`](http://php.net/manual/en/function.dir.php)

Return an instance of the Directory class.

[`getcwd`](http://php.net/manual/en/function.getcwd.php)

Gets the current working directory.

[`opendir`](http://php.net/manual/en/function.opendir.php)

Open directory handle.

[`readdir`](http://php.net/manual/en/function.readdir.php)

Read entry from directory handle.

[`rewinddir`](http://php.net/manual/en/function.rewinddir.php)

Rewind directory handle.

[`scandir`](http://php.net/manual/en/function.scandir.php)

List files and directories inside the specified path

### [File Functions](http://php.net/manual/en/ref.filesystem.php)

[`dirname`](http://php.net/manual/en/function.dirname.php)

Returns a parent directory's path.

[`is_dir`](http://php.net/manual/en/function.is-dir.php)

Tells whether the filename is a directory.

[`mkdir`](http://php.net/manual/en/function.mkdir.php)

Makes directory.

[`rmdir`](http://php.net/manual/en/function.rmdir.php)

Removes directory.

### File Handling
Read Directory Files into an Array

```php
$dir = 'example';
$files = scandir($dir, 'w') or die('Cannot read directory: '.$dir);

//implicitly creates file
foreach ($files as $file) {

//do something with $file
}
```

Open and Close Directory

```php
$dir = 'example';
$dh = opendir($dir) or die('Cannot open file: '.$file);

//access directory
closedir($dh);
```

Read Directory

```php
$dir = 'example';
if ($dh = opendir($dir)) {
  while (($file = readdir($dh)) !== false) {
    if (substr($file, 0, 1) !== '.') {
    
    //do something with $file
    }
  }
  closedir($dh);
}
```

Create a File

```php
$file = 'file.txt';
$fh = fopen($file, 'w') or die('Cannot open file: '.$file);

//implicitly creates file
fclose($fh);
```

Open and Close a File

```php
$file = 'file.txt';
$fh = fopen($file, 'w') or die('Cannot open file: '.$file);

//open file ('w','r','a')... see mode below
fclose($fh);
```

Read a File

```php
$file = 'file.txt';
$fh = fopen($file, 'r');
$data = fread($fh,filesize($file));
fclose($fh);
```

Write to a File

```php
$file = 'file.txt';
$fh = fopen($file, 'w') or die('Cannot open file: '.$file);
$data = 'This is the data';
fwrite($fh, $data);
fclose($fh);
```

Append to a File

```php
$file = 'file.txt';
$fh = fopen($file, 'a') or die('Cannot open file: '.$file);
$data = 'New data line 1';
fwrite($fh, $data);
$new_data = "\n".'New data line 2';
fwrite($fh, $new_data);
fclose($fh);
```

Delete a File

```php
$file = 'file.txt';
unlink($file);
```

### File Modes

| Mode | Description                                                                                                                                                   |
| -----| ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `r`  | Open a file for read only. File pointer starts at the beginning of the file.                                                                                  |
| `w`  | Open a file for write only. Erases the contents of the file or creates a new file if it doesn't exist. File pointer starts at the beginning of the file.      |
| `a`  | Open a file for write only. The existing data in file is preserved. File pointer starts at the end of the file. Creates a new file if the file doesn't exist. |
| `x`  | Creates a new file for write only. Returns `false` and an error if file already exists.                                                                       |
| `r+` | Open a file for read/write. File pointer starts at the beginning of the file.                                                                                 |
| `w+` | Open a file for read/write. Erases the contents of the file or creates a new file if it doesn't exist. File pointer starts at the beginning of the file.      |
| `a+` | Open a file for read/write. The existing data in file is preserved. File pointer starts at the end of the file. Creates a new file if the file doesn't exist. |
| `x+` | Creates a new file for read/write. Returns `false` and an error if file already exists.                                                                       |
