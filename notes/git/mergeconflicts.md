## ✏️

### Dealing with Merge Conflicts

[_back_](../../README.md)

---

_This will need revision..._

**Prereq**

- For the three-way diff workflow, add the following to your `.gitconfig` file :

  - Do `nvim ~/.gitconfig`

  ```
  [merge]
  conflictstyle = diff3
  ```

  - Or you can set it globally with the following command :

    - `git config --global merge.conflictstyle diff3`

  - Find all files that have merge conflicts in them...
    - `git diff --name-only --diff-filter=U`

**Neovim + Fugitive**

- Open neovim in project, open `:GStatus`
- Files marked with `U` for "unresolved", cursor over them and use keybinding : `dv`
  to display diff3 layout for diff
