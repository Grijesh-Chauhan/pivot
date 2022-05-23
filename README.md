# pivot
a command-line tool to transpose CSV like text

Simple and useful

```bash
$ git clone https://github.com/Grijesh-Chauhan/pivot.git /tmp/repo
$ mkdir ~/bin
$ mv /tmp/repo/pivot ~/bin/.
$ chmox a+x ~/bin/pivot
$ echo 'export PATH="$HOME/bin:$PATH"' >> ~/.bashrc
$ source ~/.bashrc
$ pivot --examples
```

You can achieve something like the same using `datamash` by applying `transpose` option

```bash
$ cat example.csv
"something","a","b","c","d","message"
"one","1","2","3","4","NA"
"two","#5","6","","8","world"
"three","9","10","-1","12","-1"
," 12"," 12"," 12"," 13"
"#six"," 1"," 2"," 3"," 4","5"

$ datamash transpose --no-strict --filler="" -t ','  --output-delimiter='-'   <  ~/example.csv
"something" "one" "two" "three"  "#six"
"a" "1" "#5" "9" " 12" " 1"
"b" "2" "6" "10" " 12" " 2"
"c" "3" "" "-1" " 12" " 3"
"d" "4" "8" "12" " 13" " 4"
"message" "NA" "world" "-1"  "5"
```

Although, `datamash` syntax is fairly complex for frequent tasks. It accepts a single char separator, and the output is not well formatted.

`datamash` is for the advanced use case, while I writo `pivote` is more suitable for debugging data in an input source file. Example:


```bash
$ awk 'NR == 1 || /two/' ~/example.csv | pivot -F ',"' -c
something   two
a           #5
b           6
c
d           8
message     world
```

We can check the value for a field (or all fields) for some selected record.

Give it a Try!!
