---
title: 如何檢索屬性的值（LINQ 到 XML）（C#）
ms.date: 07/20/2015
ms.assetid: 817bbe89-5979-4234-bf0c-46f63692ac8c
ms.openlocfilehash: 212ad3bb3097e7e2c76da8f165011b181f329d4c
ms.sourcegitcommit: 99b153b93bf94d0fecf7c7bcecb58ac424dfa47c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/25/2020
ms.locfileid: "80249190"
---
# <a name="how-to-retrieve-the-value-of-an-attribute-linq-to-xml-c"></a>如何檢索屬性的值（LINQ 到 XML）（C#）
這個主題顯示如何取得屬性的值。 有兩個主要方式：您可以將 <xref:System.Xml.Linq.XAttribute> 轉型為所需的型別；然後，明確的轉換運算子會將項目或屬性的內容轉換為指定的型別。 或者，您可以使用 <xref:System.Xml.Linq.XAttribute.Value%2A> 屬性。 不過，轉型通常是較好的方法。 如果將屬性強制轉換為可 null 數值型別，則在檢索可能存在或可能不存在的屬性的值時，代碼的編寫更簡單。 有關此技術的示例，請參閱[如何檢索元素的值（LINQ 到 XML）（C#）。](./how-to-retrieve-the-value-of-an-element-linq-to-xml.md)  
  
## <a name="example"></a>範例  
 若要擷取屬性的值，只要將 <xref:System.Xml.Linq.XAttribute> 物件轉型為您所需的型別即可。  
  
```csharp  
XElement root = new XElement("Root",  
                    new XAttribute("Attr", "abcde")  
                );  
Console.WriteLine(root);  
string str = (string)root.Attribute("Attr");  
Console.WriteLine(str);  
```  
  
 這個範例會產生下列輸出：  
  
```output  
<Root Attr="abcde" />  
abcde  
```  
  
## <a name="example"></a>範例  
 下列範例顯示如何擷取屬性位於命名空間之屬性的值。 如需詳細資訊，請參閱[命名空間概觀 (LINQ to XML) (C#)](namespaces-overview-linq-to-xml.md)。  
  
```csharp  
XNamespace aw = "http://www.adventure-works.com";  
XElement root = new XElement(aw + "Root",  
                    new XAttribute(aw + "Attr", "abcde")  
                );  
string str = (string)root.Attribute(aw + "Attr");  
Console.WriteLine(str);  
```  
  
 這個範例會產生下列輸出：  
  
```output  
abcde  
```  
  
## <a name="see-also"></a>另請參閱

- [LINQ to XML 座標軸 (C#)](./linq-to-xml-axes-overview.md)
