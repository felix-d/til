# sub

```
sub(pattern, replacement) → new_str
sub(pattern, hash) → new_str
sub(pattern) {|match| block } → new_str
```

Returns a copy of str with the first occurrence of pattern replaced by the second argument. The pattern is typically a Regexp; if given as a String, any regular expression metacharacters it contains will be interpreted literally, e.g. '\\d' will match a backlash followed by ‘d’, instead of a digit.

If replacement is a String it will be substituted for the matched text. It may contain back-references to the pattern’s capture groups of the form "\d", where d is a group number, or "\k<n>", where n is a group name. If it is a double-quoted string, both back-references must be preceded by an additional backslash. However, within replacement the special match variables, such as &$, will not refer to the current match.

If the second argument is a Hash, and the matched text is one of its keys, the corresponding value is the replacement string.

In the block form, the current match string is passed in as a parameter, and variables such as $1, $2, $`, $&, and $' will be set appropriately. The value returned by the block will be substituted for the match on each call.

The result inherits any tainting in the original string or any supplied replacement string.

```
"hello".sub(/[aeiou]/, '*')                  #=> "h*llo"
"hello".sub(/([aeiou])/, '<\1>')             #=> "h<e>llo"
"hello".sub(/./) {|s| s.ord.to_s + ' ' }     #=> "104 ello"
"hello".sub(/(?<foo>[aeiou])/, '*\k<foo>*')  #=> "h*e*llo"
'Is SHELL your preferred shell?'.sub(/[[:upper:]]{2,}/, ENV)
 #=> "Is /bin/bash your preferred shell?"
```

# gsub

```
gsub(pattern, replacement) → new_str
gsub(pattern, hash) → new_str
gsub(pattern) {|match| block } → new_str
gsub(pattern) → enumerator
```

Returns a copy of str with the all occurrences of pattern substituted for the second argument. The pattern is typically a Regexp; if given as a String, any regular expression metacharacters it contains will be interpreted literally, e.g. '\\d' will match a backlash followed by ‘d’, instead of a digit.

If replacement is a String it will be substituted for the matched text. It may contain back-references to the pattern’s capture groups of the form \\d, where d is a group number, or \\k<n>, where n is a group name. If it is a double-quoted string, both back-references must be preceded by an additional backslash. However, within replacement the special match variables, such as $&, will not refer to the current match.

If the second argument is a Hash, and the matched text is one of its keys, the corresponding value is the replacement string.

In the block form, the current match string is passed in as a parameter, and variables such as $1, $2, $`, $&, and $' will be set appropriately. The value returned by the block will be substituted for the match on each call.

The result inherits any tainting in the original string or any supplied replacement string.

When neither a block nor a second argument is supplied, an Enumerator is returned.

```
"hello".gsub(/[aeiou]/, '*')                  #=> "h*ll*"
"hello".gsub(/([aeiou])/, '<\1>')             #=> "h<e>ll<o>"
"hello".gsub(/./) {|s| s.ord.to_s + ' '}      #=> "104 101 108 108 111 "
"hello".gsub(/(?<foo>[aeiou])/, '{\k<foo>}')  #=> "h{e}ll{o}"
'hello'.gsub(/[eo]/, 'e' => 3, 'o' => '*')    #=> "h3ll*"
```
