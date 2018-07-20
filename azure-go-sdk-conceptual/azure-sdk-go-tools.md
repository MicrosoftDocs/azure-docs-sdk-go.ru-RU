---
title: Средства для разработчиков Go
description: Средства для работы с пакетом Azure SDK для Go и службами Azure
author: sptramer
ms.author: sttramer
manager: carmonm
ms.date: 07/13/2018
ms.topic: conceptual
ms.prod: azure
ms.technology: azure-sdk-go
ms.devlang: go
ms.openlocfilehash: dfa3912ac13e6f6d52d607f9dcc150f3a5b57602
ms.sourcegitcommit: d1790b317a8fcb4d672c654dac2a925a976589d4
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/14/2018
ms.locfileid: "39039511"
---
# <a name="tools-for-developers-using-the-azure-sdk-for-go"></a><span data-ttu-id="6585c-103">Средства для разработчиков, использующих пакет Azure SDK для Go</span><span class="sxs-lookup"><span data-stu-id="6585c-103">Tools for developers using the Azure SDK for Go</span></span>

<span data-ttu-id="6585c-104">Ниже приведены некоторые рекомендуемые средства, которые помогают эффективно писать код Go, а также обеспечивают его совместимость со службами Azure.</span><span class="sxs-lookup"><span data-stu-id="6585c-104">To be effective at writing Go code and have it work seamlessly with Azure services, here are some recommended tools.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="6585c-105">Инфраструктура CLI Azure</span><span class="sxs-lookup"><span data-stu-id="6585c-105">Azure CLI</span></span>

<span data-ttu-id="6585c-106">Azure CLI предоставляет интерфейс командной строки для создания и настройки ресурсов Azure в подписках.</span><span class="sxs-lookup"><span data-stu-id="6585c-106">The Azure CLI provides a command-line interface to create and configure Azure resources in your subscriptions.</span></span> <span data-ttu-id="6585c-107">CLI поможет вам быстро приступить к созданию распространенных и общих ресурсов Azure, чтобы вы могли сосредоточиться на использовании более сложных служб.</span><span class="sxs-lookup"><span data-stu-id="6585c-107">The CLI can help you get started building common and shared Azure resources quickly, so that you can focus on more complex usage of services.</span></span> <span data-ttu-id="6585c-108">CLI содержит функции фильтрации и создания запросов, позволяя передавать выходные данные непосредственно в используемые вами программы командной строки.</span><span class="sxs-lookup"><span data-stu-id="6585c-108">The CLI has query and filtering features so you can pipe output directly to your favorite command-line tools.</span></span> <span data-ttu-id="6585c-109">CLI можно установить в локальной системе как образ Docker или с помощью [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview).</span><span class="sxs-lookup"><span data-stu-id="6585c-109">The CLI is available for installation on your local system, as a Docker image, or through [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview).</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6585c-110">Установка Azure CLI</span><span class="sxs-lookup"><span data-stu-id="6585c-110">Install the Azure CLI</span></span>](/cli/azure/install-azure-cli)

## <a name="visual-studio-code"></a><span data-ttu-id="6585c-111">Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="6585c-111">Visual Studio Code</span></span>

<span data-ttu-id="6585c-112">Visual Studio Code — это упрощенных редактор, который полностью поддерживает язык Go с помощью расширений.</span><span class="sxs-lookup"><span data-stu-id="6585c-112">Visual Studio Code is a lightweight editor that has comprehensive support for the Go language through extensions.</span></span> <span data-ttu-id="6585c-113">В свою очередь, эти расширения поддерживают такие функции, как автозаполнение, шаблоны `impl`, рефакторинг и отладка.</span><span class="sxs-lookup"><span data-stu-id="6585c-113">These extensions include support for features like autocomplete, `impl` templates, refactoring, and debugging.</span></span> <span data-ttu-id="6585c-114">Visual Studio Code также предлагает разные расширения для распространенных средств, используемых разработчиками (включая систему управления версиями), и даже расширения для непосредственного взаимодействия со службами Azure.</span><span class="sxs-lookup"><span data-stu-id="6585c-114">Visual Studio Code also offers many extensions for common developer tools such as source control, and even offers extensions for direct interactions with Azure services.</span></span> <span data-ttu-id="6585c-115">Корпорация Майкрософт поддерживает официальное метарасширение, содержащее эти расширения Azure, включая интерактивный интерфейс для Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="6585c-115">Microsoft maintains an official meta-extension including these Azure extensions, including an interactive interface for the Azure CLI.</span></span>

