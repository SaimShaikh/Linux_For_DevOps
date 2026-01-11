# Linux Text Processing: grep, sed, AWK

Master the essential Linux text processing tools for log analysis, configuration management, and automation scripting.

## Why These Tools Matter in DevOps

- **grep**: Search and filter logs, configs, outputs instantly
- **sed**: Edit files/streams without opening editors
- **AWK**: Parse structured data, generate reports, transform outputs

These tools process **billions of lines** in production logs daily.

## Quick Reference Table

| Tool | Primary Use | Speed | Best For |
|------|-------------|-------|----------|
| `grep` | Search/Filter | Fastest | Finding patterns |
| `sed` | Edit/Replace | Fast | Stream editing |
| `AWK` | Parse/Analyse | Medium | Data processing |

---

## 1. grep - Search Like a Pro

**What**: Global Regular Expression Print - finds lines matching patterns

### When to Use
```
Log analysis, config search, pipeline filtering
```

### Essential Commands

```bash
# Basic search
grep "ERROR" /var/log/app.log

# Case insensitive
grep -i "error" app.log

# Show line numbers
grep -n "ERROR" app.log

# Recursive search
grep -r "database" /etc/

# Show context (3 lines before/after)
grep -C 3 "ERROR" app.log

# Multiple patterns
grep -E "ERROR|WARN|INFO" app.log
```

### Practical Example - Log Analysis

```bash
# Find failed login attempts with timestamps
grep -E "Failed password|Authentication failure" /var/log/auth.log
```

**Output:**
```
Jan 11 14:23:01 server sshd[1234]: Failed password for user from 192.168.1.100
Jan 11 14:25:15 server sshd[5678]: Authentication failure for root
```

### Advanced grep Examples

```bash
# Count matching lines
grep -c "ERROR" app.log

# Show only matching part
grep -o "error.*" app.log

# Invert match (show lines WITHOUT pattern)
grep -v "DEBUG" app.log

# Show file names with matches
grep -l "ERROR" /var/log/*.log

# Extended regex with word boundaries
grep -w "ERROR" app.log  # Matches ERROR as whole word only
```

---

## 2. sed - Stream Editor (Non-Interactive)

**What**: Stream EDitor - edits files/streams without opening them

### When to Use
```
Config updates, log cleanup, deployment scripts
```

### Essential Commands

```bash
# Replace first occurrence in line
sed 's/old/new/' file.txt

# Replace ALL occurrences in line
sed 's/old/new/g' file.txt

# Replace in-place (modifies original file)
sed -i 's/old/new/g' file.txt

# Delete lines matching pattern
sed '/pattern/d' file.txt

# Print specific lines
sed -n '10,20p' file.txt
```

### Practical Example - Config Management

```bash
# Update nginx config (backup first)
sudo cp /etc/nginx/nginx.conf /etc/nginx/nginx.conf.bak
sudo sed -i 's/worker_processes 1/worker_processes auto/g' /etc/nginx/nginx.conf
```

**Before:**
```
worker_processes 1;
```

**After:**
```
worker_processes auto;
```

### Advanced sed Examples

```bash
# Replace with backup (no separate cp needed)
sed -i.bak 's/old/new/g' file.txt

# Delete multiple lines
sed '1,5d' file.txt  # Delete lines 1-5

# Insert text before line
sed '5i\# New comment' file.txt

# Append text after line
sed '5a\# New comment' file.txt

# Replace with capture groups
sed 's/\(.*\) \(.*\)/\2 \1/' file.txt  # Swap columns

# Multiple operations
sed -e 's/old/new/g' -e '/pattern/d' file.txt
```

### DevOps Gold - Multi-file Update

```bash
# Update all .env files
find . -name ".env" -exec sed -i 's/DB_HOST=localhost/DB_HOST=prod-db/g' {} \;

# Update all Python files
find . -name "*.py" -exec sed -i 's/DEBUG=True/DEBUG=False/g' {} \;
```

