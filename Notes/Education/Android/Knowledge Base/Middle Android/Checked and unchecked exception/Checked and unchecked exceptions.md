![[Pasted image 20240903062836.png]]

При создании любого класса который наследует Exception компилятор Java будет говорить нам, что бы либо обернули код в try catch который использует этот класс либо пометили метод как throws(то есть это checked exception), что бы создать unchecked exception нужно класс унаследовать от RuntimeException 