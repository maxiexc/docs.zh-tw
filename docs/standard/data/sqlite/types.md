---
title: 資料類型
ms.date: 12/13/2019
description: 描述支援的資料類型，以及其周圍的一些限制。
ms.openlocfilehash: a11ff382f80cd979506d6195c299c8234c3eb8ea
ms.sourcegitcommit: c91110ef6ee3fedb591f3d628dc17739c4a7071e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/15/2020
ms.locfileid: "81389048"
---
# <a name="data-types"></a>資料類型

SQLite 僅有四種基本資料類型：整數、實數、文字及 BLOB。 傳回資料庫值做為的`object` api，只會傳回這四種類型的其中一種。 其他 .NET 類型受到 Microsoft 的支援，但值最終會在這些類型與四種基本類型的其中之一之間強制轉型。

| .NET           | SQLite  | 備註                                                       |
| -------------- | ------- | ------------------------------------------------------------- |
| Boolean        | INTEGER | `0` 或 `1`                                                    |
| Byte           | INTEGER |                                                               |
| Byte[]         | BLOB    |                                                               |
| Char           | TEXT    | UTF-8                                                         |
| Datetime       | TEXT    | yyyy-mm-dd HH： MM： ss。FFFFFFF                                   |
| DateTimeOffset | TEXT    | yyyy-mm-dd HH： MM： ss。Ss'.'fffffffzzz                                |
| Decimal        | TEXT    | `0.0###########################`編排. REAL 會有損及。 |
| Double         | real    |                                                               |
| Guid           | TEXT    | 00000000-0000-0000-0000-000000000000                          |
| Int16          | INTEGER |                                                               |
| Int32          | INTEGER |                                                               |
| Int64          | INTEGER |                                                               |
| SByte          | INTEGER |                                                               |
| Single         | real    |                                                               |
| String         | TEXT    | UTF-8                                                         |
| TimeSpan       | TEXT    | d. hh： mm： ss. fffffff                                            |
| UInt16         | INTEGER |                                                               |
| UInt32         | INTEGER |                                                               |
| UInt64         | INTEGER | 大數值溢位                                         |

## <a name="alternative-types"></a>替代類型

有些 .NET 類型可以從替代的 SQLite 類型讀取。 參數也可以設定為使用這些替代類型。 如需詳細資訊，請參閱[參數](parameters.md#alternative-types)。

| .NET           | SQLite  | 備註          |
| -------------- | ------- | ---------------- |
| Char           | INTEGER | UTF-16           |
| Datetime       | real    | Julian 日值 |
| DateTimeOffset | real    | Julian 日值 |
| Guid           | BLOB    |                  |
| TimeSpan       | real    | 以天為單位          |

例如，下列查詢會從結果集中的實際資料行讀取 TimeSpan 值。

[!code-csharp[](../../../../samples/snippets/standard/data/sqlite/DateAndTimeSample/Program.cs?name=snippet_AlternativeType)]

## <a name="column-types"></a>資料行類型

SQLite 使用動態型別系統，其中值的型別與值本身相關聯，而不是其儲存所在的資料行。 您可以隨意使用任何想要的資料行類型名稱。 然後，Sqlite 不會對這些名稱套用任何其他的語義。

資料行類型名稱會影響[類型親和性](https://www.sqlite.org/datatype3.html#type_affinity)。 其中一個常見的陷阱是，使用字串的資料行類型會嘗試將值轉換成整數或實數，這可能會導致非預期的結果。 我們建議您只使用四個基本 SQLite 類型名稱： INTEGER、REAL、TEXT 和 BLOB。

SQLite 可讓您指定類型 facet，例如長度、有效位數和小數位數，但不會由資料庫引擎強制執行。 您的應用程式會負責強制執行這些工作。

## <a name="see-also"></a>另請參閱

- [SQLite 中的資料類型](https://www.sqlite.org/datatype3.html)
