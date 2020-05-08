---
ms.openlocfilehash: 6c35174be50ffc5031d0c4183bd936b4ef27757e
ms.sourcegitcommit: d9c7ac5d06735a01c1fafe34efe9486734841a72
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/06/2020
ms.locfileid: "82859795"
---
### <a name="sse-and-sse2-comparegreaterthan-methods-properly-handle-nan-inputs"></a><span data-ttu-id="d2981-101">SSE 和 SSE2 CompareGreaterThan 方法會適當地處理 NaN 輸入</span><span class="sxs-lookup"><span data-stu-id="d2981-101">SSE and SSE2 CompareGreaterThan methods properly handle NaN inputs</span></span>

<span data-ttu-id="d2981-102">下列<xref:System.Runtime.Intrinsics.X86.Sse?displayProperty=nameWithType>和<xref:System.Runtime.Intrinsics.X86.Sse2?displayProperty=nameWithType>方法已修正，可適當地處理`NaN`輸入，並符合<xref:System.Runtime.Intrinsics.X86.Avx?displayProperty=nameWithType>類別中對等方法的硬體行為：</span><span class="sxs-lookup"><span data-stu-id="d2981-102">The following <xref:System.Runtime.Intrinsics.X86.Sse?displayProperty=nameWithType> and <xref:System.Runtime.Intrinsics.X86.Sse2?displayProperty=nameWithType> methods have been fixed to properly handle `NaN` inputs and match the hardware behavior of the equivalent methods in the <xref:System.Runtime.Intrinsics.X86.Avx?displayProperty=nameWithType> class:</span></span>

* `CompareGreaterThan`
* `CompareGreaterThanOrEqual`
* `CompareNotGreaterThan`
* `CompareNotGreaterThanOrEqual`
* `CompareScalarGreaterThan`
* `CompareScalarGreaterThanOrEqual`
* `CompareScalarNotGreaterThan`
* `CompareScalarNotGreaterThanOrEqual`

#### <a name="change-description"></a><span data-ttu-id="d2981-103">變更描述</span><span class="sxs-lookup"><span data-stu-id="d2981-103">Change description</span></span>

<span data-ttu-id="d2981-104">先前列出`NaN` <xref:System.Runtime.Intrinsics.X86.Sse>的和<xref:System.Runtime.Intrinsics.X86.Sse2>方法的輸入傳回不正確的結果。</span><span class="sxs-lookup"><span data-stu-id="d2981-104">Previously, `NaN` inputs to the listed <xref:System.Runtime.Intrinsics.X86.Sse> and <xref:System.Runtime.Intrinsics.X86.Sse2> methods returned an incorrect result.</span></span> <span data-ttu-id="d2981-105">結果也不會與<xref:System.Runtime.Intrinsics.X86.Avx>類別中對應方法所產生的結果有差異。</span><span class="sxs-lookup"><span data-stu-id="d2981-105">The result also differed from the result generated by the corresponding method in the <xref:System.Runtime.Intrinsics.X86.Avx> class.</span></span>

<span data-ttu-id="d2981-106">從 .NET 5.0 開始，這些方法會正確`NaN`地處理輸入，並傳回與<xref:System.Runtime.Intrinsics.X86.Avx>類別中對應方法相同的結果。</span><span class="sxs-lookup"><span data-stu-id="d2981-106">Starting in .NET 5.0, these methods correctly handle `NaN` inputs and return the same results as the corresponding methods in the <xref:System.Runtime.Intrinsics.X86.Avx> class.</span></span>

