Делегаты делегируют как бы getter и setter для переменной, с помощью этих "кастомных" гетеров и сеттеров мы можем в сетере сохранять значение в shared prefs а в гетере получать это значение, делегат создается с помощью ключевого слова by, а создаваемый делегат(класс) должен имплементировать interface ReadWriteProperty<T, V>, пример: 
```Kotlin
class DelegateExample : ReadWriteProperty<Any?, String> {  
    private var trimmedValue: String = ""  
  
    override fun getValue(thisRef: Any?, property: KProperty<*>): String = trimmedValue  
  
    override fun setValue(thisRef: Any?, property: KProperty<*>, value: String){ 
        trimmedValue = value.trim()  
    }  
}
```

```Kotlin
//Main activity 
private var delegate by DelegateExample() 

private fun method() {
	delegate = "some new data"
	val newData = delegate // return "some new data"
}

```