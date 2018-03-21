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
# <a name="quickstart-deploy-an-azure-virtual-machine-from-a-template-with-the-azure-sdk-for-go"></a>Краткое руководство по развертыванию виртуальной машины Azure из шаблона с помощью пакета Azure SDK для Go

В этом кратком руководстве описано, как развертывать ресурсы из шаблона с помощью пакета Azure SDK для Go. Шаблоны — это моментальные снимки всех ресурсов, содержащихся в [группе ресурсов Azure](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview). Выполняя эту задачу, вы также ознакомитесь с функциями и соглашениями пакета SDK.

По завершении работы с этим кратким руководством у вас будет запущенная виртуальная машина, в которую можно войти с помощью имени пользователя и пароля.

[!INCLUDE [quickstarts-free-trial-note](includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](includes/cloud-shell-try-it.md)]

Если используется интерфейс Azure CLI, установленный локально, для этого краткого руководства требуется установить CLI версии 2.0.24 или более поздней. Выполните команду `az --version`, чтобы убедиться, что установленный CLI соответствует этому требованию. Если вам необходимо выполнить установку или обновление, см. статью [Установка Azure CLI 2.0](/cli/azure/install-azure-cli).

## <a name="install-the-azure-sdk-for-go"></a>Установка пакета Azure SDK для Go 

[!INCLUDE [azure-sdk-go-get](includes/azure-sdk-go-get.md)]

## <a name="create-a-service-principal"></a>Создание субъекта-службы

Чтобы войти в систему не в интерактивном режиме с помощью приложения, вам понадобится субъект-служба. Субъекты-службы помогают выполнять управление доступом на основе ролей, что предусматривает создание уникальных удостоверений пользователя. Чтобы создать субъект-службу с помощью CLI, выполните следующую команду:

```azurecli-interactive
az ad sp create-for-rbac --name az-go-vm-quickstart
```

__Обязательно__ запишите значения `appId`, `password` и `tenant` в выходных данных. Эти значения использует приложение для аутентификации в Azure.

Дополнительные сведения о создании субъектов-служб и управлении ими с помощью Azure CLI 2.0 см. в статье [Создание субъекта-службы Azure с помощью Azure CLI 2.0](/cli/azure/create-an-azure-service-principal-azure-cli).

## <a name="get-the-code"></a>Получение кода

Получите пример кода и все его зависимости с помощью команды `go get`.

```bash
go get -u -d github.com/azure-samples/azure-sdk-for-go-samples/quickstart/deploy-vm/...
```

Этот код будет скомпилирован, но не будет выполняться правильно, пока вы не предоставите сведения об учетной записи Azure и созданном субъекте-службы. В файле `main.go` есть переменная (`config`), которая содержит структуру `authInfo`. В этой структуре нужно заменить значения полей, чтобы аутентификация выполнялась правильно.

```go
    config = authInfo{ // Your application credentials
        TenantID:               "", // Azure account tenantID
        SubscriptionID:         "", // Azure subscription subscriptionID
        ServicePrincipalID:     "", // Service principal appId
        ServicePrincipalSecret: "", // Service principal password/secret
    }
```

* `SubscriptionID` — ваш идентификатор подписки, который можно получить с помощью команды CLI.

  ```azurecli-interactive
  az account show --query id -o tsv
  ```

* `TenantID` — ваш идентификатор клиента. Значение `tenant` вы записали при создании субъекта-службы.
* `ServicePrincipalID` — значение `appId`, записанное при создании субъекта-службы.
* `ServicePrincipalSecret` — значение `password`, записанное при создании субъекта-службы.

Вам также нужно изменить значение в файле `vm-quickstart-params.json`.

```json
    "vm_password": {
        "value": "_"
    }
```

* `vm_password` — пароль для учетной записи пользователя виртуальной машины. Пароль должен содержать от 12 до 72 символов, включая следующие 3 символа:
  * строчная буква;
  * прописная буква;
  * число;
  * символ.

## <a name="running-the-code"></a>Выполнение кода

Выполните код быстрого запуска с помощью команды `go run`.

```bash
cd $GOPATH/src/github.com/azure-samples/azure-sdk-for-go-samples/quickstart/deploy-vm
go run main.go
```

