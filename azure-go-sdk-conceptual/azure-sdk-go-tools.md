---
title: Средства для разработчиков, использующих пакет Azure SDK для Go
description: Средства для работы с пакетом Azure SDK для Go и службами Azure
author: sptramer
ms.author: sttramer
manager: carmonm
ms.date: 09/05/2018
ms.topic: conceptual
ms.prod: azure
ms.technology: azure-sdk-go
ms.devlang: go
ms.openlocfilehash: 70cf7d645f47df29e8e42599a0acd75858144783
ms.sourcegitcommit: 8b9e10b960150dc08f046ab840d6a5627410db29
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/07/2018
ms.locfileid: "44059209"
---
# <a name="tools-for-developers-using-the-azure-sdk-for-go"></a><span data-ttu-id="adfd6-103">Средства для разработчиков, использующих пакет Azure SDK для Go</span><span class="sxs-lookup"><span data-stu-id="adfd6-103">Tools for developers using the Azure SDK for Go</span></span>

<span data-ttu-id="adfd6-104">Ниже приведены некоторые рекомендуемые средства, которые помогают эффективно писать код Go, а также обеспечивают его совместимость со службами Azure.</span><span class="sxs-lookup"><span data-stu-id="adfd6-104">To be effective at writing Go code and have it work seamlessly with Azure services, here are some recommended tools.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="adfd6-105">Инфраструктура CLI Azure</span><span class="sxs-lookup"><span data-stu-id="adfd6-105">Azure CLI</span></span>

<span data-ttu-id="adfd6-106">Azure CLI предоставляет интерфейс командной строки для создания и настройки ресурсов Azure в подписках.</span><span class="sxs-lookup"><span data-stu-id="adfd6-106">The Azure CLI provides a command-line interface to create and configure Azure resources in your subscriptions.</span></span> <span data-ttu-id="adfd6-107">CLI поможет вам быстро приступить к созданию распространенных и общих ресурсов Azure, чтобы вы могли сосредоточиться на использовании более сложных служб.</span><span class="sxs-lookup"><span data-stu-id="adfd6-107">The CLI can help you get started building common and shared Azure resources quickly, so that you can focus on more complex usage of services.</span></span> <span data-ttu-id="adfd6-108">CLI содержит функции фильтрации и создания запросов, позволяя передавать выходные данные непосредственно в используемые вами программы командной строки.</span><span class="sxs-lookup"><span data-stu-id="adfd6-108">The CLI has query and filtering features so you can pipe output directly to your favorite command-line tools.</span></span> <span data-ttu-id="adfd6-109">CLI можно установить в локальной системе как образ Docker или с помощью [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview).</span><span class="sxs-lookup"><span data-stu-id="adfd6-109">The CLI is available for installation on your local system, as a Docker image, or through [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview).</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="adfd6-110">Установка Azure CLI</span><span class="sxs-lookup"><span data-stu-id="adfd6-110">Install the Azure CLI</span></span>](/cli/azure/install-azure-cli)

## <a name="visual-studio-code"></a><span data-ttu-id="adfd6-111">Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="adfd6-111">Visual Studio Code</span></span>

<span data-ttu-id="adfd6-112">Visual Studio Code — это упрощенный редактор, который поддерживает Go.</span><span class="sxs-lookup"><span data-stu-id="adfd6-112">Visual Studio Code is a lightweight editor that offers Go support.</span></span> <span data-ttu-id="adfd6-113">Это расширение поддерживает такие функции, как автозаполнение, шаблоны `impl`, рефакторинг и отладка.</span><span class="sxs-lookup"><span data-stu-id="adfd6-113">This extension offers features like autocomplete, `impl` templates, refactoring, and debugging.</span></span> <span data-ttu-id="adfd6-114">Visual Studio Code также предоставляет доступ к системе управления версиями из редактора, а также включает расширения для работы со службами Azure.</span><span class="sxs-lookup"><span data-stu-id="adfd6-114">Visual Studio Code also offers support for in-editor access to source control, and extensions for working with Azure services.</span></span>

* [<span data-ttu-id="adfd6-115">Установка Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="adfd6-115">Install Visual Studio Code</span></span>](https://code.visualstudio.com/Download)
* [<span data-ttu-id="adfd6-116">Получение расширения Go для Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="adfd6-116">Get the Visual Studio Code Go extension</span></span>](https://code.visualstudio.com/docs/languages/go)
* [<span data-ttu-id="adfd6-117">Получение расширения "Инструменты Azure" для Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="adfd6-117">Get the Visual Studio Code Azure Tools extension</span></span>](https://marketplace.visualstudio.com/items?itemName=ms-vscode.vscode-azureextensionpack)

## <a name="cicd-with-azure-devops-project"></a><span data-ttu-id="adfd6-118">Использование CI/CD с помощью проекта Azure DevOps</span><span class="sxs-lookup"><span data-stu-id="adfd6-118">CI/CD with Azure DevOps Project</span></span>

<span data-ttu-id="adfd6-119">С помощью конвейеров проекта DevOps Azure можно настроить систему непрерывной интеграции для приложений Go.</span><span class="sxs-lookup"><span data-stu-id="adfd6-119">Azure DevOps Project pipelines allow you to set up a continuous integration system for your Go applications.</span></span> <span data-ttu-id="adfd6-120">Все что вам нужно — это репозиторий Git. Это позволит вам выполнять развертывание и тестирование непосредственно в Azure.</span><span class="sxs-lookup"><span data-stu-id="adfd6-120">All it takes is a git repo, and you can deploy and test directly on Azure.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="adfd6-121">Создание конвейера CI/CD с помощью проекта Azure DevOps</span><span class="sxs-lookup"><span data-stu-id="adfd6-121">Learn how to create a CI/CD pipeline with Azure DevOps Project</span></span>](/azure/devops-project/azure-devops-project-go)

## <a name="dependency-management-with-dep"></a><span data-ttu-id="adfd6-122">Управление зависимостями с помощью средства dep</span><span class="sxs-lookup"><span data-stu-id="adfd6-122">Dependency management with dep</span></span>

<span data-ttu-id="adfd6-123">Пакет Azure SDK для Go использует средство dep для управления зависимостями.</span><span class="sxs-lookup"><span data-stu-id="adfd6-123">The Azure SDK for Go uses dep for dependency management.</span></span> <span data-ttu-id="adfd6-124">Команда dep позволяет выполнять вытягивание и вендоринг требований для приложения Go, предотвращая появление конфликтов версий и обеспечивая правильную работу проектов.</span><span class="sxs-lookup"><span data-stu-id="adfd6-124">The dep command allows you to pull and vendor requirements for your Go application, avoiding version conflicts and ensuring that your project works correctly.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="adfd6-125">Получить диспетчер зависимостей dep</span><span class="sxs-lookup"><span data-stu-id="adfd6-125">Get the dep dependency manager</span></span>](https://github.com/golang/dep)
