---
title: 摘要
description: 針對 Azure 指南/電子書架構雲端原生 .NET 應用程式的關鍵結論摘要。
ms.date: 04/29/2020
ms.openlocfilehash: 8cad8df1f69e159caf88d3ee119278dff8726385
ms.sourcegitcommit: 046a9c22487551360e20ec39fc21eef99820a254
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/14/2020
ms.locfileid: "83395325"
---
# <a name="summary"></a>摘要

總而言之，以下是本指南的重要結論：

- **雲端原生**是關於設計現代化的應用程式，以在現代化的動態環境（例如公用、私人和混合式雲端）中採用快速的變更、大規模和復原能力。

- **[雲端原生運算基礎](https://www.cncf.io/)（由 cncf）** 是一種具影響力的開放原始碼協會，屬於超過300個主要企業。 它負責推動跨技術和雲端堆疊採用雲端原生運算。

- **由 cncf 指導方針**建議，雲端原生應用程式採用六個重要的支柱，如圖11-1 所示：

  ![雲端原生基本要素](./media/cloud-native-foundational-pillars.png)

  **圖 11-1**. 雲端原生基本要素

- 這些雲端原生的支柱包括：
  - 雲端及其基礎服務模型
  - 現代化設計原則
  - 微服務
  - 容器化和容器協調流程
  - 以雲端為基礎的支援服務，例如資料庫和訊息代理程式
  - 自動化，包括基礎結構即程式碼和程式碼部署

- **Kubernetes**是大部分雲端原生應用程式選擇的裝載環境。 較小的簡單服務有時會裝載在無伺服器平臺中，例如 Azure Functions。 在許多重要的自動化功能中，這兩種環境都會提供自動調整來處理變動量的工作負載。

- 在建立雲端原生應用程式時，**服務通訊**會成為重要的設計決策。 應用程式通常會公開 API 閘道來管理前端用戶端通訊。 之後，後端微服務會盡可能地與彼此進行通訊，以執行非同步通訊模式。

- **gRPC**是一種現代化、高效能的架構，它會演變過時的遠端程序呼叫（RPC）通訊協定。 雲端原生應用程式通常會採用 gRPC 來簡化後端服務之間的訊息處理。 gRPC 會使用 HTTP/2 作為其傳輸通訊協定。 其最高可達8倍，而不是以較小的訊息大小為60-80% 的 JSON 序列化。 gRPC 是開放原始碼，並由雲端原生運算基礎（由 CNCF）所管理。

- **分散式資料**是雲端原生應用程式通常會執行的模型。 應用程式會將商務功能隔離成小型、獨立的微服務。 每個微服務都會封裝自己的相依性、資料和狀態。 傳統的共用資料庫模型會演變成許多較小資料庫的其中一個，且每一個都與一個微服務對齊。 當冒煙清除時，我們會形成一個可公開模型的設計 `database-per-microservice` 。

- **無-SQL 資料庫**會參考高效能、非關聯式資料存放區。 他們在 excel 中使用易用性、擴充性、彈性和可用性等特性。 需要次要秒數回應時間的高容量服務，傾向于 NoSQL 資料存放區。 分散式雲端原生系統的 NoSQL 技術激增無法十分出色。

- **NewSQL**是一種新興的資料庫技術，結合了 NoSQL 的分散式擴充性和關係資料庫的 ACID 保證。 NewSQL 資料庫的目標是必須跨分散式環境處理大量資料的商務系統，其具有完整的交易/ACID 合規性。 雲端原生運算基礎（由 CNCF）具備數個 NewSQL 資料庫專案。

- **復原**是指您的系統對失敗做出反應的能力，而且仍然可以繼續運作。 雲端原生系統採用無法避免失敗的分散式架構。 應用程式必須經過結構化，才能回應適當地失敗並快速恢復為完全正常運作的狀態。

- **服務網格**是可設定的基礎結構層，具有可處理服務通訊和其他跨領域挑戰的內建功能。 它們會將跨領域責任與您的商務程式碼分離。 這些責任會移入服務 proxy。 稱為 `Sidecar pattern` ，proxy 會部署到個別的進程，以提供與商務程式碼的隔離。

- **可檢視性**是雲端原生應用程式的重要設計考慮。 當服務分散到節點叢集、集中式記錄、監視和警示時，就變成強制性。 Azure 監視器是以雲端為基礎的工具集合，其設計目的是要提供系統狀態的可見度。

- **基礎結構**即程式碼是廣為接受的最佳做法，可將平臺布建自動化。 您的基礎結構和部署會自動化、一致且可重複。 Azure Resource Manager、Terraform 和 Azure CLI 等工具，可讓您以宣告方式編寫腳本所需的雲端基礎結構。

- 程式**代碼自動化**是雲端原生應用程式的需求。 新式 CI/CD 系統有助於滿足此原則。 它們提供個別的組建和部署步驟，協助確保一致和品質的程式碼。 組建階段會將程式碼轉換成二進位成品。 發行階段會挑選二進位成品、套用外部環境設定，並將其部署至指定的環境。 Azure DevOps 和 GitHub 是功能完整的 DevOps 環境。

>[!div class="step-by-step"]
>[上一步](application-bundles.md)
