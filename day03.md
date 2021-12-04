# Day 03

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

### Java 17 by Nuno Azevedo

```java
int calculatePowerConsumption(final char[][] binaries) {
    final var gammaRate = new StringBuilder();
    final var epsilonRate = new StringBuilder();

    for (int position = 0; position < binaries[0].length; position++) {
        final char mostCommonBit = findMostCommonBit(binaries, position);
        gammaRate.append(mostCommonBit);
        epsilonRate.append(mostCommonBit ^ ONE); // Flip the bit using XOR.
    }

    return Integer.parseInt(gammaRate.toString(), 2) * Integer.parseInt(epsilonRate.toString(), 2);
}

char findMostCommonBit(final char[][] binaries, final int position) {
    int bit0 = 0;
    int bit1 = 0;

    for (final char[] binary : binaries) {
        switch (binary[position]) {
            case ZERO -> bit0++;
            case ONE -> bit1++;
        }
    }

    return bit0 > bit1 ? ZERO : ONE;
}
```

### Javascript by Pedro Lourenço

```javascript
gamma = data
  .reduce((acc, x) => x.map((y, i) => acc[i] + (y || -1)), Array(data[0].length).fill(0))
  .map(x => 1 - x >>> -1)
  .join('');

parseInt(gamma, 2) * (parseInt(gamma, 2)^(Math.pow(2, gamma.length) - 1)));
```

# Part 2

### Java 17 by Nuno Azevedo

```java
int calculateLifeSupportRating(final char[][] binaries) {
    char[][] oxygenRatings = binaries;
    char[][] co2Ratings = binaries;

    for (int position = 0; position < binaries[0].length; position++) {
        final int pos = position;

        if (oxygenRatings.length > 1) {
            final char mostCommonBit = findMostCommonBit(oxygenRatings, position);
            oxygenRatings = Arrays.stream(oxygenRatings)
                    .filter(binary -> binary[pos] == mostCommonBit)
                    .toArray(char[][]::new);
        }

        if (co2Ratings.length > 1) {
            final char leastCommonBit = Character.forDigit(findMostCommonBit(co2Ratings, position) ^ ONE, 2);
            co2Ratings = Arrays.stream(co2Ratings)
                    .filter(binary -> binary[pos] == leastCommonBit)
                    .toArray(char[][]::new);
        }
    }

    return Integer.parseInt(new String(oxygenRatings[0]), 2) * Integer.parseInt(new String(co2Ratings[0]), 2);
}
```
