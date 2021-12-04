# Day 04

https://adventofcode.com/2021/day/4

## Example

```
7,4,9,5,11,17,23,2,0,14,21,24,10,16,13,6,15,25,12,22,18,20,8,19,3,26,1

22 13 17 11  0
 8  2 23  4 24
21  9 14 16  7
 6 10  3 18  5
 1 12 20 15 19

 3 15  0  2 22
 9 18 13 17  5
19  8  7 25 23
20 11 10 24  4
14 21 16 12  6

14 21 17 24  4
10 16 15  9 19
18  8 23 26 20
22 11 13  6  5
 2  0 12  3  7
```

## Solutions

# Part 1

### Java 17 by Nuno Azevedo

```java
calculateBoardScores(bingo, (a, b) -> a);

Optional<Integer> calculateBoardScores(final Bingo bingo, final BinaryOperator<Integer> reducer) {
    final Set<Board> winners = new HashSet<>();

    return IntStream.range(0, bingo.drawnNumbersOrder().size()).boxed()
            .map(bingo::getDrawnNumbers)
            .flatMap(drawnNumbers -> bingo.boards().stream()
                    .filter(board -> board.isWinningBoard(drawnNumbers))
                    .filter(winners::add)
                    .map(board -> board.calculateBoardScore(drawnNumbers))
            )
            .reduce(reducer);
}

record Bingo(List<Integer> drawnNumbersOrder, List<Board> boards) {
    private List<Integer> getDrawnNumbers(final int round) {
        return this.drawnNumbersOrder.subList(0, round);
    }
}

record Board(List<List<Integer>> board) {
    private List<Integer> getRow(final int row) {
        return this.board.get(row);
    }

    private List<Integer> getColumn(final int column) {
        return this.board.stream().mapToInt(row -> row.get(column)).boxed().toList();
    }

    private boolean isWinningBoard(final List<Integer> drawnNumbers) {
        for (int i = 0; i < this.board.size(); i++) {
            if (drawnNumbers.containsAll(getRow(i)) || drawnNumbers.containsAll(getColumn(i))) {
                return true;
            }
        }
        return false;
    }

    private int calculateBoardScore(final List<Integer> drawnNumbers) {
        final int unmarkedNumbersSum = this.board.stream()
                .flatMap(Collection::stream)
                .filter(number -> !drawnNumbers.contains(number))
                .reduce(0, Integer::sum);

        return unmarkedNumbersSum * Objects.requireNonNull(Iterables.getLast(drawnNumbers));
    }
}
```

# Part 2

### Java 17 by Nuno Azevedo

```java
calculateBoardScores(bingo, (a, b) -> b);
```
