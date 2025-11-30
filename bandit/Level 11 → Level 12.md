- **Step 1:** Understand `rot13` → a simple substitution cipher that shifts letters by 13 places.
    
- **Step 2:** `cat data.txt` → shows contents of the file.
    
- **Step 3:**
    
    `echo "data" | tr 'A-Za-z' 'N-ZA-Mn-za-m'`
    
    - `echo "data"` → outputs the text.
        
    - `|` → pipes output to next command.
        
    - `tr 'A-Za-z' 'N-ZA-Mn-za-m'` → translates each letter into its rot13 equivalent (A→N, N→A, etc.).
        

**Password:** 7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4
