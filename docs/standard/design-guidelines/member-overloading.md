---
title: 成員多載
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- default arguments
- members [.NET Framework], overloaded
- member design guidelines [.NET Framework], overloading
- overloaded members
- signatures, members
ms.assetid: 964ba19e-8b94-4b5b-b1e3-5a0b531a0bb1
ms.openlocfilehash: c9cb178e838aab99c22089b527a6bd2e86b325de
ms.sourcegitcommit: de17a7a0a37042f0d4406f5ae5393531caeb25ba
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/24/2020
ms.locfileid: "76727835"
---
# <a name="member-overloading"></a>成員多載
成員多載表示在相同類型上建立兩個或多個成員，但只有參數的數目或類型不同，但具有相同的名稱。 例如，在下列中，會多載 `WriteLine` 方法：

```csharp
public static class Console {
    public void WriteLine();
    public void WriteLine(string value);
    public void WriteLine(bool value);
    ...
}
```

 因為只有方法、函式和索引屬性可以有參數，所以只有那些成員可以多載。

 多載是改善可重複使用之程式庫的可用性、生產力和可讀性的其中一個最重要的技巧。 參數數目的多載可讓您提供更簡單版本的函式和方法。 在參數類型上多載，可以針對在一組選取的不同類型上執行相同作業的成員，使用相同的成員名稱。

 ✔️請嘗試使用描述性參數名稱來表示較短多載所使用的預設值。

 ❌ 避免任意改變多載中的參數名稱。 如果某個多載中的參數表示的輸入與另一個多載中的參數相同，則參數應該具有相同的名稱。

 ❌ 避免在多載成員中的參數順序不一致。 具有相同名稱的參數應該會出現在所有多載的相同位置。

 ✔️只會進行最長的多載虛擬（如果需要擴充性）。 較短的多載應該只呼叫較長的多載。

 ❌ 不要使用 `ref` 或 `out` 修飾詞來多載成員。

 有些語言無法解析對多載的呼叫，如下所示。 此外，這類多載通常會有完全不同的語義，而且可能不應該是多載，而是改為兩個不同的方法。

 ❌ 沒有具有相同位置之參數的多載，以及具有不同語義的類似類型。

 ✔️允許針對選擇性引數傳遞 `null`。

 ✔️確實使用成員多載，而不是定義具有預設引數的成員。

 預設引數不符合 CLS 標準。

 *部分©2005、2009 Microsoft Corporation。已保留擁有權限。*

 獲 Pearson Education, Inc. 的授權再版，從 Krzysztof Cwalina 和 Brad Abrams 撰寫，並在 2008 年 10 月 22 日由 Addison-Wesley Professional 出版，作為 Microsoft Windows Development Series 一部份的 *Framework Design Guidelines: Conventions, Idioms, and Patterns for Reusable .NET Libraries, 2nd Edition[ 節錄。](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619)*

## <a name="see-also"></a>另請參閱

- [成員設計方針](../../../docs/standard/design-guidelines/member.md)
- [Framework 設計方針](../../../docs/standard/design-guidelines/index.md)
