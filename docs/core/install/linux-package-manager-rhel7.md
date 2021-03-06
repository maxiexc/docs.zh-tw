---
title: 在 Linux RHEL 7 套裝軟體管理器上安裝 .NET 核心 - .NET 核心
description: 使用包管理器在 RHEL 7 上安裝 .NET 核心 SDK 和運行時。
author: thraka
ms.author: adegeo
ms.date: 03/17/2020
ms.openlocfilehash: d1f1372b32c7b2471a96492d48aab5533dadb64a
ms.sourcegitcommit: 07123a475af89b6da5bb6cc51ea40ab1e8a488f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/24/2020
ms.locfileid: "80134207"
---
# <a name="rhel-7-package-manager---install-net-core"></a>RHEL 7 套裝軟體管理器 - 安裝 .NET 核心

[!INCLUDE [package-manager-switcher](includes/package-manager-switcher.md)]

本文介紹如何使用包管理器在 RHEL 7 上安裝 .NET Core。

[!INCLUDE [package-manager-intro-sdk-vs-runtime](includes/package-manager-intro-sdk-vs-runtime.md)]

## <a name="register-your-red-hat-subscription"></a>註冊您的紅帽訂閱

要在 RHEL 上安裝來自紅帽的 .NET 核心，首先需要使用紅帽訂閱管理器進行註冊。 如果系統上尚未完成此操作，或者不確定，請參閱[.NET Core 的紅帽產品文檔](https://access.redhat.com/documentation/net_core/)。

## <a name="install-the-net-core-sdk"></a>安裝 .NET Core SDK

向訂閱管理器註冊後，即可安裝並啟用 .NET 核心 SDK。 在終端中，運行以下命令以啟用 RHEL 7 點網通道並安裝。

```bash
subscription-manager repos --enable=rhel-7-server-dotnet-rpms
yum install rh-dotnet31 -y
scl enable rh-dotnet31 bash
```

## <a name="install-the-aspnet-core-runtime"></a>安裝ASP.NET核心運行時

向訂閱管理器註冊後，即可安裝並啟用ASP.NET核心運行時。 在終端中，運行以下命令。

```bash
subscription-manager repos --enable=rhel-7-server-dotnet-rpms
yum install rh-dotnet31-aspnetcore-runtime-3.1 -y
scl enable rh-dotnet31 bash
```

## <a name="install-the-net-core-runtime"></a>安裝 .NET 核心運行時

註冊訂閱管理器後，即可安裝並啟用 .NET 核心運行時。 在終端中，運行以下命令。

```bash
subscription-manager repos --enable=rhel-7-server-dotnet-rpms
yum install rh-dotnet31-dotnet-runtime-3.1 -y
scl enable rh-dotnet31 bash
```

## <a name="see-also"></a>另請參閱

- [在紅帽企業 Linux 7 上使用 .NET 核心 3.1](https://access.redhat.com/documentation/en-us/net_core/3.1/html/getting_started_guide/gs_install_dotnet)
