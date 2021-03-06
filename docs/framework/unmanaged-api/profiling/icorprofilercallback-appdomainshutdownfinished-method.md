---
title: ICorProfilerCallback::AppDomainShutdownFinished 方法
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.AppDomainShutdownFinished
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::AppDomainShutdownFinished
helpviewer_keywords:
- AppDomainShutdownFinished method [.NET Framework profiling]
- ICorProfilerCallback::AppDomainShutdownFinished method [.NET Framework profiling]
ms.assetid: 52794819-0a59-4bb1-a265-0f158cd5cd65
topic_type:
- apiref
ms.openlocfilehash: 0851ac33a2bac4fcf727cf09e5225f6b83481b50
ms.sourcegitcommit: b11efd71c3d5ce3d9449c8d4345481b9f21392c6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/29/2020
ms.locfileid: "76866672"
---
# <a name="icorprofilercallbackappdomainshutdownfinished-method"></a>ICorProfilerCallback::AppDomainShutdownFinished 方法
通知分析工具，應用程式域已從進程中卸載。  
  
## <a name="syntax"></a>語法  
  
```cpp  
HRESULT AppDomainShutdownFinished(  
    [in] AppDomainID appDomainId,  
    [in] HRESULT     hrStatus);  
```  
  
## <a name="parameters"></a>參數

- `appDomainId`

  中的 \[] 可識別用來儲存應用程式元件的網域。

- `hrStatus`

  \[in]） HRESULT，指出是否已成功卸載應用程式域。

## <a name="remarks"></a>備註  
 [ICorProfilerCallback：： AppDomainShutdownStarted](icorprofilercallback-appdomainshutdownstarted-method.md)方法傳回之後，`appDomainId` 的值對資訊要求而言是不正確。  
  
 卸載應用程式域的某些部分可能會在 `AppDomainCreationFinished` 回呼之後繼續進行。 `hrStatus` 中的失敗 HRESULT 表示失敗。 不過，`hrStatus` 中的成功 HRESULT 只會指出卸載應用程式域的第一個部分已成功。  
  
## <a name="requirements"></a>需求  
 **平台：** 請參閱[系統需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **標頭：** CorProf.idl、CorProf.h  
  
 **程式庫：** CorGuids.lib  
  
 **.NET framework 版本：** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>請參閱

- [ICorProfilerCallback 介面](icorprofilercallback-interface.md)
