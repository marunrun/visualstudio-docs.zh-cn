---
title: 数据库项目和 DAC 项目
ms.date: 11/21/2018
ms.topic: conceptual
helpviewer_keywords:
- databases, managing change
ms.assetid: 40b51f5a-d52c-44ac-8f84-037a0917af33
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 2a86d9511e470c9a810ff58e80e4cae1f9a0cb11
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62567235"
---
# <a name="database-projects-and-data-tier-applications"></a>数据库项目和数据层应用程序

可以使用数据库项目来创建新数据库，新的数据层应用程序 (Dac)，以及更新现有数据库和数据层应用程序。 数据库项目和 DAC 项目，可以大致相同的方式将这些技术应用于托管或本机代码中将版本控制和项目管理技术应用于进行数据库开发工作。 可帮助开发团队创建 DAC 项目中，数据库项目或服务器项目并将其置于版本控制之下的管理对数据库和数据库服务器的更改。 然后，您的团队成员可以签出文件，以使、 生成和测试中隔离的开发环境或沙盒，做的更改，与团队共享它们之前。 若要帮助确保代码质量，你的团队可以完成并部署到生产环境的更改之前在过渡环境中测试的特定版本的数据库的所有更改。

有关支持的数据层应用程序的数据库功能的列表，请参阅[SQL Server 对象的 DAC 支持](/sql/relational-databases/data-tier-applications/dac-support-for-sql-server-objects-and-versions)。 如果您使用您的数据库不支持的数据层应用程序的功能，您应改用数据库项目来管理对你的数据库的更改。

## <a name="common-high-level-tasks"></a>常见的高级任务

| 高级任务 | 支持内容 |
| - | - |
| **启动数据层应用程序的开发：** 使用 SQL Server 2008 引入了数据层应用程序 (DAC) 的概念。 DAC 包含的 SQL Server 数据库和支持的客户端-服务器或第 3 层应用程序所使用的实例对象的定义。 DAC 包括数据库对象，如表和视图，以及实例实体，例如登录名。 可以使用 Visual Studio 创建一个 DAC 项目，生成一个 DAC 包文件，并将 DAC 包文件发送到 SQL Server 数据库引擎实例上部署的数据库管理员。 | - [数据层应用程序](/sql/relational-databases/data-tier-applications/data-tier-applications)<br />- [SQL Server Management Studio](/sql/ssms/sql-server-management-studio-ssms) |
| **执行迭代数据库开发：** 开发人员可以签出项目的部分，并在隔离的开发环境中更新它们。 通过使用此类型的环境，可以测试所做的更改，而不影响其他团队的成员。 所做的更改完成后，您将签入版本控制，其他团队成员可以获取所做的更改和生成并将其部署到测试服务器文件。 | - [面向项目的脱机数据库开发 (SQL Server Data Tools)](/sql/ssdt/project-oriented-offline-database-development)<br />- [TRANSACT-SQL 调试器 (SQL Server Management Studio)](/sql/ssms/scripting/transact-sql-debugger) |
| **原型制作，验证测试结果和修改数据库脚本和对象：** TRANSACT-SQL 编辑器可用于执行这些常见任务之一。 | - [查询和文本编辑器 (SQL Server Management Studio)](/sql/ssms/scripting/query-and-text-editors-sql-server-management-studio) |

## <a name="see-also"></a>请参阅

- [适用于 NET 的 Visual Studio Data Tools](../data-tools/visual-studio-data-tools-for-dotnet.md)