---
title: "Box 處理可為 Null 的類型 (C# 程式設計手冊) | Microsoft Docs"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- boxing [C#], nullable types
- unboxing [C#], nullable types
- nullable types [C#], boxing and unboxing
ms.assetid: bdb5b626-abc0-405d-8f64-0f0a0bf883a4
caps.latest.revision: 12
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
ms.translationtype: Human Translation
ms.sourcegitcommit: 400dfda51d978f35c3995f90840643aaff1b9c13
ms.openlocfilehash: e4ff2e8a31ca5a59494f80597460e90107e78c8a
ms.contentlocale: zh-tw
ms.lasthandoff: 03/24/2017

---
# <a name="boxing-nullable-types-c-programming-guide"></a><span data-ttu-id="a5cac-102">Box 處理可為 Null 的類型 (C# 程式設計手冊)</span><span class="sxs-lookup"><span data-stu-id="a5cac-102">Boxing Nullable Types (C# Programming Guide)</span></span>
<span data-ttu-id="a5cac-103">如為非 Null 的物件，以可為 Null 的型別為基礎的物件僅能以 boxing 處理。</span><span class="sxs-lookup"><span data-stu-id="a5cac-103">Objects based on nullable types are only boxed if the object is non-null.</span></span> <span data-ttu-id="a5cac-104">如果 <xref:System.Nullable%601.HasValue%2A> 是 `false`，則物件參考會指派給 `null` 而不是 boxing。</span><span class="sxs-lookup"><span data-stu-id="a5cac-104">If <xref:System.Nullable%601.HasValue%2A> is `false`, the object reference is assigned to `null` instead of boxing.</span></span> <span data-ttu-id="a5cac-105">例如: </span><span class="sxs-lookup"><span data-stu-id="a5cac-105">For example:</span></span>  
  
```csharp  
bool? b = null;  
object o = b;  
// Now o is null.  
```  
  
 <span data-ttu-id="a5cac-106">如果為非 Null 的物件 - 如果 <xref:System.Nullable%601.HasValue%2A> 是 `true` - 則發生 boxing，但只有可為 Null 物件依據的基礎類型會經過 boxing 處理。</span><span class="sxs-lookup"><span data-stu-id="a5cac-106">If the object is non-null -- if <xref:System.Nullable%601.HasValue%2A> is `true` -- then boxing occurs, but only the underlying type that the nullable object is based on is boxed.</span></span> <span data-ttu-id="a5cac-107">以 boxing 處理非 Null 的可為 Null 的實值型別，會以 boxing 處理處理實值型別本身，不會處理包裝實值型別的 <xref:System.Nullable%601?displayProperty=fullName>。</span><span class="sxs-lookup"><span data-stu-id="a5cac-107">Boxing a non-null nullable value type boxes the value type itself, not the <xref:System.Nullable%601?displayProperty=fullName> that wraps the value type.</span></span> <span data-ttu-id="a5cac-108">例如: </span><span class="sxs-lookup"><span data-stu-id="a5cac-108">For example:</span></span>  
  
```csharp  
bool? b = false;  
int? i = 44;  
object bBoxed = b; // bBoxed contains a boxed bool.  
object iBoxed = i; // iBoxed contains a boxed int.  
```  
  
 <span data-ttu-id="a5cac-109">兩個經過 boxing 處理的物件，和經過 boxing 處理的不可為 Null 的型別所建立的物件相同。</span><span class="sxs-lookup"><span data-stu-id="a5cac-109">The two boxed objects are identical to those created by boxing non-nullable types.</span></span> <span data-ttu-id="a5cac-110">而且，就像經過 boxing 處理的不可為 Null 的型別，它們可以取消 boxing 處理成為可為 Null 的型別，如下例所示︰</span><span class="sxs-lookup"><span data-stu-id="a5cac-110">And, just like non-nullable boxed types, they can be unboxed into nullable types, as in the following example:</span></span>  
  
```csharp  
bool? b2 = (bool?)bBoxed;  
int? i2 = (int?)iBoxed;  
```  
  
## <a name="remarks"></a><span data-ttu-id="a5cac-111">備註</span><span class="sxs-lookup"><span data-stu-id="a5cac-111">Remarks</span></span>  
 <span data-ttu-id="a5cac-112">經過 boxing 處理後，可為 Null 之型別的行為提供兩個優點︰</span><span class="sxs-lookup"><span data-stu-id="a5cac-112">The behavior of nullable types when boxed provides two advantages:</span></span>  
  
1.  <span data-ttu-id="a5cac-113">可為 Null 的物件及其經過 boxing 處理過的對應項目，可進行 Null 測試︰</span><span class="sxs-lookup"><span data-stu-id="a5cac-113">Nullable objects and their boxed counterpart can be tested for null:</span></span>  
  
    ```csharp  
    bool? b = null;  
    object boxedB = b;  
    if (b == null)  
    {  
      // True.  
    }  
    if (boxedB == null)  
    {  
      // Also true.  
    }  
    ```  
  
2.  <span data-ttu-id="a5cac-114">經過 boxing 處理的可為 Null 的型別完全支援基礎類型的功能︰</span><span class="sxs-lookup"><span data-stu-id="a5cac-114">Boxed nullable types fully support the functionality of the underlying type:</span></span>  
  
    ```csharp  
    double? d = 44.4;  
    object iBoxed = d;  
    // Access IConvertible interface implemented by double.  
    IConvertible ic = (IConvertible)iBoxed;  
    int i = ic.ToInt32(null);  
    string str = ic.ToString();  
    ```  
  
## <a name="see-also"></a><span data-ttu-id="a5cac-115">另請參閱</span><span class="sxs-lookup"><span data-stu-id="a5cac-115">See Also</span></span>  
 <span data-ttu-id="a5cac-116">[C# 程式設計指南](../../../csharp/programming-guide/index.md) </span><span class="sxs-lookup"><span data-stu-id="a5cac-116">[C# Programming Guide](../../../csharp/programming-guide/index.md) </span></span>  
<span data-ttu-id="a5cac-117"> [可為 Null 的型別](../../../csharp/programming-guide/nullable-types/index.md) </span><span class="sxs-lookup"><span data-stu-id="a5cac-117"> [Nullable Types](../../../csharp/programming-guide/nullable-types/index.md) </span></span>  
<span data-ttu-id="a5cac-118"> [如何：識別可為 Null 的型別](../../../csharp/programming-guide/nullable-types/how-to-identify-a-nullable-type.md)</span><span class="sxs-lookup"><span data-stu-id="a5cac-118"> [How to: Identify a Nullable Type](../../../csharp/programming-guide/nullable-types/how-to-identify-a-nullable-type.md)</span></span>