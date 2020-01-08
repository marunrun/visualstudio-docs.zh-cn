---
title: 使用 Visual Studio for Mac Tools for Unity
description: 本指南介绍如何使用 Visual Studio for Mac Tools for Unity 扩展
author: therealjohn
ms.author: johmil
ms.date: 12/13/2019
ms.assetid: 83FDD7A3-5D16-4B4B-9080-078E3FB5C623
ms.openlocfilehash: 4247e5cfb936d79c2b2bea5ac68a16164f0c0ef0
ms.sourcegitcommit: 8e123bcb21279f2770b28696995450270b4ec0e9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/25/2019
ms.locfileid: "75406672"
---
# <a name="using-visual-studio-for-mac-tools-for-unity"></a>使用 Visual Studio for Mac Tools for Unity

本部分介绍如何使用 Visual Studio for Mac Tools for Unity 的集成和生产力功能，以及如何使用 Visual Studio for Mac 调试程序进行 Unity 开发。

## <a name="opening-unity-scripts-in-visual-studio-for-mac"></a>在 Visual Studio for Mac 中打开 Unity 脚本

将 Visual Studio for Mac [设置为 Unity 的外部脚本编辑器](setup-vsmac-tools-unity.md#configure-unity-for-use-with-visual-studio-for-mac)后，在 Unity 编辑器中打开任何脚本都会自动启动或切换到 Visual Studio for Mac，并打开选择的脚本。

或者，可以通过从 Unity 的“Assets”菜单中选择“Open C# Project”打开 Visual Studio for Mac，而无需在源编辑器中打开任何脚本。  

![打开 C# 项目](media/using-vsmac-tools-unity-image1.png)

## <a name="unity-documentation-access"></a>Unity 文档访问

Visual Studio for Mac Tools for Unity 包括用于访问 Unity API 文档的快捷方式。 要从 Visual Studio for Mac 访问 Unity API 文档，请将光标放置于想要了解的 Unity API 上，并按 ⌘ command + ‘  。

## <a name="intellisense-for-unity-messages"></a>针对 Unity 消息的 IntelliSense
Unity 引擎向 MonoBehaviour 脚本广播消息，允许开发人员编写对 OnMouseDown，OnTriggerEnter 等消息作出响应的代码。由于这些不是 MonoBehaviour 基类中的虚拟方法，因此一些 IDE（如 MonoDevelop）缺少适用于 Unity 消息的代码完成功能。

但是，Visual Studio for Mac Tools for Unity 将其 IntelliSense 功能扩展到 Unity 消息。 这简化了在 MonoBehaviour 脚本中实现 Unity 消息，并有助于学习 Unity API。 对 Unity 消息使用 IntelliSense：

1. 将光标置于类主体内的新行上，该类派生自 MonoBehaviour。

2. 开始键入 Unity 消息的名称，如 `OnTriggerEnter`。

3. 键入字母“ont”后，将显示 IntelliSense 建议列表  。

   ![Using IntelliSense](media/using-vsmac-tools-unity-image2.png)

4. 可通过以下三种方式更改列表中的选择：

   * 使用向上键和向下键   。

   * 使用鼠标单击所需项。

   * 继续键入所需项的名称。

5. IntelliSense 可插入所选 Unity 消息，包括任何必需的参数：

   * 通过按 Tab  。

   * 通过按 Return  。

   * 通过双击所选项。

   ![从 IntelliSense 插入 Unity 消息](media/using-vsmac-tools-unity-image3.png)

## <a name="adding-new-unity-files-and-folders"></a>添加新 Unity 文件和文件夹

始终都可在 Unity 编辑器中将新文件添加到 Unity 项目，也可通过 Visual Studio for Mac 轻松从 Visual Studio 中创建新的 Unity 脚本、着色器、结构、枚举和文件夹。

### <a name="add-a-new-c-monobehaviour-script"></a>添加新的 C# MonoBehaviour 脚本

要添加新的 C# MonoBehaviour 脚本，请在 Solution Pad 中右键单击“Assets”文件夹或它的一个子目录，并选择“Add > New MonoBehaviour”   。

![添加新的 MonoBehaviour](media/using-vsmac-tools-unity-image4.png)

### <a name="add-a-new-unity-shader"></a>添加新的 Unity 着色器

要添加新的 Unity 着色器，请在 Solution Pad 中右键单击“Assets”文件夹或一个子目录，并选择“Add > New Shader”。  

### <a name="add-a-new-folder"></a>添加新文件夹

若要添加新文件夹，请在 Solution Pad 中右键单击“Assets”文件夹或一个子目录，并选择“Add > New Folder”。  

Unity 编辑器的“Project”窗口会反映这些添加。

### <a name="to-rename-a-file-or-folder"></a>重命名文件或文件夹
在 Solution Pad 中右键单击想要重命名的项，并选择“Rename...”   。

> [!NOTE]
> 如果新的 Unity 项目中不包含任何脚本，且 Visual Studio for Mac 的 Solution Pad 中未显示“资产”文件夹，请从 Unity 编辑器内添加初始 C# 脚本。

## <a name="unity-debugging"></a>Unity 调试

可以使用 Visual Studio for Mac 调试 Unity 项目。

### <a name="start-debugging"></a>“启动调试”

若要开始调试：

1. 通过单击“Play”按钮、键入“Command + Return”或按“F5”将 Visual Studio 连接到 Unity    。

   ![在 Visual Studio 中单击“播放”](media/using-vsmac-tools-unity-image5.png)

2. 切换到 Unity 并单击“Play”按钮，在编辑器中运行游戏  。

   ![在 Unity 中单击“播放”](media/using-vsmac-tools-unity-image6.png)

3. 当游戏在连接到 Visual Studio 的情况下在 Unity 编辑器中运行时，遇到的任何断点都会中断游戏执行，并在 Visual Studio for Mac 中显示游戏遇到断点的代码行。

### <a name="start-debugging-in-a-single-step"></a>通过单个步骤启动调试

通过选择“附加到 Unity 并播放”配置，可通过一个步骤直接从 Visual Studio for Mac 完成启动调试和播放 Unity 编辑器  。

![选择“附加到 Unity 并播放”](media/using-vsmac-tools-unity-image8.png)

### <a name="stop-debugging"></a>停止调试

停止调试：

1. 在 Visual Studio for Mac 中单击“停止”按钮，或按“Shift + Command + Return”   。

   ![在 Visual Studio 中单击“停止”](media/using-vsmac-tools-unity-image7.png)

> [!NOTE]
> 如果使用“附加到 Unity 并播放”配置启动调试，“停止”按钮也将停止 Unity   。

有关在 Visual Studio for Mac 中调试的详细信息，请参阅[使用调试程序](debugging.md)。
