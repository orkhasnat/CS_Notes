😭😭 when using sed, PLEASE USE -E/-r (extended regex) or all hell breaks loose because of BRE 😭😭
---

# Using different delimiters in sed
What if, in sed, you have lots of slashes in the pattern and/or replacement?
One solution is to escape them all (the so-called tooth-saw effect):

```bash
sed 's/\/a\/b\/c\//\/d\/e\/f\//'    # change "a/b/c/" to "d/e/f/"
```

but that is ugly and unreadable. It's a not-so-known fact that sed can use any character as separator for the "s" command. Basically, sed takes whatever follows the "s" as the separator. So, our code above can be rewritten for example in one of the following ways:
```bash
sed 's_/a/b/c/_/d/e/f/_'
sed 's;/a/b/c/;/d/e/f/;'
sed 's#/a/b/c/#/d/e/f/#'
sed 's|/a/b/c/|/d/e/f/|'
sed 's /a/b/c/ /d/e/f/ '       # yes, even space
```
An even less-known fact is that you can use a different delimiter *even for patterns used in addresses*, using a special syntax:

```bash
# do this (ugly)...
sed '/\/a\/b\/c\//{do something;}'**
# ...or these (better)
sed '\#/a/b/c/#{do something;}'
sed '\_/a/b/c/_{do something;}'
sed '\%/a/b/c/%{do something;}'**
```

# Using & as the matched string

Sometimes you want to search for a pattern and add some characters, like parenthesis, around or near the pattern you found. It is easy to do this if you are looking for a particular string:
```bash
sed 's/abc/(abc)/' <old >new
```
This won't work if you don't know exactly what you will find. How can you put the string you found in the replacement string if you don't know what it is?
The solution requires the special character `&`. It corresponds to the pattern found.
```bash
sed 's/[a-z]*/(&)/' <old >new
```
You can have any number of `&` in the replacement string. You could also double a pattern, e.g. the first number of a line:
```bash
echo "123 abc" | sed 's/[0-9]*/& &/'
->> 123 123 abc
```