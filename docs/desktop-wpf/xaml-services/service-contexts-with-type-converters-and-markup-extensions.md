---
title: 適用於類型轉換子和標記延伸的服務內容
ms.date: 03/30/2017
helpviewer_keywords:
- XAML [XAML Services], type converter services how-to
ms.assetid: b4dad00f-03da-4579-a4e9-d8d72d2ccbce
ms.openlocfilehash: 59c4385eb4df8c622be6164cdb0a1a911c445ca8
ms.sourcegitcommit: c2d9718996402993cf31541f11e95531bc68bad0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/27/2020
ms.locfileid: "82071658"
---
# <a name="service-contexts-available-to-type-converters-and-markup-extensions"></a><span data-ttu-id="4136f-102">適用於類型轉換子和標記延伸的服務內容</span><span class="sxs-lookup"><span data-stu-id="4136f-102">Service Contexts Available to Type Converters and Markup Extensions</span></span>
<span data-ttu-id="4136f-103">在撰寫類型來支援使用類型轉換子和標記延伸時，通常必須先知道會在標記或周圍物件圖形結構中的何處使用類型轉換子和標記延伸。</span><span class="sxs-lookup"><span data-stu-id="4136f-103">Authors of the types that support type converter and markup extension usages must often have contextual information about where a usage is located in the markup, or in surrounding object graph structure.</span></span> <span data-ttu-id="4136f-104">要有這些資訊，才能正確地具現化所提供的物件，或是在物件圖形中建立對現有物件的物件參考。</span><span class="sxs-lookup"><span data-stu-id="4136f-104">Information might be needed so that the provided object is instantiated correctly or so that object references to existing objects in the object graph can be made.</span></span> <span data-ttu-id="4136f-105">使用 .NET XAML 服務時,可能需要的上下文將作為一系列服務介面公開。</span><span class="sxs-lookup"><span data-stu-id="4136f-105">When using .NET XAML Services, the context that might be required is exposed as a series of service interfaces.</span></span> <span data-ttu-id="4136f-106">類型轉換子或標記延伸支援程式碼可以使用從 <xref:System.Xaml.XamlObjectWriter> 或相關類型傳來的可用服務提供者內容，來查詢服務。</span><span class="sxs-lookup"><span data-stu-id="4136f-106">Type converter or markup extension support code can query for a service by using a service provider context that is available and passed through from <xref:System.Xaml.XamlObjectWriter> or related types.</span></span> <span data-ttu-id="4136f-107">XAML 結構描述內容可透過這類服務直接提供。</span><span class="sxs-lookup"><span data-stu-id="4136f-107">The XAML schema context is directly available through one such service.</span></span> <span data-ttu-id="4136f-108">本主題說明如何透過值轉換器實作存取服務內容，並列出通常可用的服務及其角色。</span><span class="sxs-lookup"><span data-stu-id="4136f-108">This topic describes how to access service contexts from a value converter implementation, and lists typically available services and their roles.</span></span>

## <a name="obtaining-services"></a><span data-ttu-id="4136f-109">取得服務</span><span class="sxs-lookup"><span data-stu-id="4136f-109">Obtaining Services</span></span>

<span data-ttu-id="4136f-110">身為值轉換器的實作者，您通常會需要存取套用值轉換器之特定類型的內容。</span><span class="sxs-lookup"><span data-stu-id="4136f-110">As an implementer of a value converter, you often need access to some type of context in which the value converter is applied.</span></span> <span data-ttu-id="4136f-111">此上下文可能包括諸如活動 XAML 架構上下文、訪問 XAML 架構上下文和 XAML 物件編寫器提供的類型映射系統等資訊。</span><span class="sxs-lookup"><span data-stu-id="4136f-111">This context might include information such as the active XAML schema context, access to the type-mapping system that the XAML schema context and XAML object writer provide, and so on.</span></span> <span data-ttu-id="4136f-112">標記延伸或類型轉換子實作適用的可用服務，會透過每個虛擬方法之簽章中的內容參數來表示。</span><span class="sxs-lookup"><span data-stu-id="4136f-112">The services available for a markup extension or type converter implementation are communicated through the context parameters that are part of the signature of each virtual method.</span></span> <span data-ttu-id="4136f-113">不論如何，您都會在內容中實作 <xref:System.IServiceProvider> ，並且可以呼叫 <xref:System.IServiceProvider.GetService%2A?displayProperty=nameWithType> 來要求服務。</span><span class="sxs-lookup"><span data-stu-id="4136f-113">In every case, you have <xref:System.IServiceProvider> implemented in the context, and can call <xref:System.IServiceProvider.GetService%2A?displayProperty=nameWithType> to request a service.</span></span>

## <a name="services-for-a-markup-extension"></a><span data-ttu-id="4136f-114">標記延伸適用的服務</span><span class="sxs-lookup"><span data-stu-id="4136f-114">Services for a Markup Extension</span></span>

