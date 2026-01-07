1. Made changes on GitHub WEB interface
2. Worked locally → `git push` → ERROR: "Invalid username or token"  
3. Token expired (GitHub PATs expire)
4. Generated NEW token but local Git still cached OLD expired token
5. Web changes existed but local unaware → potential merge conflict risk

