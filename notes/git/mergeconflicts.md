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

