---
title: 数据库项目和 DAC 项目
ms.date: 11/21/2018
ms.topic: conceptual
helpviewer_keywords:
- databases, managing change
ms.assetid: 40b51f5a-d52c-44ac-8f84-037a0917af33
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: cc8d32ddcc332264278cf76392ac69a6188ca51c
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75586726"
---
# <a name="database-projects-and-data-tier-applications"></a>数据库项目和数据层应用程序

您可以使用数据库项目创建新的数据库、新的数据层应用程序（Dac）以及更新现有的数据库和数据层应用程序。 使用数据库项目和 DAC 项目，您可以将版本控制和项目管理技术应用于您的数据库开发工作，就像将这些技术应用于托管代码或本机代码一样。 您可以通过创建 DAC 项目、数据库项目或服务器项目并将其置于版本控制下，帮助您的开发团队管理对数据库和数据库服务器所做的更改。 然后，你的团队成员可以在将其与团队共享之前，先签出文件，以便在隔离开发环境或沙盒中生成和测试更改。 为了帮助确保代码质量，你的团队可以在将更改部署到生产环境之前，在过渡环境中完成并测试该数据库的特定版本的所有更改。

有关数据层应用程序支持的数据库功能的列表，请参阅[DAC 对 SQL Server 对象的支持](/sql/relational-databases/data-tier-applications/dac-support-for-sql-server-objects-and-versions)。 如果你在数据库中使用数据层应用程序不支持的功能，则应改为使用数据库项目来管理对数据库的更改。

## <a name="common-high-level-tasks"></a>常见的高级任务

| 高级任务 | 支持内容 |
| - | - |
| **开始开发数据层应用程序：** SQL Server 2008 引入了数据层应用程序（DAC）的概念。 DAC 包含由客户端-服务器或3层应用程序使用的 SQL Server 数据库和支持实例对象的定义。 DAC 包括数据库对象（如表和视图）以及实例实体（例如登录名）。 您可以使用 Visual Studio 创建一个 DAC 项目，生成一个 DAC 包文件，然后将该 DAC 包文件发送到数据库管理员，以便部署到 SQL Server 数据库引擎的实例上。 | - [数据层应用程序](/sql/relational-databases/data-tier-applications/data-tier-applications)<br />- [SQL Server Management Studio](/sql/ssms/sql-server-management-studio-ssms) |
| **执行迭代数据库开发：** 开发人员可以查看项目的各个部分，并在独立的开发环境中对其进行更新。 通过使用这种类型的环境，您可以测试您的更改，而不会影响团队的其他成员。 更改完成后，可将文件签回版本控制中，其他团队成员可在其中获取所做的更改并将其生成并部署到测试服务器。 | [面向项目的脱机数据库开发 - （SQL Server Data Tools）](/sql/ssdt/project-oriented-offline-database-development)<br />- [transact-sql 调试器（SQL Server Management Studio）](/sql/ssms/scripting/transact-sql-debugger) |
| **原型制作，验证测试结果，修改数据库脚本和对象：** 您可以使用 Transact-sql 编辑器执行其中的一项常见任务。 | - [查询和文本编辑器（SQL Server Management Studio）](/sql/ssms/scripting/query-and-text-editors-sql-server-management-studio) |

## <a name="see-also"></a>另请参阅

- [适用于 NET 的 Visual Studio Data Tools](../data-tools/visual-studio-data-tools-for-dotnet.md)
