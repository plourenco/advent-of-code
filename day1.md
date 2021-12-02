# Day 1 (Part 1)

https://adventofcode.com/2021/day/1

## Example

```
199 (N/A - no previous measurement)
200 (increased)
208 (increased)
210 (increased)
200 (decreased)
207 (increased)
240 (increased)
269 (increased)
260 (decreased)
263 (increased)
```

## Solutions

### Python by Pedro Lourenço

```python
sum(x > list[i - 1] for i, x in enumerate(list))
```

# Day 1 (Part 2)

## Example

```
A: 607 (N/A - no previous sum)
B: 618 (increased)
C: 618 (no change)
D: 617 (decreased)
E: 647 (increased)
F: 716 (increased)
G: 769 (increased)
H: 792 (increased)
```

## Solutions

### Python by Pedro Lourenço

```python
sum(sum(list[i-3:i]) > sum(list[i-4:i-1]) for i in range(3, len(list)))
```

