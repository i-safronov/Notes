Kotlin позволяет создавать объект прямо в функции, и проделывать с ними все операции которые доступны объектам, пример: 
```Kotlin
val myObject = object { 
	val name = "MyObject" 
	fun printName() { 
	println(name) 
	} 
} 
myObject.printName() // Выведет: MyObject
```

Так же с помощью него можно имплементировать interface: 
```Kotlin
addClickable(object: Clickable {
	override fun onClick() {
		doSomething()
	}
})
```

Так же он позволяет наследование классов: 
```Kotlin 
val myObj = object: Car(name = "Super car") {
	override fun go() {
		println("Let's gooo!")
	}
}
```