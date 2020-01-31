---
title: 在雲端原生應用程式中快取
description: 瞭解雲端原生應用程式中的快取策略。
author: robvet
ms.date: 01/22/2020
ms.openlocfilehash: 2da61a01fc53233d1934df813fcba3b91a495c43
ms.sourcegitcommit: 13e79efdbd589cad6b1de634f5d6b1262b12ab01
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/28/2020
ms.locfileid: "76794965"
---
# <a name="caching-in-a-cloud-native-app"></a><span data-ttu-id="3466a-103">在雲端原生應用程式中快取</span><span class="sxs-lookup"><span data-stu-id="3466a-103">Caching in a cloud-native app</span></span>

[!INCLUDE [book-preview](../../../includes/book-preview.md)]

<span data-ttu-id="3466a-104">快取的優點很清楚。</span><span class="sxs-lookup"><span data-stu-id="3466a-104">The benefits of caching are well understood.</span></span> <span data-ttu-id="3466a-105">這項技術的運作方式是將經常存取的資料從後端資料存放區暫時複製到靠近應用程式的*快速儲存體*。</span><span class="sxs-lookup"><span data-stu-id="3466a-105">The technique works by temporarily copying frequently accessed data from a backend data store to *fast storage* that's located closer to the application.</span></span> <span data-ttu-id="3466a-106">快取通常會實作為 。</span><span class="sxs-lookup"><span data-stu-id="3466a-106">Caching is often implemented where...</span></span>

- <span data-ttu-id="3466a-107">資料會維持相對靜態。</span><span class="sxs-lookup"><span data-stu-id="3466a-107">Data remains relatively static.</span></span>
- <span data-ttu-id="3466a-108">資料存取速度很慢，特別是與快取的速度相比。</span><span class="sxs-lookup"><span data-stu-id="3466a-108">Data access is slow, especially compared to the speed of the cache.</span></span>
- <span data-ttu-id="3466a-109">資料受限於高層級的爭用。</span><span class="sxs-lookup"><span data-stu-id="3466a-109">Data is subject to high levels of contention.</span></span>

## <a name="why"></a><span data-ttu-id="3466a-110">為什麼？</span><span class="sxs-lookup"><span data-stu-id="3466a-110">Why?</span></span>

