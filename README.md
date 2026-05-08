# Bluewave School Website

Bluewave School Website is a responsive single-page school website project built with HTML, CSS, and vanilla JavaScript. It is designed to look polished in a portfolio while staying simple enough for beginners to understand and customize.

## Included files

- `index.html` — complete website with structure, styling, and interactive behavior
- `README.md` — project overview and usage notes
- `CUSTOMIZATION.md` — beginner-friendly editing guide
- `FEATURES.md` — feature summary
- `PROJECT_STRUCTURE.md` — file and folder map
- `CHANGELOG.md` — release notes
- `LICENSE` — MIT license
- `.gitignore` — common local ignore rules
- `assets/` — local SVG artwork used by the site

## Features

- Responsive layout for desktop, tablet, and mobile screens
- Sticky header with mobile menu
- Dark mode toggle saved in `localStorage`
- Scroll reveal animations for cards and sections
- Local asset-based hero and gallery illustrations
- Contact form validation with inline errors and success feedback
- Single-file front-end implementation for easy deployment

## Run locally

1. Clone or download the repository.
2. Open `index.html` in your browser.
3. No build tools or dependencies are required.

## Customization

See [`CUSTOMIZATION.md`](CUSTOMIZATION.md) for quick edits such as changing the school name, colors, images, and contact details.

## License

This project is released under the [MIT License](LICENSE).

## Reset repository to one clean initial commit (main only)

Use these steps if you want `parasverma07/school-website-project` to look brand new with exactly one commit on `main`.
⚠️ **WARNING:** This process permanently deletes git history and remote branches.

1. **Create a safe local backup first**
   Replace `/path/to/school-website-project` with your local repository path.
   ```bash
   cd /path/to/school-website-project
   backup_dir="$HOME/school-website-backup-$(date +%Y%m%d-%H%M%S)"
   mkdir -p "$backup_dir"
   rsync -a --exclude='.git' ./ "$backup_dir/"
   ```

2. **Make sure only the final required files are present**
   Review this keep-list before running.
   ```bash
   cd /path/to/school-website-project
   keep_args=( -not -name '.git' -not -name 'index.html' -not -name 'README.md' -not -name 'CUSTOMIZATION.md' -not -name 'FEATURES.md' -not -name 'PROJECT_STRUCTURE.md' -not -name 'CHANGELOG.md' -not -name 'LICENSE' -not -name '.gitignore' -not -name 'assets' )
   find . -mindepth 1 -maxdepth 1 "${keep_args[@]}" -print
   find . -mindepth 1 -maxdepth 1 "${keep_args[@]}" -exec rm -rf {} +
   ```

3. **Delete all git history and reinitialize**
   This is destructive and cannot be undone. Confirm before continuing:
   ```bash
   read -r -p "Type RESET to permanently delete local .git history and prepare remote override: " confirm
   if [ "$confirm" = "RESET" ]; then
     rm -rf .git
     git init
     git add .
     git commit -m "Initial complete school website project"
     git branch -M main
     repo_url="https://github.com/parasverma07/school-website-project.git"
     if git remote get-url origin >/dev/null 2>&1; then
       git remote set-url origin "$repo_url"
     else
       git remote add origin "$repo_url"
     fi
     git remote -v
   else
     echo "Operation cancelled. No history was removed."
   fi
   ```

4. **Force overwrite remote `main` with this single commit**
   ```bash
   git push --force origin main
   ```

5. **Delete all remote branches except `main`**
   Preview branches that will be deleted, then run delete:
   ```bash
   branches_to_delete="$(git for-each-ref --format='%(refname:strip=3)' refs/remotes/origin | awk '$0 != "HEAD" && $0 != "main"')"
   printf '%s\n' "$branches_to_delete"
   printf '%s\n' "$branches_to_delete" | while IFS= read -r branch; do
     [ -z "$branch" ] && continue
     case "$branch" in
       *[!A-Za-z0-9._/-]*)
         echo "Skipping unsafe branch name: $branch"
         continue
         ;;
     esac
     git push origin --delete "$branch"
   done
   ```

6. **Verify repository is clean**
   ```bash
   git fetch origin --prune
   git log --oneline origin/main
   git branch -r
   ```
   Expected result:
   - `git log --oneline origin/main` shows only one commit: `Initial complete school website project`
   - `git branch -r` shows only `origin/main` (and optional `origin/HEAD -> origin/main`)
