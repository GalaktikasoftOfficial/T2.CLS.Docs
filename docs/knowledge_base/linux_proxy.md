---

id: knowledge_base_linux_proxy
title: Настройка proxy на Linux (Ubuntu 20.04)
next: false
prev: false

---
### Настройка proxy на Linux (Ubuntu 20.04)

Для работы через proxy необходимо прописать адрес к proxy-серверу в переменных окружения. Так же для некоторых команд требуется отдельное указание настроек.

Адрес к proxy-серверу выглядит следующим образом:

    http://UserName:pass@SERVER:PORT

*UserName* и *pass* не обязательные параметры.

Пример: 
	
	http://TopSoftUser:topsoft@by01-tmg.topsoft.local:80

#### Настройка перемененных окружения

Для настройки через terminal необходимо выполнить следующие команды:
	
	$ export http_proxy=http://UserName:pass@SERVER:PORT
	$ export https_proxy=http://UserName:pass@SERVER:PORT

#### Настройка **apt-get**

Подробную информацию можно посмотреть [тут](https://www.serverlab.ca/tutorials/linux/administration-linux/how-to-set-the-proxy-for-apt-for-ubuntu-18-04/)

Создать новый конфигурационный файл ```proxy.conf```
	
	sudo touch /etc/apt/apt.conf.d/proxy.conf

Открыть файл ```proxy.conf``` в текстовом редакторе.

	sudo vi /etc/apt/apt.conf.d/proxy.conf

Добавить следующие строки длы настройки HTTP(s) proxy

	Acquire::http::Proxy "http://user:password@proxy.server:port/";
	Acquire::https::Proxy "http://user:password@proxy.server:port/";

Сохраните свои изменения и закройте текстовый редактор.
Ваши настройки proxy будут применены при следующем запуске утилиты **apt**

#### Curl.

Для работы утилиты **curl** необходимы настройки переменных окружения