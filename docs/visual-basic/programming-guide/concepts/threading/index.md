---
title: "執行緒處理 (Visual Basic)"
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
ms.assetid: 704bb04b-ff23-471d-ab12-3cec1c2bca59
caps.latest.revision: 4
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 840cc7df20250acb67bd09a8d39b353c772e82da
ms.contentlocale: zh-tw
ms.lasthandoff: 07/28/2017

---
# <a name="threading-visual-basic"></a><span data-ttu-id="2f7fa-102">執行緒處理 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="2f7fa-102">Threading (Visual Basic)</span></span>
<span data-ttu-id="2f7fa-103">Visual Basic 程式可以透過執行緒執行並行處理，讓您可以一次執行多項作業。</span><span class="sxs-lookup"><span data-stu-id="2f7fa-103">Threading enables your Visual Basic program to perform concurrent processing so that you can do more than one operation at a time.</span></span> <span data-ttu-id="2f7fa-104">例如，您可以使用執行緒監視使用者的輸入、執行背景工作，以及處理同時的輸入資料流。</span><span class="sxs-lookup"><span data-stu-id="2f7fa-104">For example, you can use threading to monitor input from the user, perform background tasks, and handle simultaneous streams of input.</span></span>  
  
 <span data-ttu-id="2f7fa-105">執行緒具有下列特性：</span><span class="sxs-lookup"><span data-stu-id="2f7fa-105">Threads have the following properties:</span></span>  
  
-   <span data-ttu-id="2f7fa-106">執行緒可讓您的程式執行並行處理。</span><span class="sxs-lookup"><span data-stu-id="2f7fa-106">Threads enable your program to perform concurrent processing.</span></span>  
  
-   <span data-ttu-id="2f7fa-107">.NET Framework <xref:System.Threading> 命名空間讓執行緒更方便使用。</span><span class="sxs-lookup"><span data-stu-id="2f7fa-107">The .NET Framework <xref:System.Threading> namespace makes using threads easier.</span></span>  
  
