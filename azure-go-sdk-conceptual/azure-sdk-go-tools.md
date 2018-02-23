---
title: "Средства для разработчиков Go"
description: "Средства для работы с пакетом Azure SDK для Go и службами Azure"
keywords: azure, go, golang, azure, visual studio, visual studio code
author: sptramer
ms.author: sttramer
ms.date: 01/30/2018
ms.topic: article
ms.devlang: go
manager: routlaw
ms.openlocfilehash: 4753775e608b39c6da43d64fd08c1532e03d5810
ms.sourcegitcommit: aaa8c37880332625f858a38f5918e6cf581bf48d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/15/2018
---
# <a name="tools-for-developers-using-the-azure-sdk-for-go"></a><span data-ttu-id="47661-104">Средства для разработчиков, использующих пакет Azure SDK для Go</span><span class="sxs-lookup"><span data-stu-id="47661-104">Tools for developers using the Azure SDK for Go</span></span>

<span data-ttu-id="47661-105">Ниже приведены некоторые рекомендуемые средства, которые помогают эффективно писать код Go, а также обеспечивают его совместимость со службами Azure.</span><span class="sxs-lookup"><span data-stu-id="47661-105">To be effective at writing Go code and have it work seamlessly with Azure services, here are some recommended tools.</span></span>

## <a name="azure-cli-20"></a><span data-ttu-id="47661-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="47661-106">Azure CLI 2.0</span></span>

