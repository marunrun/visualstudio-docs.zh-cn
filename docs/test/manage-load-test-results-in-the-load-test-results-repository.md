---
title: 管理负载测试结果
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- load tests, results repository
- results, load test
- load test results, repository
- Load Test Results Repository
ms.assetid: 1cd63c4b-4f74-4133-b675-5e8fbeab25f3
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 37dfd7b0aa8aed1ce94f3d4364c5b61a0957a223
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68926626"
---
# <a name="manage-load-test-results-in-the-load-test-results-repository"></a>管理“负载测试结果存储库”中的负载测试结果

运行负载测试时，在运行负载测试期间收集的任何信息都存储到负载测试结果存储库中，这是一个 SQL 数据库  。 负载测试结果储存库包含性能计数器数据和有关已记录错误的任何信息。 “结果储存库”数据库在安装控制器时创建，或者首次在本地运行负载测试时自动创建。 对于本地运行，如果没有负载测试架构，则将自动创建该数据库。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

如果修改控制器的结果储存库连接字符串以使用其他服务器，则新服务器必须运行 loadtestresultsrepository.sql 脚本才能创建该架构  。

Visual Studio Enterprise 提供命名的计数器集，用于基于某种技术来收集通用性能计数器。 在分析 IIS 服务器、ASP.NET 服务器或 SQL Server 时可使用这些计数器集。 计数器集收集的所有数据都存储在负载测试结果储存库中。

> [!IMPORTANT]
> 计数器集和性能计数器数据之间有所不同。 计数器集是元数据。 它定义应从执行特定角色（如 IIS 或 SQL Server）的计算机上收集的一组性能计数器。 计数器集是负载测试定义的一部分。 性能计数器数据是根据计数器集、计数器集到特定计算机的映射以及采样速率收集的数据。

## <a name="sql-server-versions"></a>SQL Server 版本

若要使用负载测试，可以使用随 Visual Studio 一起安装的 SQL Server Express LocalDB。 它是负载测试（包括 Microsoft Excel 集成）的默认数据库服务器。 SQL Server Express LocalDB 是面向程序开发人员的 SQL Server Express 执行模式。 SQL Server Express LocalDB 安装复制了启动 SQL Server 数据库引擎所需的最少文件。

如果团队有大量数据库需求，或项目过大而不适用于 SQL Server Express LocalDB，应考虑升级到 SQL Express 或完整的 SQL Server，以提供进一步的缩放潜能。 如果升级 SQL Server，则 SQL Server Express LocalDB 的 MDF 和 LDF 文件将存储在用户配置文件文件夹中。 可使用这些文件将负载测试数据库导入到 SQL Server Express 或 SQL Server 。

## <a name="load-test-results-store-considerations"></a>负载测试结果存储区注意事项

安装了 Visual Studio Enterprise 后，将设置负载测试结果存储区以使用安装在计算机上的 SQL Express 的实例。 SQL Express 限制为使用最大 4 GB 磁盘空间。 如果要在较长时间内运行许多负载测试，则应该考虑配置负载测试结果存储区以使用完整 SQL Server 产品的实例（如果可用）。

## <a name="load-test-analyzer-tasks"></a>负载测试分析器任务

|任务|关联主题|
|-|-----------------------|
|**设置负载测试结果存储库：** 可在 SQL 数据库中设置负载测试结果存储库。 **注意：** 在安装测试控制器时也可创建负载测试储存库。 有关详细信息，请参阅[安装和配置测试代理](../test/lab-management/install-configure-test-agents.md)。||
|**选择和查看结果存储库：** 可以选择特定结果储存库。 并不局限于使用本地结果存储区。 通常，负载测试是在一组远程代理计算机上运行。 代理或本地计算机生成的测试结果可保存到任何已创建负载测试结果存储区的 SQL 服务器中。 在这两种情况下，都必须使用“管理测试控制器”窗口标识负载测试结果的存储区  。|-   [如何：选择负载测试结果存储库](../test/how-to-select-a-load-test-results-repository.md)<br />-   [如何：访问负载测试结果进行分析](../test/how-to-access-load-test-results-for-analysis.md)|
|**从存储库中删除负载测试结果：** 可以使用“打开和管理负载测试结果”对话框，从“负载测试编辑器”中删除负载测试结果   。|-   [如何：从存储库删除负载测试结果](../test/how-to-delete-load-test-results-from-a-repository.md)|
|**将结果导入及导出储存库：** 可在“负载测试编辑器”中导入和导出负载测试结果  。|-   [如何：将负载测试结果导入存储库中](../test/how-to-import-load-test-results-into-a-repository.md)<br />-   [如何：从存储库导出负载测试结果](../test/how-to-export-load-test-results-from-a-repository.md)|

## <a name="related-tasks"></a>相关任务

[分析负载测试结果](../test/analyze-load-test-results-using-the-load-test-analyzer.md)

可以使用负载测试分析器查看正在运行的负载测试和已完成的负载测试的结果  。

## <a name="see-also"></a>请参阅

- [分析负载测试结果](../test/analyze-load-test-results-using-the-load-test-analyzer.md)
- [如何：访问负载测试结果进行分析](../test/how-to-access-load-test-results-for-analysis.md)