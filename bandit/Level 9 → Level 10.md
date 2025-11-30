- **Step 1:**  
    `grep "=" data.txt` → tried searching for password (expected `=` sign), but didn’t work because file wasn’t plain text.
    
- **Step 2:**  
    `strings data.txt` → extracts **human-readable text** from a binary or non-text file.
    
    - Showed all readable strings inside the file.
        
    - Among them was the line with the **password**.