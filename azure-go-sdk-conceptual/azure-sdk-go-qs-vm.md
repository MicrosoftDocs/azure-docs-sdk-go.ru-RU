---
title: Развертывание виртуальной машины Azure с помощью Go
description: Разверните виртуальную машину с помощью пакета Azure SDK для Go.
author: sptramer
ms.author: sttramer
manager: carmonm
ms.date: 04/03/2018
ms.topic: quickstart
ms.prod: azure
ms.technology: azure-sdk-go
ms.service: virtual-machines
ms.devlang: go
ms.openlocfilehash: 1fbcc54df2a2aebce56c5a5800361f3d3aed1ccc
ms.sourcegitcommit: f08abf902b48f8173aa6e261084ff2cfc9043305
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/03/2018
---
# <a name="quickstart-deploy-an-azure-virtual-machine-from-a-template-with-the-azure-sdk-for-go"></a><span data-ttu-id="28735-103">Краткое руководство по развертыванию виртуальной машины Azure из шаблона с помощью пакета Azure SDK для Go</span><span class="sxs-lookup"><span data-stu-id="28735-103">Quickstart: Deploy an Azure virtual machine from a template with the Azure SDK for Go</span></span>

<span data-ttu-id="28735-104">В этом кратком руководстве описано, как развертывать ресурсы из шаблона с помощью пакета Azure SDK для Go.</span><span class="sxs-lookup"><span data-stu-id="28735-104">This quickstart focuses on deploying resources from a template with the Azure SDK for Go.</span></span> <span data-ttu-id="28735-105">Шаблоны — это моментальные снимки всех ресурсов, содержащихся в [группе ресурсов Azure](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview).</span><span class="sxs-lookup"><span data-stu-id="28735-105">Templates are snapshots of all of the resources contained within an [Azure resource group](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview).</span></span> <span data-ttu-id="28735-106">Выполняя эту задачу, вы также ознакомитесь с функциями и соглашениями пакета SDK.</span><span class="sxs-lookup"><span data-stu-id="28735-106">Along the way, you'll become familiar with the functionality and conventions of the SDK while performing a useful task.</span></span>

<span data-ttu-id="28735-107">По завершении работы с этим кратким руководством у вас будет запущенная виртуальная машина, в которую можно войти с помощью имени пользователя и пароля.</span><span class="sxs-lookup"><span data-stu-id="28735-107">At the end of this quickstart, you have a running VM that you log into with a username and password.</span></span>

[!INCLUDE [quickstarts-free-trial-note](includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](includes/cloud-shell-try-it.md)]

