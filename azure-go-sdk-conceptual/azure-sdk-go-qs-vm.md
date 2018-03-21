---
title: "Развертывание виртуальной машины Azure с помощью Go"
description: "Разверните виртуальную машину с помощью пакета Azure SDK для Go."
keywords: azure, virtual machine, vm, go, golang, azure sdk
author: sptramer
ms.author: sttramer
ms.date: 02/08/2018
ms.topic: quickstart
ms.devlang: go
manager: routlaw
ms.openlocfilehash: ae460dbf21b13c40f3d564274f8b790afe005aae
ms.sourcegitcommit: af3473779cd7c2978f290fbdc51ee15eb1130840
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/15/2018
---
# <a name="quickstart-deploy-an-azure-virtual-machine-from-a-template-with-the-azure-sdk-for-go"></a><span data-ttu-id="3d43f-104">Краткое руководство по развертыванию виртуальной машины Azure из шаблона с помощью пакета Azure SDK для Go</span><span class="sxs-lookup"><span data-stu-id="3d43f-104">Quickstart: Deploy an Azure virtual machine from a template with the Azure SDK for Go</span></span>

<span data-ttu-id="3d43f-105">В этом кратком руководстве описано, как развертывать ресурсы из шаблона с помощью пакета Azure SDK для Go.</span><span class="sxs-lookup"><span data-stu-id="3d43f-105">This quickstart focuses on deploying resources from a template with the Azure SDK for Go.</span></span> <span data-ttu-id="3d43f-106">Шаблоны — это моментальные снимки всех ресурсов, содержащихся в [группе ресурсов Azure](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview).</span><span class="sxs-lookup"><span data-stu-id="3d43f-106">Templates are snapshots of all of the resources contained within an [Azure resource group](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview).</span></span> <span data-ttu-id="3d43f-107">Выполняя эту задачу, вы также ознакомитесь с функциями и соглашениями пакета SDK.</span><span class="sxs-lookup"><span data-stu-id="3d43f-107">Along the way, you'll become familiar with the functionality and conventions of the SDK while performing a useful task.</span></span>

<span data-ttu-id="3d43f-108">По завершении работы с этим кратким руководством у вас будет запущенная виртуальная машина, в которую можно войти с помощью имени пользователя и пароля.</span><span class="sxs-lookup"><span data-stu-id="3d43f-108">At the end of this quickstart, you have a running VM that you log into with a username and password.</span></span>

[!INCLUDE [quickstarts-free-trial-note](includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](includes/cloud-shell-try-it.md)]

