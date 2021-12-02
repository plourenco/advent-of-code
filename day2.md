# Day 2

https://adventofcode.com/2021/day/2

## Example

```
forward 5
down 5
forward 8
up 3
down 8
forward 2
```

## Solutions

# Part 1

### Python by Tomas Roun

```python
z = sum(v*(1 if c[0] == 'd' else -1) if c[0] != 'f' else complex(0, v) for c, v in data); int(z.real*z.imag)
```

### JS by Tomas Roun

```javascript
data.reduce(([x, y], [c, v]) => c[0] == "f" ? [x + v, y] : [x, y + v * (c[0] == "d" ? 1 : -1)], [0, 0]).reduce((p, c) => p*c, 1)
```
