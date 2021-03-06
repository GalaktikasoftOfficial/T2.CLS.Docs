# Документация "Т2 Журнализация"

Документация "T2 журналирования" - это описание проекта централизованного сбора, хранения и анализа логов.
Документация автоматически публикуется по адресу https://galaktikasoftofficial.github.io/T2.CLS.Docs/

## Ветки

**master** - основная ветка с документацией.

**gh_pages** - ветка собронного и развёрнутого сайта.

**develop** - ветка для разработки документации

## Редактирование

Для редактирования документации необходимо выполнить клонирование репозитория:

```
git clone https://github.com/GalaktikasoftOfficial/T2.CLS.Docs.git
```

Все изменения необходимо делать в отдельных ветках. Перед публикации изменений для проверки рабочие ветки необходимо сливать в ветку develop. После проверки изменений, они будут залиты в ветку master и автоматически опубликованы.

## Локальная сборка

Для запуска локального сервера необходимо выполнить команду из корневого каталога:

```
yarn docs:dev
```

Смотреть больше на https://vuepress.vuejs.org/
