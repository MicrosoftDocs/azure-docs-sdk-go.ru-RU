---
title: Пакет Azure SDK для примеров Go для вычислений и сетевого взаимодействия
description: Выбранные примеры для работы с такими вычислительными ресурсами, как виртуальные машины и виртуальные сети, с помощью пакета Azure SDK для Go.
author: sptramer
ms.author: sttramer
manager: carmonm
ms.date: 03/21/2018
ms.topic: sample
ms.prod: azure
ms.technology: azure-sdk-go
ms.service: virtual-machines
ms.devlang: go
ms.openlocfilehash: 3b31716ee42c638bab4a6dd99b9eb0d7c07e51a4
ms.sourcegitcommit: 0f581979216f7c9d4913681a6d9f6fe09af26e43
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/02/2018
ms.locfileid: "39475795"
---
# <a name="azure-sdk-for-go-samples-for-compute-and-networking"></a><span data-ttu-id="d26e5-103">Пакет Azure SDK для примеров Go для вычислений и сетевого взаимодействия</span><span class="sxs-lookup"><span data-stu-id="d26e5-103">Azure SDK for Go samples for compute and networking</span></span>

<span data-ttu-id="d26e5-104">В следующей таблице представлены ссылки на выбранные примеры исходного кода Go, который можно использовать для управления виртуальными машинами, виртуальными сетями и подсетями в Azure.</span><span class="sxs-lookup"><span data-stu-id="d26e5-104">The following table links to selected samples of Go source code that you can use to manage VMs, virtual networks, and subnets in Azure.</span></span> 

<span data-ttu-id="d26e5-105">Все примеры для пакета Azure SDK для Go доступны в репозитории [GitHub](https://github.com/Azure-Samples/azure-sdk-for-go-samples).</span><span class="sxs-lookup"><span data-stu-id="d26e5-105">All samples for the Azure SDK for Go are available on [GitHub](https://github.com/Azure-Samples/azure-sdk-for-go-samples).</span></span>

| <span data-ttu-id="d26e5-106">ИМЯ</span><span class="sxs-lookup"><span data-stu-id="d26e5-106">Name</span></span> | <span data-ttu-id="d26e5-107">ОПИСАНИЕ</span><span class="sxs-lookup"><span data-stu-id="d26e5-107">Description</span></span> |
|------|-------------|
| [<span data-ttu-id="d26e5-108">network/network</span><span class="sxs-lookup"><span data-stu-id="d26e5-108">network/network</span></span>](https://github.com/Azure-Samples/azure-sdk-for-go-samples/blob/master/network/network.go) | <span data-ttu-id="d26e5-109">Создание, обновление и удаление сетевых ресурсов, включая виртуальные сети, подсети и группы безопасности сети, а также выполнение запросов к ним.</span><span class="sxs-lookup"><span data-stu-id="d26e5-109">Create, update, delete, and query network resources including virtual networks, subnets, and network security groups.</span></span> |
| [<span data-ttu-id="d26e5-110">compute/vm_disk</span><span class="sxs-lookup"><span data-stu-id="d26e5-110">compute/vm_disk</span></span>](https://github.com/Azure-Samples/azure-sdk-for-go-samples/blob/master/compute/vm_disk.go) | <span data-ttu-id="d26e5-111">Создание, присоединение, отсоединение, обновление и шифрование дисков данных для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="d26e5-111">Create, attach, detatch, update, and encrypt data disks for a VM.</span></span> |
| [<span data-ttu-id="d26e5-112">compute/vm</span><span class="sxs-lookup"><span data-stu-id="d26e5-112">compute/vm</span></span>](https://github.com/Azure-Samples/azure-sdk-for-go-samples/blob/master/compute/vm.go) | <span data-ttu-id="d26e5-113">Создание, удаление, деактивация и администрирование виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="d26e5-113">Create, update, deactivate, and manage VMs.</span></span> |
| [<span data-ttu-id="d26e5-114">compute/vm_with_availabilityset</span><span class="sxs-lookup"><span data-stu-id="d26e5-114">compute/vm_with_availabilityset</span></span>](https://github.com/Azure-Samples/azure-sdk-for-go-samples/blob/master/compute/vm_with_availabilityset.go) | <span data-ttu-id="d26e5-115">Создание групп доступности и подсистем балансировки нагрузки для виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="d26e5-115">Create availability sets and load balancers for VMs.</span></span> |
| [<span data-ttu-id="d26e5-116">compute/vm_with_identity</span><span class="sxs-lookup"><span data-stu-id="d26e5-116">compute/vm_with_identity</span></span>](https://github.com/Azure-Samples/azure-sdk-for-go-samples/blob/master/compute/vm_with_identity.go) | <span data-ttu-id="d26e5-117">Создание и администрирование Управляемых удостоверений службы (MSI) для виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="d26e5-117">Create and manage Managed Service Identities (MSIs) for VMs.</span></span> |
