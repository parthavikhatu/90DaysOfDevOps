# Day 20 – Bash Scripting Challenge: Log Analyzer and Report Generator

## Objective

Build a real-world log analysis tool that:

* Validates user input
* Analyzes log files
* Finds errors and critical events
* Generates reports
* Archives processed logs

---

# Task 1: Input and Validation

## Why Input Validation?

Input validation prevents the script from running with missing or invalid files.

### log_analyzer.sh

**Script**

```
#!/bin/bash

set -euo pipefail

if [ $# -ne 1 ]; then
    echo "Usage: ./log_analyzer.sh <log_file>"
    exit 1
fi

LOG_FILE="$1"

if [ ! -f "$LOG_FILE" ]; then
    echo "Error: File does not exist."
    exit 1
fi
```

**Output (No Argument)**

```
./log_analyzer.sh

Usage: ./log_analyzer.sh <log_file>
```

**Output (Invalid File)**

```
./log_analyzer.sh missing.log

Error: File does not exist.
```

---

# Task 2: Error Count

## Goal

Count all lines containing:

* ERROR
* Failed

### Script

```
ERROR_COUNT=$(grep -Ei "ERROR|Failed" "$LOG_FILE" | wc -l)

echo "Total Errors: $ERROR_COUNT"
```

**Output**

```
Total Errors: 127
```

---

# Task 3: Critical Events

## Goal

Display all CRITICAL events with line numbers.

### Script

```
echo "----- Critical Events -----"

grep -n "CRITICAL" "$LOG_FILE"
```

**Output**

```
----- Critical Events -----

Line 84: 2025-07-29 10:15:23 CRITICAL Disk space below threshold

Line 217: 2025-07-29 14:32:01 CRITICAL Database connection lost
```

---

# Task 4: Top 5 Error Messages

## Goal

Identify the most frequent error messages.

### Script

```
echo "----- Top 5 Error Messages -----"

grep "ERROR" "$LOG_FILE" \
| sed 's/.*ERROR //' \
| sort \
| uniq -c \
| sort -rn \
| head -5
```

**Output**

```
----- Top 5 Error Messages -----

45 Connection timed out

32 File not found

28 Permission denied

15 Disk I/O error

9 Out of memory
```

---

# Task 5: Summary Report

## Goal

Generate a report file with:

* Analysis date
* Log file name
* Total lines processed
* Error count
* Top 5 errors
* Critical events

### Report File

```
REPORT="log_report_$(date +%Y-%m-%d).txt"
```

### Script

```
{
    echo "===== LOG ANALYSIS REPORT ====="
    echo
    echo "Date: $(date)"
    echo "Log File: $LOG_FILE"
    echo "Total Lines: $(wc -l < "$LOG_FILE")"
    echo "Total Errors: $ERROR_COUNT"
    echo

    echo "===== TOP 5 ERRORS ====="
    grep "ERROR" "$LOG_FILE" \
    | sed 's/.*ERROR //' \
    | sort \
    | uniq -c \
    | sort -rn \
    | head -5

    echo

    echo "===== CRITICAL EVENTS ====="
    grep -n "CRITICAL" "$LOG_FILE"

} > "$REPORT"
```

**Output**

```
Report Generated:

log_report_2026-02-11.txt
```

---

## Sample Report

```
===== LOG ANALYSIS REPORT =====

Date: Tue Feb 11 10:15:30 UTC 2026

Log File: sample_log.log

Total Lines: 5420

Total Errors: 127

===== TOP 5 ERRORS =====

45 Connection timed out
32 File not found
28 Permission denied
15 Disk I/O error
9 Out of memory

===== CRITICAL EVENTS =====

84: CRITICAL Disk space below threshold
217: CRITICAL Database connection lost
```

---

# Task 6 (Optional): Archive Processed Logs

## Goal

Move analyzed logs into an archive directory.

### Script

```
mkdir -p archive

mv "$LOG_FILE" archive/

echo "Log file archived successfully."
```

**Output**

```
Log file archived successfully.
```

---

# Complete log_analyzer.sh

**Script**

```
#!/bin/bash

set -euo pipefail

if [ $# -ne 1 ]; then
    echo "Usage: ./log_analyzer.sh <log_file>"
    exit 1
fi

LOG_FILE="$1"

if [ ! -f "$LOG_FILE" ]; then
    echo "Error: File does not exist."
    exit 1
fi

ERROR_COUNT=$(grep -Ei "ERROR|Failed" "$LOG_FILE" | wc -l)

REPORT="log_report_$(date +%Y-%m-%d).txt"

{
    echo "===== LOG ANALYSIS REPORT ====="
    echo
    echo "Date: $(date)"
    echo "Log File: $LOG_FILE"
    echo "Total Lines: $(wc -l < "$LOG_FILE")"
    echo "Total Errors: $ERROR_COUNT"
    echo

    echo "===== TOP 5 ERRORS ====="
    grep "ERROR" "$LOG_FILE" \
    | sed 's/.*ERROR //' \
    | sort \
    | uniq -c \
    | sort -rn \
    | head -5

    echo

    echo "===== CRITICAL EVENTS ====="
    grep -n "CRITICAL" "$LOG_FILE"

} > "$REPORT"

echo "Total Errors: $ERROR_COUNT"

echo
echo "----- Critical Events -----"
grep -n "CRITICAL" "$LOG_FILE"

mkdir -p archive
mv "$LOG_FILE" archive/

echo
echo "Report Generated: $REPORT"
echo "Log Archived Successfully"
```

---

# Key Commands Learned

```
grep
grep -n
grep -c
wc -l
sort
uniq -c
head
sed
date
mv
mkdir -p
```

---

# Interview Questions

### Why validate script arguments?

To prevent execution with missing or invalid input.

### What does grep -n do?

Displays matching lines with line numbers.

### What does grep -c do?

Counts matching lines.

### Why use sort | uniq -c?

To count repeated occurrences of text.

### What is the purpose of a log analyzer?

To identify errors, failures, and critical events quickly.

### Why archive processed logs?

To keep working directories clean and preserve historical logs.

### What does set -euo pipefail provide?

Safer script execution by detecting errors early.

---

# What I Learned

* Parsing large log files using Bash.
* Counting and categorizing errors.
* Extracting critical events for troubleshooting.
* Generating automated reports.
* Archiving processed logs for maintenance and compliance.
