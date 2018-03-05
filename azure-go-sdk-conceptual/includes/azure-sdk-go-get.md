<span data-ttu-id="36790-101">[Пакет Azure SDK для Go](https://github.com/Azure/azure-sdk-for-go) совместим с Go 1.8 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="36790-101">The [Azure SDK for Go](https://github.com/Azure/azure-sdk-for-go) is compatible with Go versions 1.8 and later.</span></span> <span data-ttu-id="36790-102">Для окружений, в которых используются [профили Azure Stack](https://docs.microsoft.com/en-us/azure/azure-stack/azure-stack-version-profiles), требуется Go версии не ниже 1.9.</span><span class="sxs-lookup"><span data-stu-id="36790-102">For environments using [Azure Stack Profiles](https://docs.microsoft.com/en-us/azure/azure-stack/azure-stack-version-profiles), Go version 1.9 is the minimum requirement.</span></span>
<span data-ttu-id="36790-103">Если вы еще не установили Go, выполните [инструкции по установке Go](https://golang.org/doc/install).</span><span class="sxs-lookup"><span data-stu-id="36790-103">If you do not have Go available on your system, follow [the Go installation instructions](https://golang.org/doc/install).</span></span>

<span data-ttu-id="36790-104">Вы можете получить пакет Azure SDK для Go и его зависимости с помощью команды `go get`.</span><span class="sxs-lookup"><span data-stu-id="36790-104">You can obtain the Azure SDK for Go and its dependencies via `go get`.</span></span>

```bash
go get -u -d github.com/Azure/azure-sdk-for-go/...
```

> [!WARNING]
> <span data-ttu-id="36790-105">Убедитесь, что в URL-адресе слово `Azure` написано с прописной буквы.</span><span class="sxs-lookup"><span data-stu-id="36790-105">Make sure that you capitalize `Azure` in the URL.</span></span> <span data-ttu-id="36790-106">В противном случае при работе с пакетом SDK могут возникнуть проблемы импорта, связанные с регистром.</span><span class="sxs-lookup"><span data-stu-id="36790-106">Doing otherwise can cause case-related import problems when working with the SDK.</span></span> <span data-ttu-id="36790-107">`Azure` также нужно указывать с прописной буквы в операторах импорта.</span><span class="sxs-lookup"><span data-stu-id="36790-107">You also need to capitalize `Azure` in your import statements.</span></span>

