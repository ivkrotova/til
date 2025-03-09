# Different Ways to Import Modules in Python

In Python, there are several methods to import modules, each serving different purposes:

1. `import`: Key-word, the standard and most common way to import modules.

2. `__import__()`: A low-level function that was historically used but is now primarily for internal use and backward compatibility.

3. `importlib`: Introduced in Python 3.1, this module provides a more flexible and Pythonic approach to importing modules, especially useful for dynamic imports.

## Evolution of the Import System

In Python 2, the `import` statement directly invoked the `__import__()` function to load modules. However, starting from Python 3.1, the `importlib` module was introduced to provide a Python-based implementation of the import mechanism, enhancing introspection and customization capabilities.

## Examples

```python
# Regular import (preferred method)
import math
print(math.sqrt(16))  # Output: 4.0

# Direct use of __import__() (not recommended)
mod = __import__('math')
print(mod.sqrt(16))  # Output: 4.0

# Using importlib for dynamic imports
import importlib
math_mod = importlib.import_module('math')
print(math_mod.sqrt(16))  # Output: 4.0
```

## Modern Import System in Python 3

The import system in Python 3 involves several steps:

1. **Check `sys.modules`**: Python first checks if the module is already loaded to avoid redundant imports.

2. **Find the Module**: Python uses an importer to locate the module, searching directories listed in `sys.path` or using custom import hooks.

3. **Load the Module**: A loader loads the module from various sources, such as a `.py` file, a compiled `.pyc` file, or a shared library.

4. **Create a Module Object**: The module object is created and added to `sys.modules`.

5. **Execute Module Code**: The module's top-level code is executed to initialize the module.

The `importlib` module exposes this machinery, allowing for dynamic imports and greater control over the import process.

## Key Functions in `importlib`

- **`importlib.import_module(name)`**: A higher-level function that imports a module by name, providing a simpler API than `__import__()`.

- **`importlib.util.find_spec(name)`**: Locates a module's specification without importing it, useful for introspection.

- **`importlib.util.module_from_spec(spec)`**: Creates a new module based on a specification, allowing for manual control over module creation.

## Summary

- **`import` Statement**: The standard method for importing modules; it internally uses the import system managed by `importlib`.

- **`__import__()` Function**: Still exists but is primarily for internal use and backward compatibility; direct use is uncommon in modern Python code.

- **`importlib` Module**: Provides a flexible and Pythonic approach to importing modules, especially useful for dynamic imports and advanced import customization.