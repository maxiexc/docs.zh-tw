---
title: HOW TO：設定自訂 WS-Metadata Exchange 繫結
ms.date: 03/30/2017
helpviewer_keywords:
- WS-Metadata Exchange [WCF]
- WS-Metadata Exchange [WCF], configuring a custom binding
ms.assetid: cdba4d73-da64-4805-bc56-9822becfd1e4
ms.openlocfilehash: 6459e3f0cf0ab72af8027bd6802a0e7aa574aece
ms.sourcegitcommit: 1c1a1f9ec0bd1efb3040d86a79f7ee94e207cca5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/03/2020
ms.locfileid: "80635789"
---
# <a name="how-to-configure-a-custom-ws-metadata-exchange-binding"></a>HOW TO：設定自訂 WS-Metadata Exchange 繫結

本文介紹如何配置自定義 WS-元數據交換綁定。 Windows 通訊基礎 (WCF) 包括四個系統定義的元數據綁定,但您可以使用所需的任何綁定發佈元數據。 本文介紹如何使用 發佈中`wsHttpBinding`繼資料 。 這個繫結會提供讓您以安全的方法公開中繼資料的選項。 本文的代碼基於[入門](../samples/getting-started-sample.md)。  
  
### <a name="using-a-configuration-file"></a>使用組態檔  
  
1. 在服務組態檔中，新增包含 `serviceMetadata` 標記的服務行為：  
  
    ```xml  
    <behaviors>  
       <serviceBehaviors>  
         <behavior name="CalculatorServiceBehavior">  
           <serviceMetadata httpGetEnabled="True"/>  
         </behavior>  
       </serviceBehaviors>  
    </behaviors>  
    ```  
  
2. 將 `behaviorConfiguration` 屬性新增至參照這個新行為的服務標記：  
  
    ```xml  
    <service name="Microsoft.ServiceModel.Samples.CalculatorService"  
    behaviorConfiguration="CalculatorServiceBehavior" />
    ```  
  
3. 新增指定 MEX 為位址、指定 `wsHttpBinding` 為繫結，並指定 <xref:System.ServiceModel.Description.IMetadataExchange> 為合約的中繼資料端點：  
  
    ```xml  
    <endpoint address="mex"  
              binding="wsHttpBinding"  
              contract="IMetadataExchange" />  
    ```  
  
4. 要驗證中繼資料交換終結點是否正常工作,請在用戶端設定檔中新增終結點標記:  
  
    ```xml  
    <endpoint name="MyMexEndpoint"               address="http://localhost:8000/servicemodelsamples/service/mex"  
              binding="wsHttpBinding"  
              contract="IMetadataExchange"/>  
    ```  
  
5. 在用戶端的 Main() 方法中，建立新的 <xref:System.ServiceModel.Description.MetadataExchangeClient> 執行個體、將其 <xref:System.ServiceModel.Description.MetadataExchangeClient.ResolveMetadataReferences%2A> 屬性設為 `true`、呼叫 <xref:System.ServiceModel.Description.MetadataExchangeClient.GetMetadata%2A>，然後逐一查看傳回的中繼資料集合：  
  
    ```csharp
    string mexAddress = "http://localhost:8000/servicemodelsamples/service/mex";  
  
    MetadataExchangeClient mexClient = new MetadataExchangeClient("MyMexEndpoint");  
    mexClient.ResolveMetadataReferences = true;  
    MetadataSet mdSet = mexClient.GetMetadata(new EndpointAddress(mexAddress));  
    foreach (MetadataSection section in mdSet.MetadataSections)  
    Console.WriteLine("Metadata section: " + section.Dialect.ToString());  
    ```  
  
### <a name="configuring-by-code"></a>以程式碼設定  
  
1. 建立 <xref:System.ServiceModel.WSHttpBinding> 繫結執行個體：  
  
    ```csharp  
    WSHttpBinding binding = new WSHttpBinding();  
    ```  
  
2. 建立 <xref:System.ServiceModel.ServiceHost> 執行個體：  
  
    ```csharp  
    ServiceHost serviceHost = new ServiceHost(typeof(CalculatorService), baseAddress);  
    ```  
  
3. 新增服務端點，並新增 <xref:System.ServiceModel.Description.ServiceMetadataBehavior> 執行個體：  
  
    ```csharp  
    serviceHost.AddServiceEndpoint(typeof(ICalculator), binding, baseAddress);  
    ServiceMetadataBehavior smb = new ServiceMetadataBehavior();  
    smb.HttpGetEnabled = true;  
    serviceHost.Description.Behaviors.Add(smb);  
    ```  
  
4. 新增中繼資料交換端點，指定稍早建立的 <xref:System.ServiceModel.WSHttpBinding>：  
  
    ```csharp  
    serviceHost.AddServiceEndpoint(typeof(IMetadataExchange), binding, mexAddress);  
    ```  
  
5. 若要驗證中繼資料交換端點是否正常運作，請在用戶端組態檔中新增端點標記：  
  
    ```xml  
    <endpoint name="MyMexEndpoint"               address="http://localhost:8000/servicemodelsamples/service/mex"  
              binding="wsHttpBinding"  
              contract="IMetadataExchange"/>  
    ```  
  
6. 在用戶端的 Main() 方法中，建立新的 <xref:System.ServiceModel.Description.MetadataExchangeClient> 執行個體、將 <xref:System.ServiceModel.Description.MetadataExchangeClient.ResolveMetadataReferences%2A> 屬性設為 `true`、呼叫 <xref:System.ServiceModel.Description.MetadataExchangeClient.GetMetadata%2A>，然後逐一查看傳回的中繼資料集合：  
  
    ```csharp  
    string mexAddress = "http://localhost:8000/servicemodelsamples/service/mex";  
  
    MetadataExchangeClient mexClient = new MetadataExchangeClient("MyMexEndpoint");  
    mexClient.ResolveMetadataReferences = true;  
    MetadataSet mdSet = mexClient.GetMetadata(new EndpointAddress(mexAddress));  
    foreach (MetadataSection section in mdSet.MetadataSections)  
    Console.WriteLine("Metadata section: " + section.Dialect.ToString());  
    ```  
  
## <a name="see-also"></a>另請參閱

- [中繼資料發行行為](../samples/metadata-publishing-behavior.md)
- [擷取中繼資料](../samples/retrieve-metadata.md)
- [中繼資料](../feature-details/metadata.md)
- [發行中繼資料](../feature-details/publishing-metadata.md)
- [發行中繼資料端點](../publishing-metadata-endpoints.md)
