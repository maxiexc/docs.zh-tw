---
title: SecurityBindingElement
ms.date: 03/30/2017
ms.assetid: ef93b6e6-3524-48a8-94d3-c8837f1872f9
ms.openlocfilehash: 1d367d0c5d14e6e75539dd2b20cdffcf2b34963d
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "61962782"
---
# <a name="securitybindingelement"></a>SecurityBindingElement
SecurityBindingElement  
  
## <a name="syntax"></a>語法  
  
```csharp
class SecurityBindingElement : BindingElement  
{  
  string DefaultAlgorithmSuite;  
  boolean IncludeTimestamp;  
  string KeyEntropyMode;  
  LocalServiceSecuritySettings LocalServiceSecuritySettings;  
  string MessageSecurityVersion;  
  string SecurityHeaderLayout;  
};  
```  
  
## <a name="methods"></a>方法  
 SecurityBindingElement 類別不會定義任何方法。  
  
## <a name="properties"></a>屬性  
 SecurityBindingElement 類別具有下列屬性：  
  
### <a name="defaultalgorithmsuite"></a>DefaultAlgorithmSuite  
 資料型別：字串  
  
 存取類型：唯讀  
  
 指定要與繫結一起使用的演算法。  
  
### <a name="includetimestamp"></a>IncludeTimestamp  
 資料型別：布林值  
  
 存取類型：唯讀  
  
 布林值，這個值會指定每個訊息是否包含時間戳記。  
  
### <a name="keyentropymode"></a>KeyEntropyMode  
 資料型別：字串  
  
 存取類型：唯讀  
  
 用於建立金鑰的 Entropy 來源。  
  
### <a name="localservicesecuritysettings"></a>LocalServiceSecuritySettings  
 資料類型：LocalServiceSecuritySettings  
  
 存取類型：唯讀  
  
 用於本機服務的繫結特定安全性屬性。  
  
### <a name="messagesecurityversion"></a>MessageSecurityVersion  
 資料型別：字串  
  
 存取類型：唯讀  
  
 用於訊息安全性的版本。  
  
### <a name="securityheaderlayout"></a>SecurityHeaderLayout  
 資料型別：字串  
  
 存取類型：唯讀  
  
 此繫結之安全性標頭中的項目順序。  
  
## <a name="requirements"></a>需求  
  
|MOF|於 Servicemodel.mof 中宣告。|  
|---------|-----------------------------------|  
|命名空間|於 root\ServiceModel 中定義|  
  
## <a name="see-also"></a>另請參閱

- <xref:System.ServiceModel.Channels.SecurityBindingElement>
