# Day 01

https://adventofcode.com/2021/day/1

## Examples

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

## Solutions in Part 1

### Python by Pedro Lourenço

```python
sum(x > list[i - 1] for i, x in enumerate(list))
```

### Java 17 by Nuno Azevedo

```java
int countNumberOfDepthIncreases(final List<Integer> measurements) {
    int increases = 0;
    int last = 0;

    for (final int measurement : measurements) {
        if (measurement > last) {
            increases++;
        }
        last = measurement;
    }

    return Math.max(increases - 1, 0); // Skip first measurement.
}
```

## Solutions in Part 2

### Python by Pedro Lourenço

```python
sum(sum(list[i-3:i]) > sum(list[i-4:i-1]) for i in range(3, len(list)))
```

### Java 17 by Nuno Azevedo

```java
int countNumberOfDepthIncreasesSlidingWindow(final List<Integer> measurements) {
    int increases = 0;
    int windowA = 0;
    int windowB = 0;
    int windowC = 0;

    for (final int measurement : measurements) {
        if (windowB + windowC + measurement > windowA + windowB + windowC) {
            increases++;
        }
        windowA = windowB;
        windowB = windowC;
        windowC = measurement;
    }

    return Math.max(increases - 3, 0); // Skip first window of measurements.
}
```
