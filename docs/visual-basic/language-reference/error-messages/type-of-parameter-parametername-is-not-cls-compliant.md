---
title: 參數 '<parametername>' 的類型不符合 CLS 標準
ms.date: 07/20/2015
f1_keywords:
- vbc40028
- bc40028
helpviewer_keywords:
- BC40028
ms.assetid: dfa1f6f9-bb88-44ad-b85f-149144363d41
ms.openlocfilehash: 1f671b75972642670e28b9e761a8174d02d39c4e
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/15/2019
ms.locfileid: "65642169"
---
# <a name="type-of-parameter-parametername-is-not-cls-compliant"></a>參數的型別 '\<參數名稱 >' 不符合 CLS 標準
程序標示為`<CLSCompliant(True)>`但宣告參數的類型會標示為`<CLSCompliant(False)>`、 未標示，或因為它不符合規範的型別不符合資格。  
  
 程序必須只使用符合 CLS 規範的型別，才能夠符合[語言獨立性以及與語言無關的元件](../../../standard/language-independence-and-language-independent-components.md) (CLS) 標準。 這適用於參數型別、傳回型別及其所有區域變數的型別。  
  
 下列 Visual Basic 資料類型不符合 CLS 標準：  
  
- [SByte 資料類型](../../../visual-basic/language-reference/data-types/sbyte-data-type.md)  
  
- [UInteger 資料類型](../../../visual-basic/language-reference/data-types/uinteger-data-type.md)  
  
- [ULong 資料類型](../../../visual-basic/language-reference/data-types/ulong-data-type.md)  
  
- [UShort 資料類型](../../../visual-basic/language-reference/data-types/ushort-data-type.md)  
  
 將 <xref:System.CLSCompliantAttribute> 套用至程式設計項目時，請將屬性的 `isCompliant` 參數設定為 `True` 或 `False` ，表示符合標準或不符合標準。 這個參數沒有預設值，您必須提供值。  
  
 如果您未將 <xref:System.CLSCompliantAttribute> 套用至項目，則視為不符合標準。  
  
 根據預設，這個訊息是一個警告。 如需隱藏警告或將警告視為錯誤的相關資訊，請參閱 [Configuring Warnings in Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic)。  
  
 **錯誤 ID:** BC40028  
  
## <a name="to-correct-this-error"></a>更正這個錯誤  
  
- 如果程序必須接受此特定型別的參數，移除<xref:System.CLSCompliantAttribute>。 程序不符合 CLS 規範。  
  
- 如果該程序必須符合 CLS 標準，變更此參數的型別以最符合 CLS 規範的型別。 例如，如果您不需要 2,147,483,647 以上的值範圍，而且不使用 `UInteger` ，則可能可以使用 `Integer` 。 如果您需要擴充範圍，則可以將 `UInteger` 取代為 `Long`。  
  
- 如果您要使用的 Automation 或 COM 物件，請記住，某些類型會有不同的資料寬度比在.NET Framework。 例如，`int` 在其他環境中通常是 16 位元。 如果您接受此元件從 16 位元整數，將它宣告為`Short`而不是`Integer`中受管理的 Visual Basic 程式碼。