---

## 3. AWK - Data Processing Powerhouse

**What**: Pattern scanning and processing language - a mini programming language for text processing

### When to Use
```
Log parsing, report generation, CSV/JSON processing
```

### Basic Structure

```bash
awk 'PATTERN { ACTION }' file
```

### Key Variables

- `$0`: Entire line
- `$1, $2, ..., $NF`: Individual columns (fields)
- `NR`: Current row number
- `NF`: Number of fields in current row
- `FS`: Field separator (default: space)
- `OFS`: Output field separator

### Essential Commands

```bash
# Print specific columns
awk '{print $1, $NF}' file.txt     # First and last column

# Sum column values
awk '{sum+=$3} END {print sum}' file.txt

# Filter by value
awk '$3 > 100 {print}' file.txt

# Custom formatting
awk '{print "User:", $1, "CPU:", $9}' top.log

# Change field separator (CSV example)
awk -F',' '{print $1, $3}' data.csv
```

### Practical Example - Resource Monitoring

```bash
# Parse top output for CPU usage
top -b -n1 | awk '/Cpu\(s\):/ {print "CPU Usage:", $2 + $4 "%"}'
```

**Output:**
```
CPU Usage: 23.5%
```

### Log Analysis Masterclass

```bash
# Count HTTP status codes from nginx log
tail -f /var/log/nginx/access.log | \
awk '{print $9}' | \
grep -E '2|3|4|5' | \
sort | uniq -c | sort -nr

# Output:
#   1250 200
#    45 404
#     3 500
```

### Advanced AWK Examples

```bash
# Calculate average response time
awk '{sum+=$NF; count++} END {print "Average:", sum/count "ms"}' response_times.log

# Extract and format data
awk 'BEGIN {print "User,Login_Time"} NR>1 {print $1","$2}' access.log

# Conditional logic
awk '$3 > 500 {print "SLOW: " $0} $3 <= 500 {print "FAST: " $0}' response.log

# String manipulation
awk '{print toupper($1), tolower($2)}' file.txt

# Count occurrences
awk '{count[$1]++} END {for (word in count) print word, count[word]}' file.txt
```

---

## Real-World DevOps Pipeline Example

**Scenario**: Monitor application health from logs

```bash
#!/bin/bash
LOG_FILE="/var/log/app/app.log"

echo "=== Application Health Report ==="
echo "Recent Errors:"
grep -i "error" $LOG_FILE | tail -5

echo -e "\nTop 5 IP Addresses:"
grep "GET" $LOG_FILE | \
awk '{print $1}' | \
sort | uniq -c | sort -nr | head -5

echo -e "\nResponse Time Summary:"
grep "response_time" $LOG_FILE | \
awk -F'[=]' '{sum+=$2; count++} END {print "Avg:", sum/count "s"}'

echo -e "\nStatus Code Distribution:"
grep "HTTP" $LOG_FILE | \
awk '{print $NF}' | \
sort | uniq -c | sort -nr
```

**Sample Output:**
```
=== Application Health Report ===
Recent Errors:
2025-01-11 14:23:45 ERROR: Database connection timeout
2025-01-11 14:24:12 ERROR: Invalid user input

Top 5 IP Addresses:
     245 192.168.1.100
     189 10.0.0.50
      67 172.16.0.25
      34 192.168.1.150
      12 10.0.0.100

Response Time Summary:
Avg: 245.67s

Status Code Distribution:
   1250 200
     45 404
      3 500
```

---

## Kubernetes & Docker Log Processing

### Filter Pod Logs by Error Level

```bash
# Get ERROR logs from specific pod
kubectl logs pod-name | grep -E "ERROR|FATAL"

# Get logs from all pods in namespace
kubectl logs -n kube-system -l app=nginx | grep "ERROR"
```

### Docker Container Log Analysis

```bash
# Real-time error monitoring
docker logs -f container-name | grep -i "error"

# Extract timestamps and messages
docker logs container-name | \
awk '{print $1, $2, $NF}' | \
tail -20
```