<span data-ttu-id="4136f-115"><xref:System.Windows.Markup.MarkupExtension> 只有一種虛擬方法，那就是 <xref:System.Windows.Markup.MarkupExtension.ProvideValue%2A>。</span><span class="sxs-lookup"><span data-stu-id="4136f-115"><xref:System.Windows.Markup.MarkupExtension> has only one virtual method, <xref:System.Windows.Markup.MarkupExtension.ProvideValue%2A>.</span></span> <span data-ttu-id="4136f-116">輸入 `serviceProvider` 參數是在 XAML 處理器呼叫標記延伸時，用以向實作表示服務的方式。</span><span class="sxs-lookup"><span data-stu-id="4136f-116">The input `serviceProvider` parameter is how the services are communicated to implementations when the markup extension is called by a XAML processor.</span></span> <span data-ttu-id="4136f-117">下列虛擬程式碼示範標記延伸實作如何在其 <xref:System.Windows.Markup.MarkupExtension.ProvideValue%2A>中查詢服務：</span><span class="sxs-lookup"><span data-stu-id="4136f-117">The following pseudocode illustrates how a markup extension implementation might query for services in its <xref:System.Windows.Markup.MarkupExtension.ProvideValue%2A>:</span></span>

```csharp
public override object ProvideValue(IServiceProvider serviceProvider)
{
...
    // Get the IXamlTypeResolver from the service provider
    if (serviceProvider == null)
    {
        throw new ArgumentNullException("serviceProvider");
    }
    IXamlTypeResolver xamlTypeResolver = serviceProvider.GetService(typeof(IXamlTypeResolver)) as IXamlTypeResolver;
    if (xamlTypeResolver == null)
   {
        throw new ArgumentException("IXamlTypeResolver"));
    }
...
}
```

## <a name="services-for-a-type-converter"></a><span data-ttu-id="4136f-118">類型轉換器適用的服務</span><span class="sxs-lookup"><span data-stu-id="4136f-118">Services for a Type Converter</span></span>

<span data-ttu-id="4136f-119"><xref:System.ComponentModel.TypeConverter> 有四個使用服務內容並支援使用 XAML 的虛擬方法。</span><span class="sxs-lookup"><span data-stu-id="4136f-119"><xref:System.ComponentModel.TypeConverter> has four virtual methods that use a service context and that support XAML usages.</span></span> <span data-ttu-id="4136f-120">每個方法都會傳遞輸入 `context` 參數。</span><span class="sxs-lookup"><span data-stu-id="4136f-120">Each of these methods passes an input `context` parameter.</span></span> <span data-ttu-id="4136f-121">這個參數屬於 <xref:System.ComponentModel.ITypeDescriptorContext>類型，但該介面繼承自 <xref:System.IServiceProvider>，因此類型轉換器實作會有 <xref:System.IServiceProvider.GetService%2A> 方法可以使用。</span><span class="sxs-lookup"><span data-stu-id="4136f-121">This parameter is of type <xref:System.ComponentModel.ITypeDescriptorContext>, but that interface inherits <xref:System.IServiceProvider>, and therefore, there is a <xref:System.IServiceProvider.GetService%2A> method available to type converter implementations.</span></span>

<span data-ttu-id="4136f-122">下列虛擬程式碼示範用於 XAML 的類型轉換子實作如何在其中一個覆寫 (在本例中為 <xref:System.ComponentModel.TypeConverter.ConvertFrom%2A>) 中查詢服務：</span><span class="sxs-lookup"><span data-stu-id="4136f-122">The following pseudocode illustrates how a type converter implementation for XAML usages might query for services in one of its overrides, in this case <xref:System.ComponentModel.TypeConverter.ConvertFrom%2A>:</span></span>

```csharp
public override object ConvertFrom(ITypeDescriptorContext typeDescriptorContext,
  CultureInfo cultureInfo,
  object source)
{
    IRootObjectProvider rootProvider = typeDescriptorContext.GetService(typeof(IRootObjectProvider)) as IRootObjectProvider;
    if (rootProvider != null && source is String)
    {
        //return something, else ...
    }
    throw GetConvertFromException(source);
}
```

## <a name="services-for-a-value-serializer"></a><span data-ttu-id="4136f-123">值序列化程式適用的服務</span><span class="sxs-lookup"><span data-stu-id="4136f-123">Services for a Value Serializer</span></span>

<span data-ttu-id="4136f-124">針對值序列化程式內容，您會使用 <xref:System.Windows.Markup.ValueSerializer> 類別專屬的服務提供者類型 <xref:System.Windows.Markup.IValueSerializerContext>。</span><span class="sxs-lookup"><span data-stu-id="4136f-124">For value serializer context, you use a service provider type that is specific to the <xref:System.Windows.Markup.ValueSerializer> class, <xref:System.Windows.Markup.IValueSerializerContext>.</span></span> <span data-ttu-id="4136f-125">該內容會傳遞給四個 <xref:System.Windows.Markup.ValueSerializer> 虛擬方法的覆寫。</span><span class="sxs-lookup"><span data-stu-id="4136f-125">That context is passed to overrides of the four <xref:System.Windows.Markup.ValueSerializer> virtual methods.</span></span> <span data-ttu-id="4136f-126">呼叫該內容中的 <xref:System.IServiceProvider.GetService%2A> ，即可取得服務。</span><span class="sxs-lookup"><span data-stu-id="4136f-126">Call <xref:System.IServiceProvider.GetService%2A> from the context to obtain services.</span></span>

## <a name="using-the-xaml-service-provider-contexts"></a><span data-ttu-id="4136f-127">使用 XAML 服務提供者內容</span><span class="sxs-lookup"><span data-stu-id="4136f-127">Using the XAML Service Provider Contexts</span></span>

