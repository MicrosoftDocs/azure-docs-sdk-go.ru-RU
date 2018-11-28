---
title: Установка пакета Azure SDK для Go
description: Сведения о том, как выполнить установку, вендоринг и настройку пакета Azure SDK для Go.
author: sptramer
ms.author: sttramer
manager: carmonm
ms.date: 03/14/2018
ms.topic: conceptual
ms.prod: azure
ms.technology: azure-sdk-go
ms.devlang: go
ms.openlocfilehash: 7990ec8bde5622078aa822fc7e66ba5c4384d682
ms.sourcegitcommit: 3d26b464f196f8675c636ae792637d4c882fb92c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/27/2018
ms.locfileid: "52337149"
---
# <a name="install-the-azure-sdk-for-go"></a><span data-ttu-id="7b50f-103">Установка пакета Azure SDK для Go</span><span class="sxs-lookup"><span data-stu-id="7b50f-103">Install the Azure SDK for Go</span></span>

<span data-ttu-id="7b50f-104">Добро пожаловать в пакет Azure SDK для Go!</span><span class="sxs-lookup"><span data-stu-id="7b50f-104">Welcome to the Azure SDK for Go!</span></span> <span data-ttu-id="7b50f-105">Этот пакет SDK позволяет взаимодействовать со службами Azure и управлять ими из приложений Go.</span><span class="sxs-lookup"><span data-stu-id="7b50f-105">The SDK allows you to manage and interact with Azure services from your Go applications.</span></span>

## <a name="get-the-azure-sdk-for-go"></a><span data-ttu-id="7b50f-106">Получение пакета Azure SDK для Go</span><span class="sxs-lookup"><span data-stu-id="7b50f-106">Get the Azure SDK for Go</span></span>

[!INCLUDE [azure-sdk-go-get](includes/azure-sdk-go-get.md)]

<span data-ttu-id="7b50f-107">Некоторые службы Azure содержат собственные пакеты SDK Go, которые не включены в основной пакет Azure SDK для Go.</span><span class="sxs-lookup"><span data-stu-id="7b50f-107">Some Azure services have their own Go SDK and aren't included in the core Azure SDK for Go package.</span></span> <span data-ttu-id="7b50f-108">В следующей таблице перечислены службы, содержащие собственные пакеты SDK, с указанием имен пакетов.</span><span class="sxs-lookup"><span data-stu-id="7b50f-108">The following table lists the services with their own SDKs and their package names.</span></span> <span data-ttu-id="7b50f-109">Все эти пакеты доступны в режиме предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="7b50f-109">These packages are all considered to be in preview.</span></span>

