---
title: 程式碼範例
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: c119657a-9ce6-4940-91e4-ac1d5f0d9584
ms.openlocfilehash: 6e0c34e1db50030c78db295f26fcc25b431d3dde
ms.sourcegitcommit: 267d092663aba36b6b2ea853034470aea493bfae
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/21/2020
ms.locfileid: "80111799"
---
# <a name="adonet-code-examples"></a>ADO.NET代碼示例

此頁上的代碼清單演示如何使用以下ADO.NET技術從資料庫檢索資料：

- ADO.NET 資料提供者：

  - [SqlClient](#sqlclient) `System.Data.SqlClient`（ ）

  - [OleDb](#oledb) `System.Data.OleDb`（ ）

  - [奧德布](#odbc)`System.Data.Odbc`（ ）

  - [甲骨文客戶](#oracleclient)`System.Data.OracleClient`（ ）

- ADO.NET Entity Framework：

  - [林Q 到實體](#linq-to-entities)

  - [具型別的 ObjectQuery](#typed-objectquery)

  - [實體用戶端](#entityclient)`System.Data.EntityClient`（ ）

- [LINQ to SQL](#linq-to-sql)

## <a name="adonet-data-provider-examples"></a>ADO.NET資料提供程式示例
下列程式碼清單將示範如何使用 ADO.NET 資料提供者來擷取資料庫中的資料。 資料會傳入 `DataReader` 中。 有關詳細資訊，請參閱[使用資料讀取器檢索資料](retrieving-data-using-a-datareader.md)。

### <a name="sqlclient"></a>SqlClient
此示例中的代碼假定您可以連接到 Microsoft SQL Server`Northwind`上的示例資料庫。 這段程式碼會建立 <xref:System.Data.SqlClient.SqlCommand>，以便從 Products 資料表中選取資料列，並且加入 <xref:System.Data.SqlClient.SqlParameter>，以便將結果限制為 UnitPrice 大於指定之參數值 (在此案例中為 5) 的資料列。 在<xref:System.Data.SqlClient.SqlConnection>`using`塊內打開 ，這可確保在代碼退出時關閉和釋放資源。 然後，程式碼會使用 <xref:System.Data.SqlClient.SqlDataReader> 來執行此命令，並且在主控台視窗中顯示結果。

 [!code-csharp[DataWorks SampleApp.SqlClient#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SampleApp.SqlClient/CS/source.cs#1)]
 [!code-vb[DataWorks SampleApp.SqlClient#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SampleApp.SqlClient/VB/source.vb#1)]

### <a name="oledb"></a>OleDb
這則範例中的程式碼會假設您可以連接至 Microsoft Access Northwind 範例資料庫。 這段程式碼會建立 <xref:System.Data.OleDb.OleDbCommand>，以便從 Products 資料表中選取資料列，並且加入 <xref:System.Data.OleDb.OleDbParameter>，以便將結果限制為 UnitPrice 大於指定之參數值 (在此案例中為 5) 的資料列。 <xref:System.Data.OleDb.OleDbConnection> 是在 `using` 區塊內部開啟，可確保程式碼結束時，系統會關閉和處置 (Dispose) 資源。 然後，程式碼會使用 <xref:System.Data.OleDb.OleDbDataReader> 來執行此命令，並且在主控台視窗中顯示結果。

 [!code-csharp[DataWorks SampleApp.OleDb#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SampleApp.OleDb/CS/source.cs#1)]
 [!code-vb[DataWorks SampleApp.OleDb#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SampleApp.OleDb/VB/source.vb#1)]

### <a name="odbc"></a>ODBC
這則範例中的程式碼會假設您可以連接至 Microsoft Access Northwind 範例資料庫。 這段程式碼會建立 <xref:System.Data.Odbc.OdbcCommand>，以便從 Products 資料表中選取資料列，並且加入 <xref:System.Data.Odbc.OdbcParameter>，以便將結果限制為 UnitPrice 大於指定之參數值 (在此案例中為 5) 的資料列。 在<xref:System.Data.Odbc.OdbcConnection>`using`塊內打開 ，這可確保在代碼退出時關閉和釋放資源。 然後，程式碼會使用 <xref:System.Data.Odbc.OdbcDataReader> 來執行此命令，並且在主控台視窗中顯示結果。

[!code-csharp[DataWorks SampleApp.Odbc#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SampleApp.Odbc/CS/source.cs#1)]
[!code-vb[DataWorks SampleApp.Odbc#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SampleApp.Odbc/VB/source.vb#1)]

### <a name="oracleclient"></a>OracleClient
這則範例中的程式碼會假設您已連接到 Oracle 伺服器上的 DEMO.CUSTOMER。 您也必須加入 System.Data.OracleClient.dll 的參考。 此程式碼會將資料傳入 <xref:System.Data.OracleClient.OracleDataReader> 中。

 [!code-csharp[DataWorks SampleApp.Oracle#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SampleApp.Oracle/CS/source.cs#1)]
 [!code-vb[DataWorks SampleApp.Oracle#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SampleApp.Oracle/VB/source.vb#1)]

## <a name="entity-framework-examples"></a>實體框架示例
下列程式碼清單將示範如何透過查詢 Entity Data Model (EDM) 中的實體，擷取資料來源中的資料。 這些示例使用基於北風示例資料庫的模型。 有關實體框架的詳細資訊，請參閱[實體框架概述](./ef/overview.md)。

### <a name="linq-to-entities"></a>LINQ to Entities
這則範例中的程式碼會使用 LINQ 查詢來傳回資料當做 Categories 物件，而這些物件會投影成僅包含 CategoryID 和 CategoryName 屬性的匿名型別。 有關詳細資訊，請參閱[LINQ 到實體概述](./ef/language-reference/linq-to-entities.md)。

```csharp
using System;
using System.Linq;
using System.Data.Objects;
using NorthwindModel;

class LinqSample
{
    public static void ExecuteQuery()
    {
        using (NorthwindEntities context = new NorthwindEntities())
        {
            try
            {
                var query = from category in context.Categories
                            select new
                            {
                                categoryID = category.CategoryID,
                                categoryName = category.CategoryName
                            };

                foreach (var categoryInfo in query)
                {
                    Console.WriteLine("\t{0}\t{1}",
                        categoryInfo.categoryID, categoryInfo.categoryName);
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine(ex.Message);
            }
        }
    }
}
```

```vb
Option Explicit On
Option Strict On

Imports System.Linq
Imports System.Data.Objects
Imports NorthwindModel

Class LinqSample
    Public Shared Sub ExecuteQuery()
        Using context As NorthwindEntities = New NorthwindEntities()
            Try
                Dim query = From category In context.Categories _
                            Select New With _
                            { _
                                .categoryID = category.CategoryID, _
                                .categoryName = category.CategoryName _
                            }

                For Each categoryInfo In query
                    Console.WriteLine(vbTab & "{0}" & vbTab & "{1}", _
                        categoryInfo.categoryID, categoryInfo.categoryName)
                Next
            Catch ex As Exception
                Console.WriteLine(ex.Message)
            End Try
        End Using
    End Sub
End Class
```

### <a name="typed-objectquery"></a>具型別的 ObjectQuery
這則範例中的程式碼會使用 <xref:System.Data.Objects.ObjectQuery%601> 來傳回資料當做 Categories 物件。 有關詳細資訊，請參閱[物件查詢](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb896241(v=vs.100))。

```csharp
using System;
using System.Data.Objects;
using NorthwindModel;

class ObjectQuerySample
{
    public static void ExecuteQuery()
    {
        using (NorthwindEntities context = new NorthwindEntities())
        {
            ObjectQuery<Categories> categoryQuery = context.Categories;

            foreach (Categories category in
                categoryQuery.Execute(MergeOption.AppendOnly))
            {
                Console.WriteLine("\t{0}\t{1}",
                    category.CategoryID, category.CategoryName);
            }
        }
    }
}
```

```vb
Option Explicit On
Option Strict On

Imports System.Data.Objects
Imports NorthwindModel

Class ObjectQuerySample
    Public Shared Sub ExecuteQuery()
        Using context As NorthwindEntities = New NorthwindEntities()
            Dim categoryQuery As ObjectQuery(Of Categories) = context.Categories

            For Each category As Categories In _
                categoryQuery.Execute(MergeOption.AppendOnly)
                Console.WriteLine(vbTab & "{0}" & vbTab & "{1}", _
                    category.CategoryID, category.CategoryName)
            Next
        End Using
    End Sub
End Class
```

### <a name="entityclient"></a>EntityClient
這則範例中的程式碼會使用 <xref:System.Data.EntityClient.EntityCommand> 來執行 Entity SQL 查詢。 這個查詢會傳回代表 Categories 實體類型之執行個體 (Instance) 的記錄清單。 <xref:System.Data.EntityClient.EntityDataReader> 可用於存取結果集中的資料記錄。 如需詳細資訊，請參閱 [適用於 Entity Framework 的 EntityClient 提供者](./ef/entityclient-provider-for-the-entity-framework.md)。

```csharp
using System;
using System.Data;
using System.Data.Common;
using System.Data.EntityClient;
using NorthwindModel;

class EntityClientSample
{
    public static void ExecuteQuery()
    {
        string queryString =
            @"SELECT c.CategoryID, c.CategoryName
                FROM NorthwindEntities.Categories AS c";

        using (EntityConnection conn =
            new EntityConnection("name=NorthwindEntities"))
        {
            try
            {
                conn.Open();
                using (EntityCommand query = new EntityCommand(queryString, conn))
                {
                    using (DbDataReader rdr =
                        query.ExecuteReader(CommandBehavior.SequentialAccess))
                    {
                        while (rdr.Read())
                        {
                            Console.WriteLine("\t{0}\t{1}", rdr[0], rdr[1]);
                        }
                    }
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine(ex.Message);
            }
        }
    }
}
```

```vb
Option Explicit On
Option Strict On

Imports System.Data
Imports System.Data.Common
Imports System.Data.EntityClient
Imports NorthwindModel

Class EntityClientSample
    Public Shared Sub ExecuteQuery()
        Dim queryString As String = _
            "SELECT c.CategoryID, c.CategoryName " & _
                "FROM NorthwindEntities.Categories AS c"

        Using conn As EntityConnection = _
            New EntityConnection("name=NorthwindEntities")

            Try
                conn.Open()
                Using query As EntityCommand = _
                New EntityCommand(queryString, conn)
                    Using rdr As DbDataReader = _
                        query.ExecuteReader(CommandBehavior.SequentialAccess)
                        While rdr.Read()
                            Console.WriteLine(vbTab & "{0}" & vbTab & "{1}", _
                                              rdr(0), rdr(1))
                        End While
                    End Using
                End Using
            Catch ex As Exception
                Console.WriteLine(ex.Message)
            End Try
        End Using
    End Sub
End Class
```

## <a name="linq-to-sql"></a>LINQ to SQL
這則範例中的程式碼會使用 LINQ 查詢來傳回資料當做 Categories 物件，而這些物件會投影成僅包含 CategoryID 和 CategoryName 屬性的匿名型別。 這則範例是以 Northwind 資料內容為基礎。 有關詳細資訊，請參閱[入門](./sql/linq/getting-started.md)。

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Northwind;

    class LinqSqlSample
    {
        public static void ExecuteQuery()
        {
            using (NorthwindDataContext db = new NorthwindDataContext())
            {
                try
                {
                    var query = from category in db.Categories
                                select new
                                {
                                    categoryID = category.CategoryID,
                                    categoryName = category.CategoryName
                                };

                    foreach (var categoryInfo in query)
                    {
                        Console.WriteLine("vbTab {0} vbTab {1}",
                            categoryInfo.categoryID, categoryInfo.categoryName);
                    }
                }
                catch (Exception ex)
                {
                    Console.WriteLine(ex.Message);
                }
            }
        }
    }
```

```vb
Option Explicit On
Option Strict On

Imports System.Collections.Generic
Imports System.Linq
Imports System.Text
Imports Northwind

Class LinqSqlSample
    Public Shared Sub ExecuteQuery()
        Using db As NorthwindDataContext = New NorthwindDataContext()
            Try
                Dim query = From category In db.Categories _
                                Select New With _
                                { _
                                    .categoryID = category.CategoryID, _
                                    .categoryName = category.CategoryName _
                                }

                For Each categoryInfo In query
                    Console.WriteLine(vbTab & "{0}" & vbTab & "{1}", _
                            categoryInfo.categoryID, categoryInfo.categoryName)
                Next
            Catch ex As Exception
                Console.WriteLine(ex.Message)
            End Try
            End Using
    End Sub
End Class
```

## <a name="see-also"></a>另請參閱

- [ADO.NET 概觀](ado-net-overview.md) \(部分機器翻譯\)
- [在 ADO.NET 中擷取和修改資料](retrieving-and-modifying-data.md)
- [建立資料應用程式](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/h0y4a0f6(v=vs.120))
- [查詢 Entity Data Model (Entity Framework 工作)](https://docs.microsoft.com/previous-versions/bb738455(v=vs.90))
- [如何：執行可傳回匿名類型集合的查詢](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb738512(v=vs.100))
