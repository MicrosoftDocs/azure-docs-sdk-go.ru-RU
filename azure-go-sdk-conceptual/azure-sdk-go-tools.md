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
# <a name="tools-for-developers-using-the-azure-sdk-for-go"></a>Средства для разработчиков, использующих пакет Azure SDK для Go

Ниже приведены некоторые рекомендуемые средства, которые помогают эффективно писать код Go, а также обеспечивают его совместимость со службами Azure.

## <a name="azure-cli"></a>Инфраструктура CLI Azure

Azure CLI предоставляет интерфейс командной строки для создания и настройки ресурсов Azure в подписках. CLI поможет вам быстро приступить к созданию распространенных и общих ресурсов Azure, чтобы вы могли сосредоточиться на использовании более сложных служб. CLI содержит функции фильтрации и создания запросов, позволяя передавать выходные данные непосредственно в используемые вами программы командной строки. CLI можно установить в локальной системе как образ Docker или с помощью [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview).

> [!div class="nextstepaction"]
> [Установка Azure CLI](/cli/azure/install-azure-cli)

## <a name="visual-studio-code"></a>Visual Studio Code.

Visual Studio Code — это упрощенных редактор, который полностью поддерживает язык Go с помощью расширений. В свою очередь, эти расширения поддерживают такие функции, как автозаполнение, шаблоны `impl`, рефакторинг и отладка. Visual Studio Code также предлагает разные расширения для распространенных средств, используемых разработчиками (включая систему управления версиями), и даже расширения для непосредственного взаимодействия со службами Azure. Корпорация Майкрософт поддерживает официальное метарасширение, содержащее эти расширения Azure, включая интерактивный интерфейс для Azure CLI.

* [Установка Visual Studio Code](https://code.visualstudio.com/Download)
* [Получение расширения Go для Visual Studio Code](https://code.visualstudio.com/docs/languages/go)
* [Получение расширения инструментов Azure](https://marketplace.visualstudio.com/items?itemName=ms-vscode.vscode-azureextensionpack)

## <a name="cicd-with-azure-devops-project"></a>Использование CI/CD с помощью проекта Azure DevOps

С помощью конвейера проекта DevOps Azure можно настроить непрерывную сборку и развертывание для приложений Go. Все, что вам нужно для развертывания и тестирования ресурсов Azure, — это доступный репозиторий Git. Конвейеры для конфигурирования легко создавать и администрировать. Так как они предоставляются непосредственно в Azure, вы можете управлять им так же, как и другими ресурсами Azure.

> [!div class="nextstepaction"]
> [Создание конвейера CI/CD с помощью проекта Azure DevOps](/devops-project/azure-devops-project-go)

## <a name="dependency-management-with-dep"></a>Управление зависимостями с помощью средства dep

Вы можете разными способами управлять зависимостями пакета и выполнять вендоринг с помощью Go, так как официальное решение пока отсутствует. Для такого управления рекомендуется использовать диспетчер зависимостей `dep`. Для вендоринга в пакете Azure SDK для Go используется средство dep, что гарантирует правильное получение зависимостей для любого другого проекта с помощью этого средства.

> [!div class="nextstepaction"]
> [Получить диспетчер зависимостей dep](https://github.com/golang/dep)
