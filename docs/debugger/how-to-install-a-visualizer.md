---
title: 如何：安装可视化工具 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- debugger, visualizers
- visualizers, installing
ms.assetid: 3310ef43-515c-4d97-b0f9-51047247d3da
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1df72c6978f5ab34a86c74dbc1ea349db5aa4457
ms.sourcegitcommit: b5cb0eb09369677514ee1f44d5d7050d34c7fbc1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/26/2019
ms.locfileid: "74491302"
---
# <a name="how-to-install-a-visualizer"></a>如何：安装可视化工具
创建了可视化工具后，您还必须安装该可视化工具，这样您才可在 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 中使用它。 安装可视化工具是个简单的过程。

> [!NOTE]
> 在 UWP 应用中，仅支持标准文本、HTML、XML 和 JSON 可视化工具。 不支持自定义（用户创建的）可视化工具。

### <a name="to-install-a-visualizer-for-visual-studio-2019"></a>安装 Visual Studio 2019 的可视化工具
  
1. 查找包含已创建的可视化工具的 DLL。

2. 将[调试器端](create-custom-visualizers-of-data.md#to-create-the-debugger-side)DLL 复制到以下位置之一：

    - VisualStudioInstallPath `\Common7\Packages\Debugger\Visualizers`

    - `My Documents\` VisualStudioVersion `\Visualizers`
    
3. 将[调试对象端](create-custom-visualizers-of-data.md#to-create-the-debuggee-side)DLL 复制到以下位置之一：

    - *VisualStudioInstallPath* `\Common7\Packages\Debugger\Visualizers\` *Framework*

    - `My Documents\` *VisualStudioVersion* `\Visualizers\`*框架*

    其中，*框架*是：
    - 运行 `.NET Framework` 运行时的调试对象的 `net2.0`。
    - 使用支持 `netstandard 2.0` （`.NET Framework v4.6.1+` 或 `.NET Core 2.0+`）的运行时 `netstandard2.0` 调试对象。
    - 运行 `.NET Core` 运行时的调试对象的 `netcoreapp`。 （支持 `.NET Core 2.0+`）

4. 重新启动调试会话。

### <a name="to-install-a-visualizer-for-visual-studio-2017-and-older"></a>安装 Visual Studio 2017 和更低版本的可视化工具

> [!IMPORTANT]
> Visual Studio 2017 及更低版本仅支持 .NET Framework 可视化工具

1. 查找包含已创建的可视化工具的 DLL。

2. 将 DLL 复制到下列位置之一：

    - VisualStudioInstallPath `\Common7\Packages\Debugger\Visualizers`

    - `My Documents\` VisualStudioVersion `\Visualizers`

3. 重新启动调试会话。

> [!NOTE]
> 若要使用托管可视化工具进行远程调试，请将 DLL 复制到远程计算机上的同一路径。

## <a name="see-also"></a>另请参阅
- [创建自定义可视化工具](../debugger/create-custom-visualizers-of-data.md)
- [如何：编写可视化工具](create-custom-visualizers-of-data.md)
