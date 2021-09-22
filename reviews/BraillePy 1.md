---
Project: "BraillePy"
Repository: "https://github.com/UltraStudioLTD/BraillePy"
Repository snapshot: "https://github.com/UltraStudioLTD/BraillePy/tree/b5a5fd900922511803bf13d421b2ac7636915cfe"
Review no: "1"
Review date: "2021-09-22"
Issue: https://github.com/willmcgugan/codereviews/issues/2
---

# BraillyPy

The project could use more detail in the README. Consider a summary of what the package does, plus a few examples of usage.

Also in the README you might want to add what versions of Python are supported.

I'm assuming this library is for translating characters between visual and brail representation.

## Formatting

The main code in braille.py uses TABS. The standard for Python is 4 spaces per-indent level. Most Python editors will do this for you automatically.

I'd also recommend adopting Black as an auto-formatter. If you run `black braille.py` it may be able to replace your tabbed indents with spaces.

## Code

Some observations of the code:

### Observation 1.

The main Braille class is defined like this:

```python
class Braille(object):
```

The `object` part is optional in Python3 and generally discouraged

### Observation 2.

The constructor accepts a lot of different parameters. It may be better to have a number of alternative constructors (classmethods) for each of the different types. For instance Braille.from_matrix, Braille.from_codepoint etc.

### Observation 3.

Overriding `__pow__` is an odd one. I would expect that on a more mathematical entities, but I'm not sure that raising a braille object to a power makes sense. That functionality may be better exposed as a method. Similarly, `__add__` and `__sub__` -- do you really need those? Does it really make sense to "add" codepoints etc together?

### Observation 4.

Try to avoid single letter variable names, for instance `x` and `i`

### Observation 5.

Some of the (private) functions are in ALL_CAPS. App caps names should be reserved for constants, so you could lower case these.

## API Design

I'm wondering if you _need_ the braille class? I'm guessing that users will only require the methods which convert from one thing to another.

The naming could be improved for those methods. Abbreviations may be easier to type, but are generally harder to remember. I'd suggest `braille_to_string` over `b2s`, etc.
