- **Step 1:**  
    `uniq -u data.txt` → shows only **unique lines** (not repeated).
    
    - But this still gave **all possible unique lines**, not just the password.
        
- **Step 2:**  
    `sort data.txt | uniq -u` → first sorts the file, then shows **lines that appear only once**.
    
    - The password was the **only non-repeating line** → found successfully.