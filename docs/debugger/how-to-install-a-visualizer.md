---
title: 如何安装可视化工具 | Microsoft Docs
ms.date: 06/10/2020
ms.topic: how-to
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
ms.openlocfilehash: b070eb361bcc3fbe4f72adfff10b5e7d19649087
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2020
ms.locfileid: "85349557"
---
# <a name="how-to-install-a-visualizer"></a>如何：安装可视化工具
创建了可视化工具后，您还必须安装该可视化工具，这样您才可在 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 中使用它。 安装可视化工具是个简单的过程。

> [!NOTE]
> UWP 应用仅支持标准文本、HTML、XML 和 JSON 可视化工具。 不支持自定义（用户创建的）可视化工具。

::: moniker range=">=vs-2019"
### <a name="to-install-a-visualizer-for-visual-studio-2019"></a>安装适用于 Visual Studio 2019 的可视化工具
  
1. 找到包含已创建的可视化工具的 DLL。

   通常，最理想的情况是调试器端 DLL 和调试对象端 DLL 指定任意 CPU 作为目标平台。 调试器端 DLL 必须为“任意 CPU”或“32 位” 。 调试对象端 DLL 的目标平台应对应于调试对象进程。

2. 将[调试器端](create-custom-visualizers-of-data.md#to-create-the-debugger-side) DLL（以及它所依赖的任意 DLL）复制到以下位置之一：

    - VisualStudioInstallPath `\Common7\Packages\Debugger\Visualizers`

    - `My Documents\` VisualStudioVersion `\Visualizers`
    
3. 将[调试对象端](create-custom-visualizers-of-data.md#to-create-the-visualizer-object-source-for-the-debuggee-side) DLL 复制到下列位置之一：

    - VisualStudioInstallPath `\Common7\Packages\Debugger\Visualizers\` Framework 

    - `My Documents\` VisualStudioVersion `\Visualizers\` Framework 

    其中 Framework：
    - 对于运行 `.NET Framework` 运行时的调试对象，为 `net2.0`。
    - 对于使用支持 `netstandard 2.0`（`.NET Framework v4.6.1+` 或 `.NET Core 2.0+`）的运行时的调试对象，为 `netstandard2.0`。
    - 对于运行 `.NET Core` 运行时的调试对象，为 `netcoreapp`。 （支持 `.NET Core 2.0+`）

   如果要创建独立可视化工具，则需要调试对象端 DLL。 此 DLL 包含数据对象的代码，该代码可实现 <xref:Microsoft.VisualStudio.DebuggerVisualizers.VisualizerObjectSource> 方法。

   如果你对调试对象端代码设定了多个目标，则必须将调试对象端 DLL 置于最小支持 TFM 的文件夹中。

4. 重新启动调试会话。

> [!NOTE]
> 此过程在 Visual Studio 2017 及更早版本中是不同的。 请参阅本文的[早期版本](how-to-install-a-visualizer.md?view=vs-2017)。
::: moniker-end

::: moniker range="vs-2017"
### <a name="to-install-a-visualizer-for-visual-studio-2017-and-older"></a>安装适用于 Visual Studio 2017 及更早版本的可视化工具

> [!IMPORTANT]
> Visual Studio 2017 及更早版本仅支持 .NET Framework 可视化工具。

1. 查找包含已创建的可视化工具的 DLL。

2. 将 DLL 复制到下列位置之一：

    - VisualStudioInstallPath `\Common7\Packages\Debugger\Visualizers`

    - `My Documents\` VisualStudioVersion `\Visualizers`

3. 重新启动调试会话。

> [!NOTE]
> 若要使用托管可视化工具进行远程调试，请将 DLL 复制到远程计算机上的同一路径。
::: moniker-end

## <a name="see-also"></a>请参阅
- [创建自定义可视化工具](../debugger/create-custom-visualizers-of-data.md)
- [如何：编写可视化工具](create-custom-visualizers-of-data.md)