<span data-ttu-id="d2981-107">Streaming SIMD Extensions （SSE）和 Streaming SIMD Extensions 2 （SSE2）產業標準架構（ISAs）不會針對這些比較方法提供直接硬體支援，因此它們會實作為軟體。</span><span class="sxs-lookup"><span data-stu-id="d2981-107">The Streaming SIMD Extensions (SSE) and Streaming SIMD Extensions 2 (SSE2) industry standard architectures (ISAs) don't provide direct hardware support for these comparison methods, so they're implemented in software.</span></span> <span data-ttu-id="d2981-108">之前，方法未正確地執行，而且不正確地`NaN`處理輸入。</span><span class="sxs-lookup"><span data-stu-id="d2981-108">Previously, the methods were improperly implemented, and they incorrectly handled `NaN` inputs.</span></span> <span data-ttu-id="d2981-109">如果是從原生移植的程式碼，則不正確的行為可能會導致錯誤。</span><span class="sxs-lookup"><span data-stu-id="d2981-109">For code ported from native, the incorrect behavior may introduce bugs.</span></span> <span data-ttu-id="d2981-110">若是256位程式碼路徑，方法也可以在<xref:System.Runtime.Intrinsics.X86.Avx>類別中對等的方法產生不同的結果。</span><span class="sxs-lookup"><span data-stu-id="d2981-110">For a 256-bit code path, the methods can also produce different results to the equivalent methods in the <xref:System.Runtime.Intrinsics.X86.Avx> class.</span></span>

<span data-ttu-id="d2981-111">如需方法先前不正確的範例，您可以將當做一般`CompareNotGreaterThan(x,y)`整數`CompareLessThanOrEqual(x,y)`來執行。</span><span class="sxs-lookup"><span data-stu-id="d2981-111">As an example of how the methods were previously incorrect, you can implement `CompareNotGreaterThan(x,y)` as `CompareLessThanOrEqual(x,y)` for regular integers.</span></span> <span data-ttu-id="d2981-112">不過，針對`NaN`輸入，該邏輯會計算錯誤的結果。</span><span class="sxs-lookup"><span data-stu-id="d2981-112">However, for `NaN` inputs, that logic computes the wrong result.</span></span> <span data-ttu-id="d2981-113">相反地， `CompareNotLessThan(y,x)`使用會`NaN`正確比較數位 *，並*將輸入納入考慮。</span><span class="sxs-lookup"><span data-stu-id="d2981-113">Instead, using `CompareNotLessThan(y,x)` compares the numbers correctly *and* takes `NaN` inputs into consideration.</span></span>

#### <a name="version-introduced"></a><span data-ttu-id="d2981-114">引進的版本</span><span class="sxs-lookup"><span data-stu-id="d2981-114">Version introduced</span></span>

<span data-ttu-id="d2981-115">5.0 Preview 4</span><span class="sxs-lookup"><span data-stu-id="d2981-115">5.0 Preview 4</span></span>

#### <a name="recommended-action"></a><span data-ttu-id="d2981-116">建議的動作</span><span class="sxs-lookup"><span data-stu-id="d2981-116">Recommended action</span></span>

- <span data-ttu-id="d2981-117">如果先前的行為是 bug，則不需要進行任何變更。</span><span class="sxs-lookup"><span data-stu-id="d2981-117">If the previous behavior was a bug, no change is required.</span></span>

- <span data-ttu-id="d2981-118">如果需要先前的行為，您可以藉由變更相關的調用來維護該行為，如下所示：</span><span class="sxs-lookup"><span data-stu-id="d2981-118">If the previous behavior was desired, you can maintain that behavior by changing the relevant invocation as follows:</span></span>

  * `CompareGreaterThan(x,y)` -> `CompareNotLessThanOrEqual(x,y)`
  * `CompareGreaterThanOrEqual(x,y)` -> `CompareNotLessThan(x,y)`
  * `CompareNotGreaterThan(x,y)` -> `CompareLessThanOrEqual(x,y)`
  * `CompareNotGreaterThanOrEqual(x,y)` -> `CompareLessThan(x,y)`
  * `CompareScalarGreaterThan(x,y)` -> `CompareScalarNotLessThanOrEqual(x,y)`
  * `CompareScalarGreaterThanOrEqual(x,y)` -> `CompareScalarNotLessThan(x,y)`
  * `CompareScalarNotGreaterThan(x,y)` -> `CompareScalarLessThanOrEqual(x,y)`
  * `CompareScalarNotGreaterThanOrEqual(x,y)` -> `CompareScalarLessThan(x,y)`

#### <a name="category"></a><span data-ttu-id="d2981-119">類別</span><span class="sxs-lookup"><span data-stu-id="d2981-119">Category</span></span>

