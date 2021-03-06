---
title: COR_PRF_GC_ROOT_KIND 列舉
ms.date: 03/30/2017
api_name:
- COR_PRF_GC_ROOT_KIND
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- COR_PRF_GC_ROOT_KIND
helpviewer_keywords:
- COR_PRF_GC_ROOT_KIND enumeration [.NET Framework profiling]
ms.assetid: b9fb1c03-417f-41d4-aed4-02cb4ade8def
topic_type:
- apiref
ms.openlocfilehash: bff45e6f6f57b95d07ac5073cb70020818cce000
ms.sourcegitcommit: b11efd71c3d5ce3d9449c8d4345481b9f21392c6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/29/2020
ms.locfileid: "76867161"
---
# <a name="cor_prf_gc_root_kind-enumeration"></a>COR_PRF_GC_ROOT_KIND 列舉
表示[ICorProfilerCallback2：： RootReferences2](icorprofilercallback2-rootreferences2-method.md)回呼所公開的垃圾收集根目錄種類。  
  
## <a name="syntax"></a>語法  
  
```cpp  
typedef enum {  
    COR_PRF_GC_ROOT_STACK = 1,  
    COR_PRF_GC_ROOT_FINALIZER = 2,  
    COR_PRF_GC_ROOT_HANDLE = 3,  
    COR_PRF_GC_ROOT_OTHER = 0  
} COR_PRF_GC_ROOT_KIND;  
```  
  
## <a name="members"></a>Members  
  
|成員|描述|  
|------------|-----------------|  
|`COR_PRF_GC_ROOT_STACK`|根是堆疊上的變數。|  
|`COR_PRF_GC_ROOT_FINALIZER`|根是完成項佇列中的專案。|  
|`COR_PRF_GC_ROOT_HANDLE`|根是垃圾收集控制碼。|  
|`COR_PRF_GC_ROOT_OTHER`|未指定根類型。|  
  
## <a name="requirements"></a>需求  
 **平台：** 請參閱[系統需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **標頭：** CorProf.idl、CorProf.h  
  
 **程式庫：** CorGuids.lib  
  
 **.NET framework 版本：** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>請參閱

- [分析列舉](profiling-enumerations.md)