<span data-ttu-id="28735-108">Если используется интерфейс Azure CLI, установленный локально, для этого краткого руководства нужно установить CLI __2.0.28__ или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="28735-108">If you use a local install of the Azure CLI, this quickstart requires CLI version __2.0.28__ or later.</span></span> <span data-ttu-id="28735-109">Выполните команду `az --version`, чтобы убедиться, что установленный CLI соответствует этому требованию.</span><span class="sxs-lookup"><span data-stu-id="28735-109">Run `az --version` to make sure your CLI install meets this requirement.</span></span> <span data-ttu-id="28735-110">Если вам необходимо выполнить установку или обновление, см. статью [Установка Azure CLI 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="28735-110">If you need to install or upgrade, see [Install the Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span>

## <a name="install-the-azure-sdk-for-go"></a><span data-ttu-id="28735-111">Установка пакета Azure SDK для Go</span><span class="sxs-lookup"><span data-stu-id="28735-111">Install the Azure SDK for Go</span></span> 

[!INCLUDE [azure-sdk-go-get](includes/azure-sdk-go-get.md)]

## <a name="create-a-service-principal"></a><span data-ttu-id="28735-112">Создание субъекта-службы</span><span class="sxs-lookup"><span data-stu-id="28735-112">Create a service principal</span></span>


<span data-ttu-id="28735-113">Чтобы войти в систему не в интерактивном режиме с помощью приложения, вам понадобится субъект-служба.</span><span class="sxs-lookup"><span data-stu-id="28735-113">To log in non-interactively with an application, you need a service principal.</span></span> <span data-ttu-id="28735-114">Субъекты-службы помогают выполнять управление доступом на основе ролей, что предусматривает создание уникальных удостоверений пользователя.</span><span class="sxs-lookup"><span data-stu-id="28735-114">Service principals are part of role-based access control (RBAC), which creates a unique user identity.</span></span> <span data-ttu-id="28735-115">Чтобы создать субъект-службу с помощью CLI, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="28735-115">To create a new service principal with the CLI, run the following command:</span></span>

```azurecli-interactive
az ad sp create-for-rbac --name az-go-vm-quickstart --sdk-auth > quickstart.auth
```

<span data-ttu-id="28735-116">Задайте в переменной среды `AZURE_AUTH_LOCATION` полный путь к этому файлу.</span><span class="sxs-lookup"><span data-stu-id="28735-116">Set the environment variable `AZURE_AUTH_LOCATION` to be the full path to this file.</span></span> <span data-ttu-id="28735-117">Пакет SDK находит и считывает учетные данные непосредственно из этого файла. Вам не нужно вносить изменения или записывать информацию, полученную от субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="28735-117">Then the SDK locates and reads the credentials directly from this file, without you having to make any changes or record information from the service principal.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="28735-118">Получение кода</span><span class="sxs-lookup"><span data-stu-id="28735-118">Get the code</span></span>

<span data-ttu-id="28735-119">Получите пример кода и все его зависимости с помощью команды `go get`.</span><span class="sxs-lookup"><span data-stu-id="28735-119">Get the quickstart code and all of its dependencies with `go get`.</span></span>

```bash
go get -u -d github.com/azure-samples/azure-sdk-for-go-samples/quickstarts/deploy-vm/...
```

<span data-ttu-id="28735-120">Если переменная `AZURE_AUTH_LOCATION` правильно установлена, изменять исходный код не нужно.</span><span class="sxs-lookup"><span data-stu-id="28735-120">You don't need to make any source code modifications if the `AZURE_AUTH_LOCATION` variable is properly set.</span></span> <span data-ttu-id="28735-121">При выполнении программы из переменной загружаются все необходимые данные для аутентификации.</span><span class="sxs-lookup"><span data-stu-id="28735-121">When the program runs, it loads all the necessary authentication information from there.</span></span>

## <a name="running-the-code"></a><span data-ttu-id="28735-122">Выполнение кода</span><span class="sxs-lookup"><span data-stu-id="28735-122">Running the code</span></span>

<span data-ttu-id="28735-123">Выполните код быстрого запуска с помощью команды `go run`.</span><span class="sxs-lookup"><span data-stu-id="28735-123">Run the quickstart with the `go run` command.</span></span>

```bash
cd $GOPATH/src/github.com/azure-samples/azure-sdk-for-go-samples/quickstarts/deploy-vm
go run main.go
```

<span data-ttu-id="28735-124">Если при развертывании произойдет сбой, вы получите сообщение о том, что возникла проблема. Но в нем могут отсутствовать подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="28735-124">If there is a failure in the deployment, you get a message indicating that there was an issue, but it may not include enough detail.</span></span> <span data-ttu-id="28735-125">Получите подробные сведения о сбое развертывания с помощью следующей команды Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="28735-125">Using the Azure CLI, get the full details of the deployment failure with the following command:</span></span>

```azurecli-interactive
az group deployment show -g GoVMQuickstart -n VMDeployQuickstart
```

<span data-ttu-id="28735-126">При успешном развертывании появится сообщение с именем пользователя, IP-адресом и паролем для входа в только что созданную виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="28735-126">If the deployment is successful, you see a message giving the username, IP address, and password for logging into the newly created virtual machine.</span></span> <span data-ttu-id="28735-127">Чтобы убедиться в работоспособности виртуальной машины, подключитесь к ней по протоколу SSH.</span><span class="sxs-lookup"><span data-stu-id="28735-127">SSH into this machine to confirm that it is up and running.</span></span>

## <a name="cleaning-up"></a><span data-ttu-id="28735-128">Очистка.</span><span class="sxs-lookup"><span data-stu-id="28735-128">Cleaning up</span></span>

<span data-ttu-id="28735-129">Чтобы очистить ресурсы, созданные при работе с этим кратким руководством, удалите группу ресурсов с помощью CLI.</span><span class="sxs-lookup"><span data-stu-id="28735-129">Clean up the resources created during this quickstart by deleting the resource group with the CLI.</span></span>

```azurecli-interactive
az group delete -n GoVMQuickstart
```

## <a name="code-in-depth"></a><span data-ttu-id="28735-130">Подробные сведения о коде</span><span class="sxs-lookup"><span data-stu-id="28735-130">Code in depth</span></span>

<span data-ttu-id="28735-131">Все операции в коде быстрого запуска состоят из блоков переменных и нескольких небольших функций. Все они рассматриваются в этой статье.</span><span class="sxs-lookup"><span data-stu-id="28735-131">What the quickstart code does is broken down into a block of variables and several small functions, each of which are discussed here.</span></span>

### <a name="variables-constants-and-types"></a><span data-ttu-id="28735-132">Переменные, константы и типы</span><span class="sxs-lookup"><span data-stu-id="28735-132">Variables, constants, and types</span></span>

<span data-ttu-id="28735-133">Это краткое руководство является автономным документом, и в нем используются глобальные константы и переменные.</span><span class="sxs-lookup"><span data-stu-id="28735-133">Since quickstart is self-contained, it uses global constants and variables.</span></span>

```go
const (
    resourceGroupName     = "GoVMQuickstart"
    resourceGroupLocation = "eastus"

    deploymentName = "VMDeployQuickstart"
    templateFile   = "vm-quickstart-template.json"
    parametersFile = "vm-quickstart-params.json"
)

// Information loaded from the authorization file to identify the client
type clientInfo struct {
    SubscriptionID string
    VMPassword     string
}

var (
    ctx        = context.Background()
    clientData clientInfo
    authorizer autorest.Authorizer
)
```

<span data-ttu-id="28735-134">Значения объявляются, чтобы присвоить имена созданным ресурсам.</span><span class="sxs-lookup"><span data-stu-id="28735-134">Values are declared which give the names of created resources.</span></span> <span data-ttu-id="28735-135">Здесь также указывается расположение, которое можно изменить, чтобы понять, как выполняются развертывания в других центрах обработки данных.</span><span class="sxs-lookup"><span data-stu-id="28735-135">The location is also specified here, which you can change to see how deployments behave in other datacenters.</span></span> <span data-ttu-id="28735-136">Не в каждом центре обработки данных доступны все необходимые ресурсы.</span><span class="sxs-lookup"><span data-stu-id="28735-136">Not every datacenter has all of the required resources available.</span></span>

<span data-ttu-id="28735-137">Тип `clientInfo` объявлен для инкапсуляции всех данных, которые должны независимо загружаться из файла аутентификации, чтобы настроить клиенты в пакете SDK и установить пароль для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="28735-137">The `clientInfo` type is declared to encapsulate all of the information that must be independently loaded from the authentication file to set up clients in the SDK and set the VM password.</span></span>

<span data-ttu-id="28735-138">Константы `templateFile` и `parametersFile` указывают на файлы, необходимые для развертывания.</span><span class="sxs-lookup"><span data-stu-id="28735-138">The `templateFile` and `parametersFile` constants point to the files needed for deployment.</span></span> <span data-ttu-id="28735-139">`authorizer` настраивается для аутентификации с помощью пакета SDK для Go. Переменная `ctx` — это [контекст Go](https://blog.golang.org/context) для сетевых операций.</span><span class="sxs-lookup"><span data-stu-id="28735-139">The `authorizer` will be configured by the Go SDK for authentication, and the `ctx` variable is a [Go context](https://blog.golang.org/context) for the network operations.</span></span>

### <a name="authentication-and-initialization"></a><span data-ttu-id="28735-140">Аутентификация и инициализация</span><span class="sxs-lookup"><span data-stu-id="28735-140">Authentication and initialization</span></span>

<span data-ttu-id="28735-141">Функция `init` отвечает за настройку аутентификации.</span><span class="sxs-lookup"><span data-stu-id="28735-141">The `init` function sets up authentication.</span></span> <span data-ttu-id="28735-142">Так как аутентификации является необходимым условием для всех операций в коде быстрого запуска, целесообразно включить ее в инициализацию.</span><span class="sxs-lookup"><span data-stu-id="28735-142">Since authentication is a precondition for everything in the quickstart, it makes sense to have it as part of initialization.</span></span> <span data-ttu-id="28735-143">Кроме того, из файла аутентификации загружаются определенные сведения, необходимые для настройки клиентов и виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="28735-143">It also loads some information needed from the authentication file to configure clients and the VM.</span></span>

```go
func init() {
    var err error
    authorizer, err = auth.NewAuthorizerFromFile(azure.PublicCloud.ResourceManagerEndpoint)
    if err != nil {
        log.Fatalf("Failed to get OAuth config: %v", err)
    }

    authInfo, err := readJSON(os.Getenv("AZURE_AUTH_LOCATION"))
    clientData.SubscriptionID = (*authInfo)["subscriptionId"].(string)
    clientData.VMPassword = (*authInfo)["clientSecret"].(string)
}
```

<span data-ttu-id="28735-144">Сначала вызывается [auth.NewAuthorizerFromFile](https://godoc.org/github.com/Azure/go-autorest/autorest/azure/auth#NewAuthorizerFromFile), чтобы загрузить данные для аутентификации из файла в расположении `AZURE_AUTH_LOCATION`.</span><span class="sxs-lookup"><span data-stu-id="28735-144">First, [auth.NewAuthorizerFromFile](https://godoc.org/github.com/Azure/go-autorest/autorest/azure/auth#NewAuthorizerFromFile) is called to load the authentication information from the file located at `AZURE_AUTH_LOCATION`.</span></span> <span data-ttu-id="28735-145">Затем этот файл вручную загружается с помощью функции `readJSON` (здесь не описана), чтобы извлечь два значения, необходимые для запуска оставшейся части программы: идентификатор подписки клиента и секрет субъекта-службы, который также используется для пароля виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="28735-145">Next, this file is loaded manually by the `readJSON` function (omitted here) to pull the two values needed to run the rest of the program: The subscription ID of the client, and the service principal's secret, which is also used for the VM's password.</span></span>

> [!WARNING]
> <span data-ttu-id="28735-146">Для упрощения пароль субъекта-службы используется повторно.</span><span class="sxs-lookup"><span data-stu-id="28735-146">To keep the quickstart simple, the service principal password is reused.</span></span> <span data-ttu-id="28735-147">__Ни в коем случае__ не используйте пароль, который предоставляет доступ к вашим ресурсам Azure, повторно в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="28735-147">In production, take care to __never__ reuse a password which gives access to your Azure resources.</span></span>

### <a name="flow-of-operations-in-main"></a><span data-ttu-id="28735-148">Последовательность операций в функции main()</span><span class="sxs-lookup"><span data-stu-id="28735-148">Flow of operations in main()</span></span>

<span data-ttu-id="28735-149">`main` — это простая функция, которая только определяет последовательность операций и выполняет проверку ошибок.</span><span class="sxs-lookup"><span data-stu-id="28735-149">The `main` function is simple, only indicating the flow of operations and performing error-checking.</span></span>

```go
func main() {
    group, err := createGroup()
    if err != nil {
        log.Fatalf("failed to create group: %v", err)
    }
    log.Printf("Created group: %v", *group.Name)

    log.Printf("Starting deployment: %s", deploymentName)
    result, err := createDeployment()
    if err != nil {
        log.Fatalf("Failed to deploy: %v", err)
    }
    if result.Name != nil {
        log.Printf("Completed deployment %v: %v", deploymentName, *result.Properties.ProvisioningState)
    } else {
        log.Printf("Completed deployment %v (no data returned to SDK)", deploymentName)
    }
    getLogin()
}
```

<span data-ttu-id="28735-150">Действия выполняются в коде в следующем порядке:</span><span class="sxs-lookup"><span data-stu-id="28735-150">The steps that the code runs through are, in order:</span></span>

* <span data-ttu-id="28735-151">создание группы ресурсов, в которую будет выполняться развертывание (`createGroup`);</span><span class="sxs-lookup"><span data-stu-id="28735-151">Create the resource group to deploy to (`createGroup`)</span></span>
* <span data-ttu-id="28735-152">создание развертывания в этой группе (`createDeployment`);</span><span class="sxs-lookup"><span data-stu-id="28735-152">Create the deployment within this group (`createDeployment`)</span></span>
* <span data-ttu-id="28735-153">получение и вывод информации для входа в развернутую виртуальную машину (`getLogin`).</span><span class="sxs-lookup"><span data-stu-id="28735-153">Obtain and display login information for the deployed VM (`getLogin`)</span></span>

### <a name="creating-the-resource-group"></a><span data-ttu-id="28735-154">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="28735-154">Creating the resource group</span></span>

<span data-ttu-id="28735-155">Функция `createGroup` создает группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="28735-155">The `createGroup` function creates the resource group.</span></span> <span data-ttu-id="28735-156">При работе с последовательностью вызова и аргументами можно увидеть, как структурируются взаимодействия служб в пакете SDK.</span><span class="sxs-lookup"><span data-stu-id="28735-156">Looking at the call flow and arguments demonstrates the way that service interactions are structured in the SDK.</span></span>

```go
func createGroup() (group resources.Group, err error) {
    groupsClient := resources.NewGroupsClient(clientData.SubscriptionID)
    groupsClient.Authorizer = authorizer

        return groupsClient.CreateOrUpdate(
                ctx,
                resourceGroupName,
                resources.Group{
                        Location: to.StringPtr(resourceGroupLocation)})
}
```

<span data-ttu-id="28735-157">Общая последовательность взаимодействия со службой Azure:</span><span class="sxs-lookup"><span data-stu-id="28735-157">The general flow of interacting with an Azure service is:</span></span>

* <span data-ttu-id="28735-158">Создайте клиент, используя метод `service.New*Client()`, где `*` — это тип ресурса для объекта `service`, с которым нужно взаимодействовать.</span><span class="sxs-lookup"><span data-stu-id="28735-158">Create the client using the `service.New*Client()` method, where `*` is the resource type of the `service` that you want to interact with.</span></span> <span data-ttu-id="28735-159">Эта функция всегда принимает идентификатор подписки.</span><span class="sxs-lookup"><span data-stu-id="28735-159">This function always takes a subscription ID.</span></span>
* <span data-ttu-id="28735-160">Задайте метод авторизации для клиента, чтобы он мог взаимодействовать с удаленным API.</span><span class="sxs-lookup"><span data-stu-id="28735-160">Set the authorization method for the client, allowing it to interact with the remote API.</span></span>
* <span data-ttu-id="28735-161">Используя метод, вызовите клиент, соответствующий удаленному API.</span><span class="sxs-lookup"><span data-stu-id="28735-161">Make the method call on the client corresponding to the remote API.</span></span> <span data-ttu-id="28735-162">Как правило, методы клиента службы принимают имя ресурса и объект метаданных.</span><span class="sxs-lookup"><span data-stu-id="28735-162">Service client methods usually take the name of the resource and a metadata object.</span></span>

<span data-ttu-id="28735-163">В этом коде функция [`to.StringPtr`](https://godoc.org/github.com/Azure/go-autorest/autorest/to#StringPtr) используется для преобразования типа.</span><span class="sxs-lookup"><span data-stu-id="28735-163">The [`to.StringPtr`](https://godoc.org/github.com/Azure/go-autorest/autorest/to#StringPtr) function is used to perform a type conversion here.</span></span> <span data-ttu-id="28735-164">Так как параметры для методов пакета SDK используют только указатели, чтобы упростить преобразования типов, предоставляются вспомогательные методы.</span><span class="sxs-lookup"><span data-stu-id="28735-164">The parameters for SDK methods almost exclusively take pointers, so convenience methods are provided to make the type conversions easy.</span></span> <span data-ttu-id="28735-165">Полный список вспомогательных преобразователей и их функций см. в документации по модулю [autorest/to](https://godoc.org/github.com/Azure/go-autorest/autorest/to).</span><span class="sxs-lookup"><span data-stu-id="28735-165">See the documentation for the [autorest/to](https://godoc.org/github.com/Azure/go-autorest/autorest/to) module for the complete list of convenience converters and their behavior.</span></span>

<span data-ttu-id="28735-166">Метод `groupsClient.CreateOrUpdate` возвращает указатель для типа данных, представляющей группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="28735-166">The `groupsClient.CreateOrUpdate` method returns a pointer to a data type representing the resource group.</span></span> <span data-ttu-id="28735-167">Возвращаемое напрямую значение такого типа указывает на быстро выполняющуюся операцию, которая должна быть синхронной.</span><span class="sxs-lookup"><span data-stu-id="28735-167">A direct return value of this kind indicates a short-running operation that is meant to be synchronous.</span></span> <span data-ttu-id="28735-168">В следующем разделе приводится пример долго выполняющейся операции и описываются способы взаимодействия с ней.</span><span class="sxs-lookup"><span data-stu-id="28735-168">In the next section, you'll see an example of a long-running operation and how to interact with it.</span></span>

### <a name="performing-the-deployment"></a><span data-ttu-id="28735-169">Выполнение развертывания</span><span class="sxs-lookup"><span data-stu-id="28735-169">Performing the deployment</span></span>

<span data-ttu-id="28735-170">Когда группа ресурсов будет создана, можно перейти к развертыванию.</span><span class="sxs-lookup"><span data-stu-id="28735-170">Once the resource group is created, it's time to run the deployment.</span></span> <span data-ttu-id="28735-171">Этот код разделен на небольшие разделы в соответствии с его логикой.</span><span class="sxs-lookup"><span data-stu-id="28735-171">This code is broken up into smaller sections to emphasize different parts of its logic.</span></span>

```go
func createDeployment() (deployment resources.DeploymentExtended, err error) {
    template, err := readJSON(templateFile)
    if err != nil {
        return
    }
    params, err := readJSON(parametersFile)
    if err != nil {
        return
    }
    (*params)["vm_password"] = map[string]string{
        "value": clientData.VMPassword,
    }
        // ...
```

<span data-ttu-id="28735-172">Файлы для развертывания загружаются с помощью функции `readJSON`, подробные сведения о которой здесь пропущены.</span><span class="sxs-lookup"><span data-stu-id="28735-172">The deployment files are loaded by `readJSON`, the details of which are skipped here.</span></span> <span data-ttu-id="28735-173">Эта функция возвращает тип `*map[string]interface{}`, который используется при создании метаданных для вызова развертывания ресурсов.</span><span class="sxs-lookup"><span data-stu-id="28735-173">This function returns a `*map[string]interface{}`, the type used in constructing the metadata for the resource deployment call.</span></span> <span data-ttu-id="28735-174">Пароль для виртуальной машины также устанавливается вручную в параметрах развертывания.</span><span class="sxs-lookup"><span data-stu-id="28735-174">The VM's password is also set manually on the deployment parameters.</span></span>

```go
        // ...

    deploymentsClient := resources.NewDeploymentsClient(clientData.SubscriptionID)
    deploymentsClient.Authorizer = authorizer

    deploymentFuture, err := deploymentsClient.CreateOrUpdate(
        ctx,
        resourceGroupName,
        deploymentName,
        resources.Deployment{
            Properties: &resources.DeploymentProperties{
                Template:   template,
                Parameters: params,
                Mode:       resources.Incremental,
            },
        },
    )
    if err != nil {
        return
    }
```

<span data-ttu-id="28735-175">Для этого кода используется тот же шаблон, что и при создании группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="28735-175">This code follows the same pattern as creating the resource group.</span></span> <span data-ttu-id="28735-176">Создается клиент, которому предоставляется возможность проходить аутентификацию в Azure, а затем вызывается метод.</span><span class="sxs-lookup"><span data-stu-id="28735-176">A new client is created, given the ability to authenticate with Azure, and then a method is called.</span></span> <span data-ttu-id="28735-177">Метод имеет такое же имя (`CreateOrUpdate`), что и соответствующий метод для групп ресурсов.</span><span class="sxs-lookup"><span data-stu-id="28735-177">The method even has the same name (`CreateOrUpdate`) as the corresponding method for resource groups.</span></span> <span data-ttu-id="28735-178">Этот шаблон используется во всем пакете SDK.</span><span class="sxs-lookup"><span data-stu-id="28735-178">This pattern is seen throughout the SDK.</span></span> <span data-ttu-id="28735-179">Методы, которые выполняют одинаковые функции, обычно имеют одно и то же имя.</span><span class="sxs-lookup"><span data-stu-id="28735-179">Methods that perform similar work normally have the same name.</span></span>

<span data-ttu-id="28735-180">Главное отличие заключается в возвращаемом значении метода `deploymentsClient.CreateOrUpdate`.</span><span class="sxs-lookup"><span data-stu-id="28735-180">The biggest difference comes in the return value of the `deploymentsClient.CreateOrUpdate` method.</span></span> <span data-ttu-id="28735-181">Это значение имеет тип [Future](https://godoc.org/github.com/Azure/go-autorest/autorest/azure#Future), который основывается на [шаблоне разработки future](https://en.wikipedia.org/wiki/Futures_and_promises).</span><span class="sxs-lookup"><span data-stu-id="28735-181">This value is of the [Future](https://godoc.org/github.com/Azure/go-autorest/autorest/azure#Future) type, which follows the [future design pattern](https://en.wikipedia.org/wiki/Futures_and_promises).</span></span> <span data-ttu-id="28735-182">Шаблоны future — это длительные операции в Azure, которые можно опрашивать, отменить или заблокировать по завершении.</span><span class="sxs-lookup"><span data-stu-id="28735-182">Futures represent a long-running operation in Azure that you can poll, cancel, or block on their completion.</span></span>

```go
        //...
    err = deploymentFuture.Future.WaitForCompletion(ctx, deploymentsClient.BaseClient.Client)
    if err != nil {
        return
    }
    deployment, err = deploymentFuture.Result(deploymentsClient)

    // Work around possible bugs or late-stage failures
    if deployment.Name == nil || err != nil {
        deployment, _ = deploymentsClient.Get(ctx, resourceGroupName, deploymentName)
    }
    return
```

<span data-ttu-id="28735-183">В нашем примере лучше дождаться завершения операции.</span><span class="sxs-lookup"><span data-stu-id="28735-183">For this example, the best thing to do is to wait for the operation to complete.</span></span> <span data-ttu-id="28735-184">Для получения значения future требуется [объект контекста](https://blog.golang.org/context) и клиент, который создал `Future`.</span><span class="sxs-lookup"><span data-stu-id="28735-184">Waiting on a future requires both a [context object](https://blog.golang.org/context) and the client that created the `Future`.</span></span> <span data-ttu-id="28735-185">В этом случае могут произойти две ошибки: ошибка, возникшая на стороне клиента при попытке вызвать метод, и ошибка при получении ответа от сервера.</span><span class="sxs-lookup"><span data-stu-id="28735-185">There are two possible error sources here: An error caused on the client side when trying to invoke the method, and an error response from the server.</span></span> <span data-ttu-id="28735-186">Последняя возвращается при вызове `deploymentFuture.Result`.</span><span class="sxs-lookup"><span data-stu-id="28735-186">The latter is returned as part of the `deploymentFuture.Result` call.</span></span>

<span data-ttu-id="28735-187">Получив сведения о развертывании, можно избежать потенциальных ошибок с отсутствием этих данных, вручную вызвав `deploymentsClient.Get`.</span><span class="sxs-lookup"><span data-stu-id="28735-187">Once the deployment information is retrieved, there is a workaround for possible bugs where the deployment information may be empty with a manual call to `deploymentsClient.Get` to ensure that the data is populated.</span></span>

### <a name="obtaining-the-assigned-ip-address"></a><span data-ttu-id="28735-188">Получение назначенного IP-адреса</span><span class="sxs-lookup"><span data-stu-id="28735-188">Obtaining the assigned IP address</span></span>

<span data-ttu-id="28735-189">Чтобы выполнять действия с созданной виртуальной машиной, требуется назначенный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="28735-189">To do anything with the newly created VM, you need the assigned IP address.</span></span> <span data-ttu-id="28735-190">IP-адреса представляют отдельные ресурсы Azure виртуальной машины, связанные с ресурсами адаптера сетевого интерфейса (NIC).</span><span class="sxs-lookup"><span data-stu-id="28735-190">IP addresses are their own separate Azure resource, bound to Network Interface Controller (NIC) resources.</span></span>

```go
func getLogin() {
    params, err := readJSON(parametersFile)
    if err != nil {
        log.Fatalf("Unable to read parameters. Get login information with `az network public-ip list -g %s", resourceGroupName)
    }

    addressClient := network.NewPublicIPAddressesClient(clientData.SubscriptionID)
    addressClient.Authorizer = authorizer
    ipName := (*params)["publicIPAddresses_QuickstartVM_ip_name"].(map[string]interface{})
    ipAddress, err := addressClient.Get(ctx, resourceGroupName, ipName["value"].(string), "")
    if err != nil {
        log.Fatalf("Unable to get IP information. Try using `az network public-ip list -g %s", resourceGroupName)
    }

    vmUser := (*params)["vm_user"].(map[string]interface{})

    log.Printf("Log in with ssh: %s@%s, password: %s",
        vmUser["value"].(string),
        *ipAddress.PublicIPAddressPropertiesFormat.IPAddress,
        clientData.VMPassword)
}
```

<span data-ttu-id="28735-191">Этот метод использует сведения, хранящиеся в файле параметров.</span><span class="sxs-lookup"><span data-stu-id="28735-191">This method relies on information that is stored in the parameters file.</span></span> <span data-ttu-id="28735-192">Код может напрямую отправить запрос к виртуальной машине для получения данных ее сетевого адаптера, отправить запрос к сетевому адаптеру для получения ресурса IP-адреса, а затем напрямую отправить запрос к ресурсу IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="28735-192">The code could query the VM directly to get its NIC, query the NIC to get its IP resource, and then query the IP resource directly.</span></span> <span data-ttu-id="28735-193">Это длинная цепочка зависимостей и операций, выполнять которые затратно.</span><span class="sxs-lookup"><span data-stu-id="28735-193">That's a long chain of dependencies and operations to resolve, making it expensive.</span></span> <span data-ttu-id="28735-194">Вместо этого мы можем загрузить данные JSON, так как они хранятся локально.</span><span class="sxs-lookup"><span data-stu-id="28735-194">Since the JSON information is local, it can be loaded instead.</span></span>

<span data-ttu-id="28735-195">Значение для пользователя виртуальной машины также загружается из JSON.</span><span class="sxs-lookup"><span data-stu-id="28735-195">The value for the VM user is also loaded from the JSON.</span></span> <span data-ttu-id="28735-196">Пароль для виртуальной машины был ранее загружен из файла аутентификации.</span><span class="sxs-lookup"><span data-stu-id="28735-196">The VM password was loaded earlier from the authentication file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="28735-197">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="28735-197">Next steps</span></span>

<span data-ttu-id="28735-198">В этом кратком руководстве вы использовали существующий шаблон и развернули его с помощью Go.</span><span class="sxs-lookup"><span data-stu-id="28735-198">In this quickstart, you took an existing template and deployed it through Go.</span></span> <span data-ttu-id="28735-199">Затем вы подключились к созданной виртуальной машине по протоколу SSH, чтобы убедиться в ее работоспособности.</span><span class="sxs-lookup"><span data-stu-id="28735-199">Then you connected to the newly created VM via SSH to ensure that it's running.</span></span>

<span data-ttu-id="28735-200">Чтобы узнать больше о работе с виртуальными машинами в среде Azure с использованием Go, ознакомьтесь с [примерами вычислительных ресурсов Azure для Go](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/compute) и [примерами управления ресурсами Azure для Go](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/resources).</span><span class="sxs-lookup"><span data-stu-id="28735-200">To continue learning about working with virtual machines in the Azure environment with Go, take a look at the [Azure compute samples for Go](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/compute) or [Azure resource management samples for Go](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/resources).</span></span>

<span data-ttu-id="28735-201">Дополнительные сведения о методах аутентификации, доступных в пакете SDK, и поддерживаемых типах аутентификации см. в статье [Аутентификация с помощью пакета Azure SDK для Go](azure-sdk-go-authorization.md).</span><span class="sxs-lookup"><span data-stu-id="28735-201">To learn more about the available authentication methods in the SDK, and which authentication types they support, see [Authentication with the Azure SDK for Go](azure-sdk-go-authorization.md).</span></span>
