---
title: 错误 - 用户无法执行存储过程 sp_enable_sql_debug | Microsoft Docs
ms.date: 11/04/2016
ms.topic: error-reference
dev_langs:
- CSharp
- VB
- FSharp
- C++
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 84326c5c1beb91269a5f097c8c5d7cb8782a7a56
ms.sourcegitcommit: ed4372bb6f4ae64f1fd712b2b253bf91d9ff96bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/09/2020
ms.locfileid: "89600149"
---
# <a name="error-user-could-not-execute-stored-procedure-sp_enable_sql_debug"></a>错误：用户无法执行存储过程 sp_enable_sql_debug

在服务器上未能执行存储过程 sp_enable_sql_debug。 这可能是由于：

- 连接问题。 需要有一个到服务器的稳定连接。

- 在服务器上缺少必要的权限。 若要在 SQL Server 2005 上调试，运行 Visual Studio 的帐户和用于连接 SQL Server 的帐户都必须是 sysadmin 角色的成员。 用于连接 SQL Server 的帐户要么是 Windows 用户帐户（如果您正在使用 Windows 身份验证），要么是具有用户 ID 和密码的帐户（如果您使用 SQL 身份验证）。

有关详细信息，请参阅[如何：设置 SQL Server 调试权限](/previous-versions/w1bhybwz(v=vs.100))。

## <a name="see-also"></a>请参阅

- [如何：设置 SQL Server 调试权限](/previous-versions/w1bhybwz(v=vs.100))
- [设置 SQL 调试](/previous-versions/visualstudio/visual-studio-2010/s4sszxst\(v\=vs.100\))