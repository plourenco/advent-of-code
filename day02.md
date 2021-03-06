# Day 02

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

## Solutions in Part 1

### Python by Tomas Roun

```python
z = sum(v*(1 if c[0] == 'd' else -1) if c[0] != 'f' else complex(0, v) for c, v in data); int(z.real*z.imag)
```

### JS by Tomas Roun

```javascript
data.reduce(([x, y], [c, v]) => c[0] == "f" ? [x + v, y] : [x, y + v * (c[0] == "d" ? 1 : -1)], [0, 0]).reduce((p, c) => p*c, 1)
```

### JS by Pedro Lourenço

```javascript
data.reduce(([h, de], [d, v]) => d[0] == 'f' ? [h + v, de] : [h, de + (d[0] == 'd' || -1) * v], [0, 0]).reduce((a, v) => a * v)
```

### F# by Pedro Lourenço

```f#
Seq.fold (fun [h; d] (x, y) -> 
  match x with 
  | "forward" -> [h + y; d] 
  | "up" -> [h; d - y] 
  | "down" -> [h; d + y] 
  | _ -> [h; d]) [0; 0] |> Seq.fold (*) 1;;
```

### Java 17 by Nuno Azevedo

```java
int processCommands(final List<Command> commands) {
    int horizontal = 0;
    int depth = 0;

    for (final Command command : commands) {
        switch (command.direction()) {
            case FORWARD -> horizontal += command.units();
            case UP -> depth -= command.units();
            case DOWN -> depth += command.units();
        }
    }

    return horizontal * depth;
}

record Command(Direction direction, int units) { }

enum Direction {
  FORWARD,
  UP,
  DOWN
}
```

## Solutions in Part 2

### JS by Pedro Lourenço

```javascript
data.reduce(([h, de, a], [d, v]) => d[0] == 'f' ? [h + v, de + a * v, a] : [h, de, a + (d[0] == 'd' || -1) * v], [0, 0, 0]).slice(0, 2).reduce((acc, v) => acc * v);
```

### Java 17 by Nuno Azevedo

```java
int processCommandsWithAim(final List<Command> commands) {
    int horizontal = 0;
    int depth = 0;
    int aim = 0;

    for (final Command command : commands) {
        switch (command.direction()) {
            case FORWARD -> {
                horizontal += command.units();
                depth += aim * command.units();
            }
            case UP -> aim -= command.units();
            case DOWN -> aim += command.units();
        }
    }

    return horizontal * depth;
}
```
