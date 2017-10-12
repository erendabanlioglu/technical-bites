- *.scala compiles to *.class
- val (const) vs var

## Lazy Val

```scala 
lazy val
lazy val a = 10 +  b
lazy val b = 16
println(a);
```

## Variable names

```scala 
val `some variable`
println(`some variable`)
val `something`
println(something)
```


## Functional loop

```scala 
var result = (1 to 100 ).reverse.mkString(",")
var result = (100 to 1 by -1).mkString(",")
```

## Smart string

```scala 
val str = """some text
                   |to tototot
                   |wow"""".stripMargin
val str = """some text
                    @to tototot
                    @wow"""".stripMargin('@')
```

## String Format

```scala
val str = "This is a %s, %s and %s".format("test", "boring", "fun")
```

change the order

```scala
val str = "This is a %3$s, %2$s and %1$s".format("test", "boring", "fun")
```

## String Interpolation

```scala 
val a = 99
println(s"$a luftballons floating in the summer sky")
println(s"${a + 3} luftballons floating in the summer sky")
```

s - bring values

```scala 
val ticketCost = 50
val bandName = "Metallica"
println(f"The $bandname%s tickets are probably $$$ticketCost%1.2f")
```

f- bring values and allow to format

```scala 
val percentIncrease = 20
val musicGenre = "Rock"
println(f"""The $bandname%s tickets are probably $$$ticketCost%1.2f
            |That's a $percentIncrease%% bump because everyone likes $musicGenre""".stripMargin)
```


