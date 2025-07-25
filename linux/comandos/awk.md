# The basic about awk command

#### Using AWK command with FOR
```sh
	files=path/*.txt
	for f in $files; do awk '/<Input here a Regex>/ {print $0}' $f; done
```

> This line above we use the FOR and AWK command to read the contents the files loaded on variable $files. But if us use only awk the execution will be more fast, see example in the next line. 

#### Using only AWK 
```sh 
	files=path/*.txt
	awk '/<Input here a Regex>/ {print $0}' $f; done
```

#### Now to do a compare execution time,  use the command time with characters {} for to grouped. Remember of to finalize the blocks of commands with dot and comma.

```sh
	files=path/*.txt
	time { for f in $files; do awk '/<Input here a Regex>/ {print $0}' $f; done; } 

	time { awk '/<Input here a Regex>/ {print $0}' $files; }
```
