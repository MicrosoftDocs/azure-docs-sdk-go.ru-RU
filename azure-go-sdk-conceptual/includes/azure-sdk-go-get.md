---
author: sptramer
ms.author: sttramer
manager: carmonm
ms.date: 09/05/2018
ms.topic: include
ms.prod: azure
ms.technology: azure-cli
ms.openlocfilehash: 5df14f939efdd0550b49261c88c8dc6518ada459
ms.sourcegitcommit: 8b9e10b960150dc08f046ab840d6a5627410db29
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/07/2018
ms.locfileid: "44059277"
---
<span data-ttu-id="1ee8e-101">[Пакет Azure SDK для Go](https://github.com/Azure/azure-sdk-for-go) совместим с Go версии 1.8 и выше.</span><span class="sxs-lookup"><span data-stu-id="1ee8e-101">The [Azure SDK for Go](https://github.com/Azure/azure-sdk-for-go) is compatible with Go versions 1.8 and higher.</span></span> <span data-ttu-id="1ee8e-102">Для окружений, в которых используются [профили Azure Stack](/azure/azure-stack/user/azure-stack-version-profiles-go), требуется Go версии не ниже 1.9.</span><span class="sxs-lookup"><span data-stu-id="1ee8e-102">For environments using [Azure Stack Profiles](/azure/azure-stack/user/azure-stack-version-profiles-go), Go version 1.9 is the minimum requirement.</span></span>
<span data-ttu-id="1ee8e-103">Чтобы установить Go, следуйте [соответствующим инструкциям](https://golang.org/doc/install).</span><span class="sxs-lookup"><span data-stu-id="1ee8e-103">If you need to install Go, follow [the Go installation instructions](https://golang.org/doc/install).</span></span>

<span data-ttu-id="1ee8e-104">Вы можете скачать пакет Azure SDK для Go и его зависимости с помощью команды `go get`.</span><span class="sxs-lookup"><span data-stu-id="1ee8e-104">You can download the Azure SDK for Go and its dependencies via `go get`.</span></span>

```bash
go get -u -d github.com/Azure/azure-sdk-for-go/...
```

> [!WARNING]
> <span data-ttu-id="1ee8e-105">Убедитесь, что в URL-адресе слово `Azure` написано с прописной буквы.</span><span class="sxs-lookup"><span data-stu-id="1ee8e-105">Make sure that you capitalize `Azure` in the URL.</span></span> <span data-ttu-id="1ee8e-106">В противном случае при работе с пакетом SDK могут возникнуть проблемы импорта, связанные с регистром.</span><span class="sxs-lookup"><span data-stu-id="1ee8e-106">Doing otherwise can cause case-related import problems when working with the SDK.</span></span> <span data-ttu-id="1ee8e-107">`Azure` также нужно указывать с прописной буквы в операторах импорта.</span><span class="sxs-lookup"><span data-stu-id="1ee8e-107">You also need to capitalize `Azure` in your import statements.</span></span>
