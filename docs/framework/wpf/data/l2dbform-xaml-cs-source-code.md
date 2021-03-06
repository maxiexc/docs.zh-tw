---
title: L2DBForm.xaml.cs 原始程式碼
ms.date: 10/22/2019
ms.topic: sample
ms.openlocfilehash: 882699a76eab3c291cd92c298287bc5d28fb08e1
ms.sourcegitcommit: 82f94a44ad5c64a399df2a03fa842db308185a76
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/25/2019
ms.locfileid: "72920857"
---
# <a name="l2dbformxamlcs-source-code"></a>L2DBForm.xaml.cs 原始程式碼

此頁面包含C# *L2DBForm.xaml.cs*檔案中原始程式碼的內容與描述。 此檔案中所包含的 L2XDBForm 部分類別可分為三個邏輯區段：資料成員、`OnRemove` 以及 `OnAddBook` 按鈕 Click 事件處理常式。

## <a name="data-members"></a>資料成員

系統會使用兩個私有資料成員，將此類別與 L2DBForm.xaml 中所使用的視窗資源產生關聯。

- 系統會將命名空間變數 `myBooks` 初始化為 `"http://www.mybooks.com"`。

- 利用下行，建構函式中的成員 `bookList` 會被初始化為 L2DBForm.xaml 中的 CDATA 字串：

    ```csharp
    bookList = (XElement)((ObjectDataProvider)Resources["LoadedBooks"]).Data;
    ```

## <a name="onaddbook-event-handler"></a>OnAddBook 事件處理常式

這個方法包含下列三個陳述式：

- 第一個條件陳述式用於輸入驗證。

- 第二個陳述式會從使用者在 [加入新的書籍] 使用者介面 (UI) 區段中輸入的字串值，建立新的 <xref:System.Xml.Linq.XElement>。

- 最後一個陳述式會將這個新書籍項目新增至 L2DBForm.xaml 的資料提供者中。 因此，動態資料繫結將會使用這個新項目，自動更新 UI；不需要使用者提供的任何額外程式碼。

## <a name="onremove-event-handler"></a>OnRemove 事件處理常式

`OnRemove` 處理常式比 `OnAddBook` 處理常式複雜的原因有兩個。 第一，原始 XML 包含保留的空白字元，因此，相符的新行 (Newline) 也必須利用書籍項目移除。 第二，為了方便起見，在已刪除項目上的選項會重新設定為清單中的前一個選項。

不過，移除所選書籍項目的核心工作僅由兩個陳述式完成：

- 首先，系統會擷取清單方塊中，與目前所選項目相關聯的書籍項目：

    ```csharp
    XElement selBook = (XElement)lbBooks.SelectedItem;
    ```

- 接著，這個項目會從資料提供者刪除：

    ```csharp
    selBook.Remove();
    ```

再次提醒，動態資料繫結會確保程式的 UI 會自動更新。

## <a name="example"></a>範例

### <a name="code"></a>程式碼

```csharp
using System;
using System.Linq;
using System.Collections;
using System.Collections.Generic;
using System.Diagnostics;
using System.Text;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Data;
using System.Windows.Input;
using System.Xml;
using System.Xml.Linq;

namespace LinqToXmlDataBinding {
    /// <summary>
    /// Interaction logic for L2XDBForm.xaml
    /// </summary>

    public partial class L2XDBForm : System.Windows.Window
    {
        XNamespace mybooks = "http://www.mybooks.com";
        XElement bookList;

        public L2XDBForm()
        {
            InitializeComponent();
            bookList = (XElement)((ObjectDataProvider)Resources["LoadedBooks"]).Data;
        }

        void OnRemoveBook(object sender, EventArgs e)
        {
            int index = lbBooks.SelectedIndex;
            if (index < 0) return;

            XElement selBook = (XElement)lbBooks.SelectedItem;
            //Get next node before removing element.
            XNode nextNode = selBook.NextNode;
            selBook.Remove();

            //Remove any matching newline node.
            if (nextNode != null && nextNode.ToString().Trim().Equals(""))
            { nextNode.Remove(); }

            //Set selected item.
            if (lbBooks.Items.Count > 0)
            {  lbBooks.SelectedItem = lbBooks.Items[index > 0 ? index - 1 : 0]; }
        }

        void OnAddBook(object sender, EventArgs e)
        {
            if (String.IsNullOrEmpty(tbAddID.Text) ||
                String.IsNullOrEmpty(tbAddValue.Text))
            {
                MessageBox.Show("Please supply both a Book ID and a Value!", "Entry Error!");
                return;
            }
            XElement newBook = new XElement(
                                mybooks + "book",
                                new XAttribute("id", tbAddID.Text),
                                tbAddValue.Text);
            bookList.Add("  ", newBook, "\r\n");
        }
    }
}
```

### <a name="comments"></a>註解

如需這些處理常式的相關聯 XAML 原始碼，請參閱 [L2DBForm.xaml 原始程式碼](l2dbform-xaml-source-code.md)。

## <a name="see-also"></a>請參閱

- [逐步解說：LinqToXmlDataBinding 範例](linq-to-xml-data-binding-sample.md)
- [L2DBForm.xaml 來源程式碼](l2dbform-xaml-source-code.md)