<span data-ttu-id="4136f-128">訪問<xref:System.IServiceProvider.GetService%2A>可用於標記擴展或類型轉換器的 XAML 服務的服務提供者作為內部類實現,僅透過介面進行曝光,以及如何將其傳遞到相關上下文中。</span><span class="sxs-lookup"><span data-stu-id="4136f-128">The service provider for <xref:System.IServiceProvider.GetService%2A> access to XAML services available to markup extensions or type converters is implemented as an internal class, with exposure only through the interface and how it is passed into the relevant context.</span></span> <span data-ttu-id="4136f-129">每當預設的 .NET XAML 服務中的 XAML 處理操作載入路徑或儲存路徑的實現呼叫需要服務上下文的相關標記擴展或類型轉換器方法時,都會傳遞此內部物件。</span><span class="sxs-lookup"><span data-stu-id="4136f-129">Whenever a XAML processing operation in the default .NET XAML Services implementations of load path or save path invokes the relevant markup extension or type converter methods that require a service context, this internal object is passed.</span></span> <span data-ttu-id="4136f-130">系統服務內容會根據當時的情況提供 `MarkupExtensionContext` 或 `TextSyntaxContext`，但這兩個類別的內容則是內部資訊。</span><span class="sxs-lookup"><span data-stu-id="4136f-130">Depending on the circumstance, the system service context provides either `MarkupExtensionContext` or `TextSyntaxContext`, but the specifics of both of these classes are internal.</span></span> <span data-ttu-id="4136f-131">您與這些類別進行的互動，僅限於透過 <xref:System.IServiceProvider.GetService%2A>向類別要求服務。</span><span class="sxs-lookup"><span data-stu-id="4136f-131">Your interaction with these classes is limited to requesting services from them, through <xref:System.IServiceProvider.GetService%2A>.</span></span>

## <a name="available-services-from-the-net-xaml-service-context"></a><span data-ttu-id="4136f-132">來自 .NET XAML 服務內容的服務</span><span class="sxs-lookup"><span data-stu-id="4136f-132">Available Services from the .NET XAML Service Context</span></span>

<span data-ttu-id="4136f-133">.NET XAML 服務為標記擴展、類型轉換器、值序列化器和可能的其他用途定義服務。</span><span class="sxs-lookup"><span data-stu-id="4136f-133">.NET XAML Services defines services for markup extensions, type converters, value serializers, and potentially other usages.</span></span> <span data-ttu-id="4136f-134">下列各節分別說明這些服務，並提供如何在實作中使用這些服務的相關指引。</span><span class="sxs-lookup"><span data-stu-id="4136f-134">The following sections describe each of these services and provide guidance about how the service might be used in an implementation.</span></span>

### <a name="iserviceprovider"></a><span data-ttu-id="4136f-135">IServiceProvider</span><span class="sxs-lookup"><span data-stu-id="4136f-135">IServiceProvider</span></span>

<span data-ttu-id="4136f-136">**參考文件**:<xref:System.IServiceProvider></span><span class="sxs-lookup"><span data-stu-id="4136f-136">**Reference documentation**: <xref:System.IServiceProvider></span></span>

<span data-ttu-id="4136f-137">**與:**.NET 中基於服務的基礎結構的基本操作,以便您可以呼<xref:System.IServiceProvider.GetService%2A?displayProperty=nameWithType>叫 。</span><span class="sxs-lookup"><span data-stu-id="4136f-137">**Relevant to:** Basic operation of a service-based infrastructure in .NET so that you can call <xref:System.IServiceProvider.GetService%2A?displayProperty=nameWithType>.</span></span>

### <a name="itypedescriptorcontext"></a><span data-ttu-id="4136f-138">ITypeDescriptorContext</span><span class="sxs-lookup"><span data-stu-id="4136f-138">ITypeDescriptorContext</span></span>

<span data-ttu-id="4136f-139">**參考文件**:<xref:System.ComponentModel.ITypeDescriptorContext></span><span class="sxs-lookup"><span data-stu-id="4136f-139">**Reference documentation**: <xref:System.ComponentModel.ITypeDescriptorContext></span></span>

<span data-ttu-id="4136f-140">衍生自 <xref:System.IServiceProvider>。</span><span class="sxs-lookup"><span data-stu-id="4136f-140">Derives from <xref:System.IServiceProvider>.</span></span> <span data-ttu-id="4136f-141">這個類別代表標準 <xref:System.ComponentModel.TypeConverter> 簽章中的內容； <xref:System.ComponentModel.TypeConverter> 是自 .NET Framework 1.0 開始便已存在的類別。</span><span class="sxs-lookup"><span data-stu-id="4136f-141">This class represents context in the standard <xref:System.ComponentModel.TypeConverter> signatures; <xref:System.ComponentModel.TypeConverter> is a class that has existed since .NET Framework 1.0.</span></span> <span data-ttu-id="4136f-142">它比 XAML 和 XAML <xref:System.ComponentModel.TypeConverter> 情節更早用於字串-值類型轉換。</span><span class="sxs-lookup"><span data-stu-id="4136f-142">It predates XAML and the XAML <xref:System.ComponentModel.TypeConverter> scenario for string-value type conversion.</span></span> <span data-ttu-id="4136f-143">在 .NET XAML 服務<xref:System.ComponentModel.TypeConverter>上下文中 ,將顯式實現</span><span class="sxs-lookup"><span data-stu-id="4136f-143">In .NET XAML Services context, methods of <xref:System.ComponentModel.TypeConverter> are implemented explicitly.</span></span> <span data-ttu-id="4136f-144">這個明確實作的行為會讓呼叫端知道， <xref:System.ComponentModel.ITypeDescriptorContext> API 與 XAML 類型系統無關，或者與從 XAML 讀取或寫入物件無關。</span><span class="sxs-lookup"><span data-stu-id="4136f-144">The explicit implementation's behavior indicates to callers that the <xref:System.ComponentModel.ITypeDescriptorContext> API is not relevant for XAML type systems, or for reading or writing objects from XAML.</span></span> <span data-ttu-id="4136f-145"><xref:System.ComponentModel.ITypeDescriptorContext.Container%2A><xref:System.ComponentModel.ITypeDescriptorContext.Instance%2A>,通常<xref:System.ComponentModel.ITypeDescriptorContext.PropertyDescriptor%2A>從 .NET XAML 服務`null`上下文返回 。</span><span class="sxs-lookup"><span data-stu-id="4136f-145"><xref:System.ComponentModel.ITypeDescriptorContext.Container%2A>, <xref:System.ComponentModel.ITypeDescriptorContext.Instance%2A>, and <xref:System.ComponentModel.ITypeDescriptorContext.PropertyDescriptor%2A> generally return `null` from .NET XAML Services contexts.</span></span>

