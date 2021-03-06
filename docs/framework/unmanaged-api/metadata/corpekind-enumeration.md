---
title: CorPEKind 列舉
ms.date: 03/30/2017
api_name:
- CorPEKind
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorPEKind
helpviewer_keywords:
- CorPEKind enumeration [.NET Framework metadata]
ms.assetid: 22dc6dea-b1b9-4982-a730-a022d586b117
topic_type:
- apiref
ms.openlocfilehash: 74670a1477546066145bd4bbf2f123a252e10b55
ms.sourcegitcommit: 9a39f2a06f110c9c7ca54ba216900d038aa14ef3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/23/2019
ms.locfileid: "74436480"
---
# <a name="corpekind-enumeration"></a>CorPEKind 列舉
包含值，描述從[IMetaDataImport2：： GetPEKind](../../../../docs/framework/unmanaged-api/metadata/imetadataimport2-getpekind-method.md)的呼叫傳回的可移植執行檔（PE）。  
  
## <a name="syntax"></a>語法  
  
```cpp  
typedef enum CorPEKind {  
  
    peNot           = 0x00000000,  
    peILonly        = 0x00000001,  
    pe32BitRequired = 0x00000002,  
    pe32Plus        = 0x00000004,  
    pe32Unmanaged   = 0x00000008,  
    pe32BitPreferred= 0x00000010  
  
} CorPEKind;  
```  
  
## <a name="members"></a>Members  
  
|成員|描述|  
|------------|-----------------|  
|`peNot`|表示這不是 PE 檔案。|  
|`peILOnly`|指出這個 PE 檔案僅包含 managed 程式碼。|  
|`pe32BitRequired`|指出這個 PE 檔案會進行 Win32 呼叫。|  
|`pe32Plus`|指出這個 PE 檔案是在64位平臺上執行。|  
|`pe32Unmanaged`|指出這個 PE 檔案是機器碼。|  
|pe32BitPreferred|指出此 PE 檔案為平臺中性，並偏好在32位環境中載入。|  
  
## <a name="remarks"></a>備註  
 這些值可用於位組合。  
  
## <a name="requirements"></a>需求  
 **平台：** 請參閱[系統需求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **標頭：** Corhdr.h。h  
  
 **.NET framework 版本：** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>另請參閱

- [中繼資料列舉](../../../../docs/framework/unmanaged-api/metadata/metadata-enumerations.md)
