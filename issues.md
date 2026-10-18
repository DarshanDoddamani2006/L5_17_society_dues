# Static Code Analysis Issues

## Issues Found in the Original Code

| **Issue** | **Type** | **Line(s)** | **Description** | **Fix Approach** |
| --------- | -------- | ----------- | --------------- | ---------------- |
| SQL injection vulnerability | Security | 9 | The SQL INSERT statement was constructed using an f-string, allowing input values to be directly inserted into the SQL query. This could allow malicious input to alter the SQL statement. | Replaced the f-string with a parameterized SQL query using `?` placeholders. |
| Use of `eval()` | Security | 21 | `eval()` executes a string as Python code and can potentially execute malicious code when the input is untrusted. | Removed `eval()` and changed the penalty function to accept numeric rate and month values directly. |
| Hard-coded password | Security | 5 | The treasurer password was directly stored in the source code, exposing the password to anyone who can access the source. | Changed the code to read the password from an environment variable. |
| Mutable default argument | Code Quality / Bug | 8 | `history=[]` is created once and reused between function calls, which can cause previous data to persist unexpectedly. | Changed the default value to `None` and created a new list inside the function. |
| Broad exception handling | Code Quality | 22 | `except Exception` catches almost every exception and can hide unexpected programming errors. | Replaced the broad exception with specific expected exception types. |
| Inconsistent return statements | Code Quality | 12–16 | The `collect()` function returned the amount when a matching record existed but did not explicitly return a value when no record existed. | Added an explicit `return None` when no matching record is found. |
| Missing function docstrings | Code Quality | 8, 12, 19, 27, 34 | Functions did not contain documentation explaining their purpose and behavior. | Added descriptive docstrings to the functions. |
| Invalid function naming style | Style | 8 | `addDue` did not follow Python's recommended `snake_case` naming convention. | Renamed the function to `add_due`. |
| Incorrect None comparison | Style | 29 | The code used `rows != None` instead of Python's recommended identity comparison. | Changed the comparison to `rows is not None`. |
| Long lines | Style | 4, 9, 13, 15 | Several lines exceeded the recommended maximum line length. | Split long statements across multiple lines. |
| Missing final newline | Style | 42 | The original Python file did not end with a newline character. | Added a newline at the end of the file. |
| Missing module docstring | Code Quality | 1 | The module did not contain a description explaining its purpose. | Added a module-level docstring. |

## Analysis Results

### Original Code

The original code contained multiple issues identified by Pylint, Bandit, and Flake8. The most significant security issues were the SQL injection vulnerability, use of `eval()`, and hard-coded password.

### Fixed Code

After applying the fixes, the program was tested again and continued to produce the expected output:

```text
2500
100
['A-102']