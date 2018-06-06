---
title: Средства для разработчиков Go
description: Средства для работы с пакетом Azure SDK для Go и службами Azure
author: sptramer
ms.author: sttramer
manager: carmonm
ms.date: 01/30/2018
ms.topic: conceptual
ms.prod: azure
ms.technology: azure-sdk-go
ms.devlang: go
ms.openlocfilehash: 1e122ab161766023ea146329a5edb13143699b8b
ms.sourcegitcommit: b81b17cbb934399c195bfdcb87137aee935f5234
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/04/2018
ms.locfileid: "34755538"
---
# <a name="tools-for-developers-using-the-azure-sdk-for-go"></a><span data-ttu-id="2921d-103">Средства для разработчиков, использующих пакет Azure SDK для Go</span><span class="sxs-lookup"><span data-stu-id="2921d-103">Tools for developers using the Azure SDK for Go</span></span>

<span data-ttu-id="2921d-104">Ниже приведены некоторые рекомендуемые средства, которые помогают эффективно писать код Go, а также обеспечивают его совместимость со службами Azure.</span><span class="sxs-lookup"><span data-stu-id="2921d-104">To be effective at writing Go code and have it work seamlessly with Azure services, here are some recommended tools.</span></span>

## <a name="azure-cli-20"></a><span data-ttu-id="2921d-105">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="2921d-105">Azure CLI 2.0</span></span>

<span data-ttu-id="2921d-106">Azure CLI 2.0 предоставляет интерфейс командной строки для создания и настройки ресурсов Azure в подписках.</span><span class="sxs-lookup"><span data-stu-id="2921d-106">The Azure 2.0 CLI provides a command-line interface to create and configure Azure resources in your subscriptions.</span></span> <span data-ttu-id="2921d-107">CLI поможет вам быстро приступить к созданию распространенных и общих ресурсов Azure, чтобы вы могли сосредоточиться на использовании более сложных служб.</span><span class="sxs-lookup"><span data-stu-id="2921d-107">The CLI can help you get started building common and shared Azure resources quickly, so that you can focus on more complex usage of services.</span></span> <span data-ttu-id="2921d-108">CLI содержит функции фильтрации и создания запросов, позволяя передавать выходные данные непосредственно в используемые вами программы командной строки.</span><span class="sxs-lookup"><span data-stu-id="2921d-108">The CLI has query and filtering features so you can pipe output directly to your favorite command-line tools.</span></span> <span data-ttu-id="2921d-109">CLI можно установить в локальной системе как образ Docker или с помощью [Azure Cloud Shell](https://docs.microsoft.com/en-us/azure/cloud-shell/overview).</span><span class="sxs-lookup"><span data-stu-id="2921d-109">The CLI is available for installation on your local system, as a Docker image, or through [Azure Cloud Shell](https://docs.microsoft.com/en-us/azure/cloud-shell/overview).</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2921d-110">Установите Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="2921d-110">Install the Azure CLI 2.0</span></span>](/cli/azure/install-azure-cli)

## <a name="visual-studio-code"></a><span data-ttu-id="2921d-111">Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="2921d-111">Visual Studio Code</span></span>

<span data-ttu-id="2921d-112">Visual Studio Code — это упрощенных редактор, который полностью поддерживает язык Go с помощью расширений.</span><span class="sxs-lookup"><span data-stu-id="2921d-112">Visual Studio Code is a lightweight editor that has comprehensive support for the Go language through extensions.</span></span> <span data-ttu-id="2921d-113">В свою очередь, эти расширения поддерживают такие функции, как автозаполнение, шаблоны `impl`, рефакторинг и отладка.</span><span class="sxs-lookup"><span data-stu-id="2921d-113">These extensions include support for features like autocomplete, `impl` templates, refactoring, and debugging.</span></span> <span data-ttu-id="2921d-114">Visual Studio Code также предлагает разные расширения для распространенных средств, используемых разработчиками (включая систему управления версиями), и даже расширения для непосредственного взаимодействия со службами Azure.</span><span class="sxs-lookup"><span data-stu-id="2921d-114">Visual Studio Code also offers many extensions for common developer tools such as source control, and even offers extensions for direct interactions with Azure services.</span></span> <span data-ttu-id="2921d-115">Корпорация Майкрософт поддерживает официальное метарасширение, содержащее эти расширения Azure, включая интерактивный интерфейс для Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="2921d-115">Microsoft maintains an official meta-extension including these Azure extensions, including an interactive interface for the Azure CLI.</span></span>

* [<span data-ttu-id="2921d-116">Установка Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="2921d-116">Install Visual Studio Code</span></span>](https://code.visualstudio.com/Download)
* [<span data-ttu-id="2921d-117">Получение расширения Go для Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="2921d-117">Get the Visual Studio Code Go extension</span></span>](https://code.visualstudio.com/docs/languages/go)
* [<span data-ttu-id="2921d-118">Получение расширения инструментов Azure</span><span class="sxs-lookup"><span data-stu-id="2921d-118">Get the Azure Tools extension</span></span>](https://marketplace.visualstudio.com/items?itemName=ms-vscode.vscode-azureextensionpack)

## <a name="dependency-management-with-dep"></a><span data-ttu-id="2921d-119">Управление зависимостями с помощью средства dep</span><span class="sxs-lookup"><span data-stu-id="2921d-119">Dependency management with dep</span></span>

<span data-ttu-id="2921d-120">Вы можете разными способами управлять зависимостями пакета и выполнять вендоринг с помощью Go, так как официальное решение пока отсутствует.</span><span class="sxs-lookup"><span data-stu-id="2921d-120">There are many ways to manage your package dependencies and do vendoring with Go, since there is no official solution yet.</span></span> <span data-ttu-id="2921d-121">Для такого управления рекомендуется использовать диспетчер зависимостей `dep`.</span><span class="sxs-lookup"><span data-stu-id="2921d-121">The recommended way to perform this management is with the `dep` dependency manager.</span></span> <span data-ttu-id="2921d-122">Для вендоринга в пакете Azure SDK для Go используется средство dep, что гарантирует правильное получение зависимостей для любого другого проекта с помощью этого средства.</span><span class="sxs-lookup"><span data-stu-id="2921d-122">The Azure SDK for Go uses dep for its vendoring, and is guaranteed to correctly get dependencies for any other project using dep.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2921d-123">Получить диспетчер зависимостей dep</span><span class="sxs-lookup"><span data-stu-id="2921d-123">Get the dep dependency manager</span></span>](https://github.com/tools/godep)