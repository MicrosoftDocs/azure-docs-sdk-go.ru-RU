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
ms.openlocfilehash: f822a9304a4744e0b0e93286303aa8bb80fec852
ms.sourcegitcommit: aaa8c37880332625f858a38f5918e6cf581bf48d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/15/2018
---
# <a name="installing-the-azure-sdk-for-go"></a><span data-ttu-id="46133-104">Установка пакета Azure SDK для Go</span><span class="sxs-lookup"><span data-stu-id="46133-104">Installing the Azure SDK for Go</span></span>

<span data-ttu-id="46133-105">Добро пожаловать в пакет Azure SDK для Go!</span><span class="sxs-lookup"><span data-stu-id="46133-105">Welcome to the Azure SDK for Go!</span></span> <span data-ttu-id="46133-106">Этот пакет SDK позволяет взаимодействовать со службами Azure и управлять ими из приложений Go.</span><span class="sxs-lookup"><span data-stu-id="46133-106">This SDK allows you to manage and interact with Azure services from your Go applications.</span></span>

## <a name="get-the-azure-sdk-for-go"></a><span data-ttu-id="46133-107">Получение пакета Azure SDK для Go</span><span class="sxs-lookup"><span data-stu-id="46133-107">Get the Azure SDK for Go</span></span>

[!INCLUDE [azure-sdk-go-get](includes/azure-sdk-go-get.md)]

<span data-ttu-id="46133-108">Для работы с Azure Storage Blob требуются отдельные пакеты SDK.</span><span class="sxs-lookup"><span data-stu-id="46133-108">Working with Azure Storage Blobs requires a separate SDK.</span></span>

```bash
go get -u -d github.com/Azure/azure-storage-blob-go/...
```

## <a name="vendoring-the-azure-sdk-for-go"></a><span data-ttu-id="46133-109">Вендоринг пакета Azure SDK для Go</span><span class="sxs-lookup"><span data-stu-id="46133-109">Vendoring the Azure SDK for Go</span></span>