<span data-ttu-id="47661-107">Azure CLI 2.0 предоставляет интерфейс командной строки для создания и настройки ресурсов Azure в подписках.</span><span class="sxs-lookup"><span data-stu-id="47661-107">The Azure 2.0 CLI provides a command-line interface to create and configure Azure resources in your subscriptions.</span></span> <span data-ttu-id="47661-108">CLI поможет вам быстро приступить к созданию распространенных и общих ресурсов Azure, чтобы вы могли сосредоточиться на использовании более сложных служб.</span><span class="sxs-lookup"><span data-stu-id="47661-108">The CLI can help you get started building common and shared Azure resources quickly, so that you can focus on more complex usage of services.</span></span> <span data-ttu-id="47661-109">CLI содержит функции фильтрации и создания запросов, позволяя передавать выходные данные непосредственно в используемые вами программы командной строки.</span><span class="sxs-lookup"><span data-stu-id="47661-109">The CLI has query and filtering features so you can pipe output directly to your favorite command-line tools.</span></span> <span data-ttu-id="47661-110">CLI можно установить в локальной системе как образ Docker или с помощью [Azure Cloud Shell](https://docs.microsoft.com/en-us/azure/cloud-shell/overview).</span><span class="sxs-lookup"><span data-stu-id="47661-110">The CLI is available for installation on your local system, as a Docker image, or through [Azure Cloud Shell](https://docs.microsoft.com/en-us/azure/cloud-shell/overview).</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="47661-111">Установите Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="47661-111">Install the Azure CLI 2.0</span></span>](/cli/azure/install-azure-cli)

## <a name="visual-studio-code"></a><span data-ttu-id="47661-112">Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="47661-112">Visual Studio Code</span></span>

<span data-ttu-id="47661-113">Visual Studio Code — это упрощенных редактор, который полностью поддерживает язык Go с помощью расширений.</span><span class="sxs-lookup"><span data-stu-id="47661-113">Visual Studio Code is a lightweight editor that has comprehensive support for the Go language through extensions.</span></span> <span data-ttu-id="47661-114">В свою очередь, эти расширения поддерживают такие функции, как автозаполнение, шаблоны `impl`, рефакторинг и отладка.</span><span class="sxs-lookup"><span data-stu-id="47661-114">These extensions include support for features like autocomplete, `impl` templates, refactoring, and debugging.</span></span> <span data-ttu-id="47661-115">Visual Studio Code также предлагает разные расширения для распространенных средств, используемых разработчиками (включая систему управления версиями), и даже расширения для непосредственного взаимодействия со службами Azure.</span><span class="sxs-lookup"><span data-stu-id="47661-115">Visual Studio Code also offers many extensions for common developer tools such as source control, and even offers extensions for direct interactions with Azure services.</span></span> <span data-ttu-id="47661-116">Корпорация Майкрософт поддерживает официальное метарасширение, содержащее эти расширения Azure, включая интерактивный интерфейс для Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="47661-116">Microsoft maintains an official meta-extension including these Azure extensions, including an interactive interface for the Azure CLI.</span></span>

* [<span data-ttu-id="47661-117">Установка Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="47661-117">Install Visual Studio Code</span></span>](https://code.visualstudio.com/Download)
* [<span data-ttu-id="47661-118">Получение расширения Go для Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="47661-118">Get the Visual Studio Code Go extension</span></span>](https://code.visualstudio.com/docs/languages/go)
* [<span data-ttu-id="47661-119">Получение расширения инструментов Azure</span><span class="sxs-lookup"><span data-stu-id="47661-119">Get the Azure Tools extension</span></span>](https://marketplace.visualstudio.com/items?itemName=ms-vscode.vscode-azureextensionpack)

## <a name="dependency-management-with-dep"></a><span data-ttu-id="47661-120">Управление зависимостями с помощью средства dep</span><span class="sxs-lookup"><span data-stu-id="47661-120">Dependency management with dep</span></span>

<span data-ttu-id="47661-121">Вы можете разными способами управлять зависимостями пакета и выполнять вендоринг с помощью Go, так как официальное решение пока отсутствует.</span><span class="sxs-lookup"><span data-stu-id="47661-121">There are many ways to manage your package dependencies and do vendoring with Go, since there is no official solution yet.</span></span> <span data-ttu-id="47661-122">Для такого управления рекомендуется использовать диспетчер зависимостей `dep`.</span><span class="sxs-lookup"><span data-stu-id="47661-122">The recommended way to perform this management is with the `dep` dependency manager.</span></span> <span data-ttu-id="47661-123">Для вендоринга в пакете Azure SDK для Go используется средство dep, что гарантирует правильное получение зависимостей для любого другого проекта с помощью этого средства.</span><span class="sxs-lookup"><span data-stu-id="47661-123">The Azure SDK for Go uses dep for its vendoring, and is guaranteed to correctly get dependencies for any other project using dep.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="47661-124">Получить диспетчер зависимостей dep</span><span class="sxs-lookup"><span data-stu-id="47661-124">Get the dep dependency manager</span></span>](https://github.com/tools/godep)

## <a name="telemetry-with-application-insights"></a><span data-ttu-id="47661-125">Телеметрия в Application Insights</span><span class="sxs-lookup"><span data-stu-id="47661-125">Telemetry with Application Insights</span></span>

<span data-ttu-id="47661-126">[Application Insights](https://azure.microsoft.com/en-us/services/application-insights/) — это решение для аналитики, которое позволяет легко собирать данные телеметрии из приложений. Оно интегрируется с экосистемой Azure, Visual Studio Team Services и GitHub.</span><span class="sxs-lookup"><span data-stu-id="47661-126">[Application Insights](https://azure.microsoft.com/en-us/services/application-insights/) is an analytics product that allows you to easily collect telemetry information from your applications and integrates with the Azure ecosystem, Visual Studio Team Services, and GitHub.</span></span> <span data-ttu-id="47661-127">Это решение можно использовать во многих приложениях. Корпорация Майкрософт также предоставляет пакет SDK для Go, который можно использовать с Application Insights.</span><span class="sxs-lookup"><span data-stu-id="47661-127">It can be used in many applications, and Microsoft offers a Go SDK for working with Application Insights.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="47661-128">Получить пакет SDK Application Insights для Go</span><span class="sxs-lookup"><span data-stu-id="47661-128">Get the Application Insights for Go SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-Go) 
