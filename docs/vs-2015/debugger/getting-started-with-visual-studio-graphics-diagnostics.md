---
title: 与图形诊断入门 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 59131181-1caa-4b7f-be4b-e84709634edf
caps.latest.revision: 10
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: e9056fdae9d0eff55c572d8e38503d88269dbde3
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65704710"
---
# <a name="getting-started-with-visual-studio-graphics-diagnostics"></a>Visual Studio 图形诊断入门
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在此部分中，你会准备首次使用图形诊断，然后从 Direct3D 应用捕获帧并在图形分析器中检查它们。

## <a name="requirements"></a>要求
 若要在 Visual Studio 2015 中使用图形诊断，你必须拥有以下版本之一：

- Visual Studio 2015 Enterprise

- Visual Studio 2015 Professional

- Visual Studio 2015 Community

  [!INCLUDE[downloadvs](../includes/downloadvs-md.md)]

### <a name="windows-10-prerequisites"></a>Windows 10 先决条件
 可选的 Windows 功能“图形工具”可提供 Windows 10 上的图形诊断所需的捕获和播放基础结构。

 有关安装图形工具的信息，请参阅[为 Windows 10 安装图形工具](#InstallGraphicsTools)。

### <a name="windows-81-prerequisites"></a>Windows 8.1 先决条件
 适用于 Windows 8.1 的 Windows 软件开发工具包 (SDK) 提供 Windows 8.1 上的图形诊断所需的捕获和播放基础结构，并支持针对 Windows 8.1 和 Windows 8 的开发。

 [下载适用于 Windows 8.1 的 Windows 软件开发工具包 (SDK) ](https://msdn.microsoft.com/windows/desktop/bg162891.aspx)

 若要从运行 Windows 8.1 的开发计算机使用运行 Windows 10 的远程播放计算机，必须在开发计算机上安装 Windows 10 SDK，并在播放计算机上安装可选的图形工具功能。

## <a name="install-graphics-tools-for-windows-10"></a><a name="InstallGraphicsTools"></a>为 Windows 10 安装图形工具
 在 Windows 10 中，图形诊断基础结构由 Windows 的一个可选功能（称为“图形工具”）提供。 在 Windows 10 上捕获和播放图形信息需要此功能（无论所捕获的应用是面向以前版本的 Windows 还是它所使用的 Direct3D 版本）。 可以选择提前安装图形工具功能；否则它会在你首次从 Visual Studio 启动图形诊断会话时按需安装。

#### <a name="to-install-graphics-tools-for-windows-10"></a>为 Windows 10 安装图形工具

1. 在 " **开始** " 菜单上，选择 " **设置**"。 此时将显示 " **设置** " 对话框。

2. 在 " **设置** " 对话框中，选择 " **系统**"，然后从系统设置列表中选择 " **已安装的应用** "。

3. 在 "**设置**" 对话框的右侧，选择 "**已安装的应用和功能**" 下的 "**管理可选功能**"。 “管理可选功能”对话框随即出现****。

4. 在“管理可选功能”对话框中，选择“添加功能”********。 可以安装的可选功能列表随即出现。

5. 从功能列表中选择“图形工具”，然后选择“安装” 。

   安装 Windows 10 SDK 时，也会自动安装图形工具功能。

> [!TIP]
> Windows 10 的可选图形工具功能可提供轻量级捕获和播放功能（如命令行捕获程序 dxcap.exe），该功能可以在未安装开发人员工具的计算机上用于支持、测试和诊断方案。 有关详细信息，请参阅[命令行捕获工具](../debugger/command-line-capture-tool.md)主题。

## <a name="using-graphics-diagnostics-for-the-first-time"></a>首次使用图形诊断
 现在你拥有所有所需内容，已准备好开始使用图形诊断。 请执行这些步骤。

### <a name="1---create-a-direct3d-app"></a>1 - 创建 Direct3D 应用
 如果你已具有自己的 Direct3D 应用来探索图形诊断，非常好！ 否则可以使用代码库中提供的 Direct3D 示例之一。

- 若要尝试使用 Visual Studio 2015 在 Windows 10 上使用 Direct3D 12 图形诊断，请尝试使用适用于 Windows 10 的 [direct3d 12 UAP 示例](https://code.msdn.microsoft.com/Direct3D-12-UAP-Sample-ecb1779f) 。

- 若要在 Windows 10 或 Windows 8.1 上尝试使用 Direct3D 11 图形诊断，可以使用 **Directx 应用 (Windows 通用) ** 或  **directx app (** Windows 8.1) 项目模板。 或者，若要了解一些更有趣的内容，请尝试 Windows 8.1 的 [DirectX 大理石迷宫游戏示例](https://code.msdn.microsoft.com/windowsapps/DirectX-Marble-Maze-Game-e4806345) 。

  确保在继续之前可以生成应用。

### <a name="2---start-a-graphics-diagnostics-session"></a>2 - 启动图形诊断会话
 现在你已准备好启动第一个图形诊断会话。 在 Visual Studio 中的主菜单上，选择 " **调试"、"图形"、"启动诊断**"，或只需按 **Alt + F5**。 这会在图形诊断下启动你的应用并在 Visual Studio 中显示诊断会话窗口。

> [!IMPORTANT]
> 如果在 Windows 10 上运行应用，并且尚未安装可选的图形工具功能，则系统会提示立即安装该功能。 必须先安装它，然后才能在 Windows 10 上使用图形诊断。

### <a name="3---capture-frames"></a>3 - 捕获帧
 只要应用启动，你便已准备好捕获帧。

##### <a name="to-capture-single-frames"></a>捕获单个帧

- 在 Visual Studio 中，从图形工具栏或诊断会话窗口选择“捕获帧”按钮。 或者，如果您的应用程序具有焦点，只需按 " **打印屏幕**" 即可。

##### <a name="to-capture-a-sequence-of-frames"></a>捕获帧序列

- 在 Visual Studio 的诊断会话窗口中，将“要捕获的帧数”设置为要按顺序捕获的帧数，然后使用上述任何捕获单个帧的方法来捕获序列。

   若要再次捕获单个帧，请设置要 **捕获** 到 `1` 的帧。

  捕获帧完成时，只需退出应用，或从图形工具栏或诊断会话窗口选择“停止”按钮。

### <a name="4--examine-captured-frames-in-the-graphics-analyzer"></a>4 – 在图形分析器中检查捕获的帧
 现在你已准备好检查刚捕获的帧。 若要开始分析帧，请从诊断会话窗口选择要检查的帧的帧号码。 这会在“图形分析器”中打开该帧，在其中可以使用图形诊断工具检查应用如何使用 Direct3D 来跟踪呈现问题，或使用“帧分析”工具来了解其性能 。

 如果从诊断会话窗口选择了错误的帧，或者要检查不同的帧，则可以从图形分析器选择一个新帧。 在图形日志窗口的“呈现目标”选项卡上，在呈现目标图像下展开“帧列表”，然后选择不同的帧进行检查 。

 若要了解有关如何结合使用图形分析器工具的详细信息，请参阅[示例](../debugger/graphics-diagnostics-examples.md)。

## <a name="see-also"></a>另请参阅
 [Direct3D 12 图形](https://msdn.microsoft.com/52094ae3-3b44-4689-9ee7-1ba1b3a779cb)