<span data-ttu-id="46133-110">Выполнить вендоринг пакета Azure SDK для Go можно с помощью средства [dep](https://github.com/golang/dep).</span><span class="sxs-lookup"><span data-stu-id="46133-110">The Azure SDK for Go may be vendored through [dep](https://github.com/golang/dep).</span></span> <span data-ttu-id="46133-111">Чтобы обеспечить стабильность, мы рекомендуем использовать вендоринг.</span><span class="sxs-lookup"><span data-stu-id="46133-111">For stability reasons, vendoring is recommended.</span></span> <span data-ttu-id="46133-112">Для поддержки `dep` добавьте `gitub.com/Azure/azure-sdk-for-go` в раздел `[[constraint]]` файла `Gopkg.toml`.</span><span class="sxs-lookup"><span data-stu-id="46133-112">In order to use `dep` support, add `gitub.com/Azure/azure-sdk-for-go` to a `[[constraint]]` section of your `Gopkg.toml`.</span></span> <span data-ttu-id="46133-113">Например, чтобы выполнить вендоринг для версии `14.0.0`, добавьте следующую запись:</span><span class="sxs-lookup"><span data-stu-id="46133-113">For example, to vendor on version `14.0.0`, add the following entry:</span></span>

```
[[constraint]]
name = "github.com/Azure/azure-sdk-for-go"
version = "14.0.0"
```

## <a name="including-the-azure-sdk-for-go-in-your-project"></a><span data-ttu-id="46133-114">Добавление пакета Azure SDK для Go в проект</span><span class="sxs-lookup"><span data-stu-id="46133-114">Including the Azure SDK for Go in your project</span></span>

<span data-ttu-id="46133-115">Чтобы использовать службы Azure из кода Go, импортируйте все службы, с которыми вы взаимодействуете, и необходимые модули `autorest`.</span><span class="sxs-lookup"><span data-stu-id="46133-115">To use Azure services from your Go code, import any services you interact with and the required `autorest` modules.</span></span>
<span data-ttu-id="46133-116">Получить полный список доступных модулей для [доступных служб](https://godoc.org/github.com/Azure/azure-sdk-for-go) и [пакетов AutoRest](https://godoc.org/github.com/Azure/go-autorest) можно на сайте GoDoc.</span><span class="sxs-lookup"><span data-stu-id="46133-116">You get a complete list of the available modules from GoDoc for [available services](https://godoc.org/github.com/Azure/azure-sdk-for-go) and [AutoRest packages](https://godoc.org/github.com/Azure/go-autorest).</span></span> <span data-ttu-id="46133-117">Ниже приводятся наиболее распространенные пакеты, которые нужно скачать в репозитории `go-autorest`:</span><span class="sxs-lookup"><span data-stu-id="46133-117">The most common packages you need from `go-autorest` are:</span></span>

| <span data-ttu-id="46133-118">Package</span><span class="sxs-lookup"><span data-stu-id="46133-118">Package</span></span> | <span data-ttu-id="46133-119">ОПИСАНИЕ</span><span class="sxs-lookup"><span data-stu-id="46133-119">Description</span></span> |
|---------|-------------|
| <span data-ttu-id="46133-120">[github.com/Azure/go-autorest/autorest][autorest]</span><span class="sxs-lookup"><span data-stu-id="46133-120">[github.com/Azure/go-autorest/autorest][autorest]</span></span> | <span data-ttu-id="46133-121">Объекты для обработки аутентификации клиента службы</span><span class="sxs-lookup"><span data-stu-id="46133-121">Objects for handling service client authentication</span></span> |
| <span data-ttu-id="46133-122">[github.com/Azure/go-autorest/autorest/azure][autorest/azure]</span><span class="sxs-lookup"><span data-stu-id="46133-122">[github.com/Azure/go-autorest/autorest/azure][autorest/azure]</span></span> | <span data-ttu-id="46133-123">Константы для взаимодействия со службами Azure</span><span class="sxs-lookup"><span data-stu-id="46133-123">Constants for interactions with Azure services</span></span> |
| <span data-ttu-id="46133-124">[github.com/Azure/go-autorest/autorest/adal][autorest/adal]</span><span class="sxs-lookup"><span data-stu-id="46133-124">[github.com/Azure/go-autorest/autorest/adal][autorest/adal]</span></span> | <span data-ttu-id="46133-125">Механизмы аутентификации для доступа к службам Azure</span><span class="sxs-lookup"><span data-stu-id="46133-125">Authentication mechanisms for accessing Azure services</span></span> |
| <span data-ttu-id="46133-126">[github.com/Azure/go-autorest/autorest/to][autorest/to]</span><span class="sxs-lookup"><span data-stu-id="46133-126">[github.com/Azure/go-autorest/autorest/to][autorest/to]</span></span> | <span data-ttu-id="46133-127">Вспомогательные приложения утверждения типа для работы со структурами данных пакета Azure SDK</span><span class="sxs-lookup"><span data-stu-id="46133-127">Type assertion helpers for working with Azure SDK data structures</span></span> |

[autorest]: https://godoc.org/github.com/Azure/go-autorest/autorest
[autorest/azure]: https://godoc.org/github.com/Azure/go-autorest/autorest/azure
[autorest/adal]: https://godoc.org/github.com/Azure/go-autorest/autorest/adal
[autorest/to]: https://godoc.org/github.com/Azure/go-autorest/autorest/to

<span data-ttu-id="46133-128">Номера версий модулей служб Azure назначаются независимо от интерфейсов API пакета SDK для этих модулей.</span><span class="sxs-lookup"><span data-stu-id="46133-128">Modules for Azure services are versioned independently from the SDK APIs for them.</span></span> <span data-ttu-id="46133-129">Эти номера версии, включенные в путь импорта модуля, основаны на _версии службы_ или _профиле_.</span><span class="sxs-lookup"><span data-stu-id="46133-129">These versions are part of the module import path, and are from either a _service version_ or a _profile_.</span></span> <span data-ttu-id="46133-130">На этом этапе рекомендуется использовать определенную версию службы для разработки и выпуска.</span><span class="sxs-lookup"><span data-stu-id="46133-130">Currently, it is recommended that you use a specific service version for both development and release.</span></span> <span data-ttu-id="46133-131">Службы находятся в папке модуля `services`.</span><span class="sxs-lookup"><span data-stu-id="46133-131">Services are located under the `services` module.</span></span> <span data-ttu-id="46133-132">Полный путь для импорта состоит из имени службы, за которым следует версия в формате `YYYY-MM-DD` и снова имя службы.</span><span class="sxs-lookup"><span data-stu-id="46133-132">The full path for the import is the name of the service, followed by the version in `YYYY-MM-DD` format, followed by the service name again.</span></span> <span data-ttu-id="46133-133">Например, чтобы добавить версию `2017-03-30` службы вычислений, выполните следующий код:</span><span class="sxs-lookup"><span data-stu-id="46133-133">For example, to include the `2017-03-30` version of the Compute service:</span></span>

```go
import "github.com/Azure/azure-sdk-for-go/services/compute/mgmt/2017-03-30/compute"
```

<span data-ttu-id="46133-134">На этом этапе рекомендуется использовать последнюю версию службы, если у вас нет причин поступить иначе.</span><span class="sxs-lookup"><span data-stu-id="46133-134">Right now it is recommended that you use the latest version of a service, unless you have a reason to do otherwise.</span></span>

<span data-ttu-id="46133-135">Если требуется общий моментальный снимок служб, вы также можете выбрать одну версию профиля.</span><span class="sxs-lookup"><span data-stu-id="46133-135">If you need a collective snapshot of services, you can also select a single profile version.</span></span> <span data-ttu-id="46133-136">В нашем случае версия `2017-03-30` относится только к заблокированному профилю, который может не содержать последние версии служб и функций.</span><span class="sxs-lookup"><span data-stu-id="46133-136">Right now, the only locked profile is version `2017-03-30`, which may not have the latest features of services.</span></span> <span data-ttu-id="46133-137">Профили находятся в папке модуля `profiles` вместе с версиями в формате `YYYY-MM-DD`.</span><span class="sxs-lookup"><span data-stu-id="46133-137">Profiles are located under the `profiles` module, with their version in the `YYYY-MM-DD` format.</span></span> <span data-ttu-id="46133-138">Службы группируются по версиям профиля.</span><span class="sxs-lookup"><span data-stu-id="46133-138">Services are grouped under their profile version.</span></span> <span data-ttu-id="46133-139">Например, чтобы импортировать модуль управления ресурсами Azure из профиля `2017-03-09`, используйте следующий код:</span><span class="sxs-lookup"><span data-stu-id="46133-139">For example, to import the Azure Resources management module from the `2017-03-09` profile:</span></span>

```go
import "github.com/Azure/azure-sdk-for-go/profiles/2017-03-09/resources/mgmt/resources"
```

> [!WARNING]
> <span data-ttu-id="46133-140">Существуют также профили `preview` и `latest`.</span><span class="sxs-lookup"><span data-stu-id="46133-140">There are also `preview` and `latest` profiles available.</span></span> <span data-ttu-id="46133-141">Мы не рекомендуем использовать их.</span><span class="sxs-lookup"><span data-stu-id="46133-141">Using them is not recommended.</span></span> <span data-ttu-id="46133-142">Это профили промежуточных версий, и поведение службы может измениться в любое время.</span><span class="sxs-lookup"><span data-stu-id="46133-142">These profiles are rolling versions and service behavior may change at any time.</span></span>

## <a name="next-steps"></a><span data-ttu-id="46133-143">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="46133-143">Next steps</span></span>

<span data-ttu-id="46133-144">Чтобы начать работу с пакетом Azure SDK для Go, используйте код быстрого запуска.</span><span class="sxs-lookup"><span data-stu-id="46133-144">To begin using the Azure SDK for Go, try out a quickstart.</span></span>

* [<span data-ttu-id="46133-145">Краткое руководство по развертыванию виртуальной машины Azure из шаблона с помощью пакета Azure SDK для Go</span><span class="sxs-lookup"><span data-stu-id="46133-145">Deploy a virtual machine from a template</span></span>](azure-sdk-go-qs-vm.md)
* [<span data-ttu-id="46133-146">Передача объектов в хранилище BLOB-объектов Azure и обратно с помощью Go</span><span class="sxs-lookup"><span data-stu-id="46133-146">Transfer objects to Azure Blob Storage with the Azure Blob SDK for Go</span></span>](/azure/storage/blobs/storage-quickstart-blobs-go?toc=%2fgo%2fazure%2ftoc.json)
* [<span data-ttu-id="46133-147">База данных Azure для PostgreSQL: подключение и запросы данных с помощью языка Go</span><span class="sxs-lookup"><span data-stu-id="46133-147">Connect to Azure Database for PostgreSQL</span></span>](/azure/postgresql/connect-go?toc=%2fgo%2fazure%2ftoc.json)

<span data-ttu-id="46133-148">Чтобы сразу приступить к работе с другими службами с помощью пакета SDK для Go, ознакомьтесь с доступными примерами кода.</span><span class="sxs-lookup"><span data-stu-id="46133-148">If you want to get started with other services in the Go SDK immediately, take a look at some of the available sample code.</span></span>

* [<span data-ttu-id="46133-149">Аутентификация с помощью служб Azure</span><span class="sxs-lookup"><span data-stu-id="46133-149">Authenticate with Azure services</span></span>](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/iam)
* [<span data-ttu-id="46133-150">Развертывание новых виртуальных машин с использованием аутентификации по SSH</span><span class="sxs-lookup"><span data-stu-id="46133-150">Deploy new virtual machines with SSH authentication</span></span>](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/compute)
* [<span data-ttu-id="46133-151">Развертывание образа контейнера в службе "Экземпляры контейнеров Azure"</span><span class="sxs-lookup"><span data-stu-id="46133-151">Deploy a container image to Azure Container Instances</span></span>](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/containerinstance)
* [<span data-ttu-id="46133-152">Создание кластера в службе Azure Kubernetes</span><span class="sxs-lookup"><span data-stu-id="46133-152">Create a cluster in Azure Kubernetes Service</span></span>](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/containerservice)
* [<span data-ttu-id="46133-153">Работа со службами хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="46133-153">Work with Azure Storage services</span></span>](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/storage)
* [<span data-ttu-id="46133-154">Все примеры для пакета Azure SDK для Go</span><span class="sxs-lookup"><span data-stu-id="46133-154">All samples for the Azure SDK for Go</span></span>](https://github.com/azure-samples/azure-sdk-for-go-samples)
