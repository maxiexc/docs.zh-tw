---
title: 如何：宣告列舉
ms.date: 07/20/2015
helpviewer_keywords:
- declarations [Visual Basic], enumerations
- enumerations [Visual Basic], declaring
- declaring enumerations [Visual Basic]
ms.assetid: db4ca1c3-f429-4c81-ae81-29e0157b29fd
ms.openlocfilehash: 042aea045313bcaf3832274acf1000f87a084b72
ms.sourcegitcommit: 17ee6605e01ef32506f8fdc686954244ba6911de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/22/2019
ms.locfileid: "74354050"
---
# <a name="how-to-declare-enumerations-visual-basic"></a>如何：宣告列舉 (Visual Basic)
您可以使用類別或模組之宣告區段中的 `Enum` 語句來建立列舉。 您無法在方法中宣告列舉。 若要指定適當的存取層級，請使用 `Private`、`Protected`、`Friend`或 `Public`。  
  
 `Enum` 型別具有名稱、基礎型別，以及一組欄位，每個都代表一個常數。 此名稱必須是有效的 Visual Basic .NET 辨識符號。 基礎類型必須是其中一個整數類型，`Byte`、`Short`、`Long` 或 `Integer`。 預設值為 `Integer`。 列舉一律是強型別，而且無法與整數數位類型互換。  
  
 列舉不能有浮點值。 如果列舉已指派具有 `Option Strict On`的浮點值，則會產生編譯器錯誤。 如果 `Off``Option Strict`，此值會自動轉換成 `Enum` 類型。  
  
 如需名稱的相關資訊，以及如何使用 `Imports` 語句來進行不必要的名稱限定，請參閱列舉[和名稱限定](../../../../visual-basic/programming-guide/language-features/constants-enums/enumerations-and-name-qualification.md)性。  
  
### <a name="to-declare-an-enumeration"></a>若要宣告列舉  
  
1. 撰寫包含程式碼存取層級、`Enum` 關鍵字和有效名稱的宣告，如下列範例所示，每個都宣告不同的 `Enum`。  
  
     [!code-vb[VbEnumsTask#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class2.vb#3)]  
  
2. 定義列舉中的常數。 根據預設，列舉中的第一個常數會初始化為 `0`，而後續的常數會初始化為比上一個常數更多的值。 例如，下列列舉 `Days`包含名為 `Sunday` 的常數，其值為 `0`、名為 `Monday` 且值為 `1`的常數、名為 `Tuesday` 的常數，其值為 `2`等等。  
  
     [!code-vb[VbEnumsTask#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class2.vb#4)]  
  
3. 您可以使用指派語句，明確地將值指派給列舉中的常數。 您可以指派任何整數值，包括負數。 例如，您可能想要值小於零的常數來表示錯誤狀況。 在下列列舉中，會明確地將值指派給常數 `Invalid` `–1`，並將值指派給常數 `Sunday` `0`。 因為它是列舉中的第一個常數，所以 `Saturday` 也會初始化為 `0`的值。 `Monday` 的值 `1` （一個大於 `Sunday`的值）;`Tuesday` 的值為 `2`，依此類推。  
  
     [!code-vb[VbEnumsTask#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class2.vb#5)]  
  
### <a name="to-declare-an-enumeration-as-an-explicit-type"></a>將列舉宣告為明確類型  
  
- 使用 `As` 子句來指定列舉的類型，如下列範例所示。  
  
     [!code-vb[VbEnumsTask#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class2.vb#6)]  
  
## <a name="see-also"></a>請參閱

- [列舉和名稱限定性條件](../../../../visual-basic/programming-guide/language-features/constants-enums/enumerations-and-name-qualification.md)
- [如何：參考列舉成員](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-refer-to-an-enumeration-member.md)
- [如何：在 Visual Basic 中逐一查看列舉](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-iterate-through-an-enumeration.md)
- [如何：決定與列舉值相關聯的字串](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-determine-the-string-associated-with-an-enumeration-value.md)
- [何時使用列舉](../../../../visual-basic/programming-guide/language-features/constants-enums/when-to-use-an-enumeration.md)
- [常數的概觀](../../../../visual-basic/programming-guide/language-features/constants-enums/constants-overview.md)
- [常數和常值資料類型](../../../../visual-basic/programming-guide/language-features/constants-enums/constant-and-literal-data-types.md)
- [常數和列舉](../../../../visual-basic/language-reference/constants-and-enumerations.md)
