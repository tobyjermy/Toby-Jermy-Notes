# 📐 Toby's Maths Notes

University lecture notes for Spring 2026 — built with Jekyll & GitHub Pages.

## Modules

| Code    | Module                            |
|---------|-----------------------------------|
| MA32023 | Bayesian Statistics               |
| MA32024 | Time Series & Spatial Statistics  |
| MA32048 | Discrete Probability              |
| MA32061 | Measure Theory & Integration      |
| MA32068 | Probability & Finance             |

## Setup

1. Create a new GitHub repository (e.g. `maths-notes`).
2. Push all these files to the `main` branch.
3. Go to **Settings → Pages** and set the source to `main` branch, root (`/`).
4. Your site will be live at `https://<username>.github.io/maths-notes/`.
5. **Important**: Update `baseurl` in `_config.yml` to match your repo name:
   ```yaml
   baseurl: "/maths-notes"
   ```

## Adding New Lecture Notes

1. Create a new `.md` file in the appropriate module folder, e.g. `ma32023/lecture-02.md`.
2. Add the YAML front matter:
   ```yaml
   ---
   layout: default
   title: "Lecture 2 — Title Here"
   ---
   ```
3. Add a back-link and start writing:
   ```markdown
   <a href="{{ '/ma32023/' | relative_url }}" class="back-link">← MA32023 Bayesian Statistics</a>

   # Lecture 2 — Title Here

   Your content here...
   ```
4. Update the module's `index.md` to add the lecture to the list.
5. Commit and push — GitHub Pages will rebuild automatically.

## Formatting Reference

### LaTeX Maths

- **Inline**: `$x^2 + y^2 = z^2$`
- **Display**: 
  ```
  $$
  \int_0^\infty e^{-x} \, dx = 1
  $$
  ```

### Code Blocks

Use fenced code blocks with a language identifier:

````
```python
import numpy as np
x = np.linspace(0, 1, 100)
```
````

### Theorems & Definitions

Use blockquotes:

```markdown
> **Theorem.** Statement of the theorem here.
```

### Tables

```markdown
| Header 1 | Header 2 |
|----------|----------|
| Cell 1   | Cell 2   |
```
