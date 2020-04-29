---
title: XML 字元實體和 XAML
ms.date: 03/30/2017
f1_keywords:
- '&'
- '&amp'
- '&gt'
- '&lt'
helpviewer_keywords:
- XAML [XAML Services], special characters
- ampersand (&) [XAML Services]
- special characters [XAML Services]
- apostrophe (') [XAML Services]
- greater-than (>) character [XAML Services]
- XAML [XAML Services], quotation mark (")
- XAML [XAML Services], apostrophe (')
- '& (ampersand) [XAML Services]'
- XAML [XAML Services], & (ampersand)
- XAML [XAML Services], escape sequence
- quotation mark (") [XAML Services]
- less-than (<) character [XAML Services]
ms.assetid: 6896d0ce-74f7-420a-9ab4-de9bbf390e8d
ms.openlocfilehash: aff96c5d0ee6bbf2bbe2f9e3b3ae091caa781f7a
ms.sourcegitcommit: c2d9718996402993cf31541f11e95531bc68bad0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/27/2020
ms.locfileid: "82071455"
---
# <a name="xml-character-entities-and-xaml"></a><span data-ttu-id="9e7ee-102">XML 字元實體和 XAML</span><span class="sxs-lookup"><span data-stu-id="9e7ee-102">XML Character Entities and XAML</span></span>

<span data-ttu-id="9e7ee-103">XAML 使用 XML 中針對特殊字元定義的字元實體。</span><span class="sxs-lookup"><span data-stu-id="9e7ee-103">XAML uses character entities defined in XML for special characters.</span></span> <span data-ttu-id="9e7ee-104">本主題說明一些特定字元實體，以及針對 XAML 中其他 XML 概念的一般考量。</span><span class="sxs-lookup"><span data-stu-id="9e7ee-104">This topic describes some specific character entities and general considerations for other XML concepts in XAML.</span></span>

## <a name="character-entities-and-escaping-issues-that-are-unique-to-xaml"></a><span data-ttu-id="9e7ee-105">XAML 特有的字元實體和逸出問題</span><span class="sxs-lookup"><span data-stu-id="9e7ee-105">Character Entities and Escaping Issues That Are Unique to XAML</span></span>

<span data-ttu-id="9e7ee-106">XAML 標記通常會使用 XML 中定義的相同字元實體和逸出序列。</span><span class="sxs-lookup"><span data-stu-id="9e7ee-106">XAML markup typically uses the same character entities and escape sequences that are defined in XML.</span></span>

<span data-ttu-id="9e7ee-107">主要的差異在於大括號 ({ 和 }) 在 XAML 中具有顯著意義，因為這些字元會通知 XAML 處理器，包含在大括號內的字元序列必須解譯為標記延伸。</span><span class="sxs-lookup"><span data-stu-id="9e7ee-107">The main exception is that braces ({ and }) have significance in XAML because these characters inform a XAML processor that a character sequence enclosed by braces must be interpreted as a markup extension.</span></span> <span data-ttu-id="9e7ee-108">如需標記延伸的詳細資訊，請參閱 [Markup Extensions for XAML Overview](markup-extensions-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="9e7ee-108">For more information about markup extensions, see [Markup Extensions for XAML Overview](markup-extensions-overview.md).</span></span>

<span data-ttu-id="9e7ee-109">不過，您還是可以使用 XAML (而不是 XML) 特有的逸出序列，將大括號顯示為常值字元。</span><span class="sxs-lookup"><span data-stu-id="9e7ee-109">However, you can still display the braces as literal characters by using an escape sequence that is particular to XAML instead of XML.</span></span> <span data-ttu-id="9e7ee-110">關於詳細資訊,請參[{}閱 逸出序列 - 標記延伸](escape-sequence-markup-extension.md)。</span><span class="sxs-lookup"><span data-stu-id="9e7ee-110">For more information, see [{} Escape Sequence - Markup Extension](escape-sequence-markup-extension.md).</span></span>

<span data-ttu-id="9e7ee-111">請注意,反斜杠\\( ) 在作為字串處理時不需要轉義序列。</span><span class="sxs-lookup"><span data-stu-id="9e7ee-111">Note that a backslash (\\) does not require an escape sequence when it is handled as a string.</span></span>

## <a name="xml-character-entities"></a><span data-ttu-id="9e7ee-112">XML 字元實體</span><span class="sxs-lookup"><span data-stu-id="9e7ee-112">XML Character Entities</span></span>

<span data-ttu-id="9e7ee-113">如前所述，通常用於撰寫 XAML 標記的大多數字元實體和逸出序列都是由 XML 定義的。</span><span class="sxs-lookup"><span data-stu-id="9e7ee-113">As mentioned previously, most character entities and escape sequences that are typically used to write XAML markup are defined by XML.</span></span> <span data-ttu-id="9e7ee-114">本主題並未提供這些實體的完整清單，您可以在外部文件 (例如 XML 規格) 中找到這些實體的詳細參考資料。</span><span class="sxs-lookup"><span data-stu-id="9e7ee-114">This topic does not provide the complete list of these entities; a detailed reference for the entities can be found in external documentation, such as in XML specifications.</span></span> <span data-ttu-id="9e7ee-115">不過，為了方便起見，本主題會列出 XAML 標記中常用的 XML 字元實體。</span><span class="sxs-lookup"><span data-stu-id="9e7ee-115">However, for convenience, this topic lists some of the specific XML character entities that are typically used in XAML markup.</span></span>

|<span data-ttu-id="9e7ee-116">字元</span><span class="sxs-lookup"><span data-stu-id="9e7ee-116">Character</span></span>|<span data-ttu-id="9e7ee-117">單位</span><span class="sxs-lookup"><span data-stu-id="9e7ee-117">Entity</span></span>|<span data-ttu-id="9e7ee-118">注意</span><span class="sxs-lookup"><span data-stu-id="9e7ee-118">Notes</span></span>|
|---------------|------------|-----------|
|<span data-ttu-id="9e7ee-119">& (連字號)</span><span class="sxs-lookup"><span data-stu-id="9e7ee-119">& (ampersand)</span></span>|<span data-ttu-id="9e7ee-120">\&amp;</span><span class="sxs-lookup"><span data-stu-id="9e7ee-120">\&amp;</span></span>|<span data-ttu-id="9e7ee-121">必須用於屬性值和項目內容。</span><span class="sxs-lookup"><span data-stu-id="9e7ee-121">Must be used both for attribute values and for content of an element.</span></span>|
|<span data-ttu-id="9e7ee-122">>(大於字元)</span><span class="sxs-lookup"><span data-stu-id="9e7ee-122">> (greater-than character)</span></span>|<span data-ttu-id="9e7ee-123">\&gt;</span><span class="sxs-lookup"><span data-stu-id="9e7ee-123">\&gt;</span></span>|<span data-ttu-id="9e7ee-124">必須用於屬性值,但>是可以接受的,因為元素的內容,只要<不位於它前面。</span><span class="sxs-lookup"><span data-stu-id="9e7ee-124">Must be used for an attribute value, but > is acceptable as the content of an element as long as < does not precede it.</span></span>|
|<span data-ttu-id="9e7ee-125"><(字元小於字元)</span><span class="sxs-lookup"><span data-stu-id="9e7ee-125">< (less-than character)</span></span>|<span data-ttu-id="9e7ee-126">\&lt;</span><span class="sxs-lookup"><span data-stu-id="9e7ee-126">\&lt;</span></span>|<span data-ttu-id="9e7ee-127">必須用於屬性值,但\<只要>不遵循元素,作為元素的內容是可以接受的。</span><span class="sxs-lookup"><span data-stu-id="9e7ee-127">Must be used for an attribute value, but \< is acceptable as the content of an element as long as > does not follow it.</span></span>|
|<span data-ttu-id="9e7ee-128">" (雙引號)</span><span class="sxs-lookup"><span data-stu-id="9e7ee-128">" (straight quotation mark)</span></span>|<span data-ttu-id="9e7ee-129">\&quot;</span><span class="sxs-lookup"><span data-stu-id="9e7ee-129">\&quot;</span></span>|<span data-ttu-id="9e7ee-130">必須用於屬性值，但可接受雙引號 (") 做為項目內容。</span><span class="sxs-lookup"><span data-stu-id="9e7ee-130">Must be used for an attribute value, but a straight quotation mark (") is acceptable as the content of an element.</span></span> <span data-ttu-id="9e7ee-131">請注意，屬性值可以使用單引號 (') 或雙引號 ('') 括住；先出現的字元會定義括住的屬性值，而另一種引號則可以接著用來括住值內的常值。</span><span class="sxs-lookup"><span data-stu-id="9e7ee-131">Note that attribute values may be enclosed either by a single straight quotation mark (') or by a straight quotation mark ("); whichever character appears first defines the attribute value enclosure, and the alternative quote can then be used as a literal within the value.</span></span>|
|<span data-ttu-id="9e7ee-132">' (單引號)</span><span class="sxs-lookup"><span data-stu-id="9e7ee-132">' (single straight quotation mark)</span></span>|<span data-ttu-id="9e7ee-133">\&apos;</span><span class="sxs-lookup"><span data-stu-id="9e7ee-133">\&apos;</span></span>|<span data-ttu-id="9e7ee-134">必須用於屬性值，但可接受單引號 (') 做為項目內容。</span><span class="sxs-lookup"><span data-stu-id="9e7ee-134">Must be used for an attribute value, but a single straight quotation mark (') is acceptable as the content of an element.</span></span> <span data-ttu-id="9e7ee-135">請注意，屬性值可以使用單引號 (') 或雙引號 ('') 括住；先出現的字元會定義括住的屬性值，而另一種引號則可以接著用來括住值內的常值。</span><span class="sxs-lookup"><span data-stu-id="9e7ee-135">Note that attribute values may be enclosed either by a single straight quotation mark (') or by a straight quotation mark ("); whichever character appears first defines the attribute value enclosure, and the alternative quote can then be used as a literal within the value.</span></span>|
|<span data-ttu-id="9e7ee-136">(數字字元對應)</span><span class="sxs-lookup"><span data-stu-id="9e7ee-136">(numeric character mappings)</span></span>|<span data-ttu-id="9e7ee-137">&#*[整數]*;或&x *[十六進位];*</span><span class="sxs-lookup"><span data-stu-id="9e7ee-137">&#*[integer]*; or &#x *[hex]*;</span></span>|<span data-ttu-id="9e7ee-138">XAML 支援將數字字元對應至使用中的編碼方式。</span><span class="sxs-lookup"><span data-stu-id="9e7ee-138">XAML supports numeric character mappings into the encoding that is active.</span></span>|
|<span data-ttu-id="9e7ee-139">(不分行空格)</span><span class="sxs-lookup"><span data-stu-id="9e7ee-139">(nonbreaking space)</span></span>|<span data-ttu-id="9e7ee-140">&\#160;(假設 UTF-8 編碼)</span><span class="sxs-lookup"><span data-stu-id="9e7ee-140">&\#160; (assuming UTF-8 encoding)</span></span>|<span data-ttu-id="9e7ee-141">對於非固定格式文件項目，或是接受文字的項目 (例如 WPF <xref:System.Windows.Controls.TextBox>)，即使 `xml:space="default"`，也不會在標記外部將不分行空格標準化。</span><span class="sxs-lookup"><span data-stu-id="9e7ee-141">For flow document elements, or elements that take text such as the WPF <xref:System.Windows.Controls.TextBox>, nonbreaking spaces are not normalized out of the markup, even for `xml:space="default"`.</span></span> <span data-ttu-id="9e7ee-142">(關於詳細資訊,請參閱[XAML 中的空白處理](white-space-processing.md)。</span><span class="sxs-lookup"><span data-stu-id="9e7ee-142">(For more information, see [White-space processing in XAML](white-space-processing.md).)</span></span>|

## <a name="xml-comment-format"></a><span data-ttu-id="9e7ee-143">XML 註解格式</span><span class="sxs-lookup"><span data-stu-id="9e7ee-143">XML Comment Format</span></span>

<span data-ttu-id="9e7ee-144">XAML 使用 XML 註解格式：註解的開頭為 `<!--`，註解的結尾為 `-->,`，而且在註解內不能出現 `--` 序列。</span><span class="sxs-lookup"><span data-stu-id="9e7ee-144">XAML uses the XML comment format: the start of the comment is `<!--`, the end of comment is `-->,` and the sequence `--` must not occur within the comment.</span></span>

## <a name="xml-processing-instructions"></a><span data-ttu-id="9e7ee-145">XML 處理指令</span><span class="sxs-lookup"><span data-stu-id="9e7ee-145">XML Processing Instructions</span></span>

<span data-ttu-id="9e7ee-146">XAML 會根據 XML 規格來處理 XML 處理指令，該規格表示必須將指令傳遞通過。</span><span class="sxs-lookup"><span data-stu-id="9e7ee-146">XAML handles XML processing instructions according to XML specifications, which state that the instructions must be passed through.</span></span> <span data-ttu-id="9e7ee-147">.NET XAML 服務中的 XAML 處理不使用任何處理說明。</span><span class="sxs-lookup"><span data-stu-id="9e7ee-147">XAML processing in .NET XAML Services  does not use any processing instructions.</span></span> <span data-ttu-id="9e7ee-148">其他使用 XAML 的現有架構，也都不會使用 XAML 的處理指令。</span><span class="sxs-lookup"><span data-stu-id="9e7ee-148">Other existing frameworks that use XAML also do not use processing instructions from XAML.</span></span>

## <a name="see-also"></a><span data-ttu-id="9e7ee-149">另請參閱</span><span class="sxs-lookup"><span data-stu-id="9e7ee-149">See also</span></span>

- [<span data-ttu-id="9e7ee-150">XAML 概觀 (WPF)</span><span class="sxs-lookup"><span data-stu-id="9e7ee-150">XAML Overview (WPF)</span></span>](../fundamentals/xaml.md)
- [<span data-ttu-id="9e7ee-151">標記延伸和 WPF XAML</span><span class="sxs-lookup"><span data-stu-id="9e7ee-151">Markup Extensions and WPF XAML</span></span>](../../framework/wpf/advanced/markup-extensions-and-wpf-xaml.md)
- [<span data-ttu-id="9e7ee-152">XamlName 文法</span><span class="sxs-lookup"><span data-stu-id="9e7ee-152">XamlName Grammar</span></span>](xamlname-grammar.md)
- [<span data-ttu-id="9e7ee-153">XAML 中的空白字元處理</span><span class="sxs-lookup"><span data-stu-id="9e7ee-153">White-space processing in XAML</span></span>](white-space-processing.md)