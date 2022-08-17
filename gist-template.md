# Creating Dial Plan using Regex

Working in the VoIP industry I often found myself lost when I had to create special dial plans matching clients' needs. The dial plan is a pattern written in Regex that allows you to control call routing based on the user input. If the input matches a specific dial plan pattern the call will be appropriately routed. 

## Summary
In this tutorial, I will be covering creating simple dial plans. A good example is preventing users from making an international call or allowing users to use 7 digit format. In the event of entering seven digits, the pattern will match with the 7-digit dial plan you created and the call will go out from the {{area code}} XXX-XXXX. Another example is creating dial plans for dynamic caller IDs.
```
{^411|[2356789]11|*xx+|900x|1[0-1]x|1[2-9]xx[2-9]xxxxxx|[2-4]xx.|<=1{{area_code}}>[2-9]xxxxxx.|x+}
```

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [Grouping Constructs](#grouping-constructs)
- [Bracket Expressions](#bracket-expressions)
- [Character Classes](#character-classes)
- [The OR Operator](#the-or-operator)
- [Flags](#flags)
- [Character Escapes](#character-escapes)

## Regex Components
Let's take a look at this dial plan. Even though the pattern seems long and difficult to understand, it becomes easier once you split it into functional pieces. The symbol | pipe is used to separate sections, each sections surves it's own purpose. The dial plan string must be wrapped inside curly brackets {} (alternative to // in JavaScript).
### Anchors
#1
```
{^411|
```
In this section, the pattern starts with ^(anchor) this allows dialing to 411
### Character Classes
#2
```
[2356789]11|
```
Matches any one digit in the [] (this is called character set) + 11. This allows dialing anything matching pattern from 211 to 911.

#3
```
1[0-1]x|
```
Allows dialing 3 digit numbers started with 1 => [0 or 1] + any digit from 0 to 9. Example: 101

#4
```
 1[2-9]xx[2-9]xxxxxx
```
Allows dialing 11 digit numbers which has leading 1. 1 will not be acceptes as the second ot 5th digit as this would go against trunk prefixes reserverd by North American Numbering Plan
#5
```
<=1{{area_code}}>[2-9]xxxxxx.|
```
This section adds 1 + area code then makes sure the fierst digit of prefix != 1 (parameter is used in this example, but it could also be hard coded)
### Quantifiers
#6
```
x+}
```
Finally x+ will catch all digits. X is a wild card and + allows any number of matches


## Author

### Github: https://github.com/Anastasia095
### Rapository: https://github.com/Anastasia095/Regex-Tutorial