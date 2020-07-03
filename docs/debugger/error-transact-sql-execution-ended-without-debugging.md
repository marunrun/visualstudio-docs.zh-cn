---
title: 错误 - Transact-SQL 执行未经调试便已结束 | Microsoft Docs
ms.date: 11/08/2018
ms.topic: error-reference
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
ms.openlocfilehash: e141fac7fba1939811c722d8e08f49531111ff7e
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2020
ms.locfileid: "85460242"
---
# <a name="error-transact-sql-execution-ended-without-debugging"></a>错误：Transact-SQL 执行未经调试便已结束

在你尝试调试 Transact-SQL 或 SQLCLR 过程，而调试器未收到来自 SQL Server 的调试消息时，就会出现此错误。

此问题可能是由网络问题或 SQL Server 上的问题造成的，但是可能性最大的原因是权限问题。

这涉及到两种帐户：

- 应用程序帐户是 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 运行时所用的用户帐户。

- 连接帐户是用于建立到 SQL Server 的连接的标识。 此帐户不一定是该连接使用 SQL 身份验证时 Visual Studio 运行所使用的标识。

  SQL 调试要求应用程序帐户必须与连接帐户匹配，或者必须是 sysadmin。

  如果使用的是 sa 之类的 SQL 帐户名，则必须在 SQL Server 上将该应用程序帐户设置为 sysadmin。 默认情况下，运行 SQL Server 的计算机上的管理员是 SQL Server sysadmin。

  若要纠正此错误，可能需要：

  - 验证权限设置。 有关详细信息，请参阅[如何：设置 SQL Server 调试权限](https://msdn.microsoft.com/84e088d0-0409-41d4-841b-f5d4b0fda414)。

  - 如果设置正确，请确保 SQL 调试也正确。

  - 请咨询网络或数据库管理员。

## <a name="see-also"></a>请参阅

- [设置 SQL 调试](/previous-versions/visualstudio/visual-studio-2010/s4sszxst(v=vs.100))
- [如何：设置 SQL Server 调试权限](https://msdn.microsoft.com/84e088d0-0409-41d4-841b-f5d4b0fda414)
- [调试器设置和准备](../debugger/debugger-settings-and-preparation.md)
- [远程调试](../debugger/remote-debugging.md)