---
title: 错误： Transact-sql 执行在不调试的情况下结束 |Microsoft Docs
ms.date: 11/08/2018
ms.topic: troubleshooting
f1_keywords:
- vs.debug.error.sqlde_sql_executed_but_not_debugged
dev_langs:
- CSharp
- VB
- FSharp
- C++
- SQL
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 94ced2902becc2e988cde5198eff28911864dcbb
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72736935"
---
# <a name="error-transact-sql-execution-ended-without-debugging"></a>错误：Transact-SQL 执行未经调试便已结束

在你尝试调试 Transact-SQL 或 SQLCLR 过程，而调试器未收到来自 SQL Server 的调试消息时，就会出现此错误。

此问题可能是由于网络问题或 SQL Server 的问题引起的，但最可能的原因是权限问题。

这涉及到两种帐户：

- 应用程序帐户是 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 运行时所用的用户帐户。

- 连接帐户是用于建立到 SQL Server 的连接的标识。 此帐户与 Visual Studio 正在运行的标识不一定相同，因为连接正在使用 SQL 身份验证。

  SQL 调试要求应用程序帐户必须与连接帐户相匹配，或者必须是 sysadmin。

  如果使用类似于 sa 的 SQL 帐户名，则必须在 SQL Server 上将应用程序帐户设置为 sysadmin。 默认情况下，运行 SQL server 的计算机上的管理员是 SQL Server sysadmin。

  若要纠正此错误，可能需要：

  - 验证权限设置。 有关详细信息，请参阅[如何：设置用于调试的 SQL Server 权限](https://msdn.microsoft.com/84e088d0-0409-41d4-841b-f5d4b0fda414)。

  - 如果设置正确，请确保 SQL 调试也正确。

  - 请咨询网络或数据库管理员。

## <a name="see-also"></a>请参阅

- [设置 SQL 调试](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/s4sszxst(v=vs.100))
- [如何：设置用于调试的 SQL Server 权限](https://msdn.microsoft.com/84e088d0-0409-41d4-841b-f5d4b0fda414)
- [调试器设置和准备](../debugger/debugger-settings-and-preparation.md)
- [Remote Debugging](../debugger/remote-debugging.md)