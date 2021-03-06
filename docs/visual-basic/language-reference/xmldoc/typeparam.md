---
title: <typeparam>
ms.date: 07/20/2015
helpviewer_keywords:
- typeparam XML tag
- <typeparam> XML tag
ms.assetid: 1bb5ba78-f060-478c-905c-77a2e43639af
ms.openlocfilehash: 00cb62827381146c172e0d15a2c64b167c21f025
ms.sourcegitcommit: 17ee6605e01ef32506f8fdc686954244ba6911de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/22/2019
ms.locfileid: "74352194"
---
# <a name="typeparam-visual-basic"></a>\<typeparam > （Visual Basic）
定義類型參數名稱和描述。  
  
## <a name="syntax"></a>語法  
  
```xml  
<typeparam name="name">description</typeparam>  
```  
  
## <a name="parameters"></a>參數  
 `name`  
 型別參數的名稱。 以雙引號 (" ") 將名稱括起來。  
  
 `description`  
 類型參數的描述。  
  
## <a name="remarks"></a>備註  
 在泛型型別或泛型成員宣告的批註中使用 `<typeparam>` 標記，以描述其中一個類型參數。  
  
 使用 [-doc](../../../visual-basic/reference/command-line-compiler/doc.md) 編譯可處理檔案的文件註解。  
  
## <a name="example"></a>範例  
 這個範例會使用 `<typeparam>` 標記來描述 `id` 參數。  
  
 [!code-vb[VbVbcnXmlDocComments#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnXmlDocComments/VB/Class1.vb#8)]  
  
## <a name="see-also"></a>請參閱

- [XML 註解標記](../../../visual-basic/language-reference/xmldoc/index.md)
