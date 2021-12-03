# Day 3

https://adventofcode.com/2021/day/3

## Example

```
00100
11110
10110
10111
10101
01111
00111
11100
10000
11001
00010
01010
```

## Solutions

# Part 1

### Python by Tomas Roun

```python
import numpy as np
d = np.array([[int(x) for x in list(line.strip())] for line in data])
d = np.round(np.sum(d, axis=0)/len(d)).astype(int)
_ = lambda x: int("".join(map(str, x)), 2)
_(d) * _(1-d)
```
