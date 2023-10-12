### Makefile Interpreter

```make
<target> [<target[s]>...]: [<prerequisite[s]>...]
    [<recipe[s]>...]
#[comments...]
<target> [<target[s]>...]: [<prerequisite[s]>...]
    [<recipe[s]>...]
...
```

License: LGPL for implementation code + WTFPL for test examles in miniLanguage

Author: Ivan Morozko

Supported functionality:
- Explicit rules parsing
    - Support multiline prerequisite definitions
    - Support multiline recipes
    - Support recipe definiton via `;` on the targets line
    - Support recipe echoing aka prefixing recipe with `@`
    - Ignore comment lines
- Explicit rules interpreting
    - Dropping circular dependencies
    - Timestamp and file presence checking
    - Result verdicts, like
        - `No rule to make target 'x', needed by 'y'`
        - `Nothing to be done for 'x'`
        - `No rule to make target 'x'`
- Variables
    - Recursively expanded variable (`=`)
    - Simply expanded variables (`:=`)
    - Conditional variable assignment (`?=`)
    - Variables substitution (`$(var)`)
- Implicit rules
    - Pattern rule definition (when the target contains `%`)
    - Automatic variable `$*`
    - Automatic variable `$@`
    - Automatic variable `$<`

TODO:
- Variables
    - Multi-line variables (`define`)
    - `$$`
    - `$(MAKE)` variable
- Add special variables
    - `.DEFAULT_GOAL`
    - `.PHONY`
- Add functions
    - `call`
        - Support recursive invocation
        - Add arguments support (`$(num)`)
    - `eval`
    - `wildcard`
    - `shell`
    - `foreach`
- Add conditionals


## Running tests

- `cd demos`
- run `dune exec demoInterpret -- <folder_name> [targets]`, where `<folder_name>` is one of the folders there
