# Code Practice Arena

<a href="https://remideso.github.io/Code-Practice-Arena/" target="_blank">Code Practice Arena</a>

A browser-based practice website containing 150 verified coding exercises:

- 50 Python exercises
- 50 machine-learning exercises written in Python
- 50 SQL exercises
- Easy, medium, and hard difficulty levels
- Hospital, social census, and business SQL databases
- Visual database schema explorer
- Progressive hints and alternative solutions
- Saved progress and attempt tracking

## Exact repository structure

Keep these two files at the root of the GitHub repository:

```text
code-practice-arena/
├── index.html
└── README.md
```

The complete application, styles, databases, questions, grading logic, and configuration are contained in `index.html`. Do not separate or rewrite it if you want the deployed version to match exactly.

## Run locally

1. Download or clone the repository.
2. Open `index.html` in a current version of Chrome, Edge, Firefox, or Safari.
3. Keep an internet connection active so the browser can load the code editor and language runtimes.

No installation, build command, Node.js server, or package manager is required.

## External browser libraries

The exact versions are loaded from jsDelivr inside `index.html`:

```html
Pyodide 0.27.7
sql.js 1.13.0
CodeMirror 5.65.16
```

CodeMirror includes:

- Python mode
- SQL mode
- Material Darker theme
- Automatic bracket and quotation-mark closing
- Matching-bracket highlighting

These CDN files are necessary for the complete experience. If they cannot load, the page provides a basic textarea fallback, but syntax colors and some smart-editor behavior will be unavailable.

## Smart editor configuration

The CodeMirror editor is initialized with the following important settings:

```javascript
{
  mode: "python",             // changes to text/x-sql on SQL pages
  theme: "material-darker",
  lineNumbers: true,
  indentUnit: 4,
  tabSize: 4,
  indentWithTabs: false,
  smartIndent: true,
  electricChars: true,
  autoCloseBrackets: true,
  matchBrackets: true,
  lineWrapping: false
}
```

Keyboard behavior:

- `Enter` preserves or increases indentation.
- `Tab` inserts four spaces or indents selected lines.
- `Shift + Tab` removes one indentation level.
- `Ctrl + Enter` runs and verifies code.
- `Cmd + Enter` does the same on macOS.
- Parentheses, brackets, braces, single quotes, and double quotes close automatically.

## Exact syntax colors

The site uses the Material Darker CodeMirror theme with these custom overrides:

| Token | Color | Hex |
|---|---|---|
| Python/SQL keywords | Purple | `#c792ea` |
| Functions, definitions, built-ins | Teal | `#4fd6be` |
| Strings | Green | `#c3e88d` |
| Numbers | Coral | `#f78c6c` |
| Comments | Muted blue-gray | `#60758c` |
| Operators | Light cyan | `#89ddff` |
| Normal editor text | Pale blue-white | `#dce8f7` |
| Editor background | Near-black navy | `#050b14` |
| Gutter background | Dark navy | `#07111e` |
| Line numbers | Blue-gray | `#52677f` |

The relevant selectors are included directly in `index.html`:

```css
.cm-s-material-darker .cm-keyword { color:#c792ea; }
.cm-s-material-darker .cm-def,
.cm-s-material-darker .cm-variable-2,
.cm-s-material-darker .cm-builtin { color:#4fd6be; }
.cm-s-material-darker .cm-string { color:#c3e88d; }
.cm-s-material-darker .cm-number { color:#f78c6c; }
.cm-s-material-darker .cm-comment { color:#60758c; font-style:italic; }
.cm-s-material-darker .cm-operator { color:#89ddff; }
```

To preserve the exact colored function text, keep the CodeMirror CDN links, theme name, modes, and CSS rules unchanged.

## Python and machine-learning execution

Python code runs entirely in the browser through Pyodide. The machine-learning page practices algorithm calculations using browser-executed Python, including:

- Regression predictions
- Classification accuracy
- Precision and recall
- Sigmoid probabilities
- K-nearest neighbors
- Train/test splitting
- Standardization
- K-means assignment
- Ensemble voting
- Drift detection

The verifier checks the produced result instead of requiring one exact code structure. Learners can use different variable names, loops, comprehensions, or functions when their output is correct.

## SQL execution and databases

SQL runs locally through SQLite using sql.js. The application creates and seeds all tables in browser memory.

### Hospital operations

```text
patients
  patient_id, age_group, city, insurance_type

departments
  department_id, department_name, floor

visits
  visit_id, patient_id, department_id,
  visit_date, wait_minutes, charge_amount
```

Relationships:

```text
patients.patient_id → visits.patient_id
departments.department_id → visits.department_id
```

### Social census

```text
communities
  community_id, neighborhood, region,
  population, median_income

census_stats
  stat_id, community_id, year,
  unemployment_rate, college_rate

services
  service_id, community_id,
  service_type, annual_visits
```

Relationships:

```text
communities.community_id → census_stats.community_id
communities.community_id → services.community_id
```

### Business sales

```text
customers
  customer_id, customer_name, region, segment

products
  product_id, product_name, category, unit_cost

sales
  sale_id, customer_id, product_id,
  sale_date, quantity, unit_price
```

Relationships:

```text
customers.customer_id → sales.customer_id
products.product_id → sales.product_id
```

All datasets are synthetic and intended only for learning.

## Questions and verification

Questions are generated in `index.html` by these functions:

```javascript
pythonQuestion(i)
mlQuestion(i)
sqlQuestion(i)
```

Each function generates exactly 50 exercises. Difficulty is assigned as follows:

```text
Questions 1–17: Easy
Questions 18–34: Medium
Questions 35–50: Hard
```

Python and machine-learning answers are verified using expected output tokens. SQL answers are verified by executing both the learner query and the hidden reference query, then comparing their result rows. SQL formatting, capitalization, aliases, and query structure can differ when the final rows match.

## Progressive hint system

Every problem immediately displays a function guide explaining:

- Function signature
- What the function does
- A short usage example

After three incorrect runs, the code-hint button unlocks.

The first hint reveals approximately 45% of the reference solution and blurs the remainder. A second button labeled **Show full code and alternatives** reveals:

- The complete reference answer
- An alternative valid implementation
- A short explanation comparing the approaches

The verifier does not require the learner to reproduce either example exactly.

## Saved progress

Progress is stored in the browser under this local-storage key:

```text
code-practice-arena-v1
```

It stores solved-question IDs and wrong-attempt counts. Browser storage is specific to the browser and computer being used; it does not automatically synchronize through GitHub.

## Publish with GitHub Pages

1. Create a GitHub repository.
2. Upload `index.html` and `README.md` to the repository root.
3. Commit the files.
4. Open **Settings → Pages**.
5. Under **Build and deployment**, choose **Deploy from a branch**.
6. Choose the `main` branch and `/ (root)` folder.
7. Save and wait for GitHub Pages to publish.

The resulting address normally follows this format:

```text
https://YOUR-USERNAME.github.io/YOUR-REPOSITORY-NAME/
```

## Recreating the site exactly

The most reliable method is to preserve the supplied `index.html`, since it is the canonical complete source. To reproduce it manually:

1. Create a single `index.html` file.
2. Copy the CDN tags and exact versions listed above.
3. Copy the complete CSS, including the CodeMirror color overrides.
4. Recreate the three navigation tabs and shared coding workspace.
5. Add the 150-question generators.
6. Add Pyodide and sql.js initialization.
7. Seed the three SQLite datasets.
8. Add output-based Python verification and result-based SQL verification.
9. Add local-storage progress tracking.
10. Add the three-attempt progressive hint system.

Changing the CodeMirror version, theme, mode files, or custom token selectors can alter the highlighting colors and behavior.