### <a name="ivalueserializercontext"></a><span data-ttu-id="4136f-146">IValueSerializerContext</span><span class="sxs-lookup"><span data-stu-id="4136f-146">IValueSerializerContext</span></span>

<span data-ttu-id="4136f-147">**參考文件**:<xref:System.Windows.Markup.IValueSerializerContext></span><span class="sxs-lookup"><span data-stu-id="4136f-147">**Reference documentation**: <xref:System.Windows.Markup.IValueSerializerContext></span></span>

<span data-ttu-id="4136f-148">衍生自 <xref:System.ComponentModel.ITypeDescriptorContext> ，也依賴明確實作來抑制與 XAML 類型系統有關的錯誤假設。</span><span class="sxs-lookup"><span data-stu-id="4136f-148">Derives from <xref:System.ComponentModel.ITypeDescriptorContext> and also relies on explicit implementations to suppress false implications about the XAML type system.</span></span> <span data-ttu-id="4136f-149">支援 <xref:System.Windows.Markup.ValueSerializer>上的靜態查閱協助方法。</span><span class="sxs-lookup"><span data-stu-id="4136f-149">Supports the static lookup helper methods on <xref:System.Windows.Markup.ValueSerializer>.</span></span>

### <a name="ixamltyperesolver"></a><span data-ttu-id="4136f-150">IXamlTypeResolver</span><span class="sxs-lookup"><span data-stu-id="4136f-150">IXamlTypeResolver</span></span>

<span data-ttu-id="4136f-151">**參考文件**:<xref:System.Windows.Markup.IXamlTypeResolver></span><span class="sxs-lookup"><span data-stu-id="4136f-151">**Reference documentation**: <xref:System.Windows.Markup.IXamlTypeResolver></span></span>

<span data-ttu-id="4136f-152">**T:System.Xaml.IDestinationTypeProvider**  <xref:System.Windows.Markup> 命名空間、System.Xaml 組件</span><span class="sxs-lookup"><span data-stu-id="4136f-152">**Defined by:**  <xref:System.Windows.Markup> namespace, System.Xaml assembly</span></span>

<span data-ttu-id="4136f-153">適用於：**T:System.Xaml.IDestinationTypeProvider** 載入路徑情節，以及與 XAML 結構描述內容的互動</span><span class="sxs-lookup"><span data-stu-id="4136f-153">**Relevant to:** Load path scenarios, and interaction with XAML schema context</span></span>

<span data-ttu-id="4136f-154">**服務 API：**  <xref:System.Windows.Markup.IXamlTypeResolver.Resolve%2A></span><span class="sxs-lookup"><span data-stu-id="4136f-154">**Service API:**  <xref:System.Windows.Markup.IXamlTypeResolver.Resolve%2A></span></span>

<span data-ttu-id="4136f-155">可能會影響 XAML 寫入器在物件圖形中建構 CLR 物件時，需要進行的 XAML 對 CLR 類型對應。</span><span class="sxs-lookup"><span data-stu-id="4136f-155">Can influence the XAML-to-CLR type mapping that is necessary when the XAML writer constructs a CLR object in an object graph.</span></span> <span data-ttu-id="4136f-156"><xref:System.Windows.Markup.IXamlTypeResolver.Resolve%2A> 會處理與 XAML 類型名稱 (<xref:System.Xaml.XamlType.Name%2A?displayProperty=nameWithType>) 對應的字串 (這個字串可能含限定前置詞)，然後傳回 CLR <xref:System.Type>。</span><span class="sxs-lookup"><span data-stu-id="4136f-156"><xref:System.Windows.Markup.IXamlTypeResolver.Resolve%2A> processes a potentially prefix-qualified string that corresponds to a XAML type name (<xref:System.Xaml.XamlType.Name%2A?displayProperty=nameWithType>), and returns a CLR <xref:System.Type>.</span></span> <span data-ttu-id="4136f-157">解析類型的作業通常高度仰賴 XAML 結構描述內容。</span><span class="sxs-lookup"><span data-stu-id="4136f-157">Resolving types is typically heavily dependent on XAML schema context.</span></span> <span data-ttu-id="4136f-158">只有 XAML 結構描述內容才可辨識已載入哪些組件，以及進行類型解析時可以或應該存取哪些組件。</span><span class="sxs-lookup"><span data-stu-id="4136f-158">Only the XAML schema context is aware of considerations such as which assemblies are loaded, and which of these assemblies can or should be accessed for type resolution.</span></span>

