## Useful terminal commands

# display content of file
`cat notes.txt`

# printing portion of file content in terminal

`sed -n '4,8p' notes.txt`

`head -8 notes.txt | tail -5`

`awk {if(NR >=4 && NR <= 8) print $0} notes.txt`