* [<span data-ttu-id="6585c-116">Установка Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="6585c-116">Install Visual Studio Code</span></span>](https://code.visualstudio.com/Download)
* [<span data-ttu-id="6585c-117">Получение расширения Go для Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="6585c-117">Get the Visual Studio Code Go extension</span></span>](https://code.visualstudio.com/docs/languages/go)
* [<span data-ttu-id="6585c-118">Получение расширения инструментов Azure</span><span class="sxs-lookup"><span data-stu-id="6585c-118">Get the Azure Tools extension</span></span>](https://marketplace.visualstudio.com/items?itemName=ms-vscode.vscode-azureextensionpack)

## <a name="cicd-with-azure-devops-project"></a><span data-ttu-id="6585c-119">Использование CI/CD с помощью проекта Azure DevOps</span><span class="sxs-lookup"><span data-stu-id="6585c-119">CI/CD with Azure DevOps Project</span></span>

<span data-ttu-id="6585c-120">С помощью конвейера проекта DevOps Azure можно настроить непрерывную сборку и развертывание для приложений Go.</span><span class="sxs-lookup"><span data-stu-id="6585c-120">With the Azure DevOps Project pipeline, you can set up a continuous build and deploy for your Go applications.</span></span> <span data-ttu-id="6585c-121">Все, что вам нужно для развертывания и тестирования ресурсов Azure, — это доступный репозиторий Git.</span><span class="sxs-lookup"><span data-stu-id="6585c-121">All you need is an available git repo, and you can set up to deploy and test directly on your Azure resources.</span></span> <span data-ttu-id="6585c-122">Конвейеры для конфигурирования легко создавать и администрировать. Так как они предоставляются непосредственно в Azure, вы можете управлять им так же, как и другими ресурсами Azure.</span><span class="sxs-lookup"><span data-stu-id="6585c-122">The configuration pipeline is easy to create and manage, and since it's provisioned directly on Azure, you can control it in the same way that you handle your other Azure resources.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6585c-123">Создание конвейера CI/CD с помощью проекта Azure DevOps</span><span class="sxs-lookup"><span data-stu-id="6585c-123">Learn how to create a CI/CD pipeline with Azure DevOps Project</span></span>](/devops-project/azure-devops-project-go)

## <a name="dependency-management-with-dep"></a><span data-ttu-id="6585c-124">Управление зависимостями с помощью средства dep</span><span class="sxs-lookup"><span data-stu-id="6585c-124">Dependency management with dep</span></span>

<span data-ttu-id="6585c-125">Вы можете разными способами управлять зависимостями пакета и выполнять вендоринг с помощью Go, так как официальное решение пока отсутствует.</span><span class="sxs-lookup"><span data-stu-id="6585c-125">There are many ways to manage your package dependencies and do vendoring with Go, since there is no official solution yet.</span></span> <span data-ttu-id="6585c-126">Для такого управления рекомендуется использовать диспетчер зависимостей `dep`.</span><span class="sxs-lookup"><span data-stu-id="6585c-126">The recommended way to perform this management is with the `dep` dependency manager.</span></span> <span data-ttu-id="6585c-127">Для вендоринга в пакете Azure SDK для Go используется средство dep, что гарантирует правильное получение зависимостей для любого другого проекта с помощью этого средства.</span><span class="sxs-lookup"><span data-stu-id="6585c-127">The Azure SDK for Go uses dep for its vendoring, and is guaranteed to correctly get dependencies for any other project using dep.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6585c-128">Получить диспетчер зависимостей dep</span><span class="sxs-lookup"><span data-stu-id="6585c-128">Get the dep dependency manager</span></span>](https://github.com/golang/dep)
