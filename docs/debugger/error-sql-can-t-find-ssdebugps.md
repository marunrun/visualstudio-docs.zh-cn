---
title: 错误 - SQL 找不到 SSDEBUGPS | Microsoft Docs
ms.date: 11/04/2016
ms.topic: error-reference
f1_keywords:
- vs.debug.error.sqlde_cant_find_ssdebugps
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
ms.openlocfilehash: 59a1a603aa44ceed46c160443508080072046e35
ms.sourcegitcommit: de98ed7edc81383e47b87ae6e61143fbbbe7bc56
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2020
ms.locfileid: "88706472"
---
# <a name="error-sql-can39t-find-ssdebugps"></a>错误：SQL 找不到 SSDEBUGPS

SSDEBUGPS.dll 为 SQL Server Debugging Host 组件。

此错误在尝试开始调试时发生，指示指定的文件在 [!INCLUDE[sqprsqlong](../debugger/includes/sqprsqlong_md.md)] 计算机上不存在。 可能的原因是从未运行远程调试安装，或是由于某种原因删除了此文件。

有两种方法可以纠正此错误：重新运行远程调试安装，以及将该文件复制到 [!INCLUDE[sqprsqlong](../debugger/includes/sqprsqlong_md.md)] 计算机上。

若要重新运行远程调试安装程序，请按照[远程调试](../debugger/remote-debugging.md)中的说明操作。

如果可以找到 ssdebugps.dll 的某个副本，则可以将其复制到 [!INCLUDE[sqprsqlong](../debugger/includes/sqprsqlong_md.md)] 计算机上。 如果存在，该文件会位于目录 \Program Files\ Common Files\Microsoft Shared\SQL Debugging 中。 在另一台 [!INCLUDE[sqprsqlong](../debugger/includes/sqprsqlong_md.md)] 计算机或安装了 Visual Studio 2005 的计算机上可以找到该文件。

将 SSDEBUGPS.dll 复制到 SQL Server 2005 计算机上：

1. 将该文件复制到 [!INCLUDE[sqprsqlong](../debugger/includes/sqprsqlong_md.md)] 计算机上具有相同名称和路径的目录中。

2. 通过打开“命令提示符”并运行下面的命令来注册该文件：

    ```cmd
    regsvr32 ssdebugps.dll
    ```
