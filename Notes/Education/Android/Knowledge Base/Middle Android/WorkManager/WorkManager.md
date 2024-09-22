WorkManager - по заявления Google, один из лучших способов для Android приложений работы в фоне, так как WorkManager может выполнятся неоднократно, у него есть своя база данных, тем самым даже после перезагрузки телефона мы сможем продолжить работу на том месте, на котором остановились 

Пример простого worker'а: 
```Kotlin
class WorkManager(  
    context: Context,  
    params: WorkerParameters  
) : CoroutineWorker(  
    appContext = context,  
    params = params  
) {  
      
    override suspend fun doWork(): Result {  
        TODO("Not yet implemented")  
    }  
      
}
```

