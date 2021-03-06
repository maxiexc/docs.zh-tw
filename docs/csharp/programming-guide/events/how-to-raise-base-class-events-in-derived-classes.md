---
title: 如何在派生類中引發基類事件 - C# 程式設計指南
ms.date: 07/20/2015
helpviewer_keywords:
- events [C#], in derived classes
ms.assetid: 2d20556a-0aad-46fc-845e-f85d86ea617a
ms.openlocfilehash: 48f95871aa8a5a33923286262093a143cbd16d40
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/14/2020
ms.locfileid: "75712321"
---
# <a name="how-to-raise-base-class-events-in-derived-classes-c-programming-guide"></a>如何在派生類中引發基類事件（C# 程式設計指南）
下列簡單的範例示範在基底類別中宣告事件的標準方式，讓事件也可以從衍生類別引發。 這個模式會在 .NET Framework 類別庫的 Windows Forms 類別中廣泛使用。  
  
 當您建立可作為其他類別之基底類別的類別時，您應該考慮到事件其實是一種特殊的委派類型，只能在宣告事件的類別內予以叫用。 衍生類別無法直接叫用在基底類別內宣告的事件。 雖然有時您可能需要只能由基底類別引發的事件，但大多時候，您應該啟用衍生類別來叫用基底類別事件。 若要這樣做，您可以在包裝事件的基底類別中建立受保護的叫用方法。 藉由呼叫或覆寫這個叫用方法，衍生類別便能夠間接叫用該事件。  
  
> [!NOTE]
> 請勿在基底類別中宣告虛擬事件並在衍生類別中加以覆寫。 C# 編譯器無法正確處理這些事件，而且無法預測衍生事件的訂閱者是否會實際訂閱基底類別事件。  
  
## <a name="example"></a>範例  
 [!code-csharp[csProgGuideEvents#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideEvents/CS/Events.cs#1)]  
  
## <a name="see-also"></a>另請參閱

- [C# 程式設計指南](../index.md)
- [事件](./index.md)
- [委派](../delegates/index.md)
- [存取修飾詞](../classes-and-structs/access-modifiers.md)
- [在 Windows Forms 中建立事件處理常式](../../../framework/winforms/creating-event-handlers-in-windows-forms.md)