<span data-ttu-id="3d43f-109">Если используется интерфейс Azure CLI, установленный локально, для этого краткого руководства требуется установить CLI версии 2.0.24 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="3d43f-109">If you use a local install of the Azure CLI, this quickstart requires CLI version 2.0.24 or later.</span></span> <span data-ttu-id="3d43f-110">Выполните команду `az --version`, чтобы убедиться, что установленный CLI соответствует этому требованию.</span><span class="sxs-lookup"><span data-stu-id="3d43f-110">Run `az --version` to make sure your CLI install meets this requirement.</span></span> <span data-ttu-id="3d43f-111">Если вам необходимо выполнить установку или обновление, см. статью [Установка Azure CLI 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="3d43f-111">If you need to install or upgrade, see [Install the Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span>

## <a name="install-the-azure-sdk-for-go"></a><span data-ttu-id="3d43f-112">Установка пакета Azure SDK для Go</span><span class="sxs-lookup"><span data-stu-id="3d43f-112">Install the Azure SDK for Go</span></span> 

[!INCLUDE [azure-sdk-go-get](includes/azure-sdk-go-get.md)]

## <a name="create-a-service-principal"></a><span data-ttu-id="3d43f-113">Создание субъекта-службы</span><span class="sxs-lookup"><span data-stu-id="3d43f-113">Create a service principal</span></span>

<span data-ttu-id="3d43f-114">Чтобы войти в систему не в интерактивном режиме с помощью приложения, вам понадобится субъект-служба.</span><span class="sxs-lookup"><span data-stu-id="3d43f-114">To log in non-interactively with an application, you need a service principal.</span></span> <span data-ttu-id="3d43f-115">Субъекты-службы помогают выполнять управление доступом на основе ролей, что предусматривает создание уникальных удостоверений пользователя.</span><span class="sxs-lookup"><span data-stu-id="3d43f-115">Service principals are part of role-based access control (RBAC), which creates a unique user identity.</span></span> <span data-ttu-id="3d43f-116">Чтобы создать субъект-службу с помощью CLI, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="3d43f-116">To create a new service principal with the CLI, run the following command:</span></span>

```azurecli-interactive
az ad sp create-for-rbac --name az-go-vm-quickstart
```

<span data-ttu-id="3d43f-117">__Обязательно__ запишите значения `appId`, `password` и `tenant` в выходных данных.</span><span class="sxs-lookup"><span data-stu-id="3d43f-117">__Make sure__ to record the `appId`, `password`, and `tenant` values in the output.</span></span> <span data-ttu-id="3d43f-118">Эти значения использует приложение для аутентификации в Azure.</span><span class="sxs-lookup"><span data-stu-id="3d43f-118">These values are used by the application to authenticate with Azure.</span></span>

<span data-ttu-id="3d43f-119">Дополнительные сведения о создании субъектов-служб и управлении ими с помощью Azure CLI 2.0 см. в статье [Создание субъекта-службы Azure с помощью Azure CLI 2.0](/cli/azure/create-an-azure-service-principal-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="3d43f-119">For more information on creating and managing service principals with the Azure CLI 2.0, see [Create an Azure service principal with Azure CLI 2.0](/cli/azure/create-an-azure-service-principal-azure-cli).</span></span>

## <a name="get-the-code"></a><span data-ttu-id="3d43f-120">Получение кода</span><span class="sxs-lookup"><span data-stu-id="3d43f-120">Get the code</span></span>

<span data-ttu-id="3d43f-121">Получите пример кода и все его зависимости с помощью команды `go get`.</span><span class="sxs-lookup"><span data-stu-id="3d43f-121">Get the quickstart code and all of its dependencies with `go get`.</span></span>

```bash
go get -u -d github.com/azure-samples/azure-sdk-for-go-samples/quickstart/deploy-vm/...
```

<span data-ttu-id="3d43f-122">Этот код будет скомпилирован, но не будет выполняться правильно, пока вы не предоставите сведения об учетной записи Azure и созданном субъекте-службы.</span><span class="sxs-lookup"><span data-stu-id="3d43f-122">This code compiles, but doesn't run correctly until you provide it information about your Azure account and the created service principal.</span></span> <span data-ttu-id="3d43f-123">В файле `main.go` есть переменная (`config`), которая содержит структуру `authInfo`.</span><span class="sxs-lookup"><span data-stu-id="3d43f-123">In `main.go` there is a variable, `config`, which contains an `authInfo` struct.</span></span> <span data-ttu-id="3d43f-124">В этой структуре нужно заменить значения полей, чтобы аутентификация выполнялась правильно.</span><span class="sxs-lookup"><span data-stu-id="3d43f-124">This struct needs to have its field values replaced in order to authenticate correctly.</span></span>

```go
    config = authInfo{ // Your application credentials
        TenantID:               "", // Azure account tenantID
        SubscriptionID:         "", // Azure subscription subscriptionID
        ServicePrincipalID:     "", // Service principal appId
        ServicePrincipalSecret: "", // Service principal password/secret
    }
```

* <span data-ttu-id="3d43f-125">`SubscriptionID` — ваш идентификатор подписки, который можно получить с помощью команды CLI.</span><span class="sxs-lookup"><span data-stu-id="3d43f-125">`SubscriptionID`: Your subscription ID, which can be obtained from the CLI command</span></span>

  ```azurecli-interactive
  az account show --query id -o tsv
  ```

* <span data-ttu-id="3d43f-126">`TenantID` — ваш идентификатор клиента. Значение `tenant` вы записали при создании субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="3d43f-126">`TenantID`: Your tenant ID, the `tenant` value recorded when creating the service principal</span></span>
* <span data-ttu-id="3d43f-127">`ServicePrincipalID` — значение `appId`, записанное при создании субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="3d43f-127">`ServicePrincipalID`: The `appId` value recorded when creating the service principal</span></span>
* <span data-ttu-id="3d43f-128">`ServicePrincipalSecret` — значение `password`, записанное при создании субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="3d43f-128">`ServicePrincipalSecret`: The `password` value recorded when creating the service principal</span></span>

<span data-ttu-id="3d43f-129">Вам также нужно изменить значение в файле `vm-quickstart-params.json`.</span><span class="sxs-lookup"><span data-stu-id="3d43f-129">You also need to edit a value in the `vm-quickstart-params.json` file.</span></span>

```json
    "vm_password": {
        "value": "_"
    }
```

* <span data-ttu-id="3d43f-130">`vm_password` — пароль для учетной записи пользователя виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="3d43f-130">`vm_password`: The password for the VM user account.</span></span> <span data-ttu-id="3d43f-131">Пароль должен содержать от 12 до 72 символов, включая следующие 3 символа:</span><span class="sxs-lookup"><span data-stu-id="3d43f-131">It must be 12-72 characters in length and contain 3 of the following characters:</span></span>
  * <span data-ttu-id="3d43f-132">строчная буква;</span><span class="sxs-lookup"><span data-stu-id="3d43f-132">A lowercase letter</span></span>
  * <span data-ttu-id="3d43f-133">прописная буква;</span><span class="sxs-lookup"><span data-stu-id="3d43f-133">An uppercase letter</span></span>
  * <span data-ttu-id="3d43f-134">число;</span><span class="sxs-lookup"><span data-stu-id="3d43f-134">A number</span></span>
  * <span data-ttu-id="3d43f-135">символ.</span><span class="sxs-lookup"><span data-stu-id="3d43f-135">A symbol</span></span>

## <a name="running-the-code"></a><span data-ttu-id="3d43f-136">Выполнение кода</span><span class="sxs-lookup"><span data-stu-id="3d43f-136">Running the code</span></span>

<span data-ttu-id="3d43f-137">Выполните код быстрого запуска с помощью команды `go run`.</span><span class="sxs-lookup"><span data-stu-id="3d43f-137">Run the quickstart with the `go run` command.</span></span>

```bash
cd $GOPATH/src/github.com/azure-samples/azure-sdk-for-go-samples/quickstart/deploy-vm
go run main.go
```

<span data-ttu-id="3d43f-138">Если при развертывании произойдет сбой, вы получите сообщение о том, что возникла проблема, но без подробных сведений.</span><span class="sxs-lookup"><span data-stu-id="3d43f-138">If there is a failure in the deployment, you get a message indicating that there was an issue, but without any specific details.</span></span> <span data-ttu-id="3d43f-139">Используя Azure CLI, получите подробные сведения о сбое развертывания с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="3d43f-139">Using the Azure CLI, get the details of the deployment failure with the following command:</span></span>

```azurecli-interactive
az group deployment show -g GoVMQuickstart -n VMDeployQuickstart
```

<span data-ttu-id="3d43f-140">При успешном развертывании появится сообщение с именем пользователя, IP-адресом и паролем для входа в только что созданную виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="3d43f-140">If the deployment is successful, you see a message giving the username, IP address, and password for logging into the newly created virtual machine.</span></span> <span data-ttu-id="3d43f-141">Чтобы убедиться в работоспособности виртуальной машины, подключитесь к ней по протоколу SSH.</span><span class="sxs-lookup"><span data-stu-id="3d43f-141">SSH into this machine to confirm that it is up and running.</span></span>

## <a name="cleaning-up"></a><span data-ttu-id="3d43f-142">Очистка.</span><span class="sxs-lookup"><span data-stu-id="3d43f-142">Cleaning up</span></span>

<span data-ttu-id="3d43f-143">Чтобы очистить ресурсы, созданные при работе с этим кратким руководством, удалите группу ресурсов с помощью CLI.</span><span class="sxs-lookup"><span data-stu-id="3d43f-143">Clean up the resources created during this quickstart by deleting the resource group with the CLI.</span></span>

```azurecli-interactive
az group delete -n GoVMQuickstart
```

## <a name="code-in-depth"></a><span data-ttu-id="3d43f-144">Подробные сведения о коде</span><span class="sxs-lookup"><span data-stu-id="3d43f-144">Code in depth</span></span>

<span data-ttu-id="3d43f-145">Все операции в коде быстрого запуска состоят из блоков переменных и нескольких небольших функций. Все они рассматриваются в этой статье.</span><span class="sxs-lookup"><span data-stu-id="3d43f-145">What the quickstart code does is broken down into a block of variables and several small functions, each of which are discussed here.</span></span>

### <a name="variable-assignments-and-structs"></a><span data-ttu-id="3d43f-146">Назначение переменных и структуры</span><span class="sxs-lookup"><span data-stu-id="3d43f-146">Variable assignments and structs</span></span>

<span data-ttu-id="3d43f-147">Так как код быстрого запуска является автономным, он использует глобальные переменные, а не параметры командной строки или переменные среды.</span><span class="sxs-lookup"><span data-stu-id="3d43f-147">Since quickstart is self-contained, it uses global variables rather than command-line options or environment variables.</span></span>

```go
type authInfo struct {
        TenantID               string
        SubscriptionID         string
        ServicePrincipalID     string
        ServicePrincipalSecret string
}
```

<span data-ttu-id="3d43f-148">Структура `authInfo` объявляется, чтобы инкапсулировать все сведения, требуемые для авторизации с помощью служб Azure.</span><span class="sxs-lookup"><span data-stu-id="3d43f-148">The `authInfo` struct is declared to encapsulate all of the information needed for authorization with Azure services.</span></span>

```go
const (
    resourceGroupName     = "GoVMQuickstart"
    resourceGroupLocation = "eastus"

    deploymentName = "VMDeployQuickstart"
    templateFile   = "vm-quickstart-template.json"
    parametersFile = "vm-quickstart-params.json"
)

var (
    config = authInfo{ // Your application credentials
        TenantID:               "", // Azure account tenantID
        SubscriptionID:         "", // Azure subscription subscriptionID
        ServicePrincipalID:     "", // Service principal appId
        ServicePrincipalSecret: "", // Service principal password/secret
    }

    ctx = context.Background()

    token *adal.ServicePrincipalToken
)
```

<span data-ttu-id="3d43f-149">Значения объявляются, чтобы присвоить имена созданным ресурсам.</span><span class="sxs-lookup"><span data-stu-id="3d43f-149">Values are declared which give the names of created resources.</span></span> <span data-ttu-id="3d43f-150">Здесь также указывается расположение, которое можно изменить, чтобы понять, как выполняются развертывания в других центрах обработки данных.</span><span class="sxs-lookup"><span data-stu-id="3d43f-150">The location is also specified here, which you can change to see how deployments behave in other datacenters.</span></span> <span data-ttu-id="3d43f-151">Не в каждом центре обработки данных доступны все необходимые ресурсы.</span><span class="sxs-lookup"><span data-stu-id="3d43f-151">Not every datacenter has all of the required resources available.</span></span>

<span data-ttu-id="3d43f-152">Константы `templateFile` и `parametersFile` указывают на файлы, необходимые для развертывания.</span><span class="sxs-lookup"><span data-stu-id="3d43f-152">The `templateFile` and `parametersFile` constants point to the files needed for deployment.</span></span> <span data-ttu-id="3d43f-153">Токен субъекта-службы приводится ниже, а переменная `ctx` представляет [контекст Go](https://blog.golang.org/context) для сетевых операций.</span><span class="sxs-lookup"><span data-stu-id="3d43f-153">The service principal token is covered later, and the `ctx` variable is a [Go context](https://blog.golang.org/context) for the network operations.</span></span>

### <a name="init-and-authorization"></a><span data-ttu-id="3d43f-154">Метод init() и авторизация</span><span class="sxs-lookup"><span data-stu-id="3d43f-154">init() and authorization</span></span>

<span data-ttu-id="3d43f-155">Метод `init()` для кода настраивает авторизацию.</span><span class="sxs-lookup"><span data-stu-id="3d43f-155">The `init()` method for the code sets up authorization.</span></span> <span data-ttu-id="3d43f-156">Так как авторизация является необходимым условием для всех операций в коде быстрого запуска, целесообразно ее включить в инициализацию.</span><span class="sxs-lookup"><span data-stu-id="3d43f-156">Since authorization is a precondition for everything in the quickstart, it makes sense to have it as part of initialization.</span></span> 

```go
// Authenticate with the Azure services over OAuth, using a service principal.
func init() {
    oauthConfig, err := adal.NewOAuthConfig(azure.PublicCloud.ActiveDirectoryEndpoint, config.TenantID)
    if err != nil {
        log.Fatalf("Failed to get OAuth config: %v\n", err)
    }
    token, err = adal.NewServicePrincipalToken(
        *oauthConfig,
        config.ServicePrincipalID,
        config.ServicePrincipalSecret,
        azure.PublicCloud.ResourceManagerEndpoint)
    if err != nil {
        log.Fatalf("faled to get token: %v\n", err)
    }
}
```

<span data-ttu-id="3d43f-157">В этом коде для авторизации выполняется два действия:</span><span class="sxs-lookup"><span data-stu-id="3d43f-157">This code completes two steps for authorization:</span></span>

* <span data-ttu-id="3d43f-158">Извлекаются сведения о конфигурации OAuth для `TenantID` путем взаимодействия с Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3d43f-158">OAuth configuration information for the `TenantID` is retrieved by interfacing with Azure Active Directory.</span></span> <span data-ttu-id="3d43f-159">Объект [`azure.PublicCloud`](https://godoc.org/github.com/Azure/go-autorest/autorest/azure#PublicCloud) содержит конечные точки, которые используются в стандартной конфигурации Azure.</span><span class="sxs-lookup"><span data-stu-id="3d43f-159">The [`azure.PublicCloud`](https://godoc.org/github.com/Azure/go-autorest/autorest/azure#PublicCloud) object contains endpoints used in the standard Azure configuration.</span></span>
* <span data-ttu-id="3d43f-160">Вызывается функция [`adal.NewServicePrincipalToken()`](https://godoc.org/github.com/Azure/go-autorest/autorest/adal#NewServicePrincipalToken).</span><span class="sxs-lookup"><span data-stu-id="3d43f-160">The [`adal.NewServicePrincipalToken()`](https://godoc.org/github.com/Azure/go-autorest/autorest/adal#NewServicePrincipalToken) function is called.</span></span> <span data-ttu-id="3d43f-161">Эта функция принимает сведения OAuth, учетные данные для входа субъекта-службы и сведения об используемом способе управления Azure.</span><span class="sxs-lookup"><span data-stu-id="3d43f-161">This function takes the OAuth information along with the service principal login, as well as which style of Azure management is being used.</span></span> <span data-ttu-id="3d43f-162">Всегда используйте значение `.ResourceManagerEndpoint`, если нет особых требований, а уверены в своих действиях.</span><span class="sxs-lookup"><span data-stu-id="3d43f-162">Unless you have specific requirements and know what you're doing, this value should always be `.ResourceManagerEndpoint`.</span></span>

### <a name="flow-of-operations-in-main"></a><span data-ttu-id="3d43f-163">Последовательность операций в функции main()</span><span class="sxs-lookup"><span data-stu-id="3d43f-163">Flow of operations in main()</span></span>

<span data-ttu-id="3d43f-164">`main()` — это простая функция, которая только определяет последовательность операций и выполняет проверку ошибок.</span><span class="sxs-lookup"><span data-stu-id="3d43f-164">The `main()` function is simple, only indicating the flow of operations and performing error-checking.</span></span>

```go
func main() {
    group, err := createGroup()
    if err != nil {
        log.Fatalf("failed to create group: %v", err)
    }
    log.Printf("created group: %v\n", *group.Name)

    log.Println("starting deployment")
    result, err := createDeployment()
    if err != nil {
        log.Fatalf("Failed to deploy correctly: %v", err)
    }
    log.Printf("Completed deployment: %v", *result.Name)
    getLogin()
}
```

<span data-ttu-id="3d43f-165">Действия выполняются в коде в следующем порядке:</span><span class="sxs-lookup"><span data-stu-id="3d43f-165">The steps that the code runs through are, in order:</span></span>

* <span data-ttu-id="3d43f-166">создание группы ресурсов, в которую будет выполняться развертывание (`createGroup()`);</span><span class="sxs-lookup"><span data-stu-id="3d43f-166">Create the resource group to deploy to (`createGroup()`)</span></span>
* <span data-ttu-id="3d43f-167">создание развертывания в этой группе (`createDeployment()`);</span><span class="sxs-lookup"><span data-stu-id="3d43f-167">Create the deployment within this group (`createDeployment()`)</span></span>
* <span data-ttu-id="3d43f-168">получение и вывод информации для входа в развернутую виртуальную машину (`getLogin()`).</span><span class="sxs-lookup"><span data-stu-id="3d43f-168">Obtain and display login information for the deployed VM (`getLogin()`)</span></span>

### <a name="creating-the-resource-group"></a><span data-ttu-id="3d43f-169">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="3d43f-169">Creating the resource group</span></span>

<span data-ttu-id="3d43f-170">Функция `createGroup()` создает группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="3d43f-170">The `createGroup()` function creates the resource group.</span></span> <span data-ttu-id="3d43f-171">При работе с последовательностью вызова и аргументами можно увидеть, как структурируются взаимодействия служб в пакете SDK.</span><span class="sxs-lookup"><span data-stu-id="3d43f-171">Looking at the call flow and arguments demonstrates the way that service interactions are structured in the SDK.</span></span>

```go
func createGroup() (group resources.Group, err error) {
        groupsClient := resources.NewGroupsClient(config.SubscriptionID)
        groupsClient.Authorizer = autorest.NewBearerAuthorizer(token)

        return groupsClient.CreateOrUpdate(
                ctx,
                resourceGroupName,
                resources.Group{
                        Location: to.StringPtr(resourceGroupLocation)})
}
```

<span data-ttu-id="3d43f-172">Общая последовательность взаимодействия со службой Azure:</span><span class="sxs-lookup"><span data-stu-id="3d43f-172">The general flow of interacting with an Azure service is:</span></span>

* <span data-ttu-id="3d43f-173">Создайте клиент, используя метод `service.NewXClient()`, где `X` — это тип ресурса для объекта `service`, с которым нужно взаимодействовать.</span><span class="sxs-lookup"><span data-stu-id="3d43f-173">Create the client using the `service.NewXClient()` method, where `X` is the resource type of the `service` that you want to interact with.</span></span> <span data-ttu-id="3d43f-174">Эта функция всегда принимает идентификатор подписки.</span><span class="sxs-lookup"><span data-stu-id="3d43f-174">This function always takes a subscription ID.</span></span>
* <span data-ttu-id="3d43f-175">Задайте метод авторизации для клиента, чтобы он мог взаимодействовать с удаленным API.</span><span class="sxs-lookup"><span data-stu-id="3d43f-175">Set the authorization method for the client, allowing it to interact with the remote API.</span></span>
* <span data-ttu-id="3d43f-176">Используя метод, вызовите клиент, соответствующий удаленному API.</span><span class="sxs-lookup"><span data-stu-id="3d43f-176">Make the method call on the client corresponding to the remote API.</span></span> <span data-ttu-id="3d43f-177">Как правило, методы клиента службы принимают имя ресурса и объект метаданных.</span><span class="sxs-lookup"><span data-stu-id="3d43f-177">Service client methods usually take the name of the resource and a metadata object.</span></span>

<span data-ttu-id="3d43f-178">В этом коде функция [`to.StringPtr()`](https://godoc.org/github.com/Azure/go-autorest/autorest/to#StringPtr) используется для преобразования типа.</span><span class="sxs-lookup"><span data-stu-id="3d43f-178">The [`to.StringPtr()`](https://godoc.org/github.com/Azure/go-autorest/autorest/to#StringPtr) function is used to perform a type conversion here.</span></span> <span data-ttu-id="3d43f-179">Так как структуры параметров для методов пакета SDK используют только указатели, эти методы предоставляются для упрощения преобразования типов.</span><span class="sxs-lookup"><span data-stu-id="3d43f-179">The parameters structs for methods of the SDK almost exclusively take pointers, so these methods are provided to make the type conversions easy.</span></span> <span data-ttu-id="3d43f-180">Полный список вспомогательных преобразователей и их функций см. в документации по модулю [autorest/to](https://godoc.org/github.com/Azure/go-autorest/autorest/to).</span><span class="sxs-lookup"><span data-stu-id="3d43f-180">See the documentation for the [autorest/to](https://godoc.org/github.com/Azure/go-autorest/autorest/to) module for the complete list and behavior of convenience converters.</span></span>

<span data-ttu-id="3d43f-181">Операция `groupsClient.CreateOrUpdate()` возвращает указатель для структуры данных, представляющей группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="3d43f-181">The `groupsClient.CreateOrUpdate()` operation returns a pointer to a data struct representing the resource group.</span></span> <span data-ttu-id="3d43f-182">Возвращаемое напрямую значение такого типа указывает на быстро выполняющуюся операцию, которая должна быть синхронной.</span><span class="sxs-lookup"><span data-stu-id="3d43f-182">A direct return value of this kind indicates a short-running operation that is meant to be synchronous.</span></span> <span data-ttu-id="3d43f-183">В следующем разделе приводится пример долго выполняющейся операции и способы взаимодействия с ней.</span><span class="sxs-lookup"><span data-stu-id="3d43f-183">In the next section, you'll see an example of a long-running operation and how to interact with them.</span></span>

### <a name="performing-the-deployment"></a><span data-ttu-id="3d43f-184">Выполнение развертывания</span><span class="sxs-lookup"><span data-stu-id="3d43f-184">Performing the deployment</span></span>

<span data-ttu-id="3d43f-185">Когда группа для хранения ресурсов будет создана, можно перейти к развертыванию.</span><span class="sxs-lookup"><span data-stu-id="3d43f-185">Once the group to contain its resources is created, it's time to run the deployment.</span></span> <span data-ttu-id="3d43f-186">Этот код разделен на небольшие разделы в соответствии с его логикой.</span><span class="sxs-lookup"><span data-stu-id="3d43f-186">This code is broken up into smaller sections to emphasize different parts of its logic.</span></span>


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

        // ...
```

<span data-ttu-id="3d43f-187">Файлы для развертывания загружаются с помощью функции `readJSON`, подробные сведения о которой здесь пропущены.</span><span class="sxs-lookup"><span data-stu-id="3d43f-187">The deployment files are loaded by `readJSON`, the details of which are skipped here.</span></span> <span data-ttu-id="3d43f-188">Эта функция возвращает тип `*map[string]interface{}`, который используется при создании метаданных для вызова развертывания ресурсов.</span><span class="sxs-lookup"><span data-stu-id="3d43f-188">This function returns a `*map[string]interface{}`, the type used in constructing the metadata for the resource deployment call.</span></span>

```go
        // ...
        
        deploymentsClient := resources.NewDeploymentsClient(config.SubscriptionID)
        deploymentsClient.Authorizer = autorest.NewBearerAuthorizer(token)

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
                log.Fatalf("Failed to create deployment: %v", err)
        }
        //...
```

<span data-ttu-id="3d43f-189">Для этого кода используется тот же шаблон, что и при создании группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="3d43f-189">This code follows the same pattern as with creating the resource group.</span></span> <span data-ttu-id="3d43f-190">Создается клиент, которому предоставляется возможность проходить аутентификацию в Azure, а затем вызывается метод.</span><span class="sxs-lookup"><span data-stu-id="3d43f-190">A new client is created, given the ability to authenticate with Azure, and then a method is called.</span></span> <span data-ttu-id="3d43f-191">Метод имеет такое же имя (`CreateOrUpdate`), что и соответствующий метод для групп ресурсов.</span><span class="sxs-lookup"><span data-stu-id="3d43f-191">The method even has the same name (`CreateOrUpdate`) as the corresponding method for resource groups.</span></span> <span data-ttu-id="3d43f-192">Этот шаблон часто повторяется в пакете SDK.</span><span class="sxs-lookup"><span data-stu-id="3d43f-192">This pattern is seen again and again in the SDK.</span></span> <span data-ttu-id="3d43f-193">Методы, которые выполняют одинаковые функции, обычно имеют одно и то же имя.</span><span class="sxs-lookup"><span data-stu-id="3d43f-193">Methods that perform similar work normally have the same name.</span></span>

<span data-ttu-id="3d43f-194">Главное отличие заключается в возвращаемом значении метода `deploymentsClient.CreateOrUpdate()`.</span><span class="sxs-lookup"><span data-stu-id="3d43f-194">The biggest difference comes in the return value of the `deploymentsClient.CreateOrUpdate()` method.</span></span> <span data-ttu-id="3d43f-195">Это значение представляет объект `Future`, который основывается на [шаблоне разработки future](https://en.wikipedia.org/wiki/Futures_and_promises).</span><span class="sxs-lookup"><span data-stu-id="3d43f-195">This value is a `Future` object, which follows the [future design pattern](https://en.wikipedia.org/wiki/Futures_and_promises).</span></span> <span data-ttu-id="3d43f-196">Структуры future — это долго выполняющиеся операции в Azure, которые можно периодически опрашивать при выполнении других задач.</span><span class="sxs-lookup"><span data-stu-id="3d43f-196">Futures represent a long-running operation in Azure that you may want to occasionally poll while performing other work.</span></span>

```go
        //...
        err = deploymentFuture.Future.WaitForCompletion(ctx, deploymentsClient.BaseClient.Client)
        if err != nil {
                log.Fatalf("Error while waiting for deployment creation: %v", err)
        }
        return deploymentFuture.Result(deploymentsClient)
}
```

<span data-ttu-id="3d43f-197">В нашем примере лучше дождаться завершения операции.</span><span class="sxs-lookup"><span data-stu-id="3d43f-197">For this example, the best thing to do is to wait for the operation to complete.</span></span> <span data-ttu-id="3d43f-198">Для получения значения future требуется [объект контекста](https://blog.golang.org/context) и клиент, который создал объект future.</span><span class="sxs-lookup"><span data-stu-id="3d43f-198">Waiting on a future requires both a [context object](https://blog.golang.org/context) and the client that created the Future object.</span></span> <span data-ttu-id="3d43f-199">В этом случае могут произойти две ошибки: ошибка, возникшая на стороне клиента при попытке вызвать метод, и ошибка при получении ответа от сервера.</span><span class="sxs-lookup"><span data-stu-id="3d43f-199">There are two possible error sources here: An error caused on the client side when trying to invoke the method, and an error response from the server.</span></span> <span data-ttu-id="3d43f-200">Последняя возвращается при вызове `deploymentFuture.Result()`.</span><span class="sxs-lookup"><span data-stu-id="3d43f-200">The latter is returned as part of the `deploymentFuture.Result()` call.</span></span>

### <a name="obtaining-the-assigned-ip-address"></a><span data-ttu-id="3d43f-201">Получение назначенного IP-адреса</span><span class="sxs-lookup"><span data-stu-id="3d43f-201">Obtaining the assigned IP address</span></span>

<span data-ttu-id="3d43f-202">Чтобы выполнять действия с созданной виртуальной машиной, требуется назначенный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="3d43f-202">To do anything with the newly created VM, you need the assigned IP address.</span></span> <span data-ttu-id="3d43f-203">IP-адреса представляют отдельные ресурсы Azure виртуальной машины, связанные с ресурсами адаптера сетевого интерфейса (NIC).</span><span class="sxs-lookup"><span data-stu-id="3d43f-203">IP addresses are their own separate Azure resource, bound to Network Interface Controller (NIC) resources.</span></span>

```go
func getLogin() {
        params, err := readJSON(parametersFile)
        if err != nil {
                log.Fatalf("Unable to read parameters. Get login information with `az network public-ip list -g %s", resourceGroupName)
        }

        addressClient := network.NewPublicIPAddressesClient(config.SubscriptionID)
        addressClient.Authorizer = autorest.NewBearerAuthorizer(token)
        ipName := (*params)["publicIPAddresses_QuickstartVM_ip_name"].(map[string]interface{})
        ipAddress, err := addressClient.Get(ctx, resourceGroupName, ipName["value"].(string), "")
        if err != nil {
                log.Fatalf("Unable to get IP information. Try using `az network public-ip list -g %s", resourceGroupName)
        }

        vmUser := (*params)["vm_user"].(map[string]interface{})
        vmPass := (*params)["vm_password"].(map[string]interface{})

        log.Printf("Log in with ssh: %s@%s, password: %s",
                vmUser["value"].(string),
                *ipAddress.PublicIPAddressPropertiesFormat.IPAddress,
                vmPass["value"].(string))
}
```

<span data-ttu-id="3d43f-204">Этот метод использует сведения, хранящиеся в файле параметров.</span><span class="sxs-lookup"><span data-stu-id="3d43f-204">This method relies on information that is stored in the parameters file.</span></span> <span data-ttu-id="3d43f-205">Код может напрямую отправить запрос к виртуальной машине для получения данных ее сетевого адаптера, отправить запрос к сетевому адаптеру для получения ресурса IP-адреса, а затем напрямую отправить запрос к ресурсу IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="3d43f-205">The code could query the VM directly to get its NIC, query the NIC to get its IP resource, and then query the IP resource directly.</span></span> <span data-ttu-id="3d43f-206">Это длинная цепочка зависимостей и операций, выполнять которые затратно.</span><span class="sxs-lookup"><span data-stu-id="3d43f-206">That's a long chain of dependencies and operations to resolve, making it expensive.</span></span> <span data-ttu-id="3d43f-207">Вместо этого мы можем загрузить данные JSON, так как они хранятся локально.</span><span class="sxs-lookup"><span data-stu-id="3d43f-207">Since the JSON information is local, it can be loaded instead.</span></span>

<span data-ttu-id="3d43f-208">Значения имени пользователя и пароля для входа в виртуальную машину аналогичным образом загружаются из JSON.</span><span class="sxs-lookup"><span data-stu-id="3d43f-208">The values for the VM user and password are likewise loaded from the JSON.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3d43f-209">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="3d43f-209">Next steps</span></span>

<span data-ttu-id="3d43f-210">В этом кратком руководстве вы использовали существующий шаблон и развернули его с помощью Go.</span><span class="sxs-lookup"><span data-stu-id="3d43f-210">In this quickstart, you took an existing template and deployed it through Go.</span></span> <span data-ttu-id="3d43f-211">Затем вы подключились к созданной виртуальной машине по протоколу SSH, чтобы убедиться в ее работоспособности.</span><span class="sxs-lookup"><span data-stu-id="3d43f-211">Then you connected to the newly created VM via SSH to ensure that it's running.</span></span>

<span data-ttu-id="3d43f-212">Чтобы узнать больше о работе с виртуальными машинами в среде Azure с использованием Go, ознакомьтесь с [примерами вычислительных ресурсов Azure для Go](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/compute) и [примерами управления ресурсами Azure для Go](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/resources).</span><span class="sxs-lookup"><span data-stu-id="3d43f-212">To continue learning about working with virtual machines in the Azure environment with Go, take a look at the [Azure compute samples for Go](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/compute) or [Azure resource management samples for Go](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/resources).</span></span>
