---
jupytext:
  text_representation:
    extension: .md
    format_name: myst
kernelspec:
  display_name: python
  language: python
  name: python3
---

(probability)=

# 5 Ejercicios de evaluación

```{code-cell} ipython3
note = "Python syntax highlighting"
print(note)
```

```{code-cell} ipython3
import numpy as np
import nbconvert as nbc
from ipywidgets import interact
import nbinteract as nbi

nbi.multiple_choice(question="What is 10 + 2 * 5?",
                    choices=['12', '60', '20'],
                    answers=2)

nbi.multiple_choice(question="Select all prime numbers.",
                    choices=['12', '3', '31'],
                    answers=[1, 2])

nbi.short_answer('What is 1+1?', answers='2', explanation='1+1 is 2')

nbi.short_answer('Enter the first name of a member of the Beatles.',
                 ['John', 'Paul', 'George', 'Ringo'])
```