| <span data-ttu-id="7b50f-110">Service</span><span class="sxs-lookup"><span data-stu-id="7b50f-110">Service</span></span> | <span data-ttu-id="7b50f-111">Package</span><span class="sxs-lookup"><span data-stu-id="7b50f-111">Package</span></span> |
|---------|---------|
| <span data-ttu-id="7b50f-112">Хранилище BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="7b50f-112">Blob Storage</span></span> | [<span data-ttu-id="7b50f-113">github.com/Azure/azure-storage-blob-go</span><span class="sxs-lookup"><span data-stu-id="7b50f-113">github.com/Azure/azure-storage-blob-go</span></span>](https://github.com/Azure/azure-storage-blob-go) |
| <span data-ttu-id="7b50f-114">Хранилище файлов</span><span class="sxs-lookup"><span data-stu-id="7b50f-114">File Storage</span></span> | [<span data-ttu-id="7b50f-115">github.com/Azure/azure-storage-file-go</span><span class="sxs-lookup"><span data-stu-id="7b50f-115">github.com/Azure/azure-storage-file-go</span></span>](https://github.com/Azure/azure-storage-file-go) |
| <span data-ttu-id="7b50f-116">Очередь службы хранилища</span><span class="sxs-lookup"><span data-stu-id="7b50f-116">Storage Queue</span></span> | [<span data-ttu-id="7b50f-117">github.com/Azure/azure-storage-queue-go</span><span class="sxs-lookup"><span data-stu-id="7b50f-117">github.com/Azure/azure-storage-queue-go</span></span>](https://github.com/Azure/azure-storage-queue-go) |
| <span data-ttu-id="7b50f-118">Концентратор событий</span><span class="sxs-lookup"><span data-stu-id="7b50f-118">Event Hub</span></span> | [<span data-ttu-id="7b50f-119">github.com/Azure/azure-event-hubs-go</span><span class="sxs-lookup"><span data-stu-id="7b50f-119">github.com/Azure/azure-event-hubs-go</span></span>](https://github.com/Azure/azure-event-hubs-go) |
| <span data-ttu-id="7b50f-120">Служебная шина Azure</span><span class="sxs-lookup"><span data-stu-id="7b50f-120">Service Bus</span></span> | [<span data-ttu-id="7b50f-121">github.com/Azure/azure-service-bus-go</span><span class="sxs-lookup"><span data-stu-id="7b50f-121">github.com/Azure/azure-service-bus-go</span></span>](https://github.com/Azure/azure-service-bus-go) |
| <span data-ttu-id="7b50f-122">Application Insights</span><span class="sxs-lookup"><span data-stu-id="7b50f-122">Application Insights</span></span> | [<span data-ttu-id="7b50f-123">github.com/Microsoft/ApplicationInsights-go</span><span class="sxs-lookup"><span data-stu-id="7b50f-123">github.com/Microsoft/ApplicationInsights-go</span></span>](https://github.com/Microsoft/ApplicationInsights-go) |

## <a name="vendor-the-azure-sdk-for-go"></a><span data-ttu-id="7b50f-124">Вендоринг пакета Azure SDK для Go</span><span class="sxs-lookup"><span data-stu-id="7b50f-124">Vendor the Azure SDK for Go</span></span>

<span data-ttu-id="7b50f-125">Выполнить вендоринг пакета Azure SDK для Go можно с помощью средства [dep](https://github.com/golang/dep).</span><span class="sxs-lookup"><span data-stu-id="7b50f-125">The Azure SDK for Go may be vendored through [dep](https://github.com/golang/dep).</span></span> <span data-ttu-id="7b50f-126">Чтобы обеспечить стабильность, мы рекомендуем использовать вендоринг.</span><span class="sxs-lookup"><span data-stu-id="7b50f-126">For stability reasons, vendoring is recommended.</span></span> <span data-ttu-id="7b50f-127">Для использования `dep` в проекте добавьте `github.com/Azure/azure-sdk-for-go` в раздел `[[constraint]]` файла `Gopkg.toml`.</span><span class="sxs-lookup"><span data-stu-id="7b50f-127">To use `dep` in your own project, add `github.com/Azure/azure-sdk-for-go` to a `[[constraint]]` section of your `Gopkg.toml`.</span></span> <span data-ttu-id="7b50f-128">Например, чтобы выполнить вендоринг для версии `14.0.0`, добавьте следующую запись:</span><span class="sxs-lookup"><span data-stu-id="7b50f-128">For example, to vendor on version `14.0.0`, add the following entry:</span></span>

```toml
[[constraint]]
name = "github.com/Azure/azure-sdk-for-go"
version = "14.0.0"
```

## <a name="include-the-azure-sdk-for-go-in-your-project"></a><span data-ttu-id="7b50f-129">Добавление пакета Azure SDK для Go в проект</span><span class="sxs-lookup"><span data-stu-id="7b50f-129">Include the Azure SDK for Go in your project</span></span>

<span data-ttu-id="7b50f-130">Чтобы использовать службы Azure из кода Go, импортируйте все службы, с которыми вы взаимодействуете, и необходимые модули `autorest`.</span><span class="sxs-lookup"><span data-stu-id="7b50f-130">To use Azure services from your Go code, import any services you interact with and the required `autorest` modules.</span></span>
<span data-ttu-id="7b50f-131">Получить полный список доступных модулей для [доступных служб](https://godoc.org/github.com/Azure/azure-sdk-for-go) и [пакетов AutoRest](https://godoc.org/github.com/Azure/go-autorest) можно на сайте GoDoc.</span><span class="sxs-lookup"><span data-stu-id="7b50f-131">You get a complete list of the available modules from GoDoc for [available services](https://godoc.org/github.com/Azure/azure-sdk-for-go) and [AutoRest packages](https://godoc.org/github.com/Azure/go-autorest).</span></span> <span data-ttu-id="7b50f-132">Ниже приводятся наиболее распространенные пакеты, которые нужно скачать в репозитории `go-autorest`:</span><span class="sxs-lookup"><span data-stu-id="7b50f-132">The most common packages you need from `go-autorest` are:</span></span>

| <span data-ttu-id="7b50f-133">Package</span><span class="sxs-lookup"><span data-stu-id="7b50f-133">Package</span></span> | <span data-ttu-id="7b50f-134">ОПИСАНИЕ</span><span class="sxs-lookup"><span data-stu-id="7b50f-134">Description</span></span> |
|---------|-------------|
| <span data-ttu-id="7b50f-135">[github.com/Azure/go-autorest/autorest][autorest]</span><span class="sxs-lookup"><span data-stu-id="7b50f-135">[github.com/Azure/go-autorest/autorest][autorest]</span></span> | <span data-ttu-id="7b50f-136">Объекты для обработки аутентификации клиента службы</span><span class="sxs-lookup"><span data-stu-id="7b50f-136">Objects for handling service client authentication</span></span> |
| <span data-ttu-id="7b50f-137">[github.com/Azure/go-autorest/autorest/azure][autorest/azure]</span><span class="sxs-lookup"><span data-stu-id="7b50f-137">[github.com/Azure/go-autorest/autorest/azure][autorest/azure]</span></span> | <span data-ttu-id="7b50f-138">Константы для взаимодействия со службами Azure</span><span class="sxs-lookup"><span data-stu-id="7b50f-138">Constants for interactions with Azure services</span></span> |
| <span data-ttu-id="7b50f-139">[github.com/Azure/go-autorest/autorest/adal][autorest/adal]</span><span class="sxs-lookup"><span data-stu-id="7b50f-139">[github.com/Azure/go-autorest/autorest/adal][autorest/adal]</span></span> | <span data-ttu-id="7b50f-140">Механизмы аутентификации для доступа к службам Azure</span><span class="sxs-lookup"><span data-stu-id="7b50f-140">Authentication mechanisms for accessing Azure services</span></span> |
| <span data-ttu-id="7b50f-141">[github.com/Azure/go-autorest/autorest/to][autorest/to]</span><span class="sxs-lookup"><span data-stu-id="7b50f-141">[github.com/Azure/go-autorest/autorest/to][autorest/to]</span></span> | <span data-ttu-id="7b50f-142">Вспомогательные приложения утверждения типа для работы со структурами данных пакета Azure SDK</span><span class="sxs-lookup"><span data-stu-id="7b50f-142">Type assertion helpers for working with Azure SDK data structures</span></span> |

[autorest]: https://godoc.org/github.com/Azure/go-autorest/autorest
[autorest/azure]: https://godoc.org/github.com/Azure/go-autorest/autorest/azure
[autorest/adal]: https://godoc.org/github.com/Azure/go-autorest/autorest/adal
[autorest/to]: https://godoc.org/github.com/Azure/go-autorest/autorest/to

<span data-ttu-id="7b50f-143">Версии пакетов Go и служб Azure управляются независимо друг от друга.</span><span class="sxs-lookup"><span data-stu-id="7b50f-143">Go packages and Azure services are versioned independently.</span></span> <span data-ttu-id="7b50f-144">Версии службы входят в путь импорта модуля (под модулем `services`).</span><span class="sxs-lookup"><span data-stu-id="7b50f-144">The service versions are part of the module import path, underneath the `services` module.</span></span> <span data-ttu-id="7b50f-145">Полный путь к модулю состоит из имени службы, за которым следует версия в формате `YYYY-MM-DD` и снова имя службы.</span><span class="sxs-lookup"><span data-stu-id="7b50f-145">The full path for the module is the name of the service, followed by the version in `YYYY-MM-DD` format, followed by the service name again.</span></span> <span data-ttu-id="7b50f-146">Например, чтобы импортировать версию `2017-03-30` службы вычислений, выполните следующий код:</span><span class="sxs-lookup"><span data-stu-id="7b50f-146">For example, to import the `2017-03-30` version of the Compute service:</span></span>

```go
import "github.com/Azure/azure-sdk-for-go/services/compute/mgmt/2017-03-30/compute"
```

<span data-ttu-id="7b50f-147">При запуске разработки рекомендуется использовать и поддерживать последнюю версию службы.</span><span class="sxs-lookup"><span data-stu-id="7b50f-147">It's recommended that you use the latest version of a service when starting development and keep it consistent.</span></span>
<span data-ttu-id="7b50f-148">Требования службы могут изменяться в разных версиях. Это может привести к ошибкам кода, даже если в это время обновления пакета SDK для Go не выполняются.</span><span class="sxs-lookup"><span data-stu-id="7b50f-148">Service requirements may change between versions that could break your code, even if there are no Go SDK updates during that time.</span></span>

<span data-ttu-id="7b50f-149">Если требуется общий моментальный снимок служб, вы также можете выбрать одну версию профиля.</span><span class="sxs-lookup"><span data-stu-id="7b50f-149">If you need a collective snapshot of services, you can also select a single profile version.</span></span> <span data-ttu-id="7b50f-150">В нашем случае версия `2017-03-09` относится только к заблокированному профилю, который может не содержать последние версии служб и функций.</span><span class="sxs-lookup"><span data-stu-id="7b50f-150">Right now, the only locked profile is version `2017-03-09`, which may not have the latest features of services.</span></span> <span data-ttu-id="7b50f-151">Профили находятся в папке модуля `profiles` вместе с версиями в формате `YYYY-MM-DD`.</span><span class="sxs-lookup"><span data-stu-id="7b50f-151">Profiles are located under the `profiles` module, with their version in the `YYYY-MM-DD` format.</span></span> <span data-ttu-id="7b50f-152">Службы группируются по версиям профиля.</span><span class="sxs-lookup"><span data-stu-id="7b50f-152">Services are grouped under their profile version.</span></span> <span data-ttu-id="7b50f-153">Например, чтобы импортировать модуль управления ресурсами Azure из профиля `2017-03-09`, используйте следующий код:</span><span class="sxs-lookup"><span data-stu-id="7b50f-153">For example, to import the Azure Resources management module from the `2017-03-09` profile:</span></span>

```go
import "github.com/Azure/azure-sdk-for-go/profiles/2017-03-09/resources/mgmt/resources"
```

> [!WARNING]
> <span data-ttu-id="7b50f-154">Существуют также профили `preview` и `latest`.</span><span class="sxs-lookup"><span data-stu-id="7b50f-154">There are also `preview` and `latest` profiles available.</span></span> <span data-ttu-id="7b50f-155">Мы не рекомендуем использовать их.</span><span class="sxs-lookup"><span data-stu-id="7b50f-155">Using them is not recommended.</span></span> <span data-ttu-id="7b50f-156">Это профили промежуточных версий, и поведение службы может измениться в любое время.</span><span class="sxs-lookup"><span data-stu-id="7b50f-156">These profiles are rolling versions and service behavior may change at any time.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7b50f-157">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="7b50f-157">Next steps</span></span>

<span data-ttu-id="7b50f-158">Чтобы начать работу с пакетом Azure SDK для Go, используйте код быстрого запуска.</span><span class="sxs-lookup"><span data-stu-id="7b50f-158">To begin using the Azure SDK for Go, try out a quickstart.</span></span>

* [<span data-ttu-id="7b50f-159">Краткое руководство по развертыванию виртуальной машины Azure из шаблона с помощью пакета Azure SDK для Go</span><span class="sxs-lookup"><span data-stu-id="7b50f-159">Deploy a virtual machine from a template</span></span>](azure-sdk-go-qs-vm.md)
* [<span data-ttu-id="7b50f-160">Передача объектов в хранилище BLOB-объектов Azure и обратно с помощью Go</span><span class="sxs-lookup"><span data-stu-id="7b50f-160">Transfer objects to Azure Blob Storage with the Azure Blob SDK for Go</span></span>](/azure/storage/blobs/storage-quickstart-blobs-go?toc=%2fgo%2fazure%2ftoc.json)
* [<span data-ttu-id="7b50f-161">База данных Azure для PostgreSQL: подключение и запросы данных с помощью языка Go</span><span class="sxs-lookup"><span data-stu-id="7b50f-161">Connect to Azure Database for PostgreSQL</span></span>](/azure/postgresql/connect-go?toc=%2fgo%2fazure%2ftoc.json)

<span data-ttu-id="7b50f-162">Чтобы сразу приступить к работе с другими службами с помощью пакета SDK для Go, ознакомьтесь с доступными примерами кода.</span><span class="sxs-lookup"><span data-stu-id="7b50f-162">If you want to get started with other services in the Go SDK immediately, take a look at some of the available sample code.</span></span>

* [<span data-ttu-id="7b50f-163">Аутентификация с помощью служб Azure</span><span class="sxs-lookup"><span data-stu-id="7b50f-163">Authenticate with Azure services</span></span>](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/internal/iam)
* [<span data-ttu-id="7b50f-164">Развертывание новых виртуальных машин с использованием аутентификации по SSH</span><span class="sxs-lookup"><span data-stu-id="7b50f-164">Deploy new virtual machines with SSH authentication</span></span>](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/compute)
* [<span data-ttu-id="7b50f-165">Развертывание образа контейнера в службе "Экземпляры контейнеров Azure"</span><span class="sxs-lookup"><span data-stu-id="7b50f-165">Deploy a container image to Azure Container Instances</span></span>](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/containerinstance)
* [<span data-ttu-id="7b50f-166">Создание кластера в службе Azure Kubernetes</span><span class="sxs-lookup"><span data-stu-id="7b50f-166">Create a cluster in Azure Kubernetes Service</span></span>](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/containerservice)
* [<span data-ttu-id="7b50f-167">Работа со службами хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="7b50f-167">Work with Azure Storage services</span></span>](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/storage)
* [<span data-ttu-id="7b50f-168">Все примеры для пакета Azure SDK для Go</span><span class="sxs-lookup"><span data-stu-id="7b50f-168">All samples for the Azure SDK for Go</span></span>](https://github.com/azure-samples/azure-sdk-for-go-samples)
