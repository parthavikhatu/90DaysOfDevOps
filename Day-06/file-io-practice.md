# Day 06 - Linux File I/O Practice

## Commands Used

### Create file
touch notes.txt

### Write first line
echo "Line 1" > notes.txt

### Append second line
echo "Line 2" >> notes.txt

### Use tee
echo "Line 3" | tee -a notes.txt

### Read file
cat notes.txt

### Read first 2 lines
head -n 2 notes.txt

### Read last 2 lines
tail -n 2 notes.txt
