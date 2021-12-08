# Day 6

https://adventofcode.com/2021/day/6

## Example

```
3, 4, 3, 1, 2
```

## Solutions

### Python by Pedro Lourenço

```python
counters = [0 for i in range(9)]
days = 80

for v in fish:
  counters[min(8, v)] += 1

while days > 0:
  days -= 1
  new_fish = counters[0]
  for i in range(0, 8):
    counters[i] = counters[i + 1]
  counters[8] = new_fish
  counters[6] += new_fish

result = sum(counters)
```

### Python by Pedro Lourenço (simplified)

```python
counters = [0 for i in range(9)]
days = 256

for v in fish:
  counters[min(8, v)] += 1

while days > 0:
  days -= 1
  new_fish = counters.pop(0)
  counters.append(new_fish)
  counters[6] += new_fish
```

