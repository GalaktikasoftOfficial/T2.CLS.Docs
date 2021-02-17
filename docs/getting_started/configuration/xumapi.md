---

id: getting_started_configuration_settings_xumapi
title: Интерфейса анализа логов
prev: false
next: false 

---

## Конфигурирование интерфейса анализа логов

### apsettings.json

#### Конфигурация по умолчанию:

```
{
	"Application": {
		"DebugMode": "false",
		"SiteMode": "false",
		"UserContext": {
			"LifeTime": "1200000", //User session duration since last access. (in milliseconds)
			"CheckFrequency": "20000" //Period of checking the user session status. (in milliseconds)
		}
	},
	"Host": {
		"PathBase": "/LogViewer"
	},
	"Xaf": {
		"ApplicationName": "LogViewer",
		"ConnectionStrings": {
			"_Default": "XpoProvider=InMemoryDataStoreProvider",
			"Default": "Data Source=.;Initial Catalog=T2.CLS.LogViewer;Integrated Security=True;Connect Timeout=30;Encrypt=False;TrustServerCertificate=False;ApplicationIntent=ReadWrite;MultiSubnetFailover=False",
			"_EasyTest": "Data Source=.;Initial Catalog=T2.CLS.LogViewer3;Integrated Security=True;Connect Timeout=30;Encrypt=False;TrustServerCertificate=False;ApplicationIntent=ReadWrite;MultiSubnetFailover=False"
		},
		"Xafari": {
			"AppHost": {
				"AppModule": "T2.CLS.LogViewer.AppModule",
				"Modules": ""
			}
		}
	},
	"ClickHouse": {
		"HttpUrl": "http://ch.domain.local:8123/",
		"User": "default",
		"Password": "topsoft",
		"DataBase": "T2PLogs"
	},
	"CORS": {
		"Origins": "https://localhost:1111"
	},
	"IdentityServerAuthenticationOptions": {
		"ApiName": "xum",
		"Authority": "https://oauth.domain.local"
	}
}
```

#### Секция **Xaf**

* **ConnectionStrings** - описание строки подключения для работы с базами данных
 * **Default** - основная строка подключения
* **Xafari**
 * **AppHost** - Настройка подключаемых модулей
 * **AppModule** - основлной модуль приложения. Всегда имеет значение: ```T2.CLS.LogViewer.AppModule```
 * **Modules** - подключение модулей для расширения функциональности

#### Секция **ClickHouse**

В данной секции настройка подключения к ClickHouse для выполнения анализа логов.

* **HttpUrl** - адрес сервера ClickHouse для работы по http протоколу.
* **User** - пользователь для доступа к базе данных.
* **Password** - пароль для пользователя.
* **DataBase** - База данных, в которой хранится анализируемый лог.

#### Другие настройки Xafari

Для более детальной настройки приложения (подключение к серверу аутентификации и

</br>
</br>

<font color="green">*\[Раздел будет дополнен\]*</font>
