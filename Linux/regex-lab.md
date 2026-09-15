
# TryHackMe Regex Lab Summary

## 📑 Core Syntax Cheat Sheet
* **Sets & Ranges:** `[abc]` (any of these) | `[a-z]` (lowercase range) | `[^abc]` (exclude these)
* **Tokens:** `\d` (digit) | `\D` (non-digit) | `\w` (alphanumeric) | `\W` (special char) | `\s` (space) | `.` (wildcard)
* **Quantifiers:** `*` (0+) | `+` (1+) | `?` (optional) | `{n}` (exact count) | `{n,m}` (range count)
* **Anchors:** `^` (line start) | `$` (line end) | `|` (OR logic) | `(...)` (capture group) | `\` (escape literal)

---

## Walkthrough (RegexR / Regex101)

### Q1: Match individual letters `c`, `o`, `g`
* **Solution:** `[cog]`
* **Explanation:** Bracketed set matches any single instance of the characters inside.

### Q2: Match `cat`, `fat`, `hat`
* **Solution:** `[cfh]at`
* **Explanation:** Matches `c`, `f`, or `h` as the starting character, immediately followed by the static string `at`.

### Q3: Match file instances like `File01`, `file2`, `File3`
* **Solution:** `[Ff]ile\d{1,2}` 
* **Explanation:** `[Ff]` handles uppercase/lowercase text. `\d{1,2}` targets a string ending in either a single or double-digit number. 

### Q4: Match variable spaces in `kali tools` 
* **Solution:** `kali\s+tools`
* **Explanation:** `\s+` dynamically accommodates single spaces, double spaces, or tabs between the two words. 

### Q5: Match generic quoted strings/variable paths 
* **Solution:** `\S*\s*\S*`
* **Explanation:** Fluidly spans across non-whitespace characters (`\S*`) and whitespace barriers (`\s*`). 

### Q6: Match lines starting with "Password:" + 10 chars (exclude '0') 
* **Solution:** `^Password:[^0]{10}` 
* **Explanation:** `^` anchors to line start. `[^0]` explicitly drops the number zero, and `{10}` enforces an exact character length. 

### Q7: Match lines explicitly starting with "username: " 
* **Solution:** `^username:\s`
* **Explanation:** Uses `^` to lock to the start of the text line, followed by `\s` for the mandatory ending space.

### Q8: Match lines not starting with a number
* **Solution:** `^\D`
* **Explanation:** Line start anchor `^` followed by uppercase `\D` (non-digit) immediately kicks out any line beginning with a number.

### Q9: Match literal `EOF$` at line end
* **Solution:** `EOF\$$`
* **Explanation:** Escapes the first dollar sign (`\$`) to read it as literal text, while the final `$` acts as the actual functional end-of-line anchor.

### Q10: Match "I use nano" or "I use vim"
* **Solution:** `I use (nano|vim)`
* **Explanation:** Employs a capture group `(...)` paired with a pipe `|` operator to act as an inline `OR` command.

### Q11: Match hashed layouts like `~$1$hash...`
* **Solution:** `^\$\d\$\S+`
* **Explanation:** Line start (`^`) → Escaped dollar (`\$`) → ID digit (`\d`) → Escaped dollar (`\$`) → Trailing string characters (`\S+`).

### Q12: Parse standard IPv4 addresses 
* **Solution:** `(\d{1,3}\.){3}\d{1,3}`
* **Explanation:** Matches 1 to 3 digits followed by an escaped literal period (`\.`). Groups and repeats this configuration exactly 3 times, ending with the final 1-3 digit octet block.

### Q13: Extract email strings into distinct fields 
* **Solution:** `(\w+)@(\w+)\.com`
* **Explanation:** Isolates user profile name `(\w+)`, crosses the `@` delimiter, isolates the corporate domain `(\w+)`, and closes on the escaped extension literal `\.com`
