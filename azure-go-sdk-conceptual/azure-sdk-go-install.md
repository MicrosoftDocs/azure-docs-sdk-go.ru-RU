---
title: Установка пакета Azure SDK для Go
description: Сведения о том, как выполнить установку, вендоринг и настройку пакета Azure SDK для Go.
author: sptramer
ms.author: sttramer
ms.date: 01/30/2018
ms.topic: article
ms.devlang: go
manager: carmonm
ms.openlocfilehash: 580daf4f2e91eabf97e3acd21bda183c559b57da
ms.sourcegitcommit: fcc1786d59d2e32c97a9a8e0748e06f564a961bd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/23/2018
---
# <a name="installing-the-azure-sdk-for-go"></a><span data-ttu-id="38322-103">Установка пакета Azure SDK для Go</span><span class="sxs-lookup"><span data-stu-id="38322-103">Installing the Azure SDK for Go</span></span>

<span data-ttu-id="38322-104">Добро пожаловать в пакет Azure SDK для Go!</span><span class="sxs-lookup"><span data-stu-id="38322-104">Welcome to the Azure SDK for Go!</span></span> <span data-ttu-id="38322-105">Этот пакет SDK позволяет взаимодействовать со службами Azure и управлять ими из приложений Go.</span><span class="sxs-lookup"><span data-stu-id="38322-105">This SDK allows you to manage and interact with Azure services from your Go applications.</span></span>

## <a name="get-the-azure-sdk-for-go"></a><span data-ttu-id="38322-106">Получение пакета Azure SDK для Go</span><span class="sxs-lookup"><span data-stu-id="38322-106">Get the Azure SDK for Go</span></span>

[!INCLUDE [azure-sdk-go-get](includes/azure-sdk-go-get.md)]

<span data-ttu-id="38322-107">Для работы с Azure Storage Blob требуются отдельные пакеты SDK.</span><span class="sxs-lookup"><span data-stu-id="38322-107">Working with Azure Storage Blobs requires a separate SDK.</span></span>

```bash
go get -u -d github.com/Azure/azure-storage-blob-go/...
```

## <a name="vendoring-the-azure-sdk-for-go"></a><span data-ttu-id="38322-108">Вендоринг пакета Azure SDK для Go</span><span class="sxs-lookup"><span data-stu-id="38322-108">Vendoring the Azure SDK for Go</span></span>

