---
title: "建立 GamePieceCollection 類別"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e4b037ee-1201-4a55-b198-0d6532ed6f35
caps.latest.revision: 8
author: wadepickett
ms.author: wpickett
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: b74702d71113c3a9dac654971e7d02f97016218b
ms.contentlocale: zh-tw
ms.lasthandoff: 07/28/2017

---
# <a name="creating-the-gamepiececollection-class"></a><span data-ttu-id="56f0d-102">建立 GamePieceCollection 類別</span><span class="sxs-lookup"><span data-stu-id="56f0d-102">Creating the GamePieceCollection Class</span></span>
<span data-ttu-id="56f0d-103">**GamePieceCollection** 類別衍生自泛型清單類別，並引入可更輕鬆管理多個 **GamePiece** 物件的方法。</span><span class="sxs-lookup"><span data-stu-id="56f0d-103">The **GamePieceCollection** class derives from the generic List class, and introduces methods to more easily manage multiple **GamePiece** objects.</span></span>  
  
## <a name="creating-the-code"></a><span data-ttu-id="56f0d-104">建立程式碼</span><span class="sxs-lookup"><span data-stu-id="56f0d-104">Creating the Code</span></span>  
 <span data-ttu-id="56f0d-105">**GamePieceCollection** 類別的建構函式會初始化 *capturedIndex* 私用成員。</span><span class="sxs-lookup"><span data-stu-id="56f0d-105">The constructor of the **GamePieceCollection** class initializes the private member *capturedIndex*.</span></span> <span data-ttu-id="56f0d-106">這個欄位用來追蹤目前滑鼠捕捉到的遊戲片段。</span><span class="sxs-lookup"><span data-stu-id="56f0d-106">This field is used to track which of the game pieces currently has the mouse capture.</span></span>  
  
 <span data-ttu-id="56f0d-107">[!code-csharp[ManipulationXNA#_GamePieceCollection_PrivateMembersAndConstructor](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/gamepiececollection.cs#_gamepiececollection_privatemembersandconstructor)]</span><span class="sxs-lookup"><span data-stu-id="56f0d-107">[!code-csharp[ManipulationXNA#_GamePieceCollection_PrivateMembersAndConstructor](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/gamepiececollection.cs#_gamepiececollection_privatemembersandconstructor)]</span></span>  
  
 <span data-ttu-id="56f0d-108">**ProcessInertia** 和 **Draw** 方法簡化了遊戲 [Game.Update](http://msdn.microsoft.com/library/microsoft.xna.framework.game.update.aspx) 和 [Game.Draw](http://msdn.microsoft.com/library/microsoft.xna.framework.game.draw.aspx) 方法中必要的程式碼，因為會列舉集合中的所有遊戲片段，並在每個 **GamePiece** 物件上呼叫個別的方法。</span><span class="sxs-lookup"><span data-stu-id="56f0d-108">The **ProcessInertia** and the **Draw** methods simplify the code needed in the game [Game.Update](http://msdn.microsoft.com/library/microsoft.xna.framework.game.update.aspx) and [Game.Draw](http://msdn.microsoft.com/library/microsoft.xna.framework.game.draw.aspx) methods by enumerating all of the game pieces in the collection and calling the respective method on each **GamePiece** object.</span></span>  
  
 <span data-ttu-id="56f0d-109">[!code-csharp[ManipulationXNA#_GamePieceCollection_ProcessInertiaAndDraw](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/gamepiececollection.cs#_gamepiececollection_processinertiaanddraw)]</span><span class="sxs-lookup"><span data-stu-id="56f0d-109">[!code-csharp[ManipulationXNA#_GamePieceCollection_ProcessInertiaAndDraw](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/gamepiececollection.cs#_gamepiececollection_processinertiaanddraw)]</span></span>  
  
 <span data-ttu-id="56f0d-110">**UpdateFromMouse** 方法也會在遊戲更新期間被呼叫。</span><span class="sxs-lookup"><span data-stu-id="56f0d-110">The **UpdateFromMouse** method is also called during game update.</span></span> <span data-ttu-id="56f0d-111">藉由第一次檢查目前的捕捉 (如果有的話) 是否仍有作用，它只會啟用一個遊戲片段讓滑鼠捕捉。</span><span class="sxs-lookup"><span data-stu-id="56f0d-111">It enables only one game piece to have the mouse capture by first checking to see if the current capture (if any) is still in effect.</span></span> <span data-ttu-id="56f0d-112">若是如此，則不允許其他片段檢查捕捉。</span><span class="sxs-lookup"><span data-stu-id="56f0d-112">If so, no other piece is allowed to check for capture.</span></span>  
  
 <span data-ttu-id="56f0d-113">如果目前沒有片段具有捕捉，則 **UpdateFromMouse** 方法會從最後一個到第一個列舉每個遊戲片段，並檢查該片段是否報告滑鼠捕捉。</span><span class="sxs-lookup"><span data-stu-id="56f0d-113">If no piece currently has the capture, the **UpdateFromMouse** method enumerates each game piece from last to first, and checks to see if that piece reports a mouse capture.</span></span> <span data-ttu-id="56f0d-114">若是如此，該片段會變成目前捕捉的片段，並且不進行任何更進一步的處理。</span><span class="sxs-lookup"><span data-stu-id="56f0d-114">If so, that piece becomes the current captured piece, and no further processing takes place.</span></span> <span data-ttu-id="56f0d-115">**UpdateFromMouse** 方法會最先檢查集合中的最後一個項目，如此一來，如果兩個片段重疊，則具有較高疊置順序者將取得捕捉。</span><span class="sxs-lookup"><span data-stu-id="56f0d-115">The **UpdateFromMouse** method checks the last item in the collection first so that if two pieces are overlapped, the one with the higher Z-order will obtain the capture.</span></span> <span data-ttu-id="56f0d-116">疊置順序並不明確，也不可以變更；它只是受遊戲片段加入集合的順序所控管。</span><span class="sxs-lookup"><span data-stu-id="56f0d-116">Z-order is not explicit nor changeable; it is governed simply by the order in which game pieces are added to the collection.</span></span>  
  
 <span data-ttu-id="56f0d-117">[!code-csharp[ManipulationXNA#_GamePieceCollection_UpdateFromMouse](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/gamepiececollection.cs#_gamepiececollection_updatefrommouse)]</span><span class="sxs-lookup"><span data-stu-id="56f0d-117">[!code-csharp[ManipulationXNA#_GamePieceCollection_UpdateFromMouse](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/gamepiececollection.cs#_gamepiececollection_updatefrommouse)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="56f0d-118">另請參閱</span><span class="sxs-lookup"><span data-stu-id="56f0d-118">See Also</span></span>  
 <span data-ttu-id="56f0d-119">[操作和慣性](../../../docs/framework/common-client-technologies/manipulations-and-inertia.md) </span><span class="sxs-lookup"><span data-stu-id="56f0d-119">[Manipulations and Inertia](../../../docs/framework/common-client-technologies/manipulations-and-inertia.md) </span></span>  
 <span data-ttu-id="56f0d-120">[在 XNA 應用程式中使用操作和慣性](../../../docs/framework/common-client-technologies/use-manipulations-and-inertia-in-an-xna-application.md) </span><span class="sxs-lookup"><span data-stu-id="56f0d-120">[Using Manipulations and Inertia in an XNA Application](../../../docs/framework/common-client-technologies/use-manipulations-and-inertia-in-an-xna-application.md) </span></span>  
 <span data-ttu-id="56f0d-121">[建立 GamePiece 類別](../../../docs/framework/common-client-technologies/creating-the-gamepiece-class.md) </span><span class="sxs-lookup"><span data-stu-id="56f0d-121">[Creating the GamePiece Class](../../../docs/framework/common-client-technologies/creating-the-gamepiece-class.md) </span></span>  
 <span data-ttu-id="56f0d-122">[建立 Game1 類別](../../../docs/framework/common-client-technologies/creating-the-game1-class.md) </span><span class="sxs-lookup"><span data-stu-id="56f0d-122">[Creating the Game1 Class](../../../docs/framework/common-client-technologies/creating-the-game1-class.md) </span></span>  
 [<span data-ttu-id="56f0d-123">完整程式碼清單</span><span class="sxs-lookup"><span data-stu-id="56f0d-123">Full Code Listings</span></span>](../../../docs/framework/common-client-technologies/full-code-listings.md)
