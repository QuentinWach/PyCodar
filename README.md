![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)
![Last Commit](https://img.shields.io/github/last-commit/QuentinWach/pycodar)
![PyPI](https://img.shields.io/pypi/v/pycodar)
[![PyPI Downloads](https://static.pepy.tech/badge/pycodar)](https://pepy.tech/projects/pycodar)

# PyCodar: A Radar for Your Code
**A simple tool for auditing and understanding your (python) codebase.**

```bash
pip install pycodar
```

+ `pycodar stats`: Summarizes the most basic stats of your directory in a single table. 📊
+ `pycodar strct`: Displays the file structure of all the files, their functions, classes, and methods in a nicely colored tree. 🗂️
+ `pycodar files`: Shows a table of all the files with counts of the lines of code, comments, empty lines, total lines, and file size. 📋
+ `pycodar calls`: Counts how often elements (modules, functions, methods) of your code are called within the code. 📞
+ `pycodar dead`: Finds (likely) unused code. ☠️


### General Overview
Type
```bash
pycodar stats
```
in your terminal to get the most basic statistics of your directory printed out:
```bash
📊 Basic Metrics
╭─────────────────────┬───────────╮
│  Total Size         │  54.21KB  │
│  Total Files        │  6        │
│  Total Directories  │  2        │
│  Total Lines        │  1,394    │
│  Code Lines         │  885      │
│  Comment Lines      │  26       │
│  Empty Lines        │  208      │
│  Functions          │  38       │
│  Classes            │  2        │
╰─────────────────────┴───────────╯
```

### Structure
```bash
pycodar strct
```
gives you something like:
```bash
🌳 File Structure
📁 Root
├── 📄 README.md
├── 📄 pyproject.toml
├── 📄 setup.py
└── 📁 pycodar
    ├── 📄 __init__.py
    ├── 📄 analyze.py
    │   ├── 🔷 CodeElementVisitor
    │   │   ├── 🔹 __init__
    │   │   ├── 🔹 visit_FunctionDef
    │   │   ├── 🔹 visit_ClassDef
    │   │   ├── 🔹 visit_Import
    │   │   ├── 🔹 visit_ImportFrom
    │   │   ├── 🔹 visit_Call
    │   │   ├── 🔹 visit_Assign
    │   │   ├── 🔹 visit_Name
    │   │   ├── 🔹 visit_Attribute
    │   │   ├── 🔹 visit_Return
    │   │   └── 🔹 visit_Decorator
    │   ├── 🔸 count_functions_and_classes
    │   ├── 🔸 get_file_size_kb
    │   ├── 🔸 count_lines
    │   ├── 🔸 analyze_code_connections
    │   ├── 🔸 analyze_directory
    │   └── 🔸 generate_report
    └── 📄 cli.py
        ├── 🔷 TestClass
        │   ├── 🔹 __init__
        │   └── 🔹 test_method
        ├── 🔸 extract_code_structure
        ├── 🔸 create_structure_tree
        ├── 🔸 parse_ignore_file
        ├── 🔸 should_ignore
        ├── 🔸 get_ignore_patterns
        ├── 🔸 format_size
        ├── 🔸 count_code_metrics
        ├── 🔸 create_metrics_table
        ├── 🔸 create_code_connections_table
        ├── 🔸 create_dead_code_table
        ├── 🔸 create_code_connections_tree
        ├── 🔸 create_file_table
        ├── 🔸 print_stats
        ├── 🔸 print_structure
        ├── 🔸 print_files
        ├── 🔸 print_calls
        ├── 🔸 print_dead_code
        ├── 🔸 process_directory
        └── 🔸 main
```

### File Statistics
Typing
```bash
pycodar files
```
will give you an overview of the lines of code, comments, empty lines, total lines and file sizes:
```bash
📁 File Distribution
╭───────────┬──────────────────┬────────┬────────────┬─────────┬─────────┬───────────╮
│  Path     │  File            │  Code  │  Comments  │  Empty  │  Total  │     Size  │
├───────────┼──────────────────┼────────┼────────────┼─────────┼─────────┼───────────┤
│  Root     │  pyproject.toml  │     0  │         0  │      0  │     43  │   1.37KB  │
│  Root     │  README.md       │     0  │         0  │      0  │     95  │   3.37KB  │
│  Root     │  setup.py        │    45  │         0  │      1  │     46  │   1.72KB  │
│  pycodar  │  __init__.py     │     7  │         1  │      3  │     11  │   0.22KB  │
│  pycodar  │  cli.py          │   384  │        18  │     90  │    492  │  18.62KB  │
│  pycodar  │  analyze.py      │   449  │         7  │    114  │    570  │  22.27KB  │
╰───────────┴──────────────────┴────────┴────────────┴─────────┴─────────┴───────────╯
```

### Calls
To check how much the modules, functions and methods in your code are actually being used, type:
```bash
pycondar calls
```
which will give you another table like:
```bash
📊 Most Called Elements
╭────────────┬─────────────────────────┬──────────╮
│  Type      │  Name                   │  Called  │
├────────────┼─────────────────────────┼──────────┤
│  Function  │  isinstance             │      28  │
│  Function  │  print                  │      22  │
│  Function  │  defaultdict            │      17  │
│  Function  │  set                    │      11  │
│  Function  │  sorted                 │      10  │
│  Function  │  len                    │      10  │
│  Function  │  str                    │       9  │
│  Function  │  open                   │       7  │
│  Function  │  Path                   │       4  │
│  Function  │  sum                    │       4  │
│  Method    │  console.print          │      22  │
│  Method    │  table.add_row          │      15  │
│  Method    │  table.add_column       │      14  │
│  Method    │  self.generic_visit     │       8  │
│  Method    │  ast.walk               │       5  │
│  Method    │  subparsers.add_parser  │       5  │
│  Method    │  ast.parse              │       4  │
│  Method    │  tree.add               │       4  │
│  Method    │  method.startswith      │       4  │
│  Method    │  file.read              │       3  │
╰────────────┴─────────────────────────┴──────────╯
```

### Dead Code
And finally, to see if there is any code that's not even used, type
```bash
💀 Potentially Unused Code
╭─────────┬─────────────────────────╮
│  Type   │  Name                   │
├─────────┼─────────────────────────┤
│  Class  │  pycodar.cli.TestClass  │
╰─────────┴─────────────────────────╯
```
which will point you at whatever code seems to be unused.

---

If you need any help / a quick reminder, type:
```bash
pycodar help
```
and if you just want to see everything all at once, type:
```bash
pycodar all
```

Thank you and enjoy! 😜