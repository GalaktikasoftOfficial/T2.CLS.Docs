---

id: getting_started_deployment_clickhouse
title: ClickHouse
prev: false
next: false

---

<h2> Установка и настройка <b>ClickHouse</b> </h2>

Для установки **ClickHouse** можно воспользоваться [инструкцией](https://clickhouse.tech/docs/ru/getting-started/install/).


### Пример установки на виртуальной машине с **Ubuntu-20.04.1**
#### 1. Работа с прокси

В некоторых случаях требуется работа через прокси. Адрес к прокси серверу выглядит следующим образом:

    http://UserName:pass@SERVER:PORT

*UserName* и *pass* не обязательные параметры. Далее адрес прокси будем писать следующего вида:

    http://your_proxy_server:port

Прокси прописывается в нескольких местах:
* Для **apt-get**. Как это cделать [тут](https://www.serverlab.ca/tutorials/linux/administration-linux/how-to-set-the-proxy-for-apt-for-ubuntu-18-04/)
* В системных переменных *proxy_http* и *proxy_https* 

```
$ export http_proxy=http://UserName:pass@SERVER:PORT
$ export https_proxy=http://UserName:pass@SERVER:PORT
```

* Для отдельных команд соответствуя их синтаксису

#### 2. Установка **ClickHouse**
	
  2.1. Установка пакета *apt-transport-https*

	$ sudo apt-get install apt-transport-https ca-certificates dirmngr

  2.2. Добавление цифровой подписи	

	$ sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv E0C56BD4


  Если требуется работать через прокси, то необходимо для команды указывать параметры

	$ sudo apt-key adv --keyserver-options http-proxy="http://your_proxy_server:port"  --keyserver hkp://keyserver.ubuntu.com:80 --recv E0C56BD4
	
  2.3. Регистрация источников пакетов **Clickhouse**
        
	$ echo "deb https://repo.clickhouse.tech/deb/stable/ main/" | sudo tee /etc/apt/sources.list.d/clickhouse.list
    $ sudo apt-get update
	
  2.4. Установка  сервера ClickHouse
	    
	$ sudo apt-get install clickhouse-server
		
  2.5. Установка  клиента ClickHouse
	    
	$ sudo apt-get install clickhouse-client
	
  2.6. Запуск сервера 
        
	$ sudo service clickhouse-server start
	
	
#### 3. Управление службой **ClickHouse**
	
  3.1. Проверка работы сервиса:
	
	$ systemctl status clickhouse-server
	
  3.2. Запуск сервиса:
  
	$ systemctl start clickhouse-server
	
  3.2. Остановка сервиса:
  
	$ systemctl stop clickhouse-server
	
	
#### 4. Проверка работоспособности

  4.1. Из **терминала**:
  
  Последовательно выполнить команды: 
  
	$ clickhouse-client
	$ select 1

  Результатом будет следующее:
  
  ![img](../../_assets/CH_Check.png)
  
  4.2. Из **браузера** (или из терминала используя **curl**)
  
	$ curl http://localhost:8123

  или 
  
	$ curl http://localhost:8123/?query=Select%201
  
 Результатом будет следующее:
  
  ![img](../../_assets/CH_Check_Br.png)
  
#### 5. Настройка пользователя для ClickHouse
  
  По умолчанию в ClickHouse используется пользователь **default** без пароля. 
  Для установки пароля:
  
  5.1. Необходимо выполнить в терминале исполнить:
  
    $ PASSWORD='MyPassword'; echo "$PASSWORD"; echo -n "$PASSWORD" | sha256sum | tr -d '-'
	
  Результатом будет 2 строки пароля в открытом и зашифрованном виде. 
  
  ![img](../../_assets/GeneratePass.png)
  
  5.2. Открываем файл /etc/clickhouse-server/users.xml.
  
  5.3. Находим секции *yandex->users->default* и добавляем тег *password_sha256_hex*

    <yandex>
	...
		<users>
		...
			<default>
				<password_sha256_hex>dc1e7c03e162397b355b6f1c895dfdf3790d98c10b920c55e91272b8eecada2a</password_sha256_hex>
				...
			</default>
		...
		</users>
	...
	</yandex>
	
  5.4. Сохраняем файл
  
  5.6. Перезапускаем сервис ClickHouse 
  
	$ systemctl restart clickhouse-server
	
  5.7. Проверяем внесённые изменения
  
    $  curl http://default:MyPassword@localhost:8123/?query=Select%201
	
	
#### 6. Другие настройки ClickHouse

Смотреть официальную документацию на [портале](https://clickhouse.tech/docs/)
    
	