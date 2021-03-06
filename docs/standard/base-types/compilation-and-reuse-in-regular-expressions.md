---
title: 規則運算式中的編譯和重複使用
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- parsing text with regular expressions, compilation
- searching with regular expressions, compilation
- .NET Framework regular expressions, engines
- .NET Framework regular expressions, compilation
- regular expressions, compilation
- compilation, regular expressions
- pattern-matching with regular expressions, compilation
- regular expressions, engines
ms.assetid: 182ec76d-5a01-4d73-996c-0b0d14fcea18
ms.openlocfilehash: b89f7f88233ecdab25ba2a74647aafeb4d8b74af
ms.sourcegitcommit: 59e36e65ac81cdd094a5a84617625b2a0ff3506e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2020
ms.locfileid: "80344183"
---
# <a name="compilation-and-reuse-in-regular-expressions"></a>規則運算式中的編譯和重複使用
只要了解規則運算式引擎如何編譯運算式，以及了解如何快取規則運算式，您就可以使大量使用規則運算式的應用程式達到最佳效能。 本主題討論編譯及快取。  
  
## <a name="compiled-regular-expressions"></a>編譯的規則運算式  
 根據預設，規則運算式引擎會將規則運算式編譯為內部指令的序列 (這些是不同於 Microsoft Intermediate Language (MSIL) 的高階程式碼)。 當引擎執行規則運算式時，它將會解譯內部程式碼。  
  
 如果 <xref:System.Text.RegularExpressions.Regex> 物件是以 <xref:System.Text.RegularExpressions.RegexOptions.Compiled?displayProperty=nameWithType> 選項所建構，它會將規則運算式明確地編譯為 MSIL 程式碼，而非高階規則運算式的內部指令。 這允許 .NET 的 Just-in-Time (JIT) 編譯器將運算式轉換為原生機器碼以達到較高效能。  構造<xref:System.Text.RegularExpressions.Regex>物件的成本可能更高，但與物件執行匹配的成本可能要小得多。

 替代方法是使用先行編譯的規則運算式。 您可以使用 <xref:System.Text.RegularExpressions.Regex.CompileToAssembly%2A> 方法，將您的所有運算式編譯為一個可重複使用的 DLL。 這樣可避免需要在執行階段進行編譯，同時仍能從已編譯之規則運算式的速度中獲益。  
  
## <a name="the-regular-expressions-cache"></a>規則運算式快取  
 為了提升效能，規則運算式引擎會維護整個應用程式的已編譯規則運算式之快取。 這個快取會儲存只有在靜態方法呼叫中使用的規則運算式模式 （不緩存提供給實例方法的正則運算式模式。這樣可以避免每次使用運算式時都需要將運算式重新解析為高級位元組代碼。  
  
 快取的規則運算式數目上限取決於 `static` (在 Visual Basic 中為 `Shared`) <xref:System.Text.RegularExpressions.Regex.CacheSize%2A?displayProperty=nameWithType> 屬性值。 根據預設，規則運算式引擎最多可快取 15 個已編譯的規則運算式。 如果編譯的規則運算式數目超出快取大小，就會捨棄最近最少使用的規則運算式，並快取新的規則運算式。  
  
 應用程式可以通過以下兩種方式之一重用正則運算式：  
  
- 使用 <xref:System.Text.RegularExpressions.Regex> 物件的靜態方法來定義規則運算式。 如果您使用的是已由另一個靜態方法調用定義的正則運算式模式，則正則運算式引擎將嘗試從緩存中檢索它。 如果緩存中不可用，引擎將編譯正則運算式並將其添加到緩存中。
  
- 在需要現有 <xref:System.Text.RegularExpressions.Regex> 物件的規則運算式模式時重複使用該物件。  
  
 由於物件具現化和規則運算式編譯會造成額外負荷，因此建立及快速終結多個 <xref:System.Text.RegularExpressions.Regex> 物件是個非常耗費資源的處理序。 對於使用大量不同規則運算式的應用程式，您可以使用靜態 `Regex` 方法的呼叫，或增加規則運算式快取的大小，以達到最佳效能。  
  
## <a name="see-also"></a>另請參閱

- [.NET 規則運算式](../../../docs/standard/base-types/regular-expressions.md)
