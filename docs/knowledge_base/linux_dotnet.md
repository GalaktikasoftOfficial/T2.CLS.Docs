---

id: knowledge_base_linux_dotnet
title: Установка .Net3.1 на Linux (Ubuntu 20.04)
next: false
prev: false

---
### Установка .Net3.1 на Linux (Ubuntu 20.04)

Для работы на Linux сервисов необходимо установить .Net3.1 SDK 
Для этого необходимо выполнить следующие команды:

	sudo apt-get update
	sudo apt-get install -y apt-transport-https
	sudo apt-get updat
	sudo apt-get install -y dotnet-sdk-3.1
	
Если Вы получите сообщения об ошибке **Unable to locate package dotnet-sdk-3.1**, то необходимо настроить APT источник Microsoft:
	
	curl -sSL https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
	sudo apt-add-repository https://packages.microsoft.com/ubuntu/20.04/prod
	sudo apt-get update
	
