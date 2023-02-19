==========
Content
==========

Azure
+++++++

Website
--------
The general answer would catch the number with re.match() and to convert that number (string) to integer with int(). Use these numbers to sort the files with sorted()

Code
import re 
import math
from pathlib import Path 

file_pattern = re.compile(r'.*?(\d+).*?')
def get_order(file):
    match = file_pattern.match(Path(file).name)
    if not match:
        return math.inf
    return int(match.groups()[0])

sorted_files = sorted(files, key=get_order)
Example input
Consider random files with one integer number in any part of the filename:

├── 012 some file.mp3
├── 1 file.txt
├── 13 file.mp3
├── 2 another file.txt
├── 3 file.csv
├── 4 file.mp3
├── 6 yet another file.txt
├── 88 name of file.mp3
├── and final 999.txt
├── and some another file7.txt
├── some 5 file.mp3
└── test.py
Example output
The get_order() could be used to sort the files, when passed to the sorted() builtin function in the key argument

In [1]: sorted(files, key=get_order)
Out[1]:
['C:\\tmp\\file_sort\\1 file.txt',
 'C:\\tmp\\file_sort\\2 another file.txt',
 'C:\\tmp\\file_sort\\3 file.csv',
 'C:\\tmp\\file_sort\\4 file.mp3',
 'C:\\tmp\\file_sort\\some 5 file.mp3',
 'C:\\tmp\\file_sort\\6 yet another file.txt',
 'C:\\tmp\\file_sort\\and some another file7.txt',
 'C:\\tmp\\file_sort\\012 some file.mp3',
 'C:\\tmp\\file_sort\\13 file.mp3',
 'C:\\tmp\\file_sort\\88 name of file.mp3',
 'C:\\tmp\\file_sort\\and final 999.txt',
 'C:\\tmp\\file_sort\\test.py']
``Short explanation
The re.compile is used to give a small speed boost (if matching multiple times same pattern)
The re.match is used to match the regular expression patterh
In the regex pattern, .*? means any character (.), zero or more times (*) non-greedily (?). \d+ matches any digit number one or more times, and the parenthesis just captures that match to the groups() list.
In case of no match (no digits in the file), the match will be None, and the get_order gives infinity; these files are sorted arbitrarily, but one could add logic for these (was not asked in this question).
The sorted() function takes key argument, which should be callable which takes one argument: The item in the list. In this case, it will be one of those file strings (full file path)
The Path(file).name just takes the filename part (without suffix) from full file path.``



Concept
-------


