---
title: 在 openSUSE 15 安裝 .NET 內核 - 套件管理員 - .NET 內核 - 套件管理員 - .NET 內核
description: 使用包管理員在 openSUSE 15 上安裝 .NET 核心 SDK 和執行時。
author: thraka
ms.author: adegeo
ms.date: 03/17/2020
ms.openlocfilehash: fc4c9e30ddb0cfd3e6fe79fa4f78206f4700eeee
ms.sourcegitcommit: 62285ec11fa8e8424bab00511a90760c60e63c95
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/20/2020
ms.locfileid: "81645668"
---
# <a name="opensuse-15-package-manager---install-net-core"></a>openSUSE 15 套件管理員 - 安裝 .NET 內核

[!INCLUDE [package-manager-switcher](./includes/package-manager-switcher.md)]

本文介紹如何使用包管理器在 openSUSE 15 上安裝 .NET Core。

[!INCLUDE [package-manager-intro-sdk-vs-runtime](includes/package-manager-intro-sdk-vs-runtime.md)]

## <a name="add-microsoft-repository-key-and-feed"></a>新增 Microsoft 儲存函式庫金鑰和來源

在安裝 .NET 之前,您需要:

- 將 Microsoft 包簽署金鑰添加到受信任金鑰清單中。
- 將儲存庫添加到包管理員。
- 安裝所需的依賴項。

每部電腦只需要執行這項作業一次。

打開終端並運行以下命令。

```bash
sudo zypper install libicu
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
wget https://packages.microsoft.com/config/opensuse/15/prod.repo
sudo mv prod.repo /etc/zypp/repos.d/microsoft-prod.repo
sudo chown root:root /etc/zypp/repos.d/microsoft-prod.repo
```

## <a name="install-the-net-core-sdk"></a>安裝 .NET 核心 SDK

更新可供安裝的產品,然後安裝 .NET 核心 SDK。 在終端中,運行以下命令。

```bash
sudo zypper install dotnet-sdk-3.1
```

## <a name="install-the-aspnet-core-runtime"></a>安裝ASP.NET核心執行時

更新可供安裝的產品,然後安裝ASP.NET運行時。 在終端中,運行以下命令。

```bash
sudo zypper install aspnetcore-runtime-3.1
```

## <a name="install-the-net-core-runtime"></a>安裝 .NET 核心執行時

更新可用於安裝的產品,然後安裝 .NET Core 運行時。 在終端中,運行以下命令。

```bash
sudo zypper install dotnet-runtime-3.1
```

## <a name="how-to-install-other-versions"></a>如何安裝其他版本

[!INCLUDE [package-manager-switcher](./includes/package-manager-heading-hack-pkgname.md)]

## <a name="troubleshoot-the-package-manager"></a>排除套件管理員故障

本節提供有關在使用包管理器安裝 .NET Core 時可能得到的常見錯誤的資訊。

### <a name="failed-to-fetch"></a>無法擷取

[!INCLUDE [package-manager-failed-to-fetch-rpm](includes/package-manager-failed-to-fetch-rpm.md)]
