---
title: 如何：安装可视化工具 |微软文档
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
ms.openlocfilehash: 499d644cc8374b070cedaf058b0e4dc17d155bdc
ms.sourcegitcommit: 5d1b2895d3a249c6bea30eb12b0ad7c0f0862d85
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80880255"
---
# <a name="how-to-install-a-visualizer"></a>如何：安装可视化工具
创建了可视化工具后，您还必须安装该可视化工具，这样您才可在 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 中使用它。 安装可视化工具是个简单的过程。

> [!NOTE]
> 在 UWP 应用中，仅支持标准文本、HTML、XML 和 JSON 可视化工具。 不支持自定义（用户创建的）可视化工具。

::: moniker range=">=vs-2019"
### <a name="to-install-a-visualizer-for-visual-studio-2019"></a>为 Visual Studio 2019 安装可视化工具
  
1. 找到包含您构建的可视化工具的 DLL。

   通常，最好调试器端 DLL 和调试器端 DLL 都指定**任何 CPU**作为目标平台。 调试器端 DLL 必须是任意**CPU**或**32 位**。 调试端 DLL 的目标平台应对应于调试器过程。

2. 将[调试器端](create-custom-visualizers-of-data.md#to-create-the-debugger-side)DLL（及其所依赖的任何 DLL）复制到以下任一位置：

    - VisualStudioInstallPath** `\Common7\Packages\Debugger\Visualizers`

    - `My Documents\` *VisualStudioVersion* `\Visualizers`
    
3. 将[调试基端](create-custom-visualizers-of-data.md#to-create-the-debuggee-side)DLL 复制到以下任一位置：

    - *可视化工作室安装路径*`\Common7\Packages\Debugger\Visualizers\`*框架*

    - `My Documents\`*可视化工作室版本*`\Visualizers\`*框架*

    *框架*可以是：
    - `net2.0`用于运行运行时的`.NET Framework`调试器。
    - `netstandard2.0`用于使用支持`netstandard 2.0`（`.NET Framework v4.6.1+`或`.NET Core 2.0+`） 的运行时的调试器。
    - `netcoreapp`用于运行运行时的`.NET Core`调试器。 （支持`.NET Core 2.0+`）

4. 重新启动调试会话。

> [!NOTE]
> 在 Visual Studio 2017 及更高级版中，该过程有所不同。 请参阅本文[的早期版本](how-to-install-a-visualizer.md?view=vs-2017)。
::: moniker-end

::: moniker range="vs-2017"
### <a name="to-install-a-visualizer-for-visual-studio-2017-and-older"></a>为 Visual Studio 2017 及更高级版安装可视化工具

> [!IMPORTANT]
> Visual Studio 2017 及更旧版仅支持 .NET 框架可视化工具。

1. 查找包含已创建的可视化工具的 DLL。

2. 将 DLL 复制到下列位置之一：

    - VisualStudioInstallPath** `\Common7\Packages\Debugger\Visualizers`

    - `My Documents\` *VisualStudioVersion* `\Visualizers`

3. 重新启动调试会话。

> [!NOTE]
> 若要使用托管可视化工具进行远程调试，请将 DLL 复制到远程计算机上的同一路径。
::: moniker-end

## <a name="see-also"></a>请参阅
- [创建自定义可视化工具](../debugger/create-custom-visualizers-of-data.md)
- [如何：编写可视化工具](create-custom-visualizers-of-data.md)
