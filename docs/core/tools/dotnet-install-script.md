---
title: dotnet-install 指令碼
description: 瞭解安裝 .NET Core SDK 和共用執行時間的 dotnet-安裝腳本。
ms.date: 04/30/2020
ms.openlocfilehash: 6728708ac5154f558954b46a22a434b05a548e84
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/12/2020
ms.locfileid: "83205921"
---
# <a name="dotnet-install-scripts-reference"></a>dotnet-install 指令碼參考

## <a name="name"></a>名稱

`dotnet-install.ps1` | `dotnet-install.sh`-用來安裝 .NET Core SDK 和共用執行時間的腳本。

## <a name="synopsis"></a>概要

Windows：

```powershell
dotnet-install.ps1 [-Architecture <ARCHITECTURE>] [-AzureFeed]
    [-Channel <CHANNEL>] [-DryRun] [-FeedCredential]
    [-InstallDir <DIRECTORY>] [-JSonFile <JSONFILE>]
    [-NoCdn] [-NoPath] [-ProxyAddress]
    [-ProxyUseDefaultCredentials] [-Runtime <RUNTIME>]
    [-SkipNonVersionedFiles] [-UncachedFeed] [-Verbose]
    [-Version <VERSION>]

dotnet-install.ps1 -Help
```

Linux/macOs：

```bash
dotnet-install.sh  [--architecture <ARCHITECTURE>] [--azure-feed]
    [--channel <CHANNEL>] [--dry-run] [--feed-credential]
    [--install-dir <DIRECTORY>] [--jsonfile <JSONFILE>]
    [--no-cdn] [--no-path] [--runtime <RUNTIME>] [--runtime-id <RID>]
    [--skip-non-versioned-files] [--uncached-feed] [--verbose]
    [--version <VERSION>]

dotnet-install.sh --help
```

## <a name="description"></a>描述

這些 `dotnet-install` 腳本是用來執行 .NET Core SDK 的非系統管理員安裝，其中包括 .NET Core CLI 和共用執行時間。

建議您使用穩定版本的腳本：

- Bash （Linux/macOS）：<https://dot.net/v1/dotnet-install.sh>
- PowerShell （Windows）：<https://dot.net/v1/dotnet-install.ps1>

這些指令碼對於自動化案例和非系統管理員安裝非常有幫助。 有兩個指令碼：一個是在 Windows 上運作的 PowerShell 指令碼，另一個是在 Linux/macOS 上運作的 Bash 指令碼。 這兩個指令碼有相同的行為。 Bash 指令碼也能讀取 PowerShell 參數，因此您可以搭配 PowerShell 參數使用 Linux/macOS 系統上的指令碼。

安裝指令碼會從 CLI 組建放置區下載 ZIP/tarball 檔案，並且繼續將它安裝在預設位置或 `-InstallDir|--install-dir` 所指定的位置。 根據預設，安裝指令碼會下載並安裝 SDK。 如果您想要只取得共用執行階段，請指定 `-Runtime|--runtime` 引數。

根據預設，指令碼會將安裝位置新增到目前工作階段的 $PATH。 指定 `-NoPath|--no-path` 引數可以覆寫此預設行為。

執行指令碼之前，請安裝所有必要的[相依性 (英文)](../install/dependencies.md)。

您可以使用 `-Version|--version` 引數安裝特定版本。 版本必須指定為三部分版本（例如 `2.1.0` ）。 如果未提供，就會使用 `latest` 版本。

安裝腳本不會更新 Windows 上的登錄。 他們只需要下載壓縮的二進位檔，並將它們複製到資料夾即可。 如果您想要更新登錄機碼值，請使用 .NET Core 安裝程式。

## <a name="options"></a>選項

- **`-Architecture|--architecture <ARCHITECTURE>`**

  要安裝的 .NET Core 二進位檔的架構。 可能的值為 `<auto>`、`amd64`、`x64`、`x86`、`arm64` 和 `arm`。 預設值為 `<auto>`，代表目前正在執行的 OS 架構。

- **`-AzureFeed|--azure-feed`**

  指定給安裝程式的 Azure 摘要 URL。 建議您不要變更這個值。 預設值是 `https://dotnetcli.azureedge.net/dotnet`。

