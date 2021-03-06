---
title: 可靠的工作階段最佳做法
ms.date: 03/30/2017
ms.assetid: b94f6e01-8070-40b6-aac7-a2cb7b4cb4f2
ms.openlocfilehash: 1d9671e7e3124d535b66de8cd8468f76dcb32b10
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "61857983"
---
# <a name="best-practices-for-reliable-sessions"></a>可靠的工作階段最佳做法

本主題會討論最佳做法的可靠工作階段。

## <a name="setting-maxtransferwindowsize"></a>設定 MaxTransferWindowSize

Windows Communication Foundation (WCF) 中的可靠工作階段會使用傳輸窗口將訊息保留在用戶端和服務。 可設定的屬性 <xref:System.ServiceModel.Channels.ReliableSessionBindingElement.MaxTransferWindowSize%2A> 代表傳輸窗口可保留的訊息數量。

在傳送端，這表示傳輸窗口可以等候認可; 期間保留的訊息數目在接收者，表示要緩衝處理服務的訊息數目。

選擇正確的大小，會影響網路效率和服務的最佳的容量。 下列各節將詳細說明選擇此屬性的值影響的值時的考量事項。

預設的傳輸窗口大小為 8 則訊息。

### <a name="efficient-use-of-the-network"></a>有效率地使用網路

在此情況下，詞彙*網路*對應至為基礎的用戶端 （傳送者） 和服務 （接收者） 之間的通訊使用的所有項目。 這包括傳輸連線及任何媒介或橋接器之間，包括 SOAP 路由器或 HTTP proxy/防火牆。

有效率地使用網路可確保充分運用網路功能。 可以透過網路每秒傳送的資料量 (*資料速率*) 和寄件者的資料傳送至接收者所花費的時間 (*延遲*) 如何有效地影響網路這項承諾。

在傳送端，屬性 <xref:System.ServiceModel.Channels.ReliableSessionBindingElement.MaxTransferWindowSize%2A> 代表其傳輸窗口在等候認可期間能夠保留的訊息數量。 如果網路延遲很高，而且為了確保回應的傳送者和有效的網路使用率，您應該增加傳輸窗口大小。

例如寄件者配合資料速率，其值為即使，延遲可能是高如果寄件者與接收者之間存在好幾個媒介或資料都必須通過失真的媒介或網路。 因此，寄件者必須等候其傳輸窗之訊息的通知，然後再接受新的訊息，以在網路上傳送。 緩衝區小而具有高延遲，較少的有效網路使用率。 相反地，太高的傳輸窗口會影響服務，因為服務可能需要擷取並更新與高比率的用戶端傳送的資料。

### <a name="running-the-service-to-capacity"></a>容量來執行服務

盡可能有效率地使用網路，在理想情況下您也想要達到最佳的產能執行的服務。 接收端上的傳輸窗口大小屬性代表接收端可以緩衝處理的訊息數量。 這項訊息緩衝處理作業不只能協助控制網路流量，同時能讓服務效能發揮到極致。 如果緩衝區是一則訊息，而且訊息抵達服務處理速度的範例，然後網路可能會捨棄訊息，並可能會浪費或是未能充分運用容量。

使用緩衝區會增加服務的可用性，因為能夠一面接收與緩衝處理先前接收的訊息時的訊息。

我們建議使用相同`MaxTransferWindowSize`寄件者和接收者。

### <a name="enabling-flow-control"></a>啟用流量控制

*流量控制*是一種機制可確保傳送者和接收者跟上彼此，也就是訊息會取用及處理，因為它們產生速度。 用戶端與服務上的傳輸窗口大小可確保傳送端與接收端都有同樣合理的同步處理時間。

我們強烈建議您設定屬性<xref:System.ServiceModel.Channels.ReliableSessionBindingElement.FlowControlEnabled%2A>至`true`當您使用 WCF 用戶端和 WCF 服務之間可靠工作階段。

## <a name="setting-maxpendingchannels"></a>設定 MaxPendingChannels

撰寫服務時，可讓來自不同的用戶端的可靠工作階段通訊，就可以有許多用戶端建立的可靠工作階段服務在相同的時間。 在這些情況中，服務將視 `MaxPendingChannels` 屬性做出回應。

當傳送端對接收端建立可靠工作階段通道時，彼此之間的信號交換會建立可靠工作階段。 一旦建立了可靠工作階段，就會將通道放到擱置的通道佇列中，等候服務來接受它。 `MaxPendingChannels` 屬性代表可處於此狀態的通道數量。

很可能是它無法在此接受多個通道的狀態中的服務。 如果佇列已滿，嘗試建立可靠工作階段遭到拒絕，並在用戶端必須重試一次。

此外，也可以在佇列中擱置的通道保持在佇列中持續時間較長。 在此同時，可靠工作階段閒置逾時可能會發生，導致通道轉換至 faulted 狀態。

在撰寫時同時服務多個用戶端的服務，您應該設定為適合您需求的值。 設定太高的值`MaxPendingChannels`屬性會影響您的工作集。

預設值為<xref:System.ServiceModel.Channels.ReliableSessionBindingElement.MaxPendingChannels%2A>是四個通道。

## <a name="reliable-sessions-and-hosting"></a>可靠工作階段與裝載

Web 裝載的服務，會使用可靠工作階段時，您應該記住下列重要事項：

- 可靠工作階段是可設定狀態的，而且可透過 AppDomain 來維護狀態。 意思就是，所有屬於可靠工作階段一部分的訊息，都必須透過同一個 AppDomain 來處理。 Web 伺服陣列與 web 處理序區伺服陣列或處理序區的大小大於一個節點無法保證此條件約束。

- 使用雙重 HTTP 通道的可靠工作階段 (例如，使用`WsDualHttpBinding`) 可能需要超過兩個 HTTP 連線每個用戶端的預設值。 這表示雙工可靠工作階段可能需要最多兩個連線每種方法，因為並行的應用程式與通訊協定訊息可以在任何時候傳輸每種方法。 某些狀況下根據服務的訊息交換模式，這表示它是可能發生死結 web 裝載的服務，使用雙重 HTTP 與可靠工作階段。 若要增加允許的 HTTP 連線，每個用戶端數目，將下列新增至相關的組態檔 (例如*web.config*有問題的服務):

  ```xml
  <configuration>
    <system.net>
      <connectionManagement>
        <add name="*" maxconnection="4" />
      </connectionManagement>
    </system.net>
  </configuration>
  ```

  值`maxconnection`屬性是所需的連線數。 在此情況下，至少應該是四個連線。
