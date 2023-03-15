---
title: Blog-on-path.md
date: 2023-03-15 15:07:10
tags:
---

# Path

The javascript path module provides a way of working with directories and file paths.

Some of the important methods provided by the path module are

- path.join
- path.resolve

## path.join

---

The path.join() method joins all given paths together using the platform-specific separator as a delimiter, after joining the paths it will normalize the resulting path and returns the normalized path as a string.

_Systax:_

```javascript
path.join([...paths]);
```

All the paths should be a string. A Type Error will be thrown if the given path is not in the string format.

_Examples:_

- When all the given paths are strings,

```javascript
console.log(path.join("path1", "path2", "path3"));
//path1/path2/path3
```

- When all the given paths are not strings,

```javascript
console.log(path.join("path1", 2, "path3"));
//TypeError [ERR_INVALID_ARG_TYPE]: The "path" argument must be of a type string.
```

- If the path segment is of length Zero then that will be ignored,

```javascript
console.log(path.join("path1", "", "path3"));
//path1/path3
```

- If the joined path string is a zero-length string then the '.' current working directory will be returned.

```javascript
console.log(path.join("", ""));
//.
```

- Other Examples

```javascript
console.log(path.join("path1", "..", "path2", "path3"));
// path2/path3
```

Here the second string represents the parent directory hence after normalization path2/path3 will be returned.

```javascript
console.log(path.join(__dirname, "path1", "path2"));

// /home/tejashri/Desktop/MountBlue/Blog_creation/BLOGS_on_JS/source/_posts/path1/path2
```

We will get the present working directory by using \_\_dirname.
"/home/tejashri/Desktop/MountBlue/Blog_creation/BLOGS_on_JS/source/\_posts" is current working directory.

```javascript
console.log(path.join("path1/path2", "path3"));
//path1/path2/path3
```

We can also provide two or more paths in a single string.

## path.resolve

---

The path.resolve() method will resolve a given number of paths into an absolute path.

_Systax:_

```javascript
path.resolve([...paths]);
```

The given paths will be processed from right to left by prepending each of the paths until the absolute path is created. The resulting path is normalized and trailing slashes are removed.

Here also the paths must be strings, and all Zero-length strings will be ignored,

_Examples:_

- When a nonstring path is given,

```javascript
console.log(path.resolve("", 2, "path3"));
//TypeError [ERR_INVALID_ARG_TYPE]: The "path" argument must be of type string
```

- When some paths are given,

```javascript
console.log(path.resolve("path1", "/path2", "path3", "path4"));
// /path1/path2/path3
```

Here the path4 is not an absolute path, so it prepends path3 i.e ,**path2/path3**, now also it is not an absolute path so again it will prepend /path2 i.e, **/path2/path3/path4**, now it is an absolute path so it will return this path without prepending path1.

- When all the paths are absolute,

```javascript
console.log(path.resolve("/path1", "/path2", "/path3"));
// /path3
```

returns **/path3** as it is an absolute path.

- When paths are not given,

```javascript
console.log(path.resolve());
// /home/tejashri/Desktop/MountBlue/Blog_creation/BLOGS_on_JS/source/_posts
```

As we are not passing any paths absolute path of the current working directory will be returned.

- If an absolute path is not generated even after prepending all the paths,

```javascript
console.log(path.resolve("", "path1/path2", "path3"));
// /home/tejashri/Desktop/MountBlue/Blog_creation/BLOGS_on_JS/source/_posts/path1/path2/path3
```

where /home/tejashri/Desktop/MountBlue/Blog_creation/BLOGS_on_JS/source/\_posts is the current working directory.

After processing all the given path segments If an absolute path has not been generated means it will take the current working directory to process and provide the resulting absolute path.
