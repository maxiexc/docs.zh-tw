---
title: HOW TO：以 WorkflowServiceHost 設定持續性
ms.date: 03/30/2017
ms.assetid: e31cd4df-13a3-4a9a-9be8-5243e0055356
ms.openlocfilehash: 4bfa66a895ae9af9cb87ff110dc82c8a8a922b49
ms.sourcegitcommit: 927b7ea6b2ea5a440c8f23e3e66503152eb85591
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2020
ms.locfileid: "81463841"
---
# <a name="how-to-configure-persistence-with-workflowservicehost"></a>HOW TO：以 WorkflowServiceHost 設定持續性
本主題描述如何設定 SQL 工作流程執行個體存放區功能，透過使用組態檔以啟用裝載於 <xref:System.ServiceModel.Activities.WorkflowServiceHost> 中之工作流程的持續性。 使用 SQL 工作流程執行個體存放區功能前，您必須建立一個用於保存工作流程執行個體的 SQL 資料庫。 有關詳細資訊,請參閱[如何:為工作流和工作流服務啟用 SQL 持久性](../../../../docs/framework/windows-workflow-foundation/how-to-enable-sql-persistence-for-workflows-and-workflow-services.md)。  
  
### <a name="to-configure-the-sql-workflow-instance-store-in-configuration"></a>若要在組態中設定 SQL 工作流程執行個體存放區  
  
1. 您可以透過 <xref:System.ServiceModel.Activities.Description.SqlWorkflowInstanceStoreBehavior> 設定 SQL 工作流程執行個體存放區的屬性，這個服務行為可以讓您透過 XML 組態變更設定。 以下設定範例展示如何使用設定檔中的<>`sqlWorkflowInstanceStore`行為元素配置 SQL 工作流實例儲存。  
  
    ```xml  
    <serviceBehaviors>  
        <behavior name="">  
            <sqlWorkflowInstanceStore
                 connectionString="provider=System.Data.SqlClient;Data Source=(local);Initial Catalog=DefaultPersistenceProviderDb;Integrated Security=True;Async=true"  
                 instanceEncodingOption="GZip | None"  
                 instanceCompletionAction="DeleteAll | DeleteNothing"  
                 instanceLockedExceptionAction="NoRetry | SimpleRetry | AggressiveRetry"  
                 hostLockRenewalPeriod="00:00:30"
                 runnableInstancesDetectionPeriod="00:00:05">  
            </sqlWorkflowInstanceStore>  
        </behavior>  
    </serviceBehaviors>  
    ```  
  
     有關如何設定 SQL 工作流實體儲存的詳細資訊,請參閱[如何:為工作流和工作流服務啟用 SQL 持久性](../../../../docs/framework/windows-workflow-foundation/how-to-enable-sql-persistence-for-workflows-and-workflow-services.md)。 有關<>`sqlWorkflowInstanceStore`行為元素的各個設定的詳細資訊,請參閱[SQL 工作流實例存儲](../../../../docs/framework/windows-workflow-foundation/sql-workflow-instance-store.md)。 Windows Server App Fabric 會提供它自己的持續性存放區。 有關詳細資訊,請參閱[Windows 伺服器應用結構持久性](https://docs.microsoft.com/previous-versions/appfabric/ee677272(v=azure.10))。  
  
    > [!NOTE]
    > 上述組態範例會使用簡化的組態。 有關詳細資訊,請參閱[簡化配置](../../../../docs/framework/wcf/simplified-configuration.md)  
  
### <a name="to-configure-the-sql-workflow-instance-store-in-code"></a>若要在程式碼中設定 SQL 工作流程執行個體存放區  
  
1. 您可以透過 <xref:System.ServiceModel.Activities.Description.SqlWorkflowInstanceStoreBehavior> 設定 SQL 工作流程執行個體存放區的屬性，這個服務行為可以讓您透過程式碼變更設定。 下列範例示範如何使用程式碼中的 <xref:System.ServiceModel.Activities.Description.SqlWorkflowInstanceStoreBehavior> 行為項目來設定 SQL 工作流程執行個體存放區。  
  
    ```csharp  
    host.Description.Behaviors.Add(new SqlWorkflowInstanceStoreBehavior  
    {  
       ConnectionString = "provider=System.Data.SqlClient;Data Source=(local);Initial Catalog=DefaultPersistenceProviderDb;Integrated Security=True;Async=true",  
       InstanceEncodingOption = "GZip | None",  
       InstanceCompletionAction = "DeleteAll | DeleteNothing",  
       InstanceLockedExceptionAction = "NoRetry | SimpleRetry | AggressiveRetry",  
       HostLockRenewalPeriod = new TimeSpan(00, 00, 30),  
       RunnableInstancesDetectionPeriod = new TimeSpan(00, 00, 05)  
    });  
    ```  
  
     有關如何設定 SQL 工作流實體儲存的詳細資訊,請參閱[如何:為工作流和工作流服務啟用 SQL 持久性](../../../../docs/framework/windows-workflow-foundation/how-to-enable-sql-persistence-for-workflows-and-workflow-services.md)。 有關<xref:System.ServiceModel.Activities.Description.SqlWorkflowInstanceStoreBehavior>行為元素的各個設定的詳細資訊,請參閱[SQL 工作流實例儲存](../../../../docs/framework/windows-workflow-foundation/sql-workflow-instance-store.md)。 Windows Server App Fabric 會提供它自己的持續性存放區。 有關詳細資訊,請參閱[Windows 伺服器應用結構持久性](https://docs.microsoft.com/previous-versions/appfabric/ee677272(v=azure.10))。  
  
    > [!NOTE]
    > 上述組態範例會使用簡化的組態。 有關詳細資訊,請參閱[簡化配置](../../../../docs/framework/wcf/simplified-configuration.md)  
  
     有關如何以程式設計方式設定持久性的範例,請參閱[如何:為工作流和工作流服務啟用持久性](../../../../docs/framework/windows-workflow-foundation/how-to-enable-persistence-for-workflows-and-workflow-services.md)。  
  
## <a name="see-also"></a>另請參閱

- [工作流服務](../../../../docs/framework/wcf/feature-details/workflow-services.md)
- [工作流程持續性](../../../../docs/framework/windows-workflow-foundation/workflow-persistence.md)
- [Windows Server App Fabric 持續性概念](https://docs.microsoft.com/previous-versions/appfabric/ee677272(v=azure.10))
