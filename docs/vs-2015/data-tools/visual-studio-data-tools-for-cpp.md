---
title: 适用于 | 的C++ Visual Studio data toolsMicrosoft Docs
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.date: 11/15/2016
ms.topic: conceptual
ms.assetid: 3a3849d9-1bc7-47d1-805e-1755223ccba2
caps.latest.revision: 12
author: jillre
ms.author: jillfra
manager: jillfra
robots: noindex,nofollow
ms.openlocfilehash: ec68d54ced85737d66c64ca2dbf7942ca81e5314
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72621212"
---
# <a name="visual-studio-data-tools-for-c"></a>适用于 C++ 的 Visual Studio Data Tools
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在C++访问数据源时，Native 通常可以提供最快的性能。 但是，Visual Studio 中C++适用于应用程序的数据工具不像 .net 应用程序一样丰富。 例如，"数据源" 窗口不能用于将数据源拖放到C++设计图面上。 如果需要对象关系层，则必须编写自己的或使用第三方产品。  对于数据绑定功能也是如此，但使用 Microsoft 基础类库的应用程序可以将数据存储在内存中，并将其显示给用户。 有关详细信息，请参阅[Visual C++中的数据访问](https://msdn.microsoft.com/library/7wtdsdkh.aspx)。

 若要连接到 SQL 数据库， C++本机应用程序可以使用 ODBC 和 OLE DB 驱动程序以及 Windows 附带的 ADO 提供程序。     它们可以连接到支持这些接口的任何数据库。 ODBC 驱动程序是标准的。 提供 OLE DB 是为了向后兼容。 有关这些数据技术的详细信息，请参阅[Windows 数据访问组件](https://msdn.microsoft.com/library/windows/desktop/aa968814\(v=vs.85\).aspx)

 若要利用 SQL Server 2005 及更高版本中的自定义功能，请使用[SQL Server Native Client](https://msdn.microsoft.com/sqlserver/aa937733)。 Native client 还在一个本机动态链接库（DLL）中包含 SQL Server ODBC 驱动程序和 SQL Server OLE DB 提供程序。 它们支持使用本机代码 Api （ODBC、OLE DB 和 ADO） Microsoft SQL Server 的应用程序。  SQL Server Native Client 安装 SQL Server Data Tools。 编程指南如下： [SQL Server Native Client 编程](https://msdn.microsoft.com/library/ms130892.aspx)。

## <a name="to-connect-to-localdb-through-odbc-and-sql-native-client-from-a-c-application"></a>通过 ODBC 连接到 localDB，并从C++应用程序 SQL Native Client

1. 安装 SQL Server Data Tools。

2. 如果需要连接到的 SQL 数据库示例，请下载 Northwind 数据库，并将其解压缩到新位置。

3. 使用 SQL Server Management Studio 将解压缩的 Northwind .mdf 文件附加到 localDB。 SQL Server Management Studio 启动时，连接到（localdb） \MSSQLLocalDB。

    ![SSMS 连接对话框](../data-tools/media/raddata-ssms-connect-dialog.png "raddata SSMS connect 对话框")

    然后，在左窗格中右键单击 localdb 节点，然后选择 "**附加**"。

    ![SSMS 附加数据库](../data-tools/media/raddata-ssms-attach-database.png "raddata SSMS 附加数据库")

4. 下载 ODBC Windows SDK 示例，并将其解压缩到新位置。 此示例显示了用于连接到数据库和发出查询和命令的基本 ODBC 命令。 可以在[Microsoft 开放式数据库连接（ODBC）](https://msdn.microsoft.com/library/windows/desktop/ms710252\(v=vs.85\).aspx)中了解有关这些函数的详细信息。 首次加载解决方案（它位于C++文件夹中）时，visual studio 会将解决方案升级到当前版本的 Visual studio。 单击“是”。

5. 若要使用 native client，需要其头文件和 lib 文件。 这些文件包含特定于 SQL Server 的函数和定义，但在 SQL .h 中定义的 ODBC 函数之外。 在 "**项目** > **属性**"  >  "**VC + + 目录**" 中，添加以下包含目录：

   **\<system 驱动器 >： \Program FILES\MICROSOFT SQL Server\110\SDK\Include**    此库目录：

   **c:\Program Files\Microsoft SQL Server\110\SDK\Lib**

6. 将这些行添加到 odbcsql 中。 #Define 防止编译无关的 OLE DB 定义。

   ```
   #define _SQLNCLI_ODBC_
   #include <sqlncli.h>
   ```

    请注意，该示例不会实际使用任何本机客户端功能，因此，编译和运行上述步骤并不是必需的。 但现在已将该项目配置为使用此功能。 有关详细信息，请参阅[SQL Server Native Client 编程](https://msdn.microsoft.com/library/ms130892\(v=sql.130\).aspx)。

7. 指定要在 ODBC 子系统中使用的驱动程序。 此示例在中将驱动程序连接字符串特性传递为命令行参数。 在 "**项目** > **属性**"  > **调试**中，添加以下命令参数：

   ```
   DRIVER="SQL Server Native Client 11.0"
   ```

8. 按 F5 生成并运行该应用程序。 你应看到一个对话框，提示你输入数据库。 输入 `(localdb)\MSSQLLocalDB`，并选中 "**使用可信连接**"。 按“确定”。 应该会看到一个控制台，其中包含表明连接成功的消息。 还应会看到命令提示符，可在其中键入 SQL 语句。 以下屏幕显示了一个示例查询和结果：

    ![ODBC 示例查询输出](../data-tools/media/raddata-odbc-sample-query-output.png "raddata ODBC 示例查询输出")

## <a name="see-also"></a>请参阅
 [在 Visual Studio 中访问数据](../data-tools/accessing-data-in-visual-studio.md)