Если при развертывании произойдет сбой, вы получите сообщение о том, что возникла проблема, но без подробных сведений. Используя Azure CLI, получите подробные сведения о сбое развертывания с помощью следующей команды:

```azurecli-interactive
az group deployment show -g GoVMQuickstart -n VMDeployQuickstart
```

При успешном развертывании появится сообщение с именем пользователя, IP-адресом и паролем для входа в только что созданную виртуальную машину. Чтобы убедиться в работоспособности виртуальной машины, подключитесь к ней по протоколу SSH.

## <a name="cleaning-up"></a>Очистка.

Чтобы очистить ресурсы, созданные при работе с этим кратким руководством, удалите группу ресурсов с помощью CLI.

```azurecli-interactive
az group delete -n GoVMQuickstart
```

## <a name="code-in-depth"></a>Подробные сведения о коде

Все операции в коде быстрого запуска состоят из блоков переменных и нескольких небольших функций. Все они рассматриваются в этой статье.

### <a name="variable-assignments-and-structs"></a>Назначение переменных и структуры

Так как код быстрого запуска является автономным, он использует глобальные переменные, а не параметры командной строки или переменные среды.

```go
type authInfo struct {
        TenantID               string
        SubscriptionID         string
        ServicePrincipalID     string
        ServicePrincipalSecret string
}
```

Структура `authInfo` объявляется, чтобы инкапсулировать все сведения, требуемые для авторизации с помощью служб Azure.

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

Значения объявляются, чтобы присвоить имена созданным ресурсам. Здесь также указывается расположение, которое можно изменить, чтобы понять, как выполняются развертывания в других центрах обработки данных. Не в каждом центре обработки данных доступны все необходимые ресурсы.

