---
title: 剪貼簿的格式無效
ms.date: 07/20/2015
f1_keywords:
- vbrID460
ms.assetid: 71a4a045-65bb-417d-b3bd-99a9fa3c53f6
ms.openlocfilehash: 15bc530d1030a8c4d720321ea249fdd7fb6cd8b6
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/28/2019
ms.locfileid: "64623090"
---
# <a name="clipboard-format-is-not-valid"></a>剪貼簿的格式無效
指定的剪貼簿格式與不相容所執行的方法。 此錯誤的可能原因包括：  
  
- 使用剪貼簿`GetText`或是`SetText`方法以外的剪貼簿格式`vbCFText`或`vbCFLink`。  
  
- 使用剪貼簿`GetData`或是`SetData`方法以外的剪貼簿格式`vbCFBitmap`， `vbCFDIB`，或`vbCFMetafile`。  
  
- 使用`GetData`或是`SetData`方法`DataObject`與 Microsoft Windows 登錄格式 （HC000-& HFFFF），保留範圍的剪貼簿格式時該剪貼簿格式尚未註冊使用 Microsoft Windows.  
  
## <a name="to-correct-this-error"></a>更正這個錯誤  
  
- 移除無效的格式，並指定一個有效的帳戶。  
  
## <a name="see-also"></a>另請參閱

- [剪貼簿：加入其他格式](/cpp/mfc/clipboard-adding-other-formats)
