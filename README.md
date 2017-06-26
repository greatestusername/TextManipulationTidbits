# Useful Text Manipulation Tidbits For Working With Twitter Messages
(use -i flag to do inline editing on a file rather than display standard output)

### show only lines between 36 and 150 characters in length
`sed -nr  '/^.{36,150}$/p' temp.txt`

### delete lines longer than 36 characters
`sed '/.\{36\}./d' file.txt`

### delete all empty lines
`sed '/^\s*$/d' file.txt`

### remove non-ascii characters
`sed 's/[\d128-\d255]//g' file.txt`

### delete lines starting with a hashtag (comments or Twitter hashtags)
`sed -i '/^#/d' filepath`

### separate all paragraphs into separate files based on a trailing symbol (In this case using \xa9 (copyright symbol))
`awk -v RS="\xa9" 'NR > 1 {print RS $0 > (NR-1)}' file.txt`

### (j)oin and (p)rint silently all lines of file.txt using ex (removing  ^M (Windows line break), character \xa9 (copyright symbol), and lines starting with a hashtag)
`ex +%j +%p -scq! file.txt | sed -e 's/\^M//g' -e 's/\xa9//g' -e '/^#/d'`

### display a count for the number of times the hastag #cool can be found in all files in the current directory (\*) (use the -r flag if you wish to search recursively in sub directories)
`grep -c -i "#cool" *`

### Substitute "the" with "ppp" (Finding "the" as a whole word with \< \> marking the spaces surrounding it)
`sed 's/\<the\>/ppp/g' file.txt`

### replace all instances of "Dang" or "dang" with "Oops"
`sed 's/[dD]ang/Oops/g' file.txt`