### <a name="iuricontext"></a><span data-ttu-id="4136f-159">IUriContext</span><span class="sxs-lookup"><span data-stu-id="4136f-159">IUriContext</span></span>

<span data-ttu-id="4136f-160">**參考文件**:<xref:System.Windows.Markup.IUriContext></span><span class="sxs-lookup"><span data-stu-id="4136f-160">**Reference documentation**: <xref:System.Windows.Markup.IUriContext></span></span>

<span data-ttu-id="4136f-161">**T:System.Xaml.IDestinationTypeProvider**  <xref:System.Windows.Markup> 命名空間、System.Xaml 組件</span><span class="sxs-lookup"><span data-stu-id="4136f-161">**Defined by:**  <xref:System.Windows.Markup> namespace, System.Xaml assembly</span></span>

<span data-ttu-id="4136f-162">**T:System.Xaml.IDestinationTypeProvider** 成員值 (URI 或 `x:Uri` 值) 的載入路徑和儲存路徑處理。</span><span class="sxs-lookup"><span data-stu-id="4136f-162">**Relevant to:** Load path and save path handling of member values that are URIs or `x:Uri` values.</span></span>

<span data-ttu-id="4136f-163">**服務 API：**  <xref:System.Windows.Markup.IUriContext.BaseUri%2A></span><span class="sxs-lookup"><span data-stu-id="4136f-163">**Service API:**  <xref:System.Windows.Markup.IUriContext.BaseUri%2A></span></span>

<span data-ttu-id="4136f-164">這項服務會報告全域可用的根 URI (如果有的話)。</span><span class="sxs-lookup"><span data-stu-id="4136f-164">This service reports a globally available URI root, if any.</span></span> <span data-ttu-id="4136f-165">根 URI 可用來將相對 URI 解析成絕對 URI，或將絕對 URI 解析成相對 URI。</span><span class="sxs-lookup"><span data-stu-id="4136f-165">The URI root can be used to resolve relative URIs to absolute URIs or vice versa.</span></span> <span data-ttu-id="4136f-166">這個情節主要與由特定架構，或由架構中常用根項目類別的功能所公開的應用程式服務有關。</span><span class="sxs-lookup"><span data-stu-id="4136f-166">This scenario is mainly relevant to application services that are exposed by a particular framework, or capabilities of a frequently used root element class in a framework.</span></span> <span data-ttu-id="4136f-167">基底 URI 可建立為 XAML 讀取器設定，接著傳遞至 XAML 物件寫入器，再由這項服務報告。</span><span class="sxs-lookup"><span data-stu-id="4136f-167">The base URI can be established as a XAML reader setting, which is then passed through to the XAML object writer and reported by this service.</span></span>

### <a name="iambientprovider"></a><span data-ttu-id="4136f-168">IAmbientProvider</span><span class="sxs-lookup"><span data-stu-id="4136f-168">IAmbientProvider</span></span>

<span data-ttu-id="4136f-169">**參考文件**:<xref:System.Xaml.IAmbientProvider></span><span class="sxs-lookup"><span data-stu-id="4136f-169">**Reference documentation**: <xref:System.Xaml.IAmbientProvider></span></span>

<span data-ttu-id="4136f-170">**T:System.Xaml.IDestinationTypeProvider**  <xref:System.Xaml> 命名空間、System.Xaml 組件</span><span class="sxs-lookup"><span data-stu-id="4136f-170">**Defined by:**  <xref:System.Xaml> namespace, System.Xaml assembly</span></span>

<span data-ttu-id="4136f-171">適用於：**T:System.Xaml.IDestinationTypeProvider** 載入路徑處理和類型查閱的延後或最佳化。</span><span class="sxs-lookup"><span data-stu-id="4136f-171">**Relevant to:** Load path handling and type lookup deferrals or optimizations.</span></span>

<span data-ttu-id="4136f-172">**服務 API:**  <xref:System.Xaml.IAmbientProvider.GetAllAmbientValues%2A>, 其他三個。</span><span class="sxs-lookup"><span data-stu-id="4136f-172">**Service APIs:**  <xref:System.Xaml.IAmbientProvider.GetAllAmbientValues%2A>, three others.</span></span>

