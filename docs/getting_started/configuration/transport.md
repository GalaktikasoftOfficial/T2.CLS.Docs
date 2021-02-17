---

id: getting_started_configuration_settings_transport
title: Транспорт
prev: false
next: false 

---

## Конфигурирование транспорта 

### appsetings.json

Пример конфигурации:

```
{
	"AllowedHosts": "*",
	"Transport": {
		"ValidateInputData": true
	},
	"Logging": {
		"LogLevel": {
			"Default": "Warning",
			"Microsoft": "Warning",
			"Microsoft.Hosting.Lifetime": "Warning"
		}
	},
	"BufferSettings": {
		"BufferPath": "LogBuffer",
		"WorkerCount": 1,
		"ReadLimit": 1024,
		"MemoryBufferLimit": 512,
		"FileBufferLimit": 0,
		"FlushTimeout": 3000,
		"ResendTimeout": 10000,
		"OutputPlugins": [ ...  ]
	}
}
```

Описание параметров: 

#### Секция **AllowedHosts**

Заголовки хостов, которым разрешен доступ к этому сервису.

Номера портов необходимо исключить.

Подстановочный знак верхнего уровня ```«*»``` разрешает все непустые хосты.

Подстановочные знаки субдоменов разрешены. Например. ```«* .example.com»``` соответствует субдоменам, таким как ```foo.example.com```, но не родительскому домену ```example.com.```

#### Секция **Transport**

Настройки обработки данных транспортом:

* ValidateInputData - проверять на целлостность входящих данных. Принимает значения: true/false.

#### Секция **BufferSettings**

Данная секция настраивает файловый буфер сервиса. 

* BufferPath - место хранения файлового буфера. Путь указывается относительно запускаемого приложения или полный путь.
* WorkerCount - указывается максимальное количество потоков, которые обрабатывают лог-записи. Предпочитаемые значения от 1 до 4 в зависимости от характеристики сервера.
* ReadLimit - 
* MemoryBufferLimit - 
* FileBufferLimit - 
* FlushTimeout -
* ResendTimeout - 
* OutputPlugins - массив настроек для выходных данных. В данном массиве отдельными объектами прописываются настройки для каждой логируемой системы. Сервис может работать в комбинированном режиме.



## Конфигурация для **Forward**

Сервис в режиме Forwarder занимается перенаправлением данных на сервисы транспорта в режиме Worker

Конфигурирование можно выполнять в нескольких файлах:

* appsetings.json - изменение стандартной конфигурации. Для этого добавляется секция OutputPlugins
* appsetings.{Environment}.json - переопределение стандартной конфигурации. В корне необходимо разместить секцию OutputPlugins
* appsetings.Forwarder.json - дополнение к стандартной конфигурации. Для применения конфигурации требуется запустить сервис с параметром ```--forwarder```

Пример конфигурации для работы сервиса в режиме Forward:

```
{
  "OutputPlugins": [
    {
      "Output": "Forward",
      "System": "CLS",
      "Servers": [
        "http://localhost:5100",
        "http://localhost:5101",
        "http://localhost:5102",
        "http://localhost:5103"
      ] 
    }
  ]
}
```

Описание параметров:
* Output - Тип плагина. Фиксированное значение "Forward"
* System - Наименование логируемой системы. 
* Servers - массив url-адресов для перенаправления пакетов. В списке могут быть сервисы в режиме и Worker Forward


## Конфигурация для **Worker**

Пример конфигурации для работы сервиса в режиме Worker:
```
{
	"OutputPlugins": [
		{
			"Output": "Clickhouse",
			"System": "CLS",
			"Host": "by01-vm42.topsoft.local",
			"Port": 8123,
			"Database": "T2P_Logs",
			"Table": "CLS",
			"User": "default",
			"Password": "topsoft",
			"Columns": [
				"EventTime",
				"EventTimeTics",
				"TimeZone",
				"SystemTag",
				"MachineName",
				"ProcessId",
				"ThreadId",
				"EnvironmentUserName",
				"Level",
				"SourceContext",
				"Message",
				"Exception"
			]
		}
	]
}
```

Описание параметров:
* Output - Тип плагина. Фиксированное значение "Clickhouse"
* System - Наименование логируемой системы. 
* Host - Адрес к Clickhouse
* Port - Порт к Clickhouse
* Database - Наименование базы данных, в которой будет храниться лог
* Table - Наименование таблицы, в которой будет храниться лог
* User - Имя пользователя, под которым будет осуществляться доступ к базе данных ClickHouse
* Password - пароль для пользователя
* Columns - массив атрибутов, которые будут сохраняться в базу данных. Колонки в таблице должны соответствовать наименованиями.






