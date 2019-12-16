---
title: "組件和全域組件快取 (Visual Basic)"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
ms.assetid: fcf78ff1-f1ab-4a5d-b6d8-00d2046b6c80
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: c5a1a3a651fc7d2b42f8ac55ab6f2d832f258bb0
ms.contentlocale: zh-tw
ms.lasthandoff: 07/28/2017

---
# <a name="assemblies-and-the-global-assembly-cache-visual-basic"></a><span data-ttu-id="68efa-102">組件和全域組件快取 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="68efa-102">Assemblies and the Global Assembly Cache (Visual Basic)</span></span>
<span data-ttu-id="68efa-103">組件會構成 .NET 型應用程式之部署、版本控制、重複使用、啟動範圍和安全性權限的基本單位。</span><span class="sxs-lookup"><span data-stu-id="68efa-103">Assemblies form the fundamental unit of deployment, version control, reuse, activation scoping, and security permissions for a .NET-based application.</span></span> <span data-ttu-id="68efa-104">組件會採用可執行檔 (.exe) 或動態連結程式庫 (.dll) 的格式，而且是 .NET Framework 的建置組塊。</span><span class="sxs-lookup"><span data-stu-id="68efa-104">Assemblies take the form of an executable (.exe) file or dynamic link library (.dll) file, and are the building blocks of the .NET Framework.</span></span> <span data-ttu-id="68efa-105">它們為通用語言執行平台提供了感知型別實作所需的資訊。</span><span class="sxs-lookup"><span data-stu-id="68efa-105">They provide the common language runtime with the information it needs to be aware of type implementations.</span></span> <span data-ttu-id="68efa-106">您可以將組件視為型別和資源的集合，其構成功能的邏輯單元，而且是為了共同運作而建置。</span><span class="sxs-lookup"><span data-stu-id="68efa-106">You can think of an assembly as a collection of types and resources that form a logical unit of functionality and are built to work together.</span></span>  
  
 <span data-ttu-id="68efa-107">組件可以包含一或多個模組。</span><span class="sxs-lookup"><span data-stu-id="68efa-107">Assemblies can contain one or more modules.</span></span> <span data-ttu-id="68efa-108">例如，大型專案的規劃方式可能是讓數個開發人員各自處理個別的模組，然後再全部組成單一組件。</span><span class="sxs-lookup"><span data-stu-id="68efa-108">For example, larger projects may be planned in such a way that several individual developers work on separate modules, all coming together to create a single assembly.</span></span> <span data-ttu-id="68efa-109">如需模組的詳細資訊，請參閱[如何：建置多檔案組件](https://msdn.microsoft.com/library/226t7yxe)主題。</span><span class="sxs-lookup"><span data-stu-id="68efa-109">For more information about modules, see the topic [How to: Build a Multifile Assembly](https://msdn.microsoft.com/library/226t7yxe).</span></span>  
  
 <span data-ttu-id="68efa-110">組件包含下列屬性：</span><span class="sxs-lookup"><span data-stu-id="68efa-110">Assemblies have the following properties:</span></span>  
  
-   <span data-ttu-id="68efa-111">組件會實作為 .exe 或 .dll 檔。</span><span class="sxs-lookup"><span data-stu-id="68efa-111">Assemblies are implemented as .exe or .dll files.</span></span>  
  
-   <span data-ttu-id="68efa-112">您可以將組件放在全域組件快取中，以在應用程式之間共用。</span><span class="sxs-lookup"><span data-stu-id="68efa-112">You can share an assembly between applications by putting it in the global assembly cache.</span></span> <span data-ttu-id="68efa-113">組件必須經強式命名後才能包含在全域組件快取內。</span><span class="sxs-lookup"><span data-stu-id="68efa-113">Assemblies must be strong-named before they can be included in the global assembly cache.</span></span> <span data-ttu-id="68efa-114">如需詳細資訊，請參閱[強式名稱的組件](https://msdn.microsoft.com/library/wd40t7ad)。</span><span class="sxs-lookup"><span data-stu-id="68efa-114">For more information, see [Strong-Named Assemblies](https://msdn.microsoft.com/library/wd40t7ad).</span></span>  
  
-   <span data-ttu-id="68efa-115">系統只會在需要時才將組件載入到記憶體。</span><span class="sxs-lookup"><span data-stu-id="68efa-115">Assemblies are only loaded into memory if they are required.</span></span> <span data-ttu-id="68efa-116">如果不使用，則不會予以載入。</span><span class="sxs-lookup"><span data-stu-id="68efa-116">If they are not used, they are not loaded.</span></span> <span data-ttu-id="68efa-117">這表示使用組件可以有效地管理大型專案中的資源。</span><span class="sxs-lookup"><span data-stu-id="68efa-117">This means that assemblies can be an efficient way to manage resources in larger projects.</span></span>  
  
-   <span data-ttu-id="68efa-118">藉由使用反映，您能以程式設計方式取得組件的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="68efa-118">You can programmatically obtain information about an assembly by using reflection.</span></span> <span data-ttu-id="68efa-119">如需詳細資訊，請參閱[反映 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/reflection.md)。</span><span class="sxs-lookup"><span data-stu-id="68efa-119">For more information, see [Reflection (Visual Basic)](../../../../visual-basic/programming-guide/concepts/reflection.md).</span></span>  
  
-   <span data-ttu-id="68efa-120">如果載入組件為僅供檢查之用，請使用像是 <xref:System.Reflection.Assembly.ReflectionOnlyLoadFrom%2A> 的方法。</span><span class="sxs-lookup"><span data-stu-id="68efa-120">If you want to load an assembly only to inspect it, use a method such as <xref:System.Reflection.Assembly.ReflectionOnlyLoadFrom%2A>.</span></span>  
  
## <a name="assembly-manifest"></a><span data-ttu-id="68efa-121">組件資訊清單</span><span class="sxs-lookup"><span data-stu-id="68efa-121">Assembly Manifest</span></span>  
 <span data-ttu-id="68efa-122">每個組件內都有「組件資訊清單」。</span><span class="sxs-lookup"><span data-stu-id="68efa-122">Within every assembly is an *assembly manifest*.</span></span> <span data-ttu-id="68efa-123">類似於目錄，組件資訊清單包含下列資訊︰</span><span class="sxs-lookup"><span data-stu-id="68efa-123">Similar to a table of contents, the assembly manifest contains the following:</span></span>  
  
-   <span data-ttu-id="68efa-124">組件的身分識別 (其名稱和版本)。</span><span class="sxs-lookup"><span data-stu-id="68efa-124">The assembly's identity (its name and version).</span></span>  
  
-   <span data-ttu-id="68efa-125">一個檔案表格，說明構成該組件的所有其他檔案，例如，您所建立為 .exe 或 .dll 檔依賴的任何其他組件，甚至是點陣圖或讀我檔案。</span><span class="sxs-lookup"><span data-stu-id="68efa-125">A file table describing all the other files that make up the assembly, for example, any other assemblies you created that your .exe or .dll file relies on, or even bitmap or Readme files.</span></span>  
  
-   <span data-ttu-id="68efa-126">一個「組件參考清單」，它是所有外部相依性的清單 - 應用程式所需的 .dll 檔或其他檔案，可能是由其他人所建立。</span><span class="sxs-lookup"><span data-stu-id="68efa-126">An *assembly reference list*, which is a list of all external dependencies—.dlls or other files your application needs that may have been created by someone else.</span></span> <span data-ttu-id="68efa-127">組件參考同時包含全域和私用物件的參考。</span><span class="sxs-lookup"><span data-stu-id="68efa-127">Assembly references contain references to both global and private objects.</span></span> <span data-ttu-id="68efa-128">全域物件位於全域組件快取中，此區域可供其他應用程式使用，有點像是 System32 目錄。</span><span class="sxs-lookup"><span data-stu-id="68efa-128">Global objects reside in the global assembly cache, an area available to other applications, somewhat like the System32 directory.</span></span> <span data-ttu-id="68efa-129"><xref:Microsoft.VisualBasic?displayProperty=fullName> 命名空間就是全域組件快取中組件的一個例子。</span><span class="sxs-lookup"><span data-stu-id="68efa-129">The <xref:Microsoft.VisualBasic?displayProperty=fullName> namespace is an example of an assembly in the global assembly cache.</span></span> <span data-ttu-id="68efa-130">私用物件必須同樣位在您的應用程式安裝目錄中或位在其底下的目錄。</span><span class="sxs-lookup"><span data-stu-id="68efa-130">Private objects must be in a directory at either the same level as or below the directory in which your application is installed.</span></span>  
  
 <span data-ttu-id="68efa-131">因為組件包含有關內容、版本管理及相依性的資訊，所以您使用 Visual Basic 建立的應用程式不依賴 Windows 登錄值就能正常運作。</span><span class="sxs-lookup"><span data-stu-id="68efa-131">Because assemblies contain information about content, versioning, and dependencies, the applications you create with Visual Basic do not rely on Windows registry values to function properly.</span></span> <span data-ttu-id="68efa-132">組件可減少 .dll 衝突，並讓您的應用程式更可靠，也更容易部署。</span><span class="sxs-lookup"><span data-stu-id="68efa-132">Assemblies reduce .dll conflicts and make your applications more reliable and easier to deploy.</span></span> <span data-ttu-id="68efa-133">在許多情況下，您只要將 .NET 型應用程式的檔案複製到目標電腦，即完成安裝。</span><span class="sxs-lookup"><span data-stu-id="68efa-133">In many cases, you can install a .NET-based application simply by copying its files to the target computer.</span></span>  
  
 <span data-ttu-id="68efa-134">如需詳細資訊，請參閱[組件資訊清單](https://msdn.microsoft.com/library/1w45z383)。</span><span class="sxs-lookup"><span data-stu-id="68efa-134">For more information see [Assembly Manifest](https://msdn.microsoft.com/library/1w45z383).</span></span>  
  
## <a name="adding-a-reference-to-an-assembly"></a><span data-ttu-id="68efa-135">加入組件的參考</span><span class="sxs-lookup"><span data-stu-id="68efa-135">Adding a Reference to an Assembly</span></span>  
 <span data-ttu-id="68efa-136">若要使用組件，您必須加入對它的參考。</span><span class="sxs-lookup"><span data-stu-id="68efa-136">To use an assembly, you must add a reference to it.</span></span> <span data-ttu-id="68efa-137">接著，您要使用 [Imports 陳述式](../../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)來選擇您想要使用之項目的命名空間。</span><span class="sxs-lookup"><span data-stu-id="68efa-137">Next, you use the [Imports statement](../../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md) to choose the namespace of the items you want to use.</span></span> <span data-ttu-id="68efa-138">在參考並匯入組件之後，您的應用程式即可使用所有可存取的類別、屬性、方法及其命名空間的其他成員，其程式碼就如同您原始程式檔的一部分。</span><span class="sxs-lookup"><span data-stu-id="68efa-138">Once an assembly is referenced and imported, all the accessible classes, properties, methods, and other members of its namespaces are available to your application as if their code were part of your source file.</span></span>  
  
## <a name="creating-an-assembly"></a><span data-ttu-id="68efa-139">建立組件</span><span class="sxs-lookup"><span data-stu-id="68efa-139">Creating an Assembly</span></span>  
 <span data-ttu-id="68efa-140">使用命令列編譯器從命令列建置來編譯您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="68efa-140">Compile your application by building it from the command line using the command-line compiler.</span></span> <span data-ttu-id="68efa-141">如需有關從命令列建置組件的詳細資訊，請參閱[從命令列建置](../../../../visual-basic/reference/command-line-compiler/building-from-the-command-line.md)。</span><span class="sxs-lookup"><span data-stu-id="68efa-141">For details about building assemblies from the command line, see [Building from the Command Line](../../../../visual-basic/reference/command-line-compiler/building-from-the-command-line.md).</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="68efa-142">若要在 Visual Studio 中建置組件，請在[建置] 功能表中選擇 [建置]。</span><span class="sxs-lookup"><span data-stu-id="68efa-142">To build an assembly in Visual Studio, on the **Build** menu choose **Build**.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="68efa-143">另請參閱</span><span class="sxs-lookup"><span data-stu-id="68efa-143">See Also</span></span>  
 <span data-ttu-id="68efa-144">[通用語言執行平台中的組件](https://msdn.microsoft.com/library/k3677y81) </span><span class="sxs-lookup"><span data-stu-id="68efa-144">[Assemblies in the Common Language Runtime](https://msdn.microsoft.com/library/k3677y81) </span></span>  
 <span data-ttu-id="68efa-145">[Friend 組件 (Visual Basic)](friend-assemblies.md) </span><span class="sxs-lookup"><span data-stu-id="68efa-145">[Friend Assemblies (Visual Basic)](friend-assemblies.md) </span></span>  
 <span data-ttu-id="68efa-146">[如何：與其他應用程式共用組件 (Visual Basic)](how-to-share-an-assembly-with-other-applications.md) </span><span class="sxs-lookup"><span data-stu-id="68efa-146">[How to: Share an Assembly with Other Applications (Visual Basic)](how-to-share-an-assembly-with-other-applications.md) </span></span>  
 <span data-ttu-id="68efa-147">[如何：載入和卸載組件 (Visual Basic)](how-to-load-and-unload-assemblies.md) </span><span class="sxs-lookup"><span data-stu-id="68efa-147">[How to: Load and Unload Assemblies (Visual Basic)](how-to-load-and-unload-assemblies.md) </span></span>  
 <span data-ttu-id="68efa-148">[如何：判斷檔案是否為組件 (Visual Basic)](how-to-determine-if-a-file-is-an-assembly.md) </span><span class="sxs-lookup"><span data-stu-id="68efa-148">[How to: Determine If a File Is an Assembly (Visual Basic)](how-to-determine-if-a-file-is-an-assembly.md) </span></span>  
 <span data-ttu-id="68efa-149">[如何：使用命令列建立和使用組件 (Visual Basic)](how-to-create-and-use-assemblies-using-the-command-line.md) </span><span class="sxs-lookup"><span data-stu-id="68efa-149">[How to: Create and Use Assemblies Using the Command Line (Visual Basic)](how-to-create-and-use-assemblies-using-the-command-line.md) </span></span>  
 <span data-ttu-id="68efa-150">[逐步解說：在 Visual Studio 中內嵌來自 Managed 組件的型別 (Visual Basic)](walkthrough-embedding-types-from-managed-assemblies-in-vs.md) </span><span class="sxs-lookup"><span data-stu-id="68efa-150">[Walkthrough: Embedding Types from Managed Assemblies in Visual Studio (Visual Basic)](walkthrough-embedding-types-from-managed-assemblies-in-vs.md) </span></span>  
 [<span data-ttu-id="68efa-151">逐步解說：在 Visual Studio 中內嵌來自 Microsoft Office 組件的型別資訊 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="68efa-151">Walkthrough: Embedding Type Information from Microsoft Office Assemblies in Visual Studio (Visual Basic)</span></span>](walkthrough-embedding-type-information-from-microsoft-office-assemblies-in-vs.md)