Константы `templateFile` и `parametersFile` указывают на файлы, необходимые для развертывания. Токен субъекта-службы приводится ниже, а переменная `ctx` представляет [контекст Go](https://blog.golang.org/context) для сетевых операций.

### <a name="init-and-authorization"></a>Метод init() и авторизация

Метод `init()` для кода настраивает авторизацию. Так как авторизация является необходимым условием для всех операций в коде быстрого запуска, целесообразно ее включить в инициализацию. 

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

В этом коде для авторизации выполняется два действия:

* Извлекаются сведения о конфигурации OAuth для `TenantID` путем взаимодействия с Azure Active Directory. Объект [`azure.PublicCloud`](https://godoc.org/github.com/Azure/go-autorest/autorest/azure#PublicCloud) содержит конечные точки, которые используются в стандартной конфигурации Azure.
* Вызывается функция [`adal.NewServicePrincipalToken()`](https://godoc.org/github.com/Azure/go-autorest/autorest/adal#NewServicePrincipalToken). Эта функция принимает сведения OAuth, учетные данные для входа субъекта-службы и сведения об используемом способе управления Azure. Всегда используйте значение `.ResourceManagerEndpoint`, если нет особых требований, а уверены в своих действиях.

### <a name="flow-of-operations-in-main"></a>Последовательность операций в функции main()

`main()` — это простая функция, которая только определяет последовательность операций и выполняет проверку ошибок.

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

Действия выполняются в коде в следующем порядке:

* создание группы ресурсов, в которую будет выполняться развертывание (`createGroup()`);
* создание развертывания в этой группе (`createDeployment()`);
* получение и вывод информации для входа в развернутую виртуальную машину (`getLogin()`).

### <a name="creating-the-resource-group"></a>Создание группы ресурсов

Функция `createGroup()` создает группу ресурсов. При работе с последовательностью вызова и аргументами можно увидеть, как структурируются взаимодействия служб в пакете SDK.

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

Общая последовательность взаимодействия со службой Azure:

* Создайте клиент, используя метод `service.NewXClient()`, где `X` — это тип ресурса для объекта `service`, с которым нужно взаимодействовать. Эта функция всегда принимает идентификатор подписки.
* Задайте метод авторизации для клиента, чтобы он мог взаимодействовать с удаленным API.
* Используя метод, вызовите клиент, соответствующий удаленному API. Как правило, методы клиента службы принимают имя ресурса и объект метаданных.

В этом коде функция [`to.StringPtr()`](https://godoc.org/github.com/Azure/go-autorest/autorest/to#StringPtr) используется для преобразования типа. Так как структуры параметров для методов пакета SDK используют только указатели, эти методы предоставляются для упрощения преобразования типов. Полный список вспомогательных преобразователей и их функций см. в документации по модулю [autorest/to](https://godoc.org/github.com/Azure/go-autorest/autorest/to).

Операция `groupsClient.CreateOrUpdate()` возвращает указатель для структуры данных, представляющей группу ресурсов. Возвращаемое напрямую значение такого типа указывает на быстро выполняющуюся операцию, которая должна быть синхронной. В следующем разделе приводится пример долго выполняющейся операции и способы взаимодействия с ней.

### <a name="performing-the-deployment"></a>Выполнение развертывания

Когда группа для хранения ресурсов будет создана, можно перейти к развертыванию. Этот код разделен на небольшие разделы в соответствии с его логикой.


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

Файлы для развертывания загружаются с помощью функции `readJSON`, подробные сведения о которой здесь пропущены. Эта функция возвращает тип `*map[string]interface{}`, который используется при создании метаданных для вызова развертывания ресурсов.

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

Для этого кода используется тот же шаблон, что и при создании группы ресурсов. Создается клиент, которому предоставляется возможность проходить аутентификацию в Azure, а затем вызывается метод. Метод имеет такое же имя (`CreateOrUpdate`), что и соответствующий метод для групп ресурсов. Этот шаблон часто повторяется в пакете SDK. Методы, которые выполняют одинаковые функции, обычно имеют одно и то же имя.

Главное отличие заключается в возвращаемом значении метода `deploymentsClient.CreateOrUpdate()`. Это значение представляет объект `Future`, который основывается на [шаблоне разработки future](https://en.wikipedia.org/wiki/Futures_and_promises). Структуры future — это долго выполняющиеся операции в Azure, которые можно периодически опрашивать при выполнении других задач.

```go
        //...
        err = deploymentFuture.Future.WaitForCompletion(ctx, deploymentsClient.BaseClient.Client)
        if err != nil {
                log.Fatalf("Error while waiting for deployment creation: %v", err)
        }
        return deploymentFuture.Result(deploymentsClient)
}
```

В нашем примере лучше дождаться завершения операции. Для получения значения future требуется [объект контекста](https://blog.golang.org/context) и клиент, который создал объект future. В этом случае могут произойти две ошибки: ошибка, возникшая на стороне клиента при попытке вызвать метод, и ошибка при получении ответа от сервера. Последняя возвращается при вызове `deploymentFuture.Result()`.

### <a name="obtaining-the-assigned-ip-address"></a>Получение назначенного IP-адреса

Чтобы выполнять действия с созданной виртуальной машиной, требуется назначенный IP-адрес. IP-адреса представляют отдельные ресурсы Azure виртуальной машины, связанные с ресурсами адаптера сетевого интерфейса (NIC).

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

Этот метод использует сведения, хранящиеся в файле параметров. Код может напрямую отправить запрос к виртуальной машине для получения данных ее сетевого адаптера, отправить запрос к сетевому адаптеру для получения ресурса IP-адреса, а затем напрямую отправить запрос к ресурсу IP-адреса. Это длинная цепочка зависимостей и операций, выполнять которые затратно. Вместо этого мы можем загрузить данные JSON, так как они хранятся локально.

Значения имени пользователя и пароля для входа в виртуальную машину аналогичным образом загружаются из JSON.

## <a name="next-steps"></a>Дополнительная информация

В этом кратком руководстве вы использовали существующий шаблон и развернули его с помощью Go. Затем вы подключились к созданной виртуальной машине по протоколу SSH, чтобы убедиться в ее работоспособности.

Чтобы узнать больше о работе с виртуальными машинами в среде Azure с использованием Go, ознакомьтесь с [примерами вычислительных ресурсов Azure для Go](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/compute) и [примерами управления ресурсами Azure для Go](https://github.com/Azure-Samples/azure-sdk-for-go-samples/tree/master/resources).
