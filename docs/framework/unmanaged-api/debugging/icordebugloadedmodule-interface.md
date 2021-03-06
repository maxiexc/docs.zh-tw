---
title: ICorDebugLoadedModule 介面
ms.date: 03/30/2017
ms.assetid: 34be6369-2e75-4a95-a538-3b29ac97cf6d
ms.openlocfilehash: d9b8245d8c37867971aa48ed3befb9cf22bd5b04
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/12/2020
ms.locfileid: "83210159"
---
# <a name="icordebugloadedmodule-interface"></a>ICorDebugLoadedModule 介面
提供載入模組的相關資訊。  
  
## <a name="methods"></a>方法  
  
|方法|描述|  
|------------|-----------------|  
|[GetBaseAddress 方法](icordebugloadedmodule-getbaseaddress-method.md)|取得載入模組的基底位址。|  
|[GetName 方法](icordebugloadedmodule-getname-method.md)|取得載入模組的名稱。|  
|[GetSize 方法](icordebugloadedmodule-getsize-method.md)|取得載入模組的大小 (以位元組為單位)。|  
  
## <a name="remarks"></a>備註  
 `ICorDebugLoadedModule` 介面是由偵錯工具實作，並由 CLR 偵錯介面用以從偵錯工具取得載入模組的相關資訊。  
  
> [!NOTE]
> 這個介面僅適用於 .NET 原生。 如果您在 .NET 原生之外針對 ICorDebug 案例實作這個介面，Common Language Runtime 會忽略這個介面。  
  
## <a name="requirements"></a>需求  
 **平台：** 請參閱[系統需求](../../get-started/system-requirements.md)。  
  
 **標頭：** CorDebug.idl、CorDebug.h  
  
 **程式庫：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]  
  
## <a name="see-also"></a>請參閱

- [偵錯介面](debugging-interfaces.md)
- [偵錯](index.md)
