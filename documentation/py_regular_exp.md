# Python Regular Expression

## Table of Content
 * [back to ToC](./table_of_content.md)
 * [python basic](./py_basics.md)
 * [Sequences - list, dict, string...](./py_sequences.md)
 * [Regular expression](./py_regular_exp.md)
 * [functions](./py_functions.md)
 * [Data Abstraction](./py_data_abstraction.md)
 * [Trees](./py_trees.md)
 * Libraries
   * [pyperclip](./py_lib_pyperclip.md)
   * [reading and writing files](./py_io.md)


## [Regular expression](https://docs.python.org/3/howto/regex.html)
```python
>>>import re
>>>strBlob = '555-555-5555'
# create regex object and use r to search as raw data
>>>strPattern = re.compile(r'\d\d\d-\d\d\d-\d\d\d\d')

# pass the string to search into regex object's search method
>>>matchedObjects = strPattern.search(strBlob)

# call group to return the first instance of matched expression
>>>print(matchedObjects.group())
555-555-5555

#parethesis in regular expression

# search for regex either bracket or complete
>>>strPattern = re.compile(r'(\d\d\d)-(\d\d\d-\d\d\d\d)')
>>>strBlob = '(555) 555-5555'
>>>matchedObjects = strPattern.search(strBlob)	
>>>areaCode, mainNumber = matchedObjects.groups()

>>>matchedObjects.group(0)
'555-555-5555'
>>>areCode = matchedObjects.group(1)
>>>matchedObjects.group(2)

#matching multipe groups with |

# finds first instace of batman or wonder woman
>>>regHero = re.compile(r'batman|wonder woman')
>>>mo1 = regHero.search('batman, superman, wonder woman')	
>>>mo2 = regHero.search('superman, wonder woman, batman')
>>>mo1.group()
batman
>>>mo2.group()
wonder woman

>>>regBat = re.compile(r'bat(man|mobile|cave|girl)')
# finds batman and batwoman. pattern in (wo)? is optional
>>>regBat = re.compile(r'bat(wo)?man')
# finds batman, batwoman, batwowoman, batwowowoman etc
>>>regbat = re.compile(r'bat(wo)*man')
# atleast 1 - finds batwoman, batwowoman but not batman
>>>regbat = re.compile(r'bat(wo)+man')

(Ha){3}  -->HaHaHa
(Ha){3,5}--> HaHaHa, HaHaHaHa, HaHaHaHaHa
(Ha){3, }--> Unbounded - 3 or more
(Ha){ ,5}--> Unbounded - 0 to 5

# searching for parethesis need escape charater even in raw string
/(, /), /|, /*, /+

#Python regex are greedy by default - ie finds the longest possible string
# finds the longest possible
>>>greedyRegex = re.compile(r'(Ha){3,5}')
# find the shortest possible
>>>nonGreedyRegex = re.compile(r'(Ha){3,5}?')
>>>mo1 = greedyRegex.search('HaHaHaHa')
>>>mo2 = nonGreedyRegex.search('HaHaHaHa')
>>>print(mo1.group() )
HaHaHaHa
>>>print(mo2.group() )
HaHaHa

>>>phoneRegex1 = re.compile(r'\d\d\d-\d\d\d-\d\d\d\d')
>>>phoneRegex2 =  re.compile(r'(\d\d\d)-(\d\d\d)-(\d\d\d\d)')
#finds all the matching exp in the string
>>>phoneRegex1.findall('asdf ads 898-959-5265 afw da 595-898-8747')
['898-959-5265', '595-898-8747'] 
#list of tuples
>>>phoneRegex2.findall('asdf ads 898-959-5265 afw da 595-898-8747')
[('898', '959', '5265'), ('595', '898', '8747')] 


\d - digits 0 to 9
\D - not (digits 0 to 9)
\w - digits, letters, and underscore
\W - not (digits, letters, and underscore)
\s - space, tab, newline
\S - not (space, tab, newline)
[0-5] - matches 0,1,2,3,4,5


# any number of digits followed by a whitespace and then any number of words
xReg = re.compile(r'\d+\s\w+')

# find vowels from string
userDef1 = re.compile(r'[aeiuoAEIOU]')

# all lower and upper alpha + digits
userDef2 = re.compile(r'[a-zA-Z0-9]')

# all lower and ending in period. no need \. inside []
userDef3 = re.compile(r'['[a-z.]')

# caret inside [] finds non regex from string
userDef4 = re.compile(r'[^aeiuoAEIOU]')

# caret as raw string means must start with given expression
userDef5 = re.compile(r'^[a-e]+')

# dollar sign means ends with given expression
userDef6 = re.compile(r'[a-e]+$')

# whole string is digits
userDef7 = re.compile(r'^d+$')

# one wild character with dot. everything but newline
userDef8 = re.compile(r'.at')

# more than one wild character with .*
r'.*'
# greedy wild character with .*?
r'.*?'

# case insensitive
re.compile(r'ayush',re.IGNORECASE)

#String substitution with regex
>>>xReg = re.compile(r'Ayush \w+')
>>>xReg.sub('King', 'My name is Ayush Maskey')
My name is King
>>>censorAgents = re.compile(r'Agent (/w) w+')
>>>censorAgents.sub('\1***', 'Agent James and Agent Bond went undercover')
Agent J*** and Agent B*** went undercover


# complicated regex into readable
# re.VERBOSE ignores white space and comments
# expression inside ''' triple quote - triple quote extends to multiple lines

phoneRegex = re.compile(r'((\d{3}|\(\d{3}\))?(\s|-|\.)?\d{3}(\s|-|\.)\d{4}(\s*(ext|x|ext.)\s*\d{2,5})?)')

VS

phoneRegex = re.compile(r'''(]
    (\d{3}|\(\d{3}\))?            # area code
    (\s|-|\.)?                    # separator
    \d{3}                         # first 3 digits
    (\s|-|\.)                     # separator
    \d{4}                         # last 4 digits
    (\s*(ext|x|ext.)\s*\d{2,5})?  # extension
    )''', re.VERBOSE)
```
