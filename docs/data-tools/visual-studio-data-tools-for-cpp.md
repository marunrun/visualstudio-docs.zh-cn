---
title: 用于 c + + 的数据工具
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
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/23/2020
ms.locfileid: "85281092"
---
# <a name="visual-studio-data-tools-for-c"></a>适用于 C++ 的 Visual Studio Data Tools

访问数据源时，本机 c + + 通常可以提供最快的性能。 但是，Visual Studio 中 c + + 应用程序的数据工具不像 .NET 应用程序的那样丰富。 例如，"**数据源**" 窗口不能用于将数据源拖放到 c + + 设计图面上。 如果需要对象关系层，则必须编写自己的或使用第三方产品。 对于数据绑定功能也是如此，但使用 Microsoft 基础类库的应用程序可以将数据存储在内存中，并将其显示给用户。 有关详细信息，请参阅[Visual C++ 中的数据访问](/cpp/data/data-access-in-cpp)。

若要连接到 SQL 数据库，本机 c + + 应用程序可以使用 ODBC 和 OLE DB 驱动程序以及 Windows 附带的 ADO 提供程序。 它们可以连接到支持这些接口的任何数据库。 ODBC 驱动程序是标准的。 提供 OLE DB 是为了向后兼容。 有关这些数据技术的详细信息，请参阅[Windows 数据访问组件](/previous-versions/windows/desktop/ms692897(v=vs.85))。

若要利用 SQL Server 2005 及更高版本中的自定义功能，请使用[SQL Server native client](/sql/relational-databases/native-client/sql-server-native-client)。 Native client 还在一个本机动态链接库（DLL）中包含 SQL Server ODBC 驱动程序和 SQL Server OLE DB 提供程序。 它们支持使用本机代码 Api （ODBC、OLE DB 和 ADO） Microsoft SQL Server 的应用程序。 SQL Server Native Client 安装 SQL Server Data Tools。 下面是编程指南： [SQL Server native client 编程](/sql/relational-databases/native-client/sql-server-native-client-programming)。

## <a name="to-connect-to-localdb-through-odbc-and-sql-native-client-from-a-c-application"></a>通过 ODBC 连接到 localDB，并从 c + + 应用程序 SQL Native Client

1. 安装 SQL Server Data Tools。

2. 如果需要连接到的 SQL 数据库示例，请下载 Northwind 数据库，并将其解压缩到新位置。

3. 使用 SQL Server Management Studio 将解压缩的*Northwind .mdf*文件附加到 localDB。 SQL Server Management Studio 启动时，连接到（localdb） \MSSQLLocalDB。

   ![SSMS 连接对话框](../data-tools/media/raddata-ssms-connect-dialog.png)

   然后，在左窗格中右键单击 localdb 节点，然后选择 "**附加**"。

   ![SSMS 附加数据库](../data-tools/media/raddata-ssms-attach-database.png)

4. 下载 ODBC Windows SDK 示例，并将其解压缩到新位置。 此示例显示了用于连接到数据库和发出查询和命令的基本 ODBC 命令。 可以在[Microsoft 开放式数据库连接（ODBC）](/sql/odbc/microsoft-open-database-connectivity-odbc)中了解有关这些函数的详细信息。 首次加载解决方案（它位于 c + + 文件夹中）时，Visual Studio 会将解决方案升级到当前版本的 Visual Studio。 单击 **“是”** 。

5. 若要使用 native client，需要其*头*文件和*lib*文件。 这些文件包含特定于 SQL Server 的函数和定义，但在 SQL .h 中定义的 ODBC 函数之外。 在**项目**  >  **属性**  >  "**VC + + 目录**" 中，添加以下包含目录：

   **%ProgramFiles%\Microsoft SQL Server\110\SDK\Include**

   此库目录：

   **%ProgramFiles%\Microsoft SQL Server\110\SDK\Lib**

6. 将这些行添加到*odbcsql*中。 #Define 防止编译无关的 OLE DB 定义。

   ```cpp
   #define _SQLNCLI_ODBC_
   #include <sqlncli.h>
   ```

    请注意，该示例不会实际使用任何本机客户端功能，因此，编译和运行上述步骤并不是必需的。 但现在已将该项目配置为使用此功能。 有关详细信息，请参阅[SQL Server Native Client 编程](/sql/relational-databases/native-client/sql-server-native-client)。

7. 指定要在 ODBC 子系统中使用的驱动程序。 此示例在中将驱动程序连接字符串特性传递为命令行参数。 在**项目**  >  **属性**  >  **调试**中，添加以下命令参数：

   ```cpp
   DRIVER="SQL Server Native Client 11.0"
   ```

8. 按**F5**生成并运行应用程序。 你应看到一个对话框，提示你输入数据库。 输入 `(localdb)\MSSQLLocalDB` ，并选中 "**使用可信连接**"。 按“确定”。 应该会看到一个控制台，其中包含表明连接成功的消息。 还应会看到命令提示符，可在其中键入 SQL 语句。 以下屏幕显示了一个示例查询和结果：

   ![ODBC 示例查询输出](../data-tools/media/raddata-odbc-sample-query-output.png)

## <a name="see-also"></a>请参阅

- [在 Visual Studio 中访问数据](../data-tools/accessing-data-in-visual-studio.md)
