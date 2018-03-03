---
title: "Установка пакета Azure SDK для Go"
description: "Сведения о том, как выполнить установку, вендоринг и настройку пакета Azure SDK для Go."
keywords: azure, sdk, go, golang, azure sdk
author: sptramer
ms.author: sttramer
ms.date: 01/30/2018
ms.topic: article
ms.devlang: go
manager: routlaw
ms.openlocfilehash: 7fc0a3ff71b0b06f616ae43cff311352fe873345
ms.sourcegitcommit: 890f5f01a70e7e376e6bb98a2030afbfc016f538
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/01/2018
---
# <a name="installing-the-azure-sdk-for-go"></a>Установка пакета Azure SDK для Go

Добро пожаловать в пакет Azure SDK для Go! Этот пакет SDK позволяет взаимодействовать со службами Azure и управлять ими из приложений Go.

## <a name="get-the-azure-sdk-for-go"></a>Получение пакета Azure SDK для Go

[!INCLUDE [azure-sdk-go-get](includes/azure-sdk-go-get.md)]

Для работы с Azure Storage Blob требуются отдельные пакеты SDK.

```bash
go get -u -d github.com/Azure/azure-storage-blob-go/...
```

## <a name="vendoring-the-azure-sdk-for-go"></a>Вендоринг пакета Azure SDK для Go

Выполнить вендоринг пакета Azure SDK для Go можно с помощью средства [dep](https://github.com/golang/dep). Чтобы обеспечить стабильность, мы рекомендуем использовать вендоринг. Для поддержки `dep` добавьте `github.com/Azure/azure-sdk-for-go` в раздел `[[constraint]]` файла `Gopkg.toml`. Например, чтобы выполнить вендоринг для версии `14.0.0`, добавьте следующую запись:

```
[[constraint]]
name = "github.com/Azure/azure-sdk-for-go"
version = "14.0.0"
```

## <a name="including-the-azure-sdk-for-go-in-your-project"></a>Добавление пакета Azure SDK для Go в проект

Чтобы использовать службы Azure из кода Go, импортируйте все службы, с которыми вы взаимодействуете, и необходимые модули `autorest`.
Получить полный список доступных модулей для [доступных служб](https://godoc.org/github.com/Azure/azure-sdk-for-go) и [пакетов AutoRest](https://godoc.org/github.com/Azure/go-autorest) можно на сайте GoDoc. Ниже приводятся наиболее распространенные пакеты, которые нужно скачать в репозитории `go-autorest`:

| Package | ОПИСАНИЕ |
|---------|-------------|
| [github.com/Azure/go-autorest/autorest][autorest] | Объекты для обработки аутентификации клиента службы |
| [github.com/Azure/go-autorest/autorest/azure][autorest/azure] | Константы для взаимодействия со службами Azure |
| [github.com/Azure/go-autorest/autorest/adal][autorest/adal] | Механизмы аутентификации для доступа к службам Azure |
| [github.com/Azure/go-autorest/autorest/to][autorest/to] | Вспомогательные приложения утверждения типа для работы со структурами данных пакета Azure SDK |

[autorest]: https://godoc.org/github.com/Azure/go-autorest/autorest
[autorest/azure]: https://godoc.org/github.com/Azure/go-autorest/autorest/azure
[autorest/adal]: https://godoc.org/github.com/Azure/go-autorest/autorest/adal
[autorest/to]: https://godoc.org/github.com/Azure/go-autorest/autorest/to

Номера версий модулей служб Azure назначаются независимо от интерфейсов API пакета SDK для этих модулей. Эти номера версии, включенные в путь импорта модуля, основаны на _версии службы_ или _профиле_. На этом этапе рекомендуется использовать определенную версию службы для разработки и выпуска. Службы находятся в папке модуля `services`. Полный путь для импорта состоит из имени службы, за которым следует версия в формате `YYYY-MM-DD` и снова имя службы. Например, чтобы добавить версию `2017-03-30` службы вычислений, выполните следующий код:

```go
import "github.com/Azure/azure-sdk-for-go/services/compute/mgmt/2017-03-30/compute"
```

На этом этапе рекомендуется использовать последнюю версию службы, если у вас нет причин поступить иначе.

Если требуется общий моментальный снимок служб, вы также можете выбрать одну версию профиля. В нашем случае версия `2017-03-30` относится только к заблокированному профилю, который может не содержать последние версии служб и функций. Профили находятся в папке модуля `profiles` вместе с версиями в формате `YYYY-MM-DD`. Службы группируются по версиям профиля. Например, чтобы импортировать модуль управления ресурсами Azure из профиля `2017-03-09`, используйте следующий код:

```go
import "github.com/Azure/azure-sdk-for-go/profiles/2017-03-09/resources/mgmt/resources"
```

> [!WARNING]
> Существуют также профили `preview` и `latest`. Мы не рекомендуем использовать их. Это профили промежуточных версий, и поведение службы может измениться в любое время.

## <a name="next-steps"></a>Дополнительная информация

Чтобы начать работу с пакетом Azure SDK для Go, используйте код быстрого запуска.

* [Краткое руководство по развертыванию виртуальной машины Azure из шаблона с помощью пакета Azure SDK для Go](azure-sdk-go-qs-vm.md)
* [Передача объектов в хранилище BLOB-объектов Azure и обратно с помощью Go](/azure/storage/blobs/storage-quickstart-blobs-go?toc=%2fgo%2fazure%2ftoc.json)
* [База данных Azure для PostgreSQL: подключение и запросы данных с помощью языка Go](/azure/postgresql/connect-go?toc=%2fgo%2fazure%2ftoc.json)

Чтобы сразу приступить к работе с другими службами с помощью пакета SDK для Go, ознакомьтесь с доступными примерами кода.

* [Аутентификация с помощью служб Azure](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/iam)
* [Развертывание новых виртуальных машин с использованием аутентификации по SSH](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/compute)
* [Развертывание образа контейнера в службе "Экземпляры контейнеров Azure"](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/containerinstance)
* [Создание кластера в службе Azure Kubernetes](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/containerservice)
* [Работа со службами хранилища Azure](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/storage)
* [Все примеры для пакета Azure SDK для Go](https://github.com/azure-samples/azure-sdk-for-go-samples)
