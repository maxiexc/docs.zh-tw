---
title: ParamArray
ms.date: 07/20/2015
f1_keywords:
- vb.ParamArray
- ParamArray
helpviewer_keywords:
- ParamArray keyword [Visual Basic]
- ParamArray keyword [Visual Basic], syntax
ms.assetid: a5f18789-92bd-488f-9c7e-cf3719963635
ms.openlocfilehash: fbc87bffebc265e6062512e96fc29a64334b3c65
ms.sourcegitcommit: 17ee6605e01ef32506f8fdc686954244ba6911de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/22/2019
ms.locfileid: "74351365"
---
# <a name="paramarray-visual-basic"></a>ParamArray (Visual Basic)
指定程式參數接受指定之類型的選擇性元素陣列。 `ParamArray` 只能用在參數清單的最後一個參數上。  
  
## <a name="remarks"></a>備註  
 `ParamArray` 可讓您將任意數目的引數傳遞至程式。 `ParamArray` 參數一律使用[ByVal](../../../visual-basic/language-reference/modifiers/byval.md)來宣告。  
  
 您可以藉由傳遞適當資料類型的陣列、以逗號分隔的值清單，或完全沒有任何內容，將一個或多個引數提供給 `ParamArray` 參數。 如需詳細資訊，請參閱[參數陣列](../../../visual-basic/programming-guide/language-features/procedures/parameter-arrays.md)中的「呼叫 ParamArray」。  
  
> [!IMPORTANT]
> 當您處理可能會無限大的陣列時，會有 overrunning 應用程式的一些內部容量的風險。 如果您接受來自呼叫程式碼的參數陣列，您應該測試其長度，如果對您的應用程式而言太大，則採取適當的步驟。  
  
 `ParamArray` 修飾詞可用於以下內容：  
  
 [Declare 陳述式](../../../visual-basic/language-reference/statements/declare-statement.md)  
  
 [Function 陳述式](../../../visual-basic/language-reference/statements/function-statement.md)  
  
 [Property 陳述式](../../../visual-basic/language-reference/statements/property-statement.md)  
  
 [Sub 陳述式](../../../visual-basic/language-reference/statements/sub-statement.md)  
  
## <a name="see-also"></a>請參閱

- [關鍵字](../../../visual-basic/language-reference/keywords/index.md)
- [參數陣列](../../../visual-basic/programming-guide/language-features/procedures/parameter-arrays.md)
