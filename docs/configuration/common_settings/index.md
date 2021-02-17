---

id: configuration_common_settings
title: Общие настройки
prev: false
next: false 

---

# Общие настройки

В данном разделе описаны настройки для запуска и взаимосвязи между сервисами.

Основные настройки содержатся в файлах конфигурации ```appsetings[.{environment}].json```

В файле ```appsetings.json``` содержатся настройки по умолчанию. 

В файле ```appsetings.Logging.json``` содержатся настройки логирования по умолчанию.

В файле ```appsetings.Development.json``` (```appsetings.Logging.Development.json```) содержится слой изменений настроек над файлом ```appsetings.json``` (```appsetings.Logging.json```). Конфигурационный файл применяется, если переменная среды установлена в значение Development. 

В файле ```appsetings.Production.json``` (```appsetings.Logging.Production.json```) содержится слой изменений настроек над файлом ```appsetings.json``` (```appsetings.Logging.json```). Конфигурационный файл применяется, если переменная среды установлена в значение Production. 

Некоторые сервисы могут содержать дополнительные файлы конфигурации. 