### Extract Metrics from Application Logs

```bash
# Parse custom log format
docker logs my-app | \
grep "request_time" | \
awk -F'=' '{sum+=$2; count++} END {print "Avg request time:", sum/count "ms"}'
```

---

## Pro Tips & Best Practices

### Performance Hierarchy
```
Fastest → grep > sed > awk > Python
Use fgrep for fixed string searches (no regex)
```

### Combine for Maximum Power

```bash
# Pipeline masterclass - analyze production logs
cat /var/log/nginx/access.log | \
grep "404" | \
sed 's/\t/ /g' | \
awk '{print $1, $7}' | \
sort | uniq -c | sort -nr | \
head -10
```

### Safety First

```bash
# Always backup before sed -i
cp file file.bak
sed -i.bak 's/old/new/g' file  # Creates automatic backup

# Test sed before applying
sed 's/old/new/g' file | head  # Preview changes

# Verify grep result count
grep -c "pattern" file  # Count matches
```

### Escape Special Characters

```bash
# Escape special regex characters
grep "price: \$50" file.txt

# Use fgrep for literal strings
fgrep "$PATH" file.txt  # Won't interpret $ as regex
```

---

## Quick Cheat Sheet

### grep Flags
```bash
-i  : Case insensitive
-n  : Show line numbers
-r  : Recursive search
-C 3: Context (3 lines before/after)
-E  : Extended regex (or |)
-v  : Invert match (exclude pattern)
-c  : Count matching lines
-l  : List files with matches
-w  : Whole word match
```

### sed Commands
```bash
s   : Substitute
d   : Delete
p   : Print
i   : Insert
a   : Append
-i  : In-place edit
-e  : Multiple commands
.bak: Create backup
```

### AWK Built-in Functions
```bash
length()    : String length
substr()    : Extract substring
index()     : Find position
tolower()   : Convert to lowercase
toupper()   : Convert to uppercase
split()     : Split string into array
gsub()      : Global substitute (like sed)
```

---

## Exercise: Combine All Three

**Challenge**: Parse access logs and find top error-prone endpoints

```bash
#!/bin/bash
# Combine grep + sed + awk for complete analysis

LOG_FILE="access.log"

echo "=== Error Analysis ==="

# Step 1: Filter errors with grep
# Step 2: Extract endpoint with sed
# Step 3: Count and sort with awk

grep -E "404|500" $LOG_FILE | \
sed 's/.*"\(GET\|POST\|PUT\) \(.*\) .*/\2/' | \
awk '{count[$1]++} END {for (url in count) print count[url], url}' | \
sort -nr | head -5
```

---

## Quick Reference Card

```
GREP:
  grep "pattern" file              → Find lines with pattern
  grep -i "pattern" file           → Case insensitive
  grep -E "pat1|pat2" file         → Multiple patterns
  grep -v "pattern" file           → Exclude pattern

SED:
  sed 's/old/new/' file            → Replace first occurrence
  sed 's/old/new/g' file           → Replace all occurrences
  sed -i 's/old/new/g' file        → Edit in-place
  sed '/pattern/d' file            → Delete matching lines
  sed -n '10,20p' file             → Print lines 10-20

AWK:
  awk '{print $1}' file            → Print first column
  awk '{sum+=$2} END {print sum}' file → Sum column
  awk '$3>100' file                → Filter by value
  awk -F',' '{print $1}' file      → Change field separator
  awk 'NR>1' file                  → Skip header row
```

---

## Learn More Resources

- `man grep` - Official grep manual
- `man sed` - Official sed manual
- `man awk` - Official AWK manual
- `info gawk` - GNU AWK documentation

---

## Contributing

Found a cool one-liner? Add it to this guide! Submit issues or PRs for improvements.

**Last Updated**: January 2026  
**Status**: Production Ready  
**DevOps Level**: Intermediate to Advanced
