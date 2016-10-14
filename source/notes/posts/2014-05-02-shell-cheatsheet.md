---
layout: note
title: Tips for Shell
author: Oneplus
category: ["Linux"]
tags:
    - "shell"
    - "sed"
    - "awk"
    - "sort"
    - "uniq"
---

There will be some case-based tips for Shell.

### 1. Replace the sequence space with newline

Input example

~~~
a b  c   d
~~~

Output example

~~~
a
b
c
d
~~~

#### Summary

`sed` is the best solution.

#### Solution

~~~
sed -r -e 's/[[:space:]]/\n/g'
~~~

### 2. Sort the unordered word list (with duplication) by frequency

#### Summary

It is very useful when counting word frequency.

#### Solution

~~~
sort | uniq -c | sort -rn
~~~

### 3. Awk print line without first column

#### Summary

This command actually clear the first column from the file.

#### Solution

~~~
awk '{$1=""; print $0}'
~~~

### 4. Show the longest line in the file

#### Summary

Taking advantage of the const `length` in `awk`

#### Solution

~~~
awk '{print $0" "length}' | sort -k2 -nr | head -1
~~~

### 5. Ignore line that match some pattern

#### Summary and Solution

Using

~~~
grep -v
~~~

### 6. Batchly replace namespace

#### Summary

Using `for` to loop over the file and `sed` to perform the replacement.

#### Solution

~~~
for f in `find ./src -type f`; do sed -i 's/oldnamespace/newnamespace' $f; done
~~~

### 7. Generate 02, ..., 24 sequence


#### Summary

`Perl` can be a better solution.

#### Solution

~~~
perl -e 'for{$i=2;$i<=24;$i++}{printf("%02d\n", $i)}'
~~~

### 8. Command line calculator

#### Awk Solution

~~~
awk '{print 1/10}'
~~~

and additional enter is needed

#### Perl Solution

More flexiable (with formatting).

~~~
perl -e 'printf("%f\n", 1./10);'
~~~
