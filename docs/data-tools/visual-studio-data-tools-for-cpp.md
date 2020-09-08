---
title: 适用于 C++ 的数据工具
ms.date: 11/04/2016
ms.topic: overview
dev_langs:
- CPP
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
- cplusplus
ms.openlocfilehash: 063efeebff92698b8e5db66880360713c73fe150
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "85281092"
---
# <a name="visual-studio-data-tools-for-c"></a>适用于 C++ 的 Visual Studio Data Tools

在你访问数据源时，本地 C++ 通常可以提供最快的性能。 Visual Studio 中适用于 C++ 应用程序的数据工具并不像适用于.NET 应用程序的工具那样丰富。 例如，不能使用“数据源”窗口将数据源拖放到 C++ 设计图面。 如果需要对象关系层，则必须编写自己的关系层或使用第三方产品。 数据绑定功能也是如此，尽管使用 Microsoft 基础类库的应用程序可以使用一些数据库类以及文档和视图将数据存储在内存中并向用户显示。 有关详细信息，请参阅 [Visual C++ 中的数据访问](/cpp/data/data-access-in-cpp)。

若要连接到 SQL 数据库，本机 C++ 应用程序可以使用 ODBC 和 OLE DB 驱动程序以及 Windows 附带的 ADO 提供程序。 它们可以连接到支持这些接口的任何数据库。 ODBC 驱动程序是标准驱动程序。 提供 OLE DB 是为了向后兼容。 有关这些数据技术的详细信息，请参阅 [Windows 数据访问组件](/previous-versions/windows/desktop/ms692897(v=vs.85))。

若要利用 SQL Server 2005 及更高版本中的自定义功能，请使用 [SQL Server Native Client](/sql/relational-databases/native-client/sql-server-native-client)。 Native Client 还在一个本机动态链接库 (DLL) 中包含 SQL Server ODBC 驱动程序和 SQL Server OLE DB 提供程序。 它们支持使用本机代码 API（ODBC、OLE DB 和 ADO）连接到 Microsoft SQL Server 的应用程序。 SQL Server Native Client 随 SQL Server Data Tools 一起安装。 下面是编程指南：[SQL Server Native Client 编程](/sql/relational-databases/native-client/sql-server-native-client-programming)。

## <a name="to-connect-to-localdb-through-odbc-and-sql-native-client-from-a-c-application"></a>通过 ODBC 和 SQL Native Client 从 C++ 应用程序连接到 localDB

1. 安装 SQL Server Data Tools。

2. 如果需要要连接到的示例 SQL 数据库，请下载 Northwind 数据库，并将其解压缩到新位置。

3. 使用 SQL Server Management Studio 将解压缩的 Northwind.mdf 文件附加到 localDB。 SQL Server Management Studio 启动时，请连接到 (localdb)\MSSQLLocalDB。

   ![SSMS 连接对话框](../data-tools/media/raddata-ssms-connect-dialog.png)

   然后在左窗格中右键单击 localdb 节点，然后选择“附加”。

   ![SSMS 附加数据库](../data-tools/media/raddata-ssms-attach-database.png)

4. 下载 ODBC Windows SDK 示例，并将其解压缩到新位置。 此示例显示用于连接到数据库并发出查询和命令的基本 ODBC 命令。 可通过 [Microsoft 开放式数据库连接 (ODBC)](/sql/odbc/microsoft-open-database-connectivity-odbc) 了解有关这些功能的详细信息。 首次加载解决方案时（位于 C++ 文件夹中），可通过 Visual Studio 将解决方案升级到 Visual Studio 的当前版本。 单击 **“是”** 。

5. 若要使用本机客户端，需要其头文件和库文件 。 除了 sql.h 中定义的 ODBC 函数外，这些文件还包含特定于 SQL Server 的函数和定义。 在“项目” > 属性” > “VC++ 目录”中，添加以下包含目录  ：

   **%ProgramFiles%\Microsoft SQL Server\110\SDK\Include**

   以及此库目录：

   **%ProgramFiles%\Microsoft SQL Server\110\SDK\Lib**

6. 在 odbcsql.cpp 中添加这些行。 #define 可防止编译无关的 OLE DB 定义。

   ```cpp
   #define _SQLNCLI_ODBC_
   #include <sqlncli.h>
   ```

    请注意，该示例实际上并未使用任何本机客户端功能，因此，无需执行上述步骤即可进行编译和运行。 但现在已将该项目配置为使用此功能。 有关详细信息，请参阅 [SQL Server Native Client 编程](/sql/relational-databases/native-client/sql-server-native-client)。

7. 指定要在 ODBC 子系统中使用的驱动程序。 此示例将驱动程序连接字符串属性作为命令行参数传入。 在“项目” > 属性” > 调试”中，添加以下命令参数  ：

   ```cpp
   DRIVER="SQL Server Native Client 11.0"
   ```

8. 按 F5 生成并运行应用程序。 驱动程序中会显示一个对话框，提示你输入数据库。 请输入 `(localdb)\MSSQLLocalDB`，并选中“使用信任连接”。 按“确定”。 应会看到一个控制台，其中包含指示连接成功的消息。 还应会看到一个命令提示符，可在其中键入 SQL 语句。 以下屏幕显示了一个示例查询和结果：

   ![ODBC 示例查询输出](../data-tools/media/raddata-odbc-sample-query-output.png)

## <a name="see-also"></a>请参阅

- [在 Visual Studio 中访问数据](../data-tools/accessing-data-in-visual-studio.md)
