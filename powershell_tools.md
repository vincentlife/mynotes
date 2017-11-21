# Get-Content
gc log.txt | select -first 10 # head
gc -TotalCount 10 log.txt     # also head
gc log.txt | select -last 10  # tail
gc -Tail 10 log.txt           # also tail (since PSv3), also much faster than above option
gc log.txt | more             # or less if you have it installed
gc log.txt | %{ $_ -replace '\d+', '($0)' }         # sed

gc log.txt -head 10 
gc log.txt -tail 10
gc log.txt -tail 10 -wait

gc log.txt -ReadCount 5 | %{$_;throw "pipeline end!"} # head
gc log.txt | %{$num=0;}{$num++;"$num $_"}             # cat -n
gc log.txt | %{$num=0;}{$num++; if($num -gt 2 -and $num -lt 7){"$num $_"}} # sed