<span data-ttu-id="38322-109">Выполнить вендоринг пакета Azure SDK для Go можно с помощью средства [dep](https://github.com/golang/dep).</span><span class="sxs-lookup"><span data-stu-id="38322-109">The Azure SDK for Go may be vendored through [dep](https://github.com/golang/dep).</span></span> <span data-ttu-id="38322-110">Чтобы обеспечить стабильность, мы рекомендуем использовать вендоринг.</span><span class="sxs-lookup"><span data-stu-id="38322-110">For stability reasons, vendoring is recommended.</span></span> <span data-ttu-id="38322-111">Для поддержки `dep` добавьте `github.com/Azure/azure-sdk-for-go` в раздел `[[constraint]]` файла `Gopkg.toml`.</span><span class="sxs-lookup"><span data-stu-id="38322-111">In order to use `dep` support, add `github.com/Azure/azure-sdk-for-go` to a `[[constraint]]` section of your `Gopkg.toml`.</span></span> <span data-ttu-id="38322-112">Например, чтобы выполнить вендоринг для версии `14.0.0`, добавьте следующую запись:</span><span class="sxs-lookup"><span data-stu-id="38322-112">For example, to vendor on version `14.0.0`, add the following entry:</span></span>

```
[[constraint]]
name = "github.com/Azure/azure-sdk-for-go"
version = "14.0.0"
```

## <a name="including-the-azure-sdk-for-go-in-your-project"></a><span data-ttu-id="38322-113">Добавление пакета Azure SDK для Go в проект</span><span class="sxs-lookup"><span data-stu-id="38322-113">Including the Azure SDK for Go in your project</span></span>

<span data-ttu-id="38322-114">Чтобы использовать службы Azure из кода Go, импортируйте все службы, с которыми вы взаимодействуете, и необходимые модули `autorest`.</span><span class="sxs-lookup"><span data-stu-id="38322-114">To use Azure services from your Go code, import any services you interact with and the required `autorest` modules.</span></span>
<span data-ttu-id="38322-115">Получить полный список доступных модулей для [доступных служб](https://godoc.org/github.com/Azure/azure-sdk-for-go) и [пакетов AutoRest](https://godoc.org/github.com/Azure/go-autorest) можно на сайте GoDoc.</span><span class="sxs-lookup"><span data-stu-id="38322-115">You get a complete list of the available modules from GoDoc for [available services](https://godoc.org/github.com/Azure/azure-sdk-for-go) and [AutoRest packages](https://godoc.org/github.com/Azure/go-autorest).</span></span> <span data-ttu-id="38322-116">Ниже приводятся наиболее распространенные пакеты, которые нужно скачать в репозитории `go-autorest`:</span><span class="sxs-lookup"><span data-stu-id="38322-116">The most common packages you need from `go-autorest` are:</span></span>

| <span data-ttu-id="38322-117">Package</span><span class="sxs-lookup"><span data-stu-id="38322-117">Package</span></span> | <span data-ttu-id="38322-118">ОПИСАНИЕ</span><span class="sxs-lookup"><span data-stu-id="38322-118">Description</span></span> |
|---------|-------------|
| <span data-ttu-id="38322-119">[github.com/Azure/go-autorest/autorest][autorest]</span><span class="sxs-lookup"><span data-stu-id="38322-119">[github.com/Azure/go-autorest/autorest][autorest]</span></span> | <span data-ttu-id="38322-120">Объекты для обработки аутентификации клиента службы</span><span class="sxs-lookup"><span data-stu-id="38322-120">Objects for handling service client authentication</span></span> |
| <span data-ttu-id="38322-121">[github.com/Azure/go-autorest/autorest/azure][autorest/azure]</span><span class="sxs-lookup"><span data-stu-id="38322-121">[github.com/Azure/go-autorest/autorest/azure][autorest/azure]</span></span> | <span data-ttu-id="38322-122">Константы для взаимодействия со службами Azure</span><span class="sxs-lookup"><span data-stu-id="38322-122">Constants for interactions with Azure services</span></span> |
| <span data-ttu-id="38322-123">[github.com/Azure/go-autorest/autorest/adal][autorest/adal]</span><span class="sxs-lookup"><span data-stu-id="38322-123">[github.com/Azure/go-autorest/autorest/adal][autorest/adal]</span></span> | <span data-ttu-id="38322-124">Механизмы аутентификации для доступа к службам Azure</span><span class="sxs-lookup"><span data-stu-id="38322-124">Authentication mechanisms for accessing Azure services</span></span> |
| <span data-ttu-id="38322-125">[github.com/Azure/go-autorest/autorest/to][autorest/to]</span><span class="sxs-lookup"><span data-stu-id="38322-125">[github.com/Azure/go-autorest/autorest/to][autorest/to]</span></span> | <span data-ttu-id="38322-126">Вспомогательные приложения утверждения типа для работы со структурами данных пакета Azure SDK</span><span class="sxs-lookup"><span data-stu-id="38322-126">Type assertion helpers for working with Azure SDK data structures</span></span> |

[autorest]: https://godoc.org/github.com/Azure/go-autorest/autorest
[autorest/azure]: https://godoc.org/github.com/Azure/go-autorest/autorest/azure
[autorest/adal]: https://godoc.org/github.com/Azure/go-autorest/autorest/adal
[autorest/to]: https://godoc.org/github.com/Azure/go-autorest/autorest/to

<span data-ttu-id="38322-127">Номера версий модулей служб Azure назначаются независимо от интерфейсов API пакета SDK для этих модулей.</span><span class="sxs-lookup"><span data-stu-id="38322-127">Modules for Azure services are versioned independently from the SDK APIs for them.</span></span> <span data-ttu-id="38322-128">Эти номера версии, включенные в путь импорта модуля, основаны на _версии службы_ или _профиле_.</span><span class="sxs-lookup"><span data-stu-id="38322-128">These versions are part of the module import path, and are from either a _service version_ or a _profile_.</span></span> <span data-ttu-id="38322-129">На этом этапе рекомендуется использовать определенную версию службы для разработки и выпуска.</span><span class="sxs-lookup"><span data-stu-id="38322-129">Currently, it is recommended that you use a specific service version for both development and release.</span></span> <span data-ttu-id="38322-130">Службы находятся в папке модуля `services`.</span><span class="sxs-lookup"><span data-stu-id="38322-130">Services are located under the `services` module.</span></span> <span data-ttu-id="38322-131">Полный путь для импорта состоит из имени службы, за которым следует версия в формате `YYYY-MM-DD` и снова имя службы.</span><span class="sxs-lookup"><span data-stu-id="38322-131">The full path for the import is the name of the service, followed by the version in `YYYY-MM-DD` format, followed by the service name again.</span></span> <span data-ttu-id="38322-132">Например, чтобы добавить версию `2017-03-30` службы вычислений, выполните следующий код:</span><span class="sxs-lookup"><span data-stu-id="38322-132">For example, to include the `2017-03-30` version of the Compute service:</span></span>

```go
import "github.com/Azure/azure-sdk-for-go/services/compute/mgmt/2017-03-30/compute"
```

<span data-ttu-id="38322-133">На этом этапе рекомендуется использовать последнюю версию службы, если у вас нет причин поступить иначе.</span><span class="sxs-lookup"><span data-stu-id="38322-133">Right now it is recommended that you use the latest version of a service, unless you have a reason to do otherwise.</span></span>

<span data-ttu-id="38322-134">Если требуется общий моментальный снимок служб, вы также можете выбрать одну версию профиля.</span><span class="sxs-lookup"><span data-stu-id="38322-134">If you need a collective snapshot of services, you can also select a single profile version.</span></span> <span data-ttu-id="38322-135">В нашем случае версия `2017-03-30` относится только к заблокированному профилю, который может не содержать последние версии служб и функций.</span><span class="sxs-lookup"><span data-stu-id="38322-135">Right now, the only locked profile is version `2017-03-30`, which may not have the latest features of services.</span></span> <span data-ttu-id="38322-136">Профили находятся в папке модуля `profiles` вместе с версиями в формате `YYYY-MM-DD`.</span><span class="sxs-lookup"><span data-stu-id="38322-136">Profiles are located under the `profiles` module, with their version in the `YYYY-MM-DD` format.</span></span> <span data-ttu-id="38322-137">Службы группируются по версиям профиля.</span><span class="sxs-lookup"><span data-stu-id="38322-137">Services are grouped under their profile version.</span></span> <span data-ttu-id="38322-138">Например, чтобы импортировать модуль управления ресурсами Azure из профиля `2017-03-09`, используйте следующий код:</span><span class="sxs-lookup"><span data-stu-id="38322-138">For example, to import the Azure Resources management module from the `2017-03-09` profile:</span></span>

```go
import "github.com/Azure/azure-sdk-for-go/profiles/2017-03-09/resources/mgmt/resources"
```

> [!WARNING]
> <span data-ttu-id="38322-139">Существуют также профили `preview` и `latest`.</span><span class="sxs-lookup"><span data-stu-id="38322-139">There are also `preview` and `latest` profiles available.</span></span> <span data-ttu-id="38322-140">Мы не рекомендуем использовать их.</span><span class="sxs-lookup"><span data-stu-id="38322-140">Using them is not recommended.</span></span> <span data-ttu-id="38322-141">Это профили промежуточных версий, и поведение службы может измениться в любое время.</span><span class="sxs-lookup"><span data-stu-id="38322-141">These profiles are rolling versions and service behavior may change at any time.</span></span>

## <a name="next-steps"></a><span data-ttu-id="38322-142">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="38322-142">Next steps</span></span>

<span data-ttu-id="38322-143">Чтобы начать работу с пакетом Azure SDK для Go, используйте код быстрого запуска.</span><span class="sxs-lookup"><span data-stu-id="38322-143">To begin using the Azure SDK for Go, try out a quickstart.</span></span>

* [<span data-ttu-id="38322-144">Краткое руководство по развертыванию виртуальной машины Azure из шаблона с помощью пакета Azure SDK для Go</span><span class="sxs-lookup"><span data-stu-id="38322-144">Deploy a virtual machine from a template</span></span>](azure-sdk-go-qs-vm.md)
* [<span data-ttu-id="38322-145">Передача объектов в хранилище BLOB-объектов Azure и обратно с помощью Go</span><span class="sxs-lookup"><span data-stu-id="38322-145">Transfer objects to Azure Blob Storage with the Azure Blob SDK for Go</span></span>](/azure/storage/blobs/storage-quickstart-blobs-go?toc=%2fgo%2fazure%2ftoc.json)
* [<span data-ttu-id="38322-146">База данных Azure для PostgreSQL: подключение и запросы данных с помощью языка Go</span><span class="sxs-lookup"><span data-stu-id="38322-146">Connect to Azure Database for PostgreSQL</span></span>](/azure/postgresql/connect-go?toc=%2fgo%2fazure%2ftoc.json)

<span data-ttu-id="38322-147">Чтобы сразу приступить к работе с другими службами с помощью пакета SDK для Go, ознакомьтесь с доступными примерами кода.</span><span class="sxs-lookup"><span data-stu-id="38322-147">If you want to get started with other services in the Go SDK immediately, take a look at some of the available sample code.</span></span>

* [<span data-ttu-id="38322-148">Аутентификация с помощью служб Azure</span><span class="sxs-lookup"><span data-stu-id="38322-148">Authenticate with Azure services</span></span>](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/iam)
* [<span data-ttu-id="38322-149">Развертывание новых виртуальных машин с использованием аутентификации по SSH</span><span class="sxs-lookup"><span data-stu-id="38322-149">Deploy new virtual machines with SSH authentication</span></span>](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/compute)
* [<span data-ttu-id="38322-150">Развертывание образа контейнера в службе "Экземпляры контейнеров Azure"</span><span class="sxs-lookup"><span data-stu-id="38322-150">Deploy a container image to Azure Container Instances</span></span>](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/containerinstance)
* [<span data-ttu-id="38322-151">Создание кластера в службе Azure Kubernetes</span><span class="sxs-lookup"><span data-stu-id="38322-151">Create a cluster in Azure Kubernetes Service</span></span>](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/containerservice)
* [<span data-ttu-id="38322-152">Работа со службами хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="38322-152">Work with Azure Storage services</span></span>](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/storage)
* [<span data-ttu-id="38322-153">Все примеры для пакета Azure SDK для Go</span><span class="sxs-lookup"><span data-stu-id="38322-153">All samples for the Azure SDK for Go</span></span>](https://github.com/azure-samples/azure-sdk-for-go-samples)