<span data-ttu-id="4136f-173">XAML 中的環境概念是一種將類型的特定成員標記為環境成員的技術。</span><span class="sxs-lookup"><span data-stu-id="4136f-173">The ambience concept in XAML is a technique for marking a particular member of a type as ambient.</span></span> <span data-ttu-id="4136f-174">或者，您也可以將類型設為環境類型，使所有包含該類型之執行個體的屬性值都被視為環境屬性。</span><span class="sxs-lookup"><span data-stu-id="4136f-174">Alternatively, a type can be ambient so that all property values that hold an instance of the type should be considered ambient properties.</span></span> <span data-ttu-id="4136f-175">在物件圖形中 XAML 節點資料流更深層和做為子系的標記延伸或類型轉換器，可以在載入時存取環境屬性或類型執行個體，或是在儲存時使用環境結構的資訊。</span><span class="sxs-lookup"><span data-stu-id="4136f-175">Markup extensions or type converters that are further along the XAML node stream and that are descendants in the object graph can access the ambient property or type instance at load time; or they can use knowledge of the ambient structure at save time.</span></span> <span data-ttu-id="4136f-176">這可能會影響其他服務 (例如 <xref:System.Windows.Markup.IXamlTypeResolver> 或 `x:Type`) 的類型解析作業所需的限定程度。</span><span class="sxs-lookup"><span data-stu-id="4136f-176">This can affect the degree of qualification that is needed to resolve types for other services, such as for <xref:System.Windows.Markup.IXamlTypeResolver> or for `x:Type`.</span></span> <span data-ttu-id="4136f-177">另請參閱 <xref:System.Xaml.AmbientPropertyValue>。</span><span class="sxs-lookup"><span data-stu-id="4136f-177">See also <xref:System.Xaml.AmbientPropertyValue>.</span></span>

### <a name="ixamlschemacontextprovider"></a><span data-ttu-id="4136f-178">IXamlSchemaContextProvider</span><span class="sxs-lookup"><span data-stu-id="4136f-178">IXamlSchemaContextProvider</span></span>

<span data-ttu-id="4136f-179">**參考文件**:<xref:System.Xaml.IXamlSchemaContextProvider></span><span class="sxs-lookup"><span data-stu-id="4136f-179">**Reference documentation**: <xref:System.Xaml.IXamlSchemaContextProvider></span></span>

<span data-ttu-id="4136f-180">**T:System.Xaml.IDestinationTypeProvider**  <xref:System.Xaml> 命名空間、System.Xaml 組件</span><span class="sxs-lookup"><span data-stu-id="4136f-180">**Defined by:**  <xref:System.Xaml> namespace, System.Xaml assembly</span></span>

<span data-ttu-id="4136f-181">適用於：**T:System.Xaml.IDestinationTypeProvider** 載入路徑，以及任何必須將 XAML 類型解析成支援類型的作業。</span><span class="sxs-lookup"><span data-stu-id="4136f-181">**Relevant to:** Load path, and any operation that must resolve a XAML type to a backing type.</span></span>

<span data-ttu-id="4136f-182">**服務 API：**  <xref:System.Xaml.IXamlSchemaContextProvider.SchemaContext%2A></span><span class="sxs-lookup"><span data-stu-id="4136f-182">**Service API:**  <xref:System.Xaml.IXamlSchemaContextProvider.SchemaContext%2A></span></span>

<span data-ttu-id="4136f-183">所有延後載入作業都需要 XAML 結構描述內容，因為相同的結構描述內容必須套用至延後的區域，才能整合延後的內容。</span><span class="sxs-lookup"><span data-stu-id="4136f-183">XAML schema context is necessary for any defer load operations, because the same schema context must act on the deferred area in order to integrate the deferred content.</span></span> <span data-ttu-id="4136f-184">如需 XAML 結構描述內容所扮演角色的詳細資訊，請參閱 [T:System.Xaml.IDestinationTypeProvider](../../../api/index.md)。</span><span class="sxs-lookup"><span data-stu-id="4136f-184">For more information about the role of the XAML schema context, see [XAML Services](../../../api/index.md).</span></span>

### <a name="irootobjectprovider"></a><span data-ttu-id="4136f-185">IRootObjectProvider</span><span class="sxs-lookup"><span data-stu-id="4136f-185">IRootObjectProvider</span></span>

<span data-ttu-id="4136f-186">**參考文件**:<xref:System.Xaml.IRootObjectProvider></span><span class="sxs-lookup"><span data-stu-id="4136f-186">**Reference documentation**: <xref:System.Xaml.IRootObjectProvider></span></span>

<span data-ttu-id="4136f-187">**T:System.Xaml.IDestinationTypeProvider**  <xref:System.Xaml> 命名空間、System.Xaml 組件</span><span class="sxs-lookup"><span data-stu-id="4136f-187">**Defined by:**  <xref:System.Xaml> namespace, System.Xaml assembly</span></span>

<span data-ttu-id="4136f-188">適用於：**T:System.Xaml.IDestinationTypeProvider** 載入路徑。</span><span class="sxs-lookup"><span data-stu-id="4136f-188">**Relevant to:** Load path.</span></span>

<span data-ttu-id="4136f-189">**服務 API：**  <xref:System.Xaml.IRootObjectProvider.RootObject%2A></span><span class="sxs-lookup"><span data-stu-id="4136f-189">**Service API:**  <xref:System.Xaml.IRootObjectProvider.RootObject%2A></span></span>

<span data-ttu-id="4136f-190">這項服務與由特定架構，或由架構中常用根項目類別的功能所公開的應用程式服務有關。</span><span class="sxs-lookup"><span data-stu-id="4136f-190">The service is relevant to application services that are exposed by a particular framework or by capabilities of a frequently used root element class in a framework.</span></span> <span data-ttu-id="4136f-191">連接程式碼後置和事件連接，就是一種需要取得根物件的情節。</span><span class="sxs-lookup"><span data-stu-id="4136f-191">One scenario for obtaining the root object is connecting code-behind and event wiring.</span></span> <span data-ttu-id="4136f-192">例如， `x:Class` 的 WPF 實作可用來編譯標記，以及連接在 XAML 標記中的任何其他位置找到的任何事件處理常式屬性。</span><span class="sxs-lookup"><span data-stu-id="4136f-192">For example, the WPF implementation of `x:Class` is used for markup compile and wiring of any event handler attribute that is found at any other position in the XAML markup.</span></span> <span data-ttu-id="4136f-193">進行標記編譯時，標記和程式碼後置定義部分類別的連接點是在根項目。</span><span class="sxs-lookup"><span data-stu-id="4136f-193">The connection point of markup and code-behind defined partial classes for markup compile is at the root element.</span></span>

