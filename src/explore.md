### How big is the data set?
```bash
wc -l clean_dialog.csv 
```
--> 36860 lines 

### What is the structure of the data? 

```bash
head clean_dialog.csv
```
--> fields: "title","writer","pony","dialog"

title is the episode title, pony is the pony that is speaking etc. all entries are strings. 

### How many episodes does it cover? 

Want to get number of unique values in the title col
```bash
csvtool col 1 clean_dialog.csv | tail -n +2 | sort -u | wc -l
```
--> 197

### Unexpected aspect 
There are actions in the dialog in square brackets - would need to be removed if want to analyze just dialog. 

### Analyzing speaker frequency 
``` bash
total=$(csvtool col 3 clean_dialog.csv | tail -n +2 | wc -l)
echo $total

echo "pony_name,total_line_count,percent_all_lines" > line_percentages.csv

count=$(csvtool col 3 clean_dialog.csv | grep -cx "Twilight Sparkle")
percent=$(awk -v c="$count" -v t="$total" 'BEGIN {printf "%.2f", c/t*100}')
echo "Twilight Sparkle,$count,$percent" >> line_percentages.csv

count=$(csvtool col 3 clean_dialog.csv | grep -cx "Rarity")
percent=$(awk -v c="$count" -v t="$total" 'BEGIN {printf "%.2f", c/t*100}')
echo "Rarity,$count,$percent" >> line_percentages.csv

count=$(csvtool col 3 clean_dialog.csv | grep -cx "Pinkie Pie")
percent=$(awk -v c="$count" -v t="$total" 'BEGIN {printf "%.2f", c/t*100}')
echo "Pinkie Pie,$count,$percent" >> line_percentages.csv

count=$(csvtool col 3 clean_dialog.csv | grep -cx "Rainbow Dash")
percent=$(awk -v c="$count" -v t="$total" 'BEGIN {printf "%.2f", c/t*100}')
echo "Rainbow Dash,$count,$percent" >> line_percentages.csv

count=$(csvtool col 3 clean_dialog.csv | grep -cx "Fluttershy")
percent=$(awk -v c="$count" -v t="$total" 'BEGIN {printf "%.2f", c/t*100}')
echo "Fluttershy,$count,$percent" >> line_percentages.csv
```

csv contents: 
pony_name,total_line_count,percent_all_lines\
Twilight Sparkle,4745,12.87\
Rarity,2660,7.22\
Pinkie Pie,2833,7.69\
Rainbow Dash,3072,8.33\
Fluttershy,2109,5.72\

