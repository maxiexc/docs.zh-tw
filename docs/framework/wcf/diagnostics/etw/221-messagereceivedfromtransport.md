---
title: 221 - MessageReceivedFromTransport
ms.date: 03/30/2017
ms.assetid: 4995f0d5-c182-4d97-981f-6951da6df1fb
ms.openlocfilehash: 98dbf2728242fa73b3e54b7cf32f9e227e5251b2
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "61781715"
---
# <a name="221---messagereceivedfromtransport"></a>221 - MessageReceivedFromTransport
## <a name="properties"></a>屬性  
  
|||  
|-|-|  
|識別碼|221|  
|關鍵字|EndToEndMonitoring，Troubleshooting，ServiceModel|  
|層級|資訊|  
|通道|Microsoft-Windows-Application Server-Applications/Analytic|  
  
## <a name="description"></a>描述  
 當服務模型收到來自傳輸的訊息時，便會發生此事件。  
  
## <a name="message"></a>訊息  
 發送器收到來自傳輸的訊息。 相互關聯 ID == '%1'。  
  
## <a name="details"></a>詳細資料  
  
|資料項目名稱|資料項目型別|描述|  
|--------------------|--------------------|-----------------|  
|相互關聯 ID|`xs:GUID`|活動識別碼，會將來自服務或用戶端的 `MessageSentToTransport` 事件，與另一端對應的 `MessageReceivedFromTransport` 相互關聯。|  
|HostReference|`xs:string`|若為 Web 託管服務，此欄位會唯一識別 Web 階層架構中的服務。 其格式定義為 ' Web Site Name Application Virtual Path&#124;Service Virtual Path&#124;ServiceName'。 範例：' Default Web Site/CalculatorApplication&#124;/CalculatorService.svc&#124;CalculatorService'。|  
|AppDomain|`xs:string`|由 AppDomain.CurrentDomain.FriendlyName 傳回的字串。|
