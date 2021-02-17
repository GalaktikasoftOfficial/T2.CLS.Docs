---

id: getting_started_configuration_settings_storedservice
title: Сервис хранения
prev: false
next: false 

---

<h2> Конфигурирование сервиса хранения </h2>


### apsettings.json

#### Конфигурация по умолчанию:

```
{
    "Logging": {
        "LogLevel": {
            "Default": "Debug",
            "System": "Information",
            "Microsoft": "Information"
        }
    },
    "AllowedHosts": "*",
    "Storage": {
        "HttpUrl": "http://192.168.208.3:8123/",
        "User": "default",
        "Password": "topsoft",
        "DataBase": "T2PLogs",
        "DataPath": "/var/lib/clickhouse/data",
        "ArchivePath": "/var/lib/clickhouse/archive"
    }
}
```

#### Секция Logging 

Сексия Logging отвечает за минимальный уровень логирования по источникам.

Возможные варианты уровня логирования:

* Trace
* Debug 
* Information
* Warning
* Error
* Critical 
* None

#### Секция AllowedHosts 

Заголовки хостов, которым разрешен доступ к этому сервису.

Номера портов необходимо исключить.

Подстановочный знак верхнего уровня ```«*»``` разрешает все непустые хосты.

Подстановочные знаки субдоменов разрешены. Например. ```«* .example.com»``` соответствует субдоменам, таким как ```foo.example.com```, но не родительскому домену ```example.com.```

#### Секция Storage

Предназначена для описания параметров подключения к базе данных ClickHouse и доступа к файлам данных.

* HttpUrl - url-адрес для доступа к ClickHouse по http/https протоколу.
* User - имя пользователя для подключения к ClickHouse.
* Password - пароль для пользователя .
* DataBase - база данных, которая будет создана и в которой будут размещаться таблицы логов.
* DataPath - путь к файлам данных ClickHouse для архивации устаревших партиций.
* ArchivePath - путь к месту хранения устаревших партиций.

### Файлы конфигурации логируемых систем

Файлы конфигураций систем содержатся в каталоге ```SystemConfig```.

Для каждой системы или части системы относится отдельный файл. Имя файла имеет вид: ```{system_name}.json```

Пример конфигурации:

```
{
  "Name": "CLS",
  "PartitionLifetime": "30.00:00:00",
  "DateTimeField": "EventTime",
  "SortFields": [ "EventTimeTics" ],
  "Fields": [
    {
      "Name": "EventTime",
      "TypeName": "DateTime"
    },
    {
      "Name": "EventTimeTics",
      "TypeName": "UInt64"
    },
    {
      "Name": "TimeZone",
      "TypeName": "String"
    },
    {
      "Name": "SystemTag",
      "TypeName": "String"
    },
    {
      "Name": "MachineName",
      "TypeName": "String"
    },
    {
      "Name": "ProcessId",
      "TypeName": "Int16"
    },
    {
      "Name": "ThreadId",
      "TypeName": "Int16"
    },
    {
      "Name": "EnvironmentUserName",
      "TypeName": "String"
    },
    {
      "Name": "Level",
      "TypeName": "Byte"
    },
    {
      "Name": "SourceContext",
      "TypeName": "String"
    },
    {
      "Name": "Message",
      "TypeName": "String"
    },
    {
      "Name": "Exception",
      "TypeName": "String"
    }
  ]
}
```

Описание атрибутов: 
* Name - Наименование системы. В Базе данных ClickHouse будет создана таблица с таким именем.
* PartitionLifetime - Время жизни партиции. Имеет формат ```{days}.{hours}:{minutes}.{seconds}```.
* DateTimeField  - поле для выполнения партиционирования по дате и времени (чаще всего это время генерации записи лога).
* SortFields - поле для сортировки данных (чаще всего это время генерации записи лога в Long формате).
* Fields - коллекция полей таблицы
	* Name - наименование поля
	* TypeName - тип поля. Возможные варианты: DateTime, Byte, Int16, Int32, Int64, UInt16, UInt32, UInt64, String