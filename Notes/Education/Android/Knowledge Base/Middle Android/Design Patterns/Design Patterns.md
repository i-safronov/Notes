Основные паттерны проектирования: 
- Observable 
- Builder 
- Singelton 

## Singelton(являеться антипаттерном)
Относиться к классу порождающих, его особенность в том, что в контексте приложения он будет единым и его тело тоже будет едино на весь проект 

Пример singelton: 
```Java
public class Example {  
    private Example() {  }  
  
    private static Example instance = null;  
  
    public static Example instance() {  
        if (instance == null) {  
            instance = new Example();  
        }  
  
        return instance;  
    }  
}
```

## Builder - строитель 
```Kotlin
data class Settings(  
    val version: Int,  
    val sensitivity: Double,  
    val resolution: Double  
)  
  
class SettingsBuilder {  
  
    var version: Int = 1  
    var sensitivity: Double = 1.9  
    var resolution: Double = 4.3  
  
    fun setVersion(version: Int): SettingsBuilder {  
        this.version = version  
        return this  
    }  
  
    fun setSensitivity(sensitivity: Double): SettingsBuilder {  
        this.sensitivity = sensitivity  
        return this  
    }  
  
    fun setResolution(resolution: Double): SettingsBuilder {  
        this.resolution = resolution  
        return this  
    }  
  
    fun build() = Settings(  
        version = version,  
        sensitivity = sensitivity,  
        resolution = resolution  
    )  
}  
  
fun main() {  
    val settings: Settings = SettingsBuilder()  
        .setResolution(1.2)  
        .setVersion(2)  
        .setSensitivity(2.1)  
        .build()  
}
```

## Observable - наблюдатель 

```Kotlin
class UserObservable {  
  
    private var currentUsers = 0  
    private var observers = mutableListOf<Observer<Int>>()  
  
    init {  
        process()  
    }  
  
    fun add(observer: Observer<Int>) {  
        observers.add(observer)  
    }  
  
    private fun process() {  
        val time = Timer()  
        time.schedule(  
            object: TimerTask() {  
                override fun run() {  
                    currentUsers += Random.nextInt(20)  
                    observers.forEach {  
                        it.onChanged(currentUsers)  
                    }  
                }  
            }, 200, 1000)  
    }  
}
```