-   <span data-ttu-id="2f7fa-108">執行緒會共用應用程式的資源。</span><span class="sxs-lookup"><span data-stu-id="2f7fa-108">Threads share the application's resources.</span></span> <span data-ttu-id="2f7fa-109">如需詳細資訊，請參閱 [Using Threads and Threading](https://msdn.microsoft.com/library/e1dx6b2h) (使用 Thread 與 Threading)。</span><span class="sxs-lookup"><span data-stu-id="2f7fa-109">For more information, see [Using Threads and Threading](https://msdn.microsoft.com/library/e1dx6b2h).</span></span>  
  
 <span data-ttu-id="2f7fa-110">根據預設，Visual Basic 程式都有一個執行緒。</span><span class="sxs-lookup"><span data-stu-id="2f7fa-110">By default, a Visual Basic program has one thread.</span></span> <span data-ttu-id="2f7fa-111">但您可以建立輔助執行緒來與主要執行緒一起並行執行程式碼。</span><span class="sxs-lookup"><span data-stu-id="2f7fa-111">However, auxiliary threads can be created and used to execute code in parallel with the primary thread.</span></span> <span data-ttu-id="2f7fa-112">這些執行緒通常稱為*背景工作執行緒*。</span><span class="sxs-lookup"><span data-stu-id="2f7fa-112">These threads are often called *worker threads*.</span></span>  
  
 <span data-ttu-id="2f7fa-113">背景工作執行緒可用於執行耗時或時間要求嚴格的工作，但不會佔用主要執行緒。</span><span class="sxs-lookup"><span data-stu-id="2f7fa-113">Worker threads can be used to perform time-consuming or time-critical tasks without tying up the primary thread.</span></span> <span data-ttu-id="2f7fa-114">例如，伺服器應用程式中通常會使用背景工作執行緒來滿足傳入的要求，而且無須等待前一個要求完成就能達成。</span><span class="sxs-lookup"><span data-stu-id="2f7fa-114">For example, worker threads are often used in server applications to fulfill incoming requests without waiting for the previous request to be completed.</span></span> <span data-ttu-id="2f7fa-115">背景工作執行緒在桌面應用程式中也可用於執行「背景」工作，讓驅動使用者介面項目的主要執行緒能夠持續回應使用者動作。</span><span class="sxs-lookup"><span data-stu-id="2f7fa-115">Worker threads are also used to perform "background" tasks in desktop applications so that the main thread--which drives user interface elements--remains responsive to user actions.</span></span>  
  
 <span data-ttu-id="2f7fa-116">執行緒可以解決輸送量與回應性的問題，但也可能會引發資源共用的問題，像是死結及競爭狀況。</span><span class="sxs-lookup"><span data-stu-id="2f7fa-116">Threading solves problems with throughput and responsiveness, but it can also introduce resource-sharing issues such as deadlocks and race conditions.</span></span> <span data-ttu-id="2f7fa-117">多執行緒最適合需要不同資源的工作，例如檔案控制及網路連線。</span><span class="sxs-lookup"><span data-stu-id="2f7fa-117">Multiple threads are best for tasks that require different resources such as file handles and network connections.</span></span> <span data-ttu-id="2f7fa-118">為單一資源指派多個執行緒除可能會導致同步問題之外，還可能經常因為等候其他執行緒戰勝使用多執行的目標而造成執行緒受阻無法執行。</span><span class="sxs-lookup"><span data-stu-id="2f7fa-118">Assigning multiple threads to a single resource is likely to cause synchronization issues, and having threads frequently blocked when waiting for other threads defeats the purpose of using multiple threads.</span></span>  
  
 <span data-ttu-id="2f7fa-119">常見的策略是使用背景工作處理序來執行耗時或時間要求嚴格，但又不需要太多其他執行緒所用之資源的工作。</span><span class="sxs-lookup"><span data-stu-id="2f7fa-119">A common strategy is to use worker threads to perform time-consuming or time-critical tasks that do not require many of the resources used by other threads.</span></span> <span data-ttu-id="2f7fa-120">當然，您程式中的一些資源仍須能夠讓多執行緒存取。</span><span class="sxs-lookup"><span data-stu-id="2f7fa-120">Naturally, some resources in your program must be accessed by multiple threads.</span></span> <span data-ttu-id="2f7fa-121">對於這些情況，<xref:System.Threading>命名空間提供了一些類別可用於同步執行緒。</span><span class="sxs-lookup"><span data-stu-id="2f7fa-121">For these cases, the <xref:System.Threading> namespace provides classes for synchronizing threads.</span></span> <span data-ttu-id="2f7fa-122">這些類別包括 <xref:System.Threading.Mutex>、<xref:System.Threading.Monitor>、<xref:System.Threading.Interlocked>、<xref:System.Threading.AutoResetEvent> 及 <xref:System.Threading.ManualResetEvent>。</span><span class="sxs-lookup"><span data-stu-id="2f7fa-122">These classes include <xref:System.Threading.Mutex>, <xref:System.Threading.Monitor>, <xref:System.Threading.Interlocked>, <xref:System.Threading.AutoResetEvent>, and <xref:System.Threading.ManualResetEvent>.</span></span>  
  
 <span data-ttu-id="2f7fa-123">您可以其中一些類別來同步多執行緒的活動，但有一些執行緒的支援則來自 Visual Basic 語言。</span><span class="sxs-lookup"><span data-stu-id="2f7fa-123">You can use some or all these classes to synchronize the activities of multiple threads, but some support for threading is supported by the Visual Basic language.</span></span> <span data-ttu-id="2f7fa-124">例如 [SyncLock 陳述式](../../../../visual-basic/language-reference/statements/synclock-statement.md)可以透過隱含使用 <xref:System.Threading.Monitor> 來提供同步功能。</span><span class="sxs-lookup"><span data-stu-id="2f7fa-124">For example, the [SyncLock Statement](../../../../visual-basic/language-reference/statements/synclock-statement.md) provides synchronization features through implicit use of <xref:System.Threading.Monitor>.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="2f7fa-125">自 [!INCLUDE[net_v40_long](~/includes/net-v40-long-md.md)] 起，多執行緒程式設計因為 <xref:System.Threading.Tasks.Parallel?displayProperty=fullName> 及 <xref:System.Threading.Tasks.Task?displayProperty=fullName> 類別、[平行 LINQ (PLINQ)](https://msdn.microsoft.com/library/dd460688)、<xref:System.Collections.Concurrent?displayProperty=fullName> 命名空間中的新並行集合類別，以及以工作 (而非執行緒) 概念為基礎的新程式設計模型而獲得大幅簡化。</span><span class="sxs-lookup"><span data-stu-id="2f7fa-125">Beginning with the [!INCLUDE[net_v40_long](~/includes/net-v40-long-md.md)], multithreaded programming is greatly simplified with the <xref:System.Threading.Tasks.Parallel?displayProperty=fullName> and <xref:System.Threading.Tasks.Task?displayProperty=fullName> classes, [Parallel LINQ (PLINQ)](https://msdn.microsoft.com/library/dd460688), new concurrent collection classes in the <xref:System.Collections.Concurrent?displayProperty=fullName> namespace, and a new programming model that is based on the concept of tasks rather than threads.</span></span> <span data-ttu-id="2f7fa-126">如需詳細資訊，請參閱[平行程式設計](https://msdn.microsoft.com/library/dd460693)。</span><span class="sxs-lookup"><span data-stu-id="2f7fa-126">For more information, see [Parallel Programming](https://msdn.microsoft.com/library/dd460693).</span></span>  
  
## <a name="related-topics"></a><span data-ttu-id="2f7fa-127">相關主題</span><span class="sxs-lookup"><span data-stu-id="2f7fa-127">Related Topics</span></span>  
  
|<span data-ttu-id="2f7fa-128">標題</span><span class="sxs-lookup"><span data-stu-id="2f7fa-128">Title</span></span>|<span data-ttu-id="2f7fa-129">說明</span><span class="sxs-lookup"><span data-stu-id="2f7fa-129">Description</span></span>|  
|-----------|-----------------|  
|[<span data-ttu-id="2f7fa-130">多執行緒應用程式 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="2f7fa-130">Multithreaded Applications (Visual Basic)</span></span>](../../../../visual-basic/programming-guide/concepts/threading/multithreaded-applications.md)|<span data-ttu-id="2f7fa-131">說明如何建立及使用執行緒。</span><span class="sxs-lookup"><span data-stu-id="2f7fa-131">Describes how to create and use threads.</span></span>|  
|[<span data-ttu-id="2f7fa-132">多執行緒程序的參數和傳回值 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="2f7fa-132">Parameters and Return Values for Multithreaded Procedures (Visual Basic)</span></span>](../../../../visual-basic/programming-guide/concepts/threading/parameters-and-return-values-for-multithreaded-procedures.md)|<span data-ttu-id="2f7fa-133">說明多執行緒應用程式如何傳遞及傳回參數。</span><span class="sxs-lookup"><span data-stu-id="2f7fa-133">Describes how to pass and return parameters with multithreaded applications.</span></span>|  
|[<span data-ttu-id="2f7fa-134">逐步解說：使用 BackgroundWorker 元件進行多執行緒處理 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="2f7fa-134">Walkthrough: Multithreading with the BackgroundWorker Component (Visual Basic)</span></span>](../../../../visual-basic/programming-guide/concepts/threading/walkthrough-multithreading-with-the-backgroundworker-component.md)|<span data-ttu-id="2f7fa-135">示範如何建立簡單的多執行緒應用程式。</span><span class="sxs-lookup"><span data-stu-id="2f7fa-135">Shows how to create a simple multithreaded application.</span></span>|  
|[<span data-ttu-id="2f7fa-136">執行緒同步處理 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="2f7fa-136">Thread Synchronization (Visual Basic)</span></span>](../../../../visual-basic/programming-guide/concepts/threading/thread-synchronization.md)|<span data-ttu-id="2f7fa-137">說明如何控制執行緒的互動。</span><span class="sxs-lookup"><span data-stu-id="2f7fa-137">Describes how to control the interactions of threads.</span></span>|  
|[<span data-ttu-id="2f7fa-138">執行緒計時器 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="2f7fa-138">Thread Timers (Visual Basic)</span></span>](../../../../visual-basic/programming-guide/concepts/threading/thread-timers.md)|<span data-ttu-id="2f7fa-139">說明如何定期對個別的執行緒執行程序。</span><span class="sxs-lookup"><span data-stu-id="2f7fa-139">Describes how to run procedures on separate threads at fixed intervals.</span></span>|  
|[<span data-ttu-id="2f7fa-140">執行緒集區 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="2f7fa-140">Thread Pooling (Visual Basic)</span></span>](../../../../visual-basic/programming-guide/concepts/threading/thread-pooling.md)|<span data-ttu-id="2f7fa-141">說明如何使用系統管理的背景工作執行緒集區。</span><span class="sxs-lookup"><span data-stu-id="2f7fa-141">Describes how to use a pool of worker threads that are managed by the system.</span></span>|  
|[<span data-ttu-id="2f7fa-142">如何：使用執行緒集區 (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="2f7fa-142">How to: Use a Thread Pool (Visual Basic)</span></span>](../../../../visual-basic/programming-guide/concepts/threading/how-to-use-a-thread-pool.md)|<span data-ttu-id="2f7fa-143">示範如何同步執行緒集區中多執行緒的使用。</span><span class="sxs-lookup"><span data-stu-id="2f7fa-143">Demonstrates synchronized use of multiple threads in the thread pool.</span></span>|  
|[<span data-ttu-id="2f7fa-144">執行緒處理</span><span class="sxs-lookup"><span data-stu-id="2f7fa-144">Threading</span></span>](https://msdn.microsoft.com/library/3e8s7xdd)|<span data-ttu-id="2f7fa-145">說明如何在.NET Framework 中實作執行緒。</span><span class="sxs-lookup"><span data-stu-id="2f7fa-145">Describes how to implement threading in the .NET Framework.</span></span>|
