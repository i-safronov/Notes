Value class - обертка над его полем, то есть у данного класса может быть только одно поле и оно обязательно, в месте создания/использования данного класса, компилятор заменит имя класса на его поле, пример: 
```Kotlin
@JvmInline  
value class ValueClass(val input: String)

fun useIt() {
	val valueClass = ValueClass(input = "use it") // for compilator it's just "use it"
}
```

