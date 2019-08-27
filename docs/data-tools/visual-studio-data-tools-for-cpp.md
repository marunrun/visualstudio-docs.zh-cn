---
title: 适用于 data toolsC++
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CPP
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- data-storage
- cplusplus
ms.openlocfilehash: 5157f1d6a851e0784e79dfbfe5b94aef0490a026
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62565200"
---
# <a name="visual-studio-data-tools-for-c"></a>适用于 C++ 的 Visual Studio Data Tools

本机C++访问数据源时，通常可以提供最快的性能。 但是，数据工具，用于C++Visual Studio 中的应用程序不是因为它是.NET 应用程序的丰富。 例如，**数据源**不能使用窗口拖放到数据源C++设计图面。 如果您需要的对象关系层，将需要自己编写，或使用第三方产品。 同样适用于数据绑定功能，虽然使用 Microsoft 基础类库的应用程序可以使用一些数据库类中的，文档和视图，以及在内存中存储数据并将其显示给用户。 有关详细信息，请参阅[视觉对象中的数据访问C++ ](/cpp/data/data-access-in-cpp)。

若要连接到 SQL 数据库，本机C++应用程序可以使用 ODBC 和 OLE DB 驱动程序和 Windows 附带的 ADO 提供程序。 这些可以连接到支持这些接口的任何数据库。 ODBC 驱动程序是标准。 提供 OLE DB 是为了向后兼容。 这些数据技术的详细信息，请参阅[Windows 数据访问组件](/previous-versions/windows/desktop/ms692897(v=vs.85))。

若要利用 SQL Server 2005 中的自定义功能和更高版本，使用[SQL Server 本机客户端](/sql/relational-databases/native-client/sql-server-native-client)。 Native client 还包含 SQL Server ODBC 驱动程序和一个本机动态链接库 (DLL) 中的 SQL Server OLE DB 提供程序。 这些支持使用 Microsoft SQL server 的本机代码 Api （ODBC、 OLE DB 和 ADO） 的应用程序。 SQL Server Native Client 随同 SQL Server Data Tools 安装。 此处是编程指南：[SQL Server 本机客户端编程](/sql/relational-databases/native-client/sql-server-native-client-programming)。

## <a name="to-connect-to-localdb-through-odbc-and-sql-native-client-from-a-c-application"></a>若要连接到 localDB 通过 ODBC 和 SQL Native ClientC++应用程序

1. 安装 SQL Server Data Tools。

2. 如果你需要可连接到的示例 SQL 数据库，下载 Northwind 数据库，并将其解压缩到新位置。

3. 使用 SQL Server Management Studio 将附加已解压缩*Northwind.mdf*到 localDB 的文件。 当 SQL Server Management Studio 启动时，连接到 (localdb) \MSSQLLocalDB。

   ![SSMS 连接对话框](../data-tools/media/raddata-ssms-connect-dialog.png)

   在左窗格中，localdb 节点上右键单击，然后选择**附加**。

   ![SSMS 将数据库附加](../data-tools/media/raddata-ssms-attach-database.png)

4. 下载 ODBC Windows SDK 示例中，并将其解压缩到新位置。 此示例演示用于连接到数据库并发出查询和命令的基本 ODBC 命令。 您可以了解有关在这些函数的详细信息[Microsoft 开放式数据库连接 (ODBC)](/sql/odbc/microsoft-open-database-connectivity-odbc)。 首次加载解决方案 (在C++文件夹)，Visual Studio 将提供的用于升级到当前版本的 Visual Studio 的解决方案。 单击 **“是”**。

5. 若要使用的本机客户端，您需要其*标头*文件并*lib*文件。 这些文件包含函数和特定于 SQL Server，超出 sql.h 中定义的 ODBC 函数定义。 在中**项目** > **属性** > **VC + + 目录**，添加以下包含目录：

   **%ProgramFiles%\Microsoft SQL Server\110\SDK\Include**

   和此库目录：

   **%ProgramFiles%\Microsoft SQL Server\110\SDK\Lib**

6. 将这些行中的添加*odbcsql.cpp*。 #Define 会阻止从正在编译不相关的 OLE DB 定义。

   ```cpp
   #define _SQLNCLI_ODBC_
   #include <sqlncli.h>
   ```

    请注意，该示例不实际使用任何本机客户端功能，因此不需要为其进行编译和运行前面的步骤。 但项目现在已配置为你要使用此功能。 有关详细信息，请参阅 [SQL Server Native Client 编程](/sql/relational-databases/native-client/sql-server-native-client)。

7. 指定要使用 ODBC 子系统中的驱动程序。 该示例将作为命令行参数传递中的驱动程序连接字符串属性。 在中**项目** > **属性** > **调试**，添加此参数，命令：

   ```cpp
   DRIVER="SQL Server Native Client 11.0"
   ```

8. 按 F5 生成并运行该应用程序。 应看到一个对话框会提示你输入的数据库驱动程序中。 输入`(localdb)\MSSQLLocalDB`，并检查**使用信任连接**。 按“确定”。 应会看到具有消息，以表明成功的连接的控制台。 此外应该看到命令提示符下可以在其中键入 SQL 语句中。 以下屏幕显示的示例查询和结果：

   ![ODBC 示例查询输出](../data-tools/media/raddata-odbc-sample-query-output.png)

## <a name="see-also"></a>请参阅

- [在 Visual Studio 中访问数据](../data-tools/accessing-data-in-visual-studio.md)