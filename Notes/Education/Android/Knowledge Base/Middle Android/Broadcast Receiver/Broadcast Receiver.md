Broadcast Receiver - широковещательный приемник, предназначен для передачи событий на общую область и каждый по своему может на это событие отреагировать. 
То есть например на телефон кто то звонит, система Android посылает событие в Broadcast Receiver о том, что на телефон звонят и уже все остальные могут на это отреагировать. 

Зарегистрировать Broadcast Receiver можно как через Android Manifest:
```xml
<receiver
	android:name=".MyBroadcastReceiver"
	android:exported=false>

	<intent-filter>
		<action android:name="action_name" />
	</intent-filter>


</receiver>
```

Так и через код:
```Kotlin
val filter = IntentFilter("action_name")
context.registerReceiver(receiver, filter, ContextCompact.RECEIVER_NOT_EXPORTED)
```

Пример: 
```Kotlin
class BroadcastReceiver: BroadcastReceiver() {  
    override fun onReceive(context: Context?, intent: Intent?) {  
        when (intent?.action) {  
            "action_name" -> {  
                //TODO something  
            }  
              
            else -> {  
                //TODO handle else   
}  
        }  
    }  
}
```