- **`-Channel|--channel <CHANNEL>`**

  指定安裝的來源通道。 可能的值包括：

  - `Current` - 最新版本。
  - `LTS` - 長期支援通道 (最新的支援版本)。
  - 代表特定版本的 X.Y 格式兩段式版本 (例如 `2.1` 或 `3.0`)。
  - 分支名稱：例如， `release/3.1.1xx` 或 `master` （針對夜間版本）。 使用此選項可從預覽頻道安裝版本。 使用[安裝程式和二進位](https://github.com/dotnet/core-sdk#installers-and-binaries)檔中列出的通道名稱。

  預設值是 `LTS`。 如需有關 .NET 支援通道的詳細資訊，請參閱 [.NET Core 支援政策](https://dotnet.microsoft.com/platform/support/policy/dotnet-core) \(英文\) 頁面。

- **`-DryRun|--dry-run`**

  如果設定，指令碼將不會執行安裝。 取而代之的是，會顯示以一致方式安裝目前所要求的 .NET Core CLI 版本時，所要使用的命令列。 例如，如果您指定 `latest` 版本，就會顯示特定版本的連結，以便在建置指令碼中以決定性方式使用此命令。 如果您想要自行進行安裝或下載，它也會顯示二進位檔位置。

- **`-FeedCredential|--feed-credential`**

  用來作為要附加至 Azure 摘要的查詢字串。 這可允許變更 URL 以使用非公用 Blob 儲存體帳戶。

- **`-Help|--help`**

  印出指令碼的說明。

- **`-InstallDir|--install-dir <DIRECTORY>`**

  指定安裝路徑。 如果目錄不存在，則會建立它。 預設值是 *%LocalAppData%\Microsoft\dotnet*。 二進位檔會直接放在此目錄中。

- **`-JSonFile|--jsonfile <JSONFILE>`**

  指定將用來判斷 SDK 版本之[global json](global-json.md)檔案的路徑。 *Global. json*檔案必須有的值 `sdk:version` 。

- **`-NoCdn|--no-cdn`**

  不允許從 [Azure 內容傳遞網路 (CDN)](https://docs.microsoft.com/azure/cdn/cdn-overview) 下載，而直接使用未快取的摘要。

- **`-NoPath|--no-path`**

  如果設定，就不會將安裝資料夾匯出至目前工作階段的路徑。 根據預設，腳本會修改路徑，使 .NET Core CLI 在安裝後立即可供使用。

- **`-ProxyAddress`**

  如果設定，安裝程式會使用此 Proxy 進行 Web 要求。 （僅適用于 Windows。）

- **`ProxyUseDefaultCredentials`**

  如果設定，當使用 Proxy 位址時，安裝程式會使用目前使用者的認證。 （僅適用于 Windows。）

- **`-Runtime|--runtime <RUNTIME>`**

  只安裝共用執行階段，而不是整個 SDK。 可能的值包括：

  - `dotnet` - `Microsoft.NETCore.App` 共用執行階段。
  - `aspnetcore` - `Microsoft.AspNetCore.App` 共用執行階段。
  - `windowsdesktop` - `Microsoft.WindowsDesktop.App` 共用執行階段。

- **`--runtime-id <RID>`**

  指定要安裝工具的[執行時間識別碼](../rid-catalog.md)。 用於 `linux-x64` 可移植的 Linux。 （僅適用于 Linux/macOS）。

- **`-SharedRuntime|--shared-runtime`**

  > [!NOTE]
  > 此參數已被淘汰，在未來的指令碼版本中可能會將其移除。 建議的替代方案是 `-Runtime|--runtime` 選項。

  只安裝共用執行階段位元，而不是整個 SDK。 此選項相當於指定 `-Runtime|--runtime dotnet` 。

- **`-SkipNonVersionedFiles|--skip-non-versioned-files`**

  如果已經有非版本控制的檔案 (例如 *dotnet.exe*) 存在，便略過其安裝。

- **`-UncachedFeed|--uncached-feed`**

  允許變更此安裝程式所使用之未快取摘要的 URL。 建議您不要變更這個值。

- **`-Verbose|--verbose`**

  顯示診斷資訊。

- **`-Version|--version <VERSION>`**

  代表特定的組建版本。 可能的值包括：

  - `latest` - 通道上的最新組建 (與 `-Channel` 選項搭配使用)。
  - `coherent` - 通道上的最新一致性組建；使用最新的穩定套件組合 (與分支名稱 `-Channel` 選項搭配使用)。
  - 代表特定組建版本的 X.Y.Z 格式三段式版本；取代 `-Channel` 選項。 例如： `2.0.0-preview2-006120` 。

  如果未指定，`-Version` 會預設為 `latest`。

## <a name="examples"></a>範例

- 將最新的長期支援 (LTS) 版本安裝至預設位置︰

  Windows：

  ```powershell
  ./dotnet-install.ps1 -Channel LTS
  ```

  macOS/Linux：

  ```bash
  ./dotnet-install.sh --channel LTS
  ```

- 將3.1 通道的最新版本安裝至指定的位置：

  Windows：

  ```powershell
  ./dotnet-install.ps1 -Channel 3.1 -InstallDir C:\cli
  ```

  macOS/Linux：

  ```bash
  ./dotnet-install.sh --channel 3.1 --install-dir ~/cli
  ```

- 安裝共用執行時間的3.0.0 版本：

  Windows：

  ```powershell
  ./dotnet-install.ps1 -Runtime dotnet -Version 3.0.0
  ```

  macOS/Linux：

  ```bash
  ./dotnet-install.sh --runtime dotnet --version 3.0.0
  ```

- 取得指令碼並在公司 Proxy 後方安裝 2.1.2 版本 (僅適用於 Windows)：

  ```powershell
  Invoke-WebRequest 'https://dot.net/v1/dotnet-install.ps1' -Proxy $env:HTTP_PROXY -ProxyUseDefaultCredentials -OutFile 'dotnet-install.ps1';
  ./dotnet-install.ps1 -InstallDir '~/.dotnet' -Version '2.1.2' -ProxyAddress $env:HTTP_PROXY -ProxyUseDefaultCredentials;
  ```

- 取得指令碼並安裝 .NET Core CLI 單行範例：

  Windows：

  ```powershell
  # Run a separate PowerShell process because the script calls exit, so it will end the current PowerShell session.
  &powershell -NoProfile -ExecutionPolicy unrestricted -Command "[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12; &([scriptblock]::Create((Invoke-WebRequest -UseBasicParsing 'https://dot.net/v1/dotnet-install.ps1'))) <additional install-script args>"
  ```

  macOS/Linux：

  ```bash
  curl -sSL https://dot.net/v1/dotnet-install.sh | bash /dev/stdin <additional install-script args>
  ```

## <a name="see-also"></a>請參閱

- [.NET Core 版本](https://github.com/dotnet/core/releases)
- [.NET Core 執行階段和 SDK 下載封存](https://github.com/dotnet/core/blob/master/release-notes/download-archive.md)
