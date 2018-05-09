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
ms.openlocfilehash: 2ea44fb8a4fdd6098bb44d3b5092cfbc352b424d
ms.sourcegitcommit: f08abf902b48f8173aa6e261084ff2cfc9043305
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/03/2018
---
# <a name="tools-for-developers-using-the-azure-sdk-for-go"></a>Средства для разработчиков, использующих пакет Azure SDK для Go

Ниже приведены некоторые рекомендуемые средства, которые помогают эффективно писать код Go, а также обеспечивают его совместимость со службами Azure.

## <a name="azure-cli-20"></a>Azure CLI 2.0

Azure CLI 2.0 предоставляет интерфейс командной строки для создания и настройки ресурсов Azure в подписках. CLI поможет вам быстро приступить к созданию распространенных и общих ресурсов Azure, чтобы вы могли сосредоточиться на использовании более сложных служб. CLI содержит функции фильтрации и создания запросов, позволяя передавать выходные данные непосредственно в используемые вами программы командной строки. CLI можно установить в локальной системе как образ Docker или с помощью [Azure Cloud Shell](https://docs.microsoft.com/en-us/azure/cloud-shell/overview).

> [!div class="nextstepaction"]
> [Установите Azure CLI 2.0](/cli/azure/install-azure-cli)

## <a name="visual-studio-code"></a>Visual Studio Code.

Visual Studio Code — это упрощенных редактор, который полностью поддерживает язык Go с помощью расширений. В свою очередь, эти расширения поддерживают такие функции, как автозаполнение, шаблоны `impl`, рефакторинг и отладка. Visual Studio Code также предлагает разные расширения для распространенных средств, используемых разработчиками (включая систему управления версиями), и даже расширения для непосредственного взаимодействия со службами Azure. Корпорация Майкрософт поддерживает официальное метарасширение, содержащее эти расширения Azure, включая интерактивный интерфейс для Azure CLI.

* [Установка Visual Studio Code](https://code.visualstudio.com/Download)
* [Получение расширения Go для Visual Studio Code](https://code.visualstudio.com/docs/languages/go)
* [Получение расширения инструментов Azure](https://marketplace.visualstudio.com/items?itemName=ms-vscode.vscode-azureextensionpack)

## <a name="dependency-management-with-dep"></a>Управление зависимостями с помощью средства dep

Вы можете разными способами управлять зависимостями пакета и выполнять вендоринг с помощью Go, так как официальное решение пока отсутствует. Для такого управления рекомендуется использовать диспетчер зависимостей `dep`. Для вендоринга в пакете Azure SDK для Go используется средство dep, что гарантирует правильное получение зависимостей для любого другого проекта с помощью этого средства.

> [!div class="nextstepaction"]
> [Получить диспетчер зависимостей dep](https://github.com/tools/godep)

## <a name="telemetry-with-application-insights"></a>Телеметрия в Application Insights

[Application Insights](https://azure.microsoft.com/en-us/services/application-insights/) — это решение для аналитики, которое позволяет легко собирать данные телеметрии из приложений. Оно интегрируется с экосистемой Azure, Visual Studio Team Services и GitHub. Это решение можно использовать во многих приложениях. Корпорация Майкрософт также предоставляет пакет SDK для Go, который можно использовать с Application Insights.

> [!div class="nextstepaction"]
> [Получить пакет SDK Application Insights для Go](https://github.com/Microsoft/ApplicationInsights-Go) 
