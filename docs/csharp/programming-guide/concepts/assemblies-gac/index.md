---
title: "組件和全域組件快取 (C#)"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: 149f5ca5-5b34-4746-9542-1ae43b2d0256
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 2b98bd872bfdcbebb34fff3d878b92f39e27bbe0
ms.contentlocale: zh-tw
ms.lasthandoff: 07/28/2017

---
# <a name="assemblies-and-the-global-assembly-cache-c"></a><span data-ttu-id="791c1-102">組件和全域組件快取 (C#)</span><span class="sxs-lookup"><span data-stu-id="791c1-102">Assemblies and the Global Assembly Cache (C#)</span></span>
<span data-ttu-id="791c1-103">組件會構成 .NET 型應用程式之部署、版本控制、重複使用、啟動範圍和安全性權限的基本單位。</span><span class="sxs-lookup"><span data-stu-id="791c1-103">Assemblies form the fundamental unit of deployment, version control, reuse, activation scoping, and security permissions for a .NET-based application.</span></span> <span data-ttu-id="791c1-104">組件會採用可執行檔 (.exe) 或動態連結程式庫 (.dll) 的格式，而且是 .NET Framework 的建置組塊。</span><span class="sxs-lookup"><span data-stu-id="791c1-104">Assemblies take the form of an executable (.exe) file or dynamic link library (.dll) file, and are the building blocks of the .NET Framework.</span></span> <span data-ttu-id="791c1-105">它們為通用語言執行平台提供了感知型別實作所需的資訊。</span><span class="sxs-lookup"><span data-stu-id="791c1-105">They provide the common language runtime with the information it needs to be aware of type implementations.</span></span> <span data-ttu-id="791c1-106">您可以將組件視為型別和資源的集合，其構成功能的邏輯單元，而且是為了共同運作而建置。</span><span class="sxs-lookup"><span data-stu-id="791c1-106">You can think of an assembly as a collection of types and resources that form a logical unit of functionality and are built to work together.</span></span>  
  
 <span data-ttu-id="791c1-107">組件可以包含一或多個模組。</span><span class="sxs-lookup"><span data-stu-id="791c1-107">Assemblies can contain one or more modules.</span></span> <span data-ttu-id="791c1-108">例如，大型專案的規劃方式可能是讓數個開發人員各自處理個別的模組，然後再全部組成單一組件。</span><span class="sxs-lookup"><span data-stu-id="791c1-108">For example, larger projects may be planned in such a way that several individual developers work on separate modules, all coming together to create a single assembly.</span></span> <span data-ttu-id="791c1-109">如需模組的詳細資訊，請參閱[如何：建置多檔案組件](https://msdn.microsoft.com/library/226t7yxe)主題。</span><span class="sxs-lookup"><span data-stu-id="791c1-109">For more information about modules, see the topic [How to: Build a Multifile Assembly](https://msdn.microsoft.com/library/226t7yxe).</span></span>  
  
 <span data-ttu-id="791c1-110">組件包含下列屬性：</span><span class="sxs-lookup"><span data-stu-id="791c1-110">Assemblies have the following properties:</span></span>  
  
-   <span data-ttu-id="791c1-111">組件會實作為 .exe 或 .dll 檔。</span><span class="sxs-lookup"><span data-stu-id="791c1-111">Assemblies are implemented as .exe or .dll files.</span></span>  
  
-   <span data-ttu-id="791c1-112">您可以將組件放在全域組件快取中，以在應用程式之間共用。</span><span class="sxs-lookup"><span data-stu-id="791c1-112">You can share an assembly between applications by putting it in the global assembly cache.</span></span> <span data-ttu-id="791c1-113">組件必須經強式命名後才能包含在全域組件快取內。</span><span class="sxs-lookup"><span data-stu-id="791c1-113">Assemblies must be strong-named before they can be included in the global assembly cache.</span></span> <span data-ttu-id="791c1-114">如需詳細資訊，請參閱[強式名稱的組件](https://msdn.microsoft.com/library/wd40t7ad)。</span><span class="sxs-lookup"><span data-stu-id="791c1-114">For more information, see [Strong-Named Assemblies](https://msdn.microsoft.com/library/wd40t7ad).</span></span>  
  
-   <span data-ttu-id="791c1-115">系統只會在需要時才將組件載入到記憶體。</span><span class="sxs-lookup"><span data-stu-id="791c1-115">Assemblies are only loaded into memory if they are required.</span></span> <span data-ttu-id="791c1-116">如果不使用，則不會予以載入。</span><span class="sxs-lookup"><span data-stu-id="791c1-116">If they are not used, they are not loaded.</span></span> <span data-ttu-id="791c1-117">這表示使用組件可以有效地管理大型專案中的資源。</span><span class="sxs-lookup"><span data-stu-id="791c1-117">This means that assemblies can be an efficient way to manage resources in larger projects.</span></span>  
  
-   <span data-ttu-id="791c1-118">藉由使用反映，您能以程式設計方式取得組件的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="791c1-118">You can programmatically obtain information about an assembly by using reflection.</span></span> <span data-ttu-id="791c1-119">如需詳細資訊，請參閱[反映 (C#)](../../../../csharp/programming-guide/concepts/reflection.md)。</span><span class="sxs-lookup"><span data-stu-id="791c1-119">For more information, see [Reflection (C#)](../../../../csharp/programming-guide/concepts/reflection.md).</span></span>  
  
-   <span data-ttu-id="791c1-120">如果載入組件是僅供檢查之用，請使用像是 <xref:System.Reflection.Assembly.ReflectionOnlyLoadFrom%2A> 的方法。</span><span class="sxs-lookup"><span data-stu-id="791c1-120">If you want to load an assembly only to inspect it, use a method such as <xref:System.Reflection.Assembly.ReflectionOnlyLoadFrom%2A>.</span></span>  
  
## <a name="assembly-manifest"></a><span data-ttu-id="791c1-121">組件資訊清單</span><span class="sxs-lookup"><span data-stu-id="791c1-121">Assembly Manifest</span></span>  
 <span data-ttu-id="791c1-122">每個組件內都有「組件資訊清單」。</span><span class="sxs-lookup"><span data-stu-id="791c1-122">Within every assembly is an *assembly manifest*.</span></span> <span data-ttu-id="791c1-123">類似於目錄，組件資訊清單包含下列資訊︰</span><span class="sxs-lookup"><span data-stu-id="791c1-123">Similar to a table of contents, the assembly manifest contains the following:</span></span>  
  
-   <span data-ttu-id="791c1-124">組件的身分識別 (其名稱和版本)。</span><span class="sxs-lookup"><span data-stu-id="791c1-124">The assembly's identity (its name and version).</span></span>  
  
-   <span data-ttu-id="791c1-125">一個檔案表格，說明構成該組件的所有其他檔案，例如，您所建立為 .exe 或 .dll 檔依賴的任何其他組件，甚至是點陣圖或讀我檔案。</span><span class="sxs-lookup"><span data-stu-id="791c1-125">A file table describing all the other files that make up the assembly, for example, any other assemblies you created that your .exe or .dll file relies on, or even bitmap or Readme files.</span></span>  
  
-   <span data-ttu-id="791c1-126">一個「組件參考清單」，它是所有外部相依性的清單 - 應用程式所需的 .dll 檔或其他檔案，可能是由其他人所建立。</span><span class="sxs-lookup"><span data-stu-id="791c1-126">An *assembly reference list*, which is a list of all external dependencies—.dlls or other files your application needs that may have been created by someone else.</span></span> <span data-ttu-id="791c1-127">組件參考同時包含全域和私用物件的參考。</span><span class="sxs-lookup"><span data-stu-id="791c1-127">Assembly references contain references to both global and private objects.</span></span> <span data-ttu-id="791c1-128">全域物件位於全域組件快取中，此區域可供其他應用程式使用。</span><span class="sxs-lookup"><span data-stu-id="791c1-128">Global objects reside in the global assembly cache, an area available to other applications.</span></span> <span data-ttu-id="791c1-129">私用物件必須同樣位在您的應用程式安裝目錄中或位在其底下的目錄。</span><span class="sxs-lookup"><span data-stu-id="791c1-129">Private objects must be in a directory at either the same level as or below the directory in which your application is installed.</span></span>  
  
 <span data-ttu-id="791c1-130">因為組件包含內容、版本設定及相依性的相關資訊，所以您使用 C# 建立的應用程式不依賴 Windows 登錄值就能正常運作。</span><span class="sxs-lookup"><span data-stu-id="791c1-130">Because assemblies contain information about content, versioning, and dependencies, the applications you create with C# do not rely on Windows registry values to function properly.</span></span> <span data-ttu-id="791c1-131">組件可減少 .dll 衝突，並讓您的應用程式更可靠，也更容易部署。</span><span class="sxs-lookup"><span data-stu-id="791c1-131">Assemblies reduce .dll conflicts and make your applications more reliable and easier to deploy.</span></span> <span data-ttu-id="791c1-132">在許多情況下，您只要將 .NET 型應用程式的檔案複製到目標電腦，即完成安裝。</span><span class="sxs-lookup"><span data-stu-id="791c1-132">In many cases, you can install a .NET-based application simply by copying its files to the target computer.</span></span>  
  
 <span data-ttu-id="791c1-133">如需詳細資訊，請參閱[組件資訊清單](https://msdn.microsoft.com/library/1w45z383)。</span><span class="sxs-lookup"><span data-stu-id="791c1-133">For more information see [Assembly Manifest](https://msdn.microsoft.com/library/1w45z383).</span></span>  
  
## <a name="adding-a-reference-to-an-assembly"></a><span data-ttu-id="791c1-134">加入組件的參考</span><span class="sxs-lookup"><span data-stu-id="791c1-134">Adding a Reference to an Assembly</span></span>  
 <span data-ttu-id="791c1-135">若要使用組件，您必須加入對它的參考。</span><span class="sxs-lookup"><span data-stu-id="791c1-135">To use an assembly, you must add a reference to it.</span></span> <span data-ttu-id="791c1-136">接著，您要使用 [using 指示詞](../../../../csharp/language-reference/keywords/using-directive.md)來選擇您想要使用之項目的命名空間。</span><span class="sxs-lookup"><span data-stu-id="791c1-136">Next, you use the [using directive](../../../../csharp/language-reference/keywords/using-directive.md) to choose the namespace of the items you want to use.</span></span> <span data-ttu-id="791c1-137">在參考並匯入組件之後，您的應用程式即可使用所有可存取的類別、屬性、方法及其命名空間的其他成員，其程式碼就如同您原始程式檔的一部分。</span><span class="sxs-lookup"><span data-stu-id="791c1-137">Once an assembly is referenced and imported, all the accessible classes, properties, methods, and other members of its namespaces are available to your application as if their code were part of your source file.</span></span>  
  
 <span data-ttu-id="791c1-138">在 C# 中，您也可以在單一應用程式中使用同一組件的兩種版本。</span><span class="sxs-lookup"><span data-stu-id="791c1-138">In C#, you can also use two versions of the same assembly in a single application.</span></span> <span data-ttu-id="791c1-139">如需詳細資訊，請參閱[外部別名](../../../../csharp/language-reference/keywords/extern-alias.md)。</span><span class="sxs-lookup"><span data-stu-id="791c1-139">For more information, see [extern alias](../../../../csharp/language-reference/keywords/extern-alias.md).</span></span>  
  
## <a name="creating-an-assembly"></a><span data-ttu-id="791c1-140">建立組件</span><span class="sxs-lookup"><span data-stu-id="791c1-140">Creating an Assembly</span></span>  
 <span data-ttu-id="791c1-141">若要編譯您的應用程式，請在 [建置] 功能表上按一下 [建置]，或使用命令列編譯器從命令列建置。</span><span class="sxs-lookup"><span data-stu-id="791c1-141">Compile your application by clicking **Build** on the **Build** menu or by building it from the command line using the command-line compiler.</span></span> <span data-ttu-id="791c1-142">如需從命令列建置組件的詳細資料，請參閱[使用 csc.exe 建置命令列](../../../../csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md)。</span><span class="sxs-lookup"><span data-stu-id="791c1-142">For details about building assemblies from the command line, see [Command-line Building With csc.exe](../../../../csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md).</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="791c1-143">若要在 Visual Studio 中建置組件，請在[建置] 功能表中選擇 [建置]。</span><span class="sxs-lookup"><span data-stu-id="791c1-143">To build an assembly in Visual Studio, on the **Build** menu choose **Build**.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="791c1-144">另請參閱</span><span class="sxs-lookup"><span data-stu-id="791c1-144">See Also</span></span>  
 <span data-ttu-id="791c1-145">[C# 程式設計指南](../../../../csharp/programming-guide/index.md) </span><span class="sxs-lookup"><span data-stu-id="791c1-145">[C# Programming Guide](../../../../csharp/programming-guide/index.md) </span></span>  
 <span data-ttu-id="791c1-146">[通用語言執行平台中的組件](https://msdn.microsoft.com/library/k3677y81) </span><span class="sxs-lookup"><span data-stu-id="791c1-146">[Assemblies in the Common Language Runtime](https://msdn.microsoft.com/library/k3677y81) </span></span>  
 <span data-ttu-id="791c1-147">[Friend 組件 (C#)](friend-assemblies.md) </span><span class="sxs-lookup"><span data-stu-id="791c1-147">[Friend Assemblies (C#)](friend-assemblies.md) </span></span>  
 <span data-ttu-id="791c1-148">[如何：與其他應用程式共用組件 (C#)](how-to-share-an-assembly-with-other-applications.md) </span><span class="sxs-lookup"><span data-stu-id="791c1-148">[How to: Share an Assembly with Other Applications (C#)](how-to-share-an-assembly-with-other-applications.md) </span></span>  
 <span data-ttu-id="791c1-149">[如何：載入和卸載組件 (C#)](how-to-load-and-unload-assemblies.md) </span><span class="sxs-lookup"><span data-stu-id="791c1-149">[How to: Load and Unload Assemblies (C#)](how-to-load-and-unload-assemblies.md) </span></span>  
 <span data-ttu-id="791c1-150">[如何：判斷檔案是否為組件 (C#)](how-to-determine-if-a-file-is-an-assembly.md) </span><span class="sxs-lookup"><span data-stu-id="791c1-150">[How to: Determine If a File Is an Assembly (C#)](how-to-determine-if-a-file-is-an-assembly.md) </span></span>  
 <span data-ttu-id="791c1-151">[如何：使用命令列建立和使用組件 (C#)](how-to-create-and-use-assemblies-using-the-command-line.md) </span><span class="sxs-lookup"><span data-stu-id="791c1-151">[How to: Create and Use Assemblies Using the Command Line (C#)](how-to-create-and-use-assemblies-using-the-command-line.md) </span></span>  
 <span data-ttu-id="791c1-152">[逐步解說：在 Visual Studio 中內嵌來自 Managed 組件的型別 (C#)](walkthrough-embedding-types-from-managed-assemblies-in-visual-studio.md) </span><span class="sxs-lookup"><span data-stu-id="791c1-152">[Walkthrough: Embedding Types from Managed Assemblies in Visual Studio (C#)](walkthrough-embedding-types-from-managed-assemblies-in-visual-studio.md) </span></span>  
 [<span data-ttu-id="791c1-153">逐步解說：在 Visual Studio 中內嵌來自 Microsoft Office 組件的類型資訊 (C#)</span><span class="sxs-lookup"><span data-stu-id="791c1-153">Walkthrough: Embedding Type Information from Microsoft Office Assemblies in Visual Studio (C#)</span></span>](walkthrough-embedding-type-information-from-microsoft-office-assemblies.md)
