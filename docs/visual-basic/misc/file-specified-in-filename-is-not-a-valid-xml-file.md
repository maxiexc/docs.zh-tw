---
title: 檔案名稱中指定的檔案不是有效的 XML 檔案
ms.date: 07/20/2015
ms.assetid: c4c30bf3-e0ad-4bc8-89e0-2c3e49e9793b
ms.openlocfilehash: 5a54e5e7e7c75bb7d766b1bbda10f401fa8b99af
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/15/2019
ms.locfileid: "65640840"
---
# <a name="file-specified-in-filename-is-not-a-valid-xml-file"></a>檔案名稱中指定的檔案不是有效的 XML 檔案

您提供的檔案名稱不是有效的 XML 檔案。 若要指定 XML 文件所允許的結構和內容，您可以使用文件類型定義 (DTD)、Microsoft XDR (XML-Data Reduced) 結構描述或 XML 結構描述定義語言 (XSD) 結構描述。 XSD 結構描述會指定.NET Framework 中的 XML 文法的慣用的方法。

> [!NOTE]
> 在某些舊版 Visual Studio 中， **XML 設計工具** 是具類型資料集和 XML 結構描述的設計工具。 **XML 設計工具** 仍可用來建立及編輯 XML 結構描述檔案。 不過，在 Visual Studio 2012 中，建立和編輯具類型資料集的設計工具是**Dataset 設計工具**。 如需詳細資訊，請參閱 <<c0> [ 建立和編輯具類型資料集](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/314t4see(v=vs.120))。

## <a name="to-correct-this-error"></a>更正這個錯誤

- 確認您提供的檔案名稱正確。

- 將您要檢查的 XML 檔案載入 **XML 設計工具**，以檢查指定的檔案是否包含有效的 XML。 從 [XML]  功能表按一下 [驗證 XML] 。 [工作清單] 中會顯示錯誤。

- 如果 XML 檔案有關聯的 XML 結構描述，請確認項目出現在定義的結構中，而且個別項目的內容符合結構描述中所指定的宣告資料類型。

## <a name="see-also"></a>另請參閱

- <xref:System.Xml>
- [如何：剖析檔案路徑](../../visual-basic/developing-apps/programming/drives-directories-files/how-to-parse-file-paths.md)
