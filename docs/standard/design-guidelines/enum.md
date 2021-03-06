---
title: 列舉設計
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- type design guidelines, enumerations
- simple enumerations
- enumerations [.NET Framework], design guidelines
- class library design guidelines [.NET Framework], enumerations
- flags enumerations
ms.assetid: dd53c952-9d9a-4736-86ff-9540e815d545
ms.openlocfilehash: 3b24bfefd3edb0585e9c6369e9b8151b17151661
ms.sourcegitcommit: de17a7a0a37042f0d4406f5ae5393531caeb25ba
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/24/2020
ms.locfileid: "76741709"
---
# <a name="enum-design"></a>列舉設計

列舉是一種特殊的實值型別。 列舉有兩種類型：簡單列舉和旗標列舉。

簡單列舉代表一組小型封閉的選擇。 簡單列舉的常見範例是一組色彩。

旗標列舉是設計用來支援列舉值的位運算。 旗標列舉的常見範例是選項清單。

✔️確實要使用列舉來表示值集合的強型別參數、屬性和傳回值。

✔️偏好使用列舉，而不是靜態常數。

❌ 不要將列舉用於開啟的集合（例如作業系統版本、朋友的名稱等）。

❌ 不提供預定的保留列舉值，供日後使用。

您一律可以在稍後的階段中，直接將值新增至現有的列舉。 如需將值加入至列舉的詳細資訊，請參閱[將值加入至](#add_value)列舉。 保留的值只會會污染實際值的集合，而且通常會導致使用者錯誤。

❌ 避免公開只具有一個值的列舉。

確保 C Api 未來擴充性的常見作法是將保留參數新增至方法簽章。 這類保留參數可以用單一預設值來表示為列舉。 這不應該在受控 Api 中完成。 方法多載允許在未來的版本中新增參數。

❌ 不包含 enum 中的 sentinel 值。

雖然它們有時對架構開發人員很有用，但 sentinel 值對架構的使用者會造成混淆。 它們可用來追蹤列舉的狀態，而不是列舉所表示之集合中的其中一個值。

✔️在簡單列舉上提供零值。

請考慮呼叫值，例如 "None"。 如果這類的值不適用於此特定列舉，則列舉的最常見預設值應指派為零的基礎值。

✔️考慮使用 <xref:System.Int32> （大部分程式設計語言中的預設值）做為列舉的基礎類型，除非下列任何一項為 true：

- 列舉是旗標列舉，而且您有超過32個旗標，或未來預期會有更多旗標。

- 基礎類型必須與 <xref:System.Int32> 不同，以便更容易與非受控程式碼的互通性需要不同大小的列舉。

- 較小的基礎類型會導致空間大幅節省。 如果您預期列舉主要是做為控制流程的引數，則大小不會有太大的差異。 若有下列情況，節省的大小可能會很明顯：

  - 您預期列舉會當做非常頻繁具現化的結構或類別中的欄位使用。

  - 您預期使用者會建立大型陣列或列舉實例的集合。

  - 您預期會序列化大量的列舉實例。

針對記憶體中的使用方式，請注意，managed 物件一律 `DWORD`對齊，因此，您在實例中有效地需要多個列舉或其他小型結構來封裝較小的 enum，以便進行差異，因為總實例大小一律會無條件進位到 `DWORD`。

✔️使用名詞或名詞片語來進行名稱旗標列舉，以及使用單數或名詞片語進行簡單列舉。

❌ 不會直接延伸 <xref:System.Enum?displayProperty=nameWithType>。

<xref:System.Enum?displayProperty=nameWithType> 是 CLR 用來建立使用者定義列舉的特殊類型。 大部分的程式設計語言都會提供程式設計項目，讓您能夠存取這項功能。 例如，在 `enum` C#關鍵字中，是用來定義列舉型別（enumeration）。

<a name="design"></a>

### <a name="designing-flag-enums"></a>設計旗標列舉

✔️請將 <xref:System.FlagsAttribute?displayProperty=nameWithType> 套用至旗標列舉。 請勿將此屬性套用至簡單列舉。

✔️在旗標列舉值中使用兩個的乘冪，讓它們可以使用位 OR 運算自由地結合。

✔️請考慮為常用的旗標組合提供特殊的列舉值。

位運算是一種先進的概念，而且不應該為簡單的工作所需。 <xref:System.IO.FileAccess.ReadWrite> 是這種特殊值的範例。

❌ 避免建立旗標列舉，其中某些值的組合無效。

❌ 避免使用旗標列舉值零，除非值表示「已清除所有旗標」，而且會適當地命名，如同下一個指導方針所規定。

✔️ DO 將旗標列舉的零值命名 `None`。 針對旗標列舉，此值必須一律表示「已清除所有旗標」。

<a name="add_value"></a>

### <a name="adding-value-to-enums"></a>將值加入至列舉

在您已寄出值之後，您必須將其新增至列舉，這是很常見的情況。 從現有的 API 傳回新加入的值時，可能會發生應用程式相容性問題，因為撰寫不良的應用程式可能無法正確地處理新的值。

✔️考慮將值加入至列舉，儘管有較小的相容性風險。

如果您的實際資料是因為新增至列舉而造成的應用程式不相容，請考慮新增新的 API 來傳回新的和舊的值，並取代舊的 API，這應該會繼續只傳回舊的值。 這可確保您現有的應用程式保持相容。

*部分©2005、2009 Microsoft Corporation。已保留擁有權限。*

獲 Pearson Education, Inc. 的授權再版，從 Krzysztof Cwalina 和 Brad Abrams 撰寫，並在 2008 年 10 月 22 日由 Addison-Wesley Professional 出版，作為 Microsoft Windows Development Series 一部份的 *Framework Design Guidelines: Conventions, Idioms, and Patterns for Reusable .NET Libraries, 2nd Edition[ 節錄。](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619)*

## <a name="see-also"></a>另請參閱

- [類型設計方針](../../../docs/standard/design-guidelines/type.md)
- [Framework 設計方針](../../../docs/standard/design-guidelines/index.md)