### <a name="ixamlnamespaceresolver"></a><span data-ttu-id="4136f-194">IXamlNamespaceResolver</span><span class="sxs-lookup"><span data-stu-id="4136f-194">IXamlNamespaceResolver</span></span>

<span data-ttu-id="4136f-195">**參考文件**:<xref:System.Xaml.IXamlNamespaceResolver></span><span class="sxs-lookup"><span data-stu-id="4136f-195">**Reference documentation**: <xref:System.Xaml.IXamlNamespaceResolver></span></span>

<span data-ttu-id="4136f-196">**T:System.Xaml.IDestinationTypeProvider**  <xref:System.Xaml> 命名空間、System.Xaml 組件</span><span class="sxs-lookup"><span data-stu-id="4136f-196">**Defined by:**  <xref:System.Xaml> namespace, System.Xaml assembly</span></span>

<span data-ttu-id="4136f-197">適用於：**T:System.Xaml.IDestinationTypeProvider** 載入路徑、儲存路徑。</span><span class="sxs-lookup"><span data-stu-id="4136f-197">**Relevant to:** Load path, save path.</span></span>

<span data-ttu-id="4136f-198">**服務 API:**<xref:System.Xaml.IXamlNamespaceResolver.GetNamespace%2A>用於載<xref:System.Xaml.IXamlNamespaceResolver.GetNamespacePrefixes%2A>入路徑 ,用於保存路徑。</span><span class="sxs-lookup"><span data-stu-id="4136f-198">**Service API:** <xref:System.Xaml.IXamlNamespaceResolver.GetNamespace%2A> for load path, <xref:System.Xaml.IXamlNamespaceResolver.GetNamespacePrefixes%2A> for save path.</span></span>

<span data-ttu-id="4136f-199"><xref:System.Xaml.IXamlNamespaceResolver> 是一項服務，可根據 XAML 命名空間的前置詞，傳回 XAML 命名空間在起始 XAML 標記中的識別項 / URI。</span><span class="sxs-lookup"><span data-stu-id="4136f-199"><xref:System.Xaml.IXamlNamespaceResolver> is a service that can return a XAML namespace identifier / URI based on its prefix as mapped in the originating XAML markup.</span></span>

### <a name="iprovidevaluetarget"></a><span data-ttu-id="4136f-200">IProvideValueTarget</span><span class="sxs-lookup"><span data-stu-id="4136f-200">IProvideValueTarget</span></span>

<span data-ttu-id="4136f-201">**參考文件**:<xref:System.Windows.Markup.IProvideValueTarget></span><span class="sxs-lookup"><span data-stu-id="4136f-201">**Reference documentation**: <xref:System.Windows.Markup.IProvideValueTarget></span></span>

<span data-ttu-id="4136f-202">**T:System.Xaml.IDestinationTypeProvider**  <xref:System.Windows.Markup> 命名空間、System.Xaml 組件</span><span class="sxs-lookup"><span data-stu-id="4136f-202">**Defined by:**  <xref:System.Windows.Markup> namespace, System.Xaml assembly</span></span>

<span data-ttu-id="4136f-203">適用於：**T:System.Xaml.IDestinationTypeProvider** 載入路徑和儲存路徑。</span><span class="sxs-lookup"><span data-stu-id="4136f-203">**Relevant to:** Load path and save path.</span></span>

<span data-ttu-id="4136f-204">**服務 API:** <xref:System.Windows.Markup.IProvideValueTarget.TargetObject%2A> <xref:System.Windows.Markup.IProvideValueTarget.TargetProperty%2A>.  </span><span class="sxs-lookup"><span data-stu-id="4136f-204">**Service APIs:**  <xref:System.Windows.Markup.IProvideValueTarget.TargetObject%2A>, <xref:System.Windows.Markup.IProvideValueTarget.TargetProperty%2A>.</span></span>

<span data-ttu-id="4136f-205"><xref:System.Windows.Markup.IProvideValueTarget> 可讓類型轉換器或標記延伸取得有關其在載入時之作用位置的內容。</span><span class="sxs-lookup"><span data-stu-id="4136f-205"><xref:System.Windows.Markup.IProvideValueTarget> enables a type converter or markup extension to obtain context about where it is acting at load time.</span></span> <span data-ttu-id="4136f-206">實作可以使用這個內容讓某個使用方式無效。</span><span class="sxs-lookup"><span data-stu-id="4136f-206">Implementations might use this context to invalidate a usage.</span></span> <span data-ttu-id="4136f-207">例如，WPF 在其某些標記延伸 (例如 <xref:System.Windows.DynamicResourceExtension>) 內具有邏輯。</span><span class="sxs-lookup"><span data-stu-id="4136f-207">For example, WPF has logic inside some of its markup extensions such as <xref:System.Windows.DynamicResourceExtension>.</span></span> <span data-ttu-id="4136f-208">這個邏輯會檢查 <xref:System.Windows.Markup.IProvideValueTarget.TargetProperty%2A> ，以確定該延伸只會用來設定相依性屬性 (或其他非相依性屬性的簡短清單)。</span><span class="sxs-lookup"><span data-stu-id="4136f-208">The logic checks the <xref:System.Windows.Markup.IProvideValueTarget.TargetProperty%2A> to make sure that the extension is only used to set dependency properties (or a short list of other non-dependency properties).</span></span>

