---
title: 要求-回覆服務
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Communication Foundation [WCF], request-reply services
- contracts [WCF], request-reply services
- WCF [WCF], request-reply services
- request-reply contracts [WCF]
ms.assetid: 2fa710f1-47f4-4598-b063-3ab3bd22ebba
ms.openlocfilehash: f58da6f1cdaad1b976659ee2e9febe12cc07726f
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/14/2019
ms.locfileid: "70991147"
---
# <a name="request-reply-services"></a>要求-回覆服務
要求-回復服務是 Windows Communication Foundation （WCF）中的預設作業合約類型。 用戶端呼叫服務作業然後等候服務回應。 您可以使用同步 (用戶端會鎖定，直到其接收到來自服務或呼叫階段的回應) 或非同步 (用戶端會呼叫服務作業、繼續工作，然後接收來自其他執行緒服務的回應) 方式呼叫服務作業。  
  
 若要建立要求-回覆服務合約，請定義服務合約然後將 <xref:System.ServiceModel.OperationContractAttribute> 類別套用至每個作業，如同下列範例程式碼所示。  
  
```csharp
[ServiceContract(Namespace="http://Microsoft.ServiceModel.Samples")]  
public interface IRequestReplyCalculator  
{  
    [OperationContract]  
    double Add(double n1, double n2);  
}  
```  
  
 您不需要將 <xref:System.ServiceModel.OperationContractAttribute.IsOneWay%2A> 屬性設定為 `false`，因為這是預設行為。  
  
## <a name="see-also"></a>另請參閱

- [單向服務](../../../../docs/framework/wcf/feature-details/one-way-services.md)
- [雙工服務](../../../../docs/framework/wcf/feature-details/duplex-services.md)