<span data-ttu-id="3466a-111">如 Microsoft 快取[指引](https://docs.microsoft.com/azure/architecture/best-practices/caching)中所述，快取可以提升個別微服務和整個系統的效能、擴充性和可用性。</span><span class="sxs-lookup"><span data-stu-id="3466a-111">As discussed in the [Microsoft caching guidance](https://docs.microsoft.com/azure/architecture/best-practices/caching), caching can increase performance, scalability, and availability for individual microservices and the system as a whole.</span></span> <span data-ttu-id="3466a-112">它可減少對資料存放區處理大量並行要求的延遲和競爭。</span><span class="sxs-lookup"><span data-stu-id="3466a-112">It reduces the latency and contention of handling large volumes of concurrent requests to a data store.</span></span> <span data-ttu-id="3466a-113">隨著資料量和使用者數目的增加，快取的優點就愈大。</span><span class="sxs-lookup"><span data-stu-id="3466a-113">As data volume and the number of users increase, the greater the benefits of caching become.</span></span>

<span data-ttu-id="3466a-114">當用戶端重複讀取不可變或不常變更的資料時，快取最有效率。</span><span class="sxs-lookup"><span data-stu-id="3466a-114">Caching is most effective when a client repeatedly reads data that is immutable or that changes infrequently.</span></span> <span data-ttu-id="3466a-115">範例包括參考資訊（例如產品和價格資訊），或許多耗用大量共用靜態資源的結構。</span><span class="sxs-lookup"><span data-stu-id="3466a-115">Examples include reference information such as product and pricing information, or shared static resources that are costly to construct.</span></span>

<span data-ttu-id="3466a-116">雖然微服務應該是無狀態的，但在絕對必要時，分散式快取可以支援平行存取會話狀態資料。</span><span class="sxs-lookup"><span data-stu-id="3466a-116">While microservices should be stateless, a distributed cache can support concurrent access to session state data when absolutely required.</span></span>

<span data-ttu-id="3466a-117">也請考慮快取以避免重複計算。</span><span class="sxs-lookup"><span data-stu-id="3466a-117">Also consider caching to avoid repetitive computations.</span></span> <span data-ttu-id="3466a-118">如果作業轉換資料或執行複雜的計算，請快取後續要求的結果。</span><span class="sxs-lookup"><span data-stu-id="3466a-118">If an operation transforms data or performs a complicated calculation, cache the result for subsequent requests.</span></span>

## <a name="caching-architecture"></a><span data-ttu-id="3466a-119">快取架構</span><span class="sxs-lookup"><span data-stu-id="3466a-119">Caching architecture</span></span>

<span data-ttu-id="3466a-120">雲端原生應用程式通常會執行分散式快取架構。</span><span class="sxs-lookup"><span data-stu-id="3466a-120">Cloud native applications typically implement a distributed caching architecture.</span></span> <span data-ttu-id="3466a-121">快取是以雲端為基礎的[支援服務](./definition.md#backing-services)來裝載，並與微服務分開。</span><span class="sxs-lookup"><span data-stu-id="3466a-121">The cache is hosted as a cloud-based [backing service](./definition.md#backing-services), separate from the microservices.</span></span> <span data-ttu-id="3466a-122">圖5-20 顯示架構。</span><span class="sxs-lookup"><span data-stu-id="3466a-122">Figure 5-20 shows the architecture.</span></span>

![在雲端原生應用程式中快取](media/caching-in-a-cloud-native-app.png)

<span data-ttu-id="3466a-124">**圖 5-19**：雲端原生應用程式中的快取</span><span class="sxs-lookup"><span data-stu-id="3466a-124">**Figure 5-19**: Caching in a cloud native app</span></span>

<span data-ttu-id="3466a-125">在上圖中，請注意快取是獨立的，並由微服務共用。</span><span class="sxs-lookup"><span data-stu-id="3466a-125">In the previous figure, note how the cache is independent of and shared by the microservices.</span></span> <span data-ttu-id="3466a-126">在此案例中， [API 閘道](./front-end-communication.md)會叫用快取。</span><span class="sxs-lookup"><span data-stu-id="3466a-126">In this scenario, the cache is invoked by the [API Gateway](./front-end-communication.md).</span></span> <span data-ttu-id="3466a-127">如第4章所述，閘道可作為所有傳入要求的前端。</span><span class="sxs-lookup"><span data-stu-id="3466a-127">As discussed in chapter 4, the gateway serves as a front end for all incoming requests.</span></span> <span data-ttu-id="3466a-128">分散式快取會盡可能傳回快取的資料，以增加系統回應能力。</span><span class="sxs-lookup"><span data-stu-id="3466a-128">The distributed cache increases system responsiveness by returning cached data whenever possible.</span></span> <span data-ttu-id="3466a-129">此外，將快取與服務分開，可讓快取獨立相應增加或相應放大，以滿足更多的流量需求。</span><span class="sxs-lookup"><span data-stu-id="3466a-129">Additionally, separating the cache from the services allows the cache to scale up or out independently to meet increased traffic demands.</span></span>

<span data-ttu-id="3466a-130">此圖顯示常見的快取模式，稱為另行快取[模式](https://docs.microsoft.com/azure/architecture/patterns/cache-aside)。</span><span class="sxs-lookup"><span data-stu-id="3466a-130">The figure presents a common caching pattern known as the [cache-aside pattern](https://docs.microsoft.com/azure/architecture/patterns/cache-aside).</span></span> <span data-ttu-id="3466a-131">針對連入要求，您必須先查詢快取（步驟 \#1）來取得回應。</span><span class="sxs-lookup"><span data-stu-id="3466a-131">For an incoming request, you first query the cache (step \#1) for a response.</span></span> <span data-ttu-id="3466a-132">如果找到，則會立即傳回資料。</span><span class="sxs-lookup"><span data-stu-id="3466a-132">If found, the data is returned immediately.</span></span> <span data-ttu-id="3466a-133">如果資料不存在於快取中（稱為快取[遺漏](https://www.techopedia.com/definition/6308/cache-miss)），則會從下游服務中的本機資料庫抓取（步驟 \#2）。</span><span class="sxs-lookup"><span data-stu-id="3466a-133">If the data doesn't exist in the cache (known as a [cache miss](https://www.techopedia.com/definition/6308/cache-miss)), it's retrieved from a local database in a downstream service (step \#2).</span></span> <span data-ttu-id="3466a-134">然後會將它寫入快取以供未來的要求（步驟 \#3），並傳回給呼叫者。</span><span class="sxs-lookup"><span data-stu-id="3466a-134">It's then written to the cache for future requests (step \#3), and returned to the caller.</span></span> <span data-ttu-id="3466a-135">請小心定期收回快取的資料，讓系統維持及時且一致的狀態。</span><span class="sxs-lookup"><span data-stu-id="3466a-135">Care must be taken to periodically evict cached data so that the system remains timely and consistent.</span></span>

<span data-ttu-id="3466a-136">當共用快取增加時，將其資料分割到多個節點上可能會有好處。</span><span class="sxs-lookup"><span data-stu-id="3466a-136">As a shared cache grows, it might prove beneficial to partition its data across multiple nodes.</span></span> <span data-ttu-id="3466a-137">這麼做可協助將爭用降到最低，並改善擴充性。</span><span class="sxs-lookup"><span data-stu-id="3466a-137">Doing so can help minimize contention and improve scalability.</span></span> <span data-ttu-id="3466a-138">許多快取服務都支援動態新增和移除節點，以及跨分割區重新平衡資料的功能。</span><span class="sxs-lookup"><span data-stu-id="3466a-138">Many Caching services support the ability to dynamically add and remove nodes and rebalance data across partitions.</span></span> <span data-ttu-id="3466a-139">這種方法通常牽涉到叢集。</span><span class="sxs-lookup"><span data-stu-id="3466a-139">This approach typically involves clustering.</span></span> <span data-ttu-id="3466a-140">叢集會將同盟節點的集合公開為順暢的單一快取。</span><span class="sxs-lookup"><span data-stu-id="3466a-140">Clustering exposes a collection of federated nodes as a seamless, single cache.</span></span> <span data-ttu-id="3466a-141">不過，在內部，資料會在節點間散佈，並遵循預先定義的散發策略來平均平衡負載。</span><span class="sxs-lookup"><span data-stu-id="3466a-141">Internally, however, the data is dispersed across the nodes following a predefined distribution strategy that balances the load evenly.</span></span>

## <a name="azure-cache-for-redis"></a><span data-ttu-id="3466a-142">Azure Cache for Redis</span><span class="sxs-lookup"><span data-stu-id="3466a-142">Azure Cache for Redis</span></span>

<span data-ttu-id="3466a-143">[Azure Cache For Redis](https://azure.microsoft.com/services/cache/)是安全的資料快取和訊息代理程式服務，完全由 Microsoft 管理。</span><span class="sxs-lookup"><span data-stu-id="3466a-143">[Azure Cache for Redis](https://azure.microsoft.com/services/cache/) is a secure data caching and messaging broker service, fully managed by Microsoft.</span></span> <span data-ttu-id="3466a-144">以「平臺即服務」（PaaS）供應專案的形式取用，可提供高輸送量和低延遲的資料存取。</span><span class="sxs-lookup"><span data-stu-id="3466a-144">Consumed as a Platform as a Service (PaaS) offering, it provides high throughput and low-latency access to data.</span></span> <span data-ttu-id="3466a-145">服務可供 Azure 內部或外部的任何應用程式存取。</span><span class="sxs-lookup"><span data-stu-id="3466a-145">The service is accessible to any application within or outside of Azure.</span></span>

<span data-ttu-id="3466a-146">Azure Cache for Redis 服務會管理跨 Azure 資料中心裝載之開放原始碼 Redis 伺服器的存取權。</span><span class="sxs-lookup"><span data-stu-id="3466a-146">The Azure Cache for Redis service manages access to open-source Redis servers hosted across Azure data centers.</span></span> <span data-ttu-id="3466a-147">此服務的作用是提供管理、存取控制和安全性的外觀。</span><span class="sxs-lookup"><span data-stu-id="3466a-147">The service acts as a facade providing management, access control, and security.</span></span> <span data-ttu-id="3466a-148">服務原本就支援一組豐富的資料結構，包括字串、雜湊、清單和集合。</span><span class="sxs-lookup"><span data-stu-id="3466a-148">The service natively supports a rich set of data structures, including strings, hashes, lists, and sets.</span></span> <span data-ttu-id="3466a-149">如果您的應用程式已使用 Redis，它會與 Azure Cache for Redis 一起正常搭配使用。</span><span class="sxs-lookup"><span data-stu-id="3466a-149">If your application already uses Redis, it will work as-is with Azure Cache for Redis.</span></span>

<span data-ttu-id="3466a-150">Azure Cache for Redis 不只是簡單的快取伺服器。</span><span class="sxs-lookup"><span data-stu-id="3466a-150">Azure Cache for Redis is more than a simple cache server.</span></span> <span data-ttu-id="3466a-151">它可以支援數種案例來增強微服務架構：</span><span class="sxs-lookup"><span data-stu-id="3466a-151">It can support a number of scenarios to enhance a microservices architecture:</span></span>

- <span data-ttu-id="3466a-152">記憶體中的資料存放區</span><span class="sxs-lookup"><span data-stu-id="3466a-152">An in-memory data store</span></span>
- <span data-ttu-id="3466a-153">分散式非關係資料庫</span><span class="sxs-lookup"><span data-stu-id="3466a-153">A distributed non-relational database</span></span>
- <span data-ttu-id="3466a-154">訊息代理程式</span><span class="sxs-lookup"><span data-stu-id="3466a-154">A message broker</span></span>
- <span data-ttu-id="3466a-155">設定或探索伺服器</span><span class="sxs-lookup"><span data-stu-id="3466a-155">A configuration or discovery server</span></span>
  
<span data-ttu-id="3466a-156">在 advanced 案例中，快取資料的複本可以[保存到磁片](https://docs.microsoft.com/azure/azure-cache-for-redis/cache-how-to-premium-persistence)中。</span><span class="sxs-lookup"><span data-stu-id="3466a-156">For advanced scenarios, a copy of the cached data can be [persisted to disk](https://docs.microsoft.com/azure/azure-cache-for-redis/cache-how-to-premium-persistence).</span></span> <span data-ttu-id="3466a-157">如果嚴重事件同時停用主要和複本快取，則會從最新的快照集重建快取。</span><span class="sxs-lookup"><span data-stu-id="3466a-157">If a catastrophic event disables both the primary and replica caches, the cache is reconstructed from the most recent snapshot.</span></span>

<span data-ttu-id="3466a-158">Azure Redis 快取適用于多個預先定義的設定和定價層。</span><span class="sxs-lookup"><span data-stu-id="3466a-158">Azure Redis Cache is available across a number of predefined configurations and pricing tiers.</span></span>  <span data-ttu-id="3466a-159">進階層提供許多企業層級[的功能，](https://docs.microsoft.com/azure/azure-cache-for-redis/cache-premium-tier-intro)例如叢集、資料持續性、異地複寫和虛擬網路隔離。</span><span class="sxs-lookup"><span data-stu-id="3466a-159">The [Premium tier](https://docs.microsoft.com/azure/azure-cache-for-redis/cache-premium-tier-intro) features many enterprise-level features such as clustering, data persistence, geo-replication, and virtual-network isolation.</span></span>

>[!div class="step-by-step"]
><span data-ttu-id="3466a-160">[上一頁](relational-vs-nosql-data.md)
>[下一頁](elastic-search-in-azure.md)</span><span class="sxs-lookup"><span data-stu-id="3466a-160">[Previous](relational-vs-nosql-data.md)
[Next](elastic-search-in-azure.md)</span></span>