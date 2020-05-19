---
title: 准备调试 Windows 服务 | Microsoft Docs
ms.custom: seodec18
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging [Visual Studio], Windows services
- Windows Service applications, debugging
ms.assetid: ac0a99f7-ec3d-4a20-b17f-698a817fdcc2
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3161f6d2c328e8e33dd82ed206aa8aa20e654cc9
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72738079"
---
# <a name="debugging-preparation-windows-services"></a>调试准备：Windows 服务
Windows 服务是一种在 Microsoft Windows 的后台中运行的程序。 Telnet 服务和 Windows 时间服务（它更新计算机的可见时钟）都属于 Windows 服务。 Windows 服务不能从 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 内部运行；它必须在服务控制管理器的上下文中运行。 有关详细信息，请参阅[创建 Windows 服务](/dotnet/framework/windows-services/how-to-create-windows-services)、[调试 Windows 服务应用程序](/dotnet/framework/windows-services/how-to-debug-windows-service-applications)和 [Windows 服务应用程序](/dotnet/framework/windows-services/index)。

## <a name="see-also"></a>请参阅
- [调试托管代码](../debugger/debugging-managed-code.md)
- [C#, F#, and Visual Basic Project Types](../debugger/debugging-preparation-csharp-f-hash-and-visual-basic-project-types.md)（C#、F# 和 Visual Basic 项目类型）
- [C# 调试配置的项目设置](../debugger/project-settings-for-csharp-debug-configurations.md)
- [Visual Basic 调试配置的项目设置](../debugger/project-settings-for-a-visual-basic-debug-configuration.md)
- [如何：调试 OnStart 方法](../debugger/how-to-debug-the-onstart-method.md)