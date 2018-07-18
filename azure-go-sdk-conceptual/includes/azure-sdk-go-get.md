---
author: sptramer
ms.author: sttramer
manager: carmonm
ms.date: 02/14/2018
ms.topic: include
ms.prod: azure
ms.technology: azure-cli
ms.openlocfilehash: d021dd8ef4744b7c50b296b231bf63481f92411a
ms.sourcegitcommit: 2a3bd491e087a1d0e7d269bed896c029357d62a6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/12/2018
ms.locfileid: "38988074"
---
[Пакет Azure SDK для Go](https://github.com/Azure/azure-sdk-for-go) совместим с Go 1.8 и более поздних версий. Для окружений, в которых используются [профили Azure Stack](https://docs.microsoft.com/azure/azure-stack/azure-stack-version-profiles), требуется Go версии не ниже 1.9.
Если вы еще не установили Go, выполните [инструкции по установке Go](https://golang.org/doc/install).

Вы можете получить пакет Azure SDK для Go и его зависимости с помощью команды `go get`.

```bash
go get -u -d github.com/Azure/azure-sdk-for-go/...
```

> [!WARNING]
> Убедитесь, что в URL-адресе слово `Azure` написано с прописной буквы. В противном случае при работе с пакетом SDK могут возникнуть проблемы импорта, связанные с регистром. `Azure` также нужно указывать с прописной буквы в операторах импорта.
