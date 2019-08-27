---
title: 调试准备：Windows 服务 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
- VB
- CSharp
helpviewer_keywords:
- debugging [Visual Studio], Windows services
- Windows Service applications, debugging
ms.assetid: ac0a99f7-ec3d-4a20-b17f-698a817fdcc2
caps.latest.revision: 23
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 2e68792b62e3e5538476063b5298579ecc58e4db
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65691307"
---
# <a name="debugging-preparation-windows-services"></a>调试准备：Windows 服务
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Windows 服务是一种在 Microsoft Windows 的后台中运行的程序。 Telnet 服务和 Windows 时间服务（它更新计算机的可见时钟）都属于 Windows 服务。 Windows 服务不能从 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 内部运行；它必须在服务控制管理器的上下文中运行。 有关详细信息，请参阅[创建 Windows 服务](https://msdn.microsoft.com/library/0f5e2cbb-d95d-477c-b2b5-4b990e6b86ff)、[调试 Windows 服务应用程序](https://msdn.microsoft.com/library/63ab0800-0f05-4f1e-88e6-94c73fd920a2)和 [Windows 服务应用程序](https://msdn.microsoft.com/library/ba72d648-9553-4849-b829-069ad5ea014b)。  
  
## <a name="see-also"></a>请参阅  
 [调试托管代码](../debugger/debugging-managed-code.md)   
 [C#、F#、和 Visual Basic 项目类型](../debugger/debugging-preparation-csharp-f-hash-and-visual-basic-project-types.md)   
 [C# 调试配置的项目设置](../debugger/project-settings-for-csharp-debug-configurations.md)   
 [Visual Basic 调试配置的项目设置](../debugger/project-settings-for-a-visual-basic-debug-configuration.md)   
 [如何：调试 OnStart 方法](../debugger/how-to-debug-the-onstart-method.md)