<span data-ttu-id="d2981-120">Core .NET 程式庫</span><span class="sxs-lookup"><span data-stu-id="d2981-120">Core .NET libraries</span></span>

#### <a name="affected-apis"></a><span data-ttu-id="d2981-121">受影響的 API</span><span class="sxs-lookup"><span data-stu-id="d2981-121">Affected APIs</span></span>

- <xref:System.Runtime.Intrinsics.X86.Sse.CompareGreaterThan(System.Runtime.Intrinsics.Vector128{System.Single},System.Runtime.Intrinsics.Vector128{System.Single})?displayProperty=fullName>
- <xref:System.Runtime.Intrinsics.X86.Sse.CompareGreaterThanOrEqual(System.Runtime.Intrinsics.Vector128{System.Single},System.Runtime.Intrinsics.Vector128{System.Single})?displayProperty=fullName>
- <xref:System.Runtime.Intrinsics.X86.Sse.CompareNotGreaterThan(System.Runtime.Intrinsics.Vector128{System.Single},System.Runtime.Intrinsics.Vector128{System.Single})?displayProperty=fullName>
- <xref:System.Runtime.Intrinsics.X86.Sse.CompareNotGreaterThanOrEqual(System.Runtime.Intrinsics.Vector128{System.Single},System.Runtime.Intrinsics.Vector128{System.Single})?displayProperty=fullName>
- <xref:System.Runtime.Intrinsics.X86.Sse.CompareScalarGreaterThan(System.Runtime.Intrinsics.Vector128{System.Single},System.Runtime.Intrinsics.Vector128{System.Single})?displayProperty=fullName>
- <xref:System.Runtime.Intrinsics.X86.Sse.CompareScalarGreaterThanOrEqual(System.Runtime.Intrinsics.Vector128{System.Single},System.Runtime.Intrinsics.Vector128{System.Single})?displayProperty=fullName>
- <xref:System.Runtime.Intrinsics.X86.Sse.CompareScalarNotGreaterThan(System.Runtime.Intrinsics.Vector128{System.Single},System.Runtime.Intrinsics.Vector128{System.Single})?displayProperty=fullName>
- <xref:System.Runtime.Intrinsics.X86.Sse.CompareScalarNotGreaterThanOrEqual(System.Runtime.Intrinsics.Vector128{System.Single},System.Runtime.Intrinsics.Vector128{System.Single})?displayProperty=fullName>

- <xref:System.Runtime.Intrinsics.X86.Sse2.CompareGreaterThan(System.Runtime.Intrinsics.Vector128{System.Double},System.Runtime.Intrinsics.Vector128{System.Double})?displayProperty=fullName>
- <xref:System.Runtime.Intrinsics.X86.Sse2.CompareGreaterThanOrEqual(System.Runtime.Intrinsics.Vector128{System.Double},System.Runtime.Intrinsics.Vector128{System.Double})?displayProperty=fullName>
- <xref:System.Runtime.Intrinsics.X86.Sse2.CompareNotGreaterThan(System.Runtime.Intrinsics.Vector128{System.Double},System.Runtime.Intrinsics.Vector128{System.Double})?displayProperty=fullName>
- <xref:System.Runtime.Intrinsics.X86.Sse2.CompareNotGreaterThanOrEqual(System.Runtime.Intrinsics.Vector128{System.Double},System.Runtime.Intrinsics.Vector128{System.Double})?displayProperty=fullName>
- <xref:System.Runtime.Intrinsics.X86.Sse2.CompareScalarGreaterThan(System.Runtime.Intrinsics.Vector128{System.Double},System.Runtime.Intrinsics.Vector128{System.Double})?displayProperty=fullName>
- <xref:System.Runtime.Intrinsics.X86.Sse2.CompareScalarGreaterThanOrEqual(System.Runtime.Intrinsics.Vector128{System.Double},System.Runtime.Intrinsics.Vector128{System.Double})?displayProperty=fullName>
- <xref:System.Runtime.Intrinsics.X86.Sse2.CompareScalarNotGreaterThan(System.Runtime.Intrinsics.Vector128{System.Double},System.Runtime.Intrinsics.Vector128{System.Double})?displayProperty=fullName>
- <xref:System.Runtime.Intrinsics.X86.Sse2.CompareScalarNotGreaterThanOrEqual(System.Runtime.Intrinsics.Vector128{System.Double},System.Runtime.Intrinsics.Vector128{System.Double})?displayProperty=fullName>

