---
title: 如何聲明和使用讀寫屬性 - C# 程式設計指南
ms.date: 07/20/2015
helpviewer_keywords:
- get accessor [C#], declaring properties
- set accessor [C#]
- properties [C#], declaring
- read/write properties [C#]
- accessors [C#], declaring properties with
ms.assetid: a4962fef-af7e-4c4b-a929-4ae4d646ab8a
ms.openlocfilehash: 4b9db5f15746ab9a1f42239150c6783154723371
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/14/2020
ms.locfileid: "79170282"
---
# <a name="how-to-declare-and-use-read-write-properties-c-programming-guide"></a>如何聲明和使用讀寫屬性（C# 程式設計指南）
屬性會提供公用資料成員的便利性，卻沒有不受保護、控制和驗證存取物件資料所附帶的風險。 這是透過「存取子」** 完成的：從基礎資料成員指派和擷取值的特殊方法。 [set](../../language-reference/keywords/set.md) 存取子可讓資料成員被指派，而 [get](../../language-reference/keywords/get.md) 存取子可擷取資料成員值。  
  
 這個範例會示範有兩個屬性的 `Person` 類別：`Name` (字串) 和 `Age` (整數)。 這兩個屬性都提供 `get` 和 `set` 存取子，所以它們被視為讀取/寫入屬性。  
  
## <a name="example"></a>範例  
 [!code-csharp[csProgGuideObjects#33](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#33)]  
  
## <a name="robust-programming"></a>穩固程式設計  
 在上例中，`Name` 和 `Age` 屬性是[公用的](../../language-reference/keywords/public.md)，且同時包含 `get` 和 `set` 存取子。 這可讓任何物件讀取和寫入這些屬性。 但有時候會很想排除其中一個存取子。 例如，省略 `set` 存取子會讓屬性變成唯讀的：  
  
 [!code-csharp[csProgGuideObjects#87](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#87)]  
  
 或者，您也可以向公眾公開某個存取子，但讓其他存取子為私用或受保護的。 如需詳細資訊，請參閱[非對稱存取子的存取範圍](./restricting-accessor-accessibility.md)。  
  
 屬性一旦宣告，即可當成類別的欄位使用。 這在取得和設定屬性值時，可使用非常自然的語法，如下列陳述式所示：  
  
 [!code-csharp[csProgGuideObjects#35](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#35)]  
  
 請注意，在屬性 `set` 方法中提供特殊的 `value` 變數。 此變數包含使用者指定的值，例如：  
  
 [!code-csharp[csProgGuideObjects#36](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#36)]  
  
 請注意可以使用更簡潔的語法在 `Person` 物件上遞增 `Age` 屬性：  
  
 [!code-csharp[csProgGuideObjects#37](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#37)]  
  
 如果分別使用 `set` 和 `get` 方法建立了屬性模型，對等的程式碼可能看起來像這樣：  
  
```csharp  
person.SetAge(person.GetAge() + 1);
```  
  
 本例中覆寫 `ToString` 方法：  
  
 [!code-csharp[csProgGuideObjects#38](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#38)]  
  
 請注意，程式中未明確使用 `ToString`。 預設會由 `WriteLine` 呼叫叫用。  
  
## <a name="see-also"></a>另請參閱

- [C# 程式設計指南](../index.md)
- [屬性](./properties.md)
- [類別和結構](./index.md)
