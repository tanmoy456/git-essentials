**Create/update .gitignore**

```
echo ".DS_Store" > .gitignore
```

**Commit**

```
git add .gitignore && git commit -m "Add .gitignore (macOS)"
git push
```
**Global Mac Fix (All Future Repos)**
```
echo ".DS_Store" >> ~/.gitignore_global
git config --global core.excludesfile ~/.gitignore_global
```