<!--

### Affected APIs

- `M:System.Runtime.Intrinsics.X86.Sse.CompareGreaterThan(System.Runtime.Intrinsics.Vector128{System.Single},System.Runtime.Intrinsics.Vector128{System.Single})`
- `M:System.Runtime.Intrinsics.X86.Sse.CompareGreaterThanOrEqual(System.Runtime.Intrinsics.Vector128{System.Single},System.Runtime.Intrinsics.Vector128{System.Single})`
- `M:System.Runtime.Intrinsics.X86.Sse.CompareNotGreaterThan(System.Runtime.Intrinsics.Vector128{System.Single},System.Runtime.Intrinsics.Vector128{System.Single})`
- `M:System.Runtime.Intrinsics.X86.Sse.CompareNotGreaterThanOrEqual(System.Runtime.Intrinsics.Vector128{System.Single},System.Runtime.Intrinsics.Vector128{System.Single})`
- `M:System.Runtime.Intrinsics.X86.Sse.CompareScalarGreaterThan(System.Runtime.Intrinsics.Vector128{System.Single},System.Runtime.Intrinsics.Vector128{System.Single})`
- `M:System.Runtime.Intrinsics.X86.Sse.CompareScalarGreaterThanOrEqual(System.Runtime.Intrinsics.Vector128{System.Single},System.Runtime.Intrinsics.Vector128{System.Single})`
- `M:System.Runtime.Intrinsics.X86.Sse.CompareScalarNotGreaterThan(System.Runtime.Intrinsics.Vector128{System.Single},System.Runtime.Intrinsics.Vector128{System.Single})`
- `M:System.Runtime.Intrinsics.X86.Sse.CompareScalarNotGreaterThanOrEqual(System.Runtime.Intrinsics.Vector128{System.Single},System.Runtime.Intrinsics.Vector128{System.Single})`

- `M:System.Runtime.Intrinsics.X86.Sse2.CompareGreaterThan(System.Runtime.Intrinsics.Vector128{System.Double},System.Runtime.Intrinsics.Vector128{System.Double})`
- `M:System.Runtime.Intrinsics.X86.Sse2.CompareGreaterThanOrEqual(System.Runtime.Intrinsics.Vector128{System.Double},System.Runtime.Intrinsics.Vector128{System.Double})`
- `M:System.Runtime.Intrinsics.X86.Sse2.CompareNotGreaterThan(System.Runtime.Intrinsics.Vector128{System.Double},System.Runtime.Intrinsics.Vector128{System.Double})`
- `M:System.Runtime.Intrinsics.X86.Sse2.CompareNotGreaterThanOrEqual(System.Runtime.Intrinsics.Vector128{System.Double},System.Runtime.Intrinsics.Vector128{System.Double})`
- `M:System.Runtime.Intrinsics.X86.Sse2.CompareScalarGreaterThan(System.Runtime.Intrinsics.Vector128{System.Double},System.Runtime.Intrinsics.Vector128{System.Double})`
- `M:System.Runtime.Intrinsics.X86.Sse2.CompareScalarGreaterThanOrEqual(System.Runtime.Intrinsics.Vector128{System.Double},System.Runtime.Intrinsics.Vector128{System.Double})`
- `M:System.Runtime.Intrinsics.X86.Sse2.CompareScalarNotGreaterThan(System.Runtime.Intrinsics.Vector128{System.Double},System.Runtime.Intrinsics.Vector128{System.Double})`
- `M:System.Runtime.Intrinsics.X86.Sse2.CompareScalarNotGreaterThanOrEqual(System.Runtime.Intrinsics.Vector128{System.Double},System.Runtime.Intrinsics.Vector128{System.Double})`

-->