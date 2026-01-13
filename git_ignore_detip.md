# Create/update .gitignore
echo ".DS_Store" > .gitignore

# Commit & done
git add .gitignore && git commit -m "Add .gitignore (macOS)"
git push