### <a name="ixamlnameresolver"></a><span data-ttu-id="4136f-209">IXamlNameResolver</span><span class="sxs-lookup"><span data-stu-id="4136f-209">IXamlNameResolver</span></span>

<span data-ttu-id="4136f-210">**參考文件**:<xref:System.Xaml.IXamlNameResolver></span><span class="sxs-lookup"><span data-stu-id="4136f-210">**Reference documentation**: <xref:System.Xaml.IXamlNameResolver></span></span>

<span data-ttu-id="4136f-211">**T:System.Xaml.IDestinationTypeProvider**  <xref:System.Xaml> 命名空間、System.Xaml 組件</span><span class="sxs-lookup"><span data-stu-id="4136f-211">**Defined by:**  <xref:System.Xaml> namespace, System.Xaml assembly</span></span>

<span data-ttu-id="4136f-212">**與:** 載入路徑物件圖定義,解析由`x:Name``x:Reference`或特定於框架的技術標識的物件。</span><span class="sxs-lookup"><span data-stu-id="4136f-212">**Relevant to:** Load path object graph definition, resolving objects identified by `x:Name`, `x:Reference`, or framework-specific techniques.</span></span>

<span data-ttu-id="4136f-213">**T:System.Xaml.IDestinationTypeProvider**  <xref:System.Xaml.IXamlNameResolver.Resolve%2A>；其他適用於進階情節 (例如處理向前參考) 的 API。</span><span class="sxs-lookup"><span data-stu-id="4136f-213">**Service APIs:**  <xref:System.Xaml.IXamlNameResolver.Resolve%2A>; other APIs for more advanced scenarios such as dealing with forward references.</span></span>

<span data-ttu-id="4136f-214">.NET XAML`x:Reference`服務的處理實現依賴於此服務。</span><span class="sxs-lookup"><span data-stu-id="4136f-214">.NET XAML Services implementation of `x:Reference` handling relies on this service.</span></span> <span data-ttu-id="4136f-215">特定架構或是支援該架構的工具，會使用這項服務來處理 `x:Name` 或是已用<xref:System.Windows.Markup.RuntimeNamePropertyAttribute> 屬性化(Attributed) 的對等屬性 (Property)。</span><span class="sxs-lookup"><span data-stu-id="4136f-215">Specific frameworks or tools that support the framework use this service for `x:Name` handling or equivalent (<xref:System.Windows.Markup.RuntimeNamePropertyAttribute> attributed) property handling.</span></span>

### <a name="idestinationtypeprovider"></a><span data-ttu-id="4136f-216">IDestinationTypeProvider</span><span class="sxs-lookup"><span data-stu-id="4136f-216">IDestinationTypeProvider</span></span>

<span data-ttu-id="4136f-217">**參考文件**:<xref:System.Xaml.IDestinationTypeProvider></span><span class="sxs-lookup"><span data-stu-id="4136f-217">**Reference documentation**: <xref:System.Xaml.IDestinationTypeProvider></span></span>

<span data-ttu-id="4136f-218">**T:System.Xaml.IDestinationTypeProvider**  <xref:System.Xaml> 命名空間、System.Xaml 組件</span><span class="sxs-lookup"><span data-stu-id="4136f-218">**Defined by:**  <xref:System.Xaml> namespace, System.Xaml assembly</span></span>

<span data-ttu-id="4136f-219">適用於：**T:System.Xaml.IDestinationTypeProvider** 間接 CLR 類型資訊的載入路徑解析。</span><span class="sxs-lookup"><span data-stu-id="4136f-219">**Relevant to:** Load path resolution of indirect CLR type information.</span></span>

<span data-ttu-id="4136f-220">**服務 API：** <xref:System.Xaml.IDestinationTypeProvider.GetDestinationType%2A></span><span class="sxs-lookup"><span data-stu-id="4136f-220">**Service API:** <xref:System.Xaml.IDestinationTypeProvider.GetDestinationType%2A></span></span>

<span data-ttu-id="4136f-221">如需詳細資訊，請參閱 <xref:System.Xaml.IDestinationTypeProvider>。</span><span class="sxs-lookup"><span data-stu-id="4136f-221">For more information, see <xref:System.Xaml.IDestinationTypeProvider>.</span></span>

## <a name="see-also"></a><span data-ttu-id="4136f-222">另請參閱</span><span class="sxs-lookup"><span data-stu-id="4136f-222">See also</span></span>

- <xref:System.Windows.Markup.MarkupExtension>
- <xref:System.Xaml.XamlObjectWriter>
- [<span data-ttu-id="4136f-223">XAML 標記延伸概觀</span><span class="sxs-lookup"><span data-stu-id="4136f-223">Markup Extensions for XAML Overview</span></span>](markup-extensions-overview.md)
- [<span data-ttu-id="4136f-224">XAML 類型轉換子概觀</span><span class="sxs-lookup"><span data-stu-id="4136f-224">Type Converters for XAML Overview</span></span>](type-converters-overview.md)