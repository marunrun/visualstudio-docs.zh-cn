---
title: 管理 Python 应用程序项目
description: Visual Studio 中的项目管理文件之间的依赖项和应用程序中的关系复杂性。
ms.date: 03/18/2019
ms.topic: conceptual
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: d50cbfbd517073544ebd172627d24bd7c3878fa5
ms.sourcegitcommit: e98db44f3a33529b0ba188d24390efd09e548191
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/25/2019
ms.locfileid: "71254204"
---
# <a name="python-projects-in-visual-studio"></a>Visual Studio 中的 Python 项目

通常仅使用文件夹和文件定义 Python 应用程序，但如果程序变大，并且可能会涉及自动生成文件、适用于 Web 应用程序的 JavaScript 等，这种结构就会变得复杂。 Visual Studio 项目帮助管理复杂性问题。 该项目（  .pyproj 文件）标识与项目关联的所有源文件和内容文件，包含每个文件的生成信息，维护这些信息并与源代码管理系统集成，并帮助你将应用程序组织为逻辑组件。

![解决方案资源管理器中的 Python 项目](media/projects-solution-explorer.png)

此外，项目始终在 Visual Studio 解决方案  内进行管理，而解决方案中可包含任意数量可相互引用的项目。 例如，Python 项目可能引用实现扩展模块的 C++ 项目。 在此关系的基础上，开始调试 Python 项目时，Visual Studio 会自动生成 C++ 项目（如有需要）。 （有关综合讨论，请参阅 [Visual Studio 中的解决方案和项目](../ide/solutions-and-projects-in-visual-studio.md)。）

Visual Studio 提供多种 Python 项目模板用于快速设置多个应用程序结构，包括用于根据现有文件夹树创建项目的模板和用于创建干净的空项目的模板。 若要查看索引，请参阅[项目模板](#project-templates)。

<a name="lightweight-usage-project-free"></a>

::: moniker range=">=vs-2019"
> [!Tip]
> Visual Studio 2019 支持打开包含 Python 代码的文件夹并在不创建 Visual Studio 项目和解决方案文件的情况下运行该代码。 有关详细信息，请参阅[快速入门：打开并运行文件夹中的 Python 代码](quickstart-05-python-visual-studio-open-folder.md)。 但是，使用项目文件会获得本部分所述的优势。
::: moniker-end

> [!Tip]
> 即使没有项目，Visual Studio 的所有版本也能正常运行 Python 代码。 例如，可以单独打开 Python 文件并充分利用自动完成、IntelliSense 和调试功能（在编辑器中单击右键，并选择“启动调试”）  。 因为此类代码始终使用默认的全局环境，但是，如果代码针对其他环境，则可能出现不正确的完成或错误。 此外，Visual Studio 将分析打开的单个文件所在文件夹中的所有文件和包，这可能会占用相当多的 CPU 时间。
>
> 如[根据现有文件创建项目](#create-project-from-existing-files)中所述，根据现有代码创建 Visual Studio 项目非常简单。

|   |   |
|---|---|
| ![视频的摄像机图标](../install/media/video-icon.png "观看视频") | [深入了解：将源代码管理用于 Python 项目](https://youtu.be/Aq8eqApnugM)（youtube.com，8 分 55 秒）。 |

## <a name="add-files-assign-a-startup-file-and-set-environments"></a>添加文件、分配启动文件和设置环境

开发应用程序时，通常需要将不同类型的新文件添加到项目。 通过以下两种方式可以添加此类文件：右键单击项目并选择“添加”   > “现有项”  ，然后浏览到要添加的文件；或选择“添加”   > “新建项”  ，随后将打开包含各种项模板的对话框。 如[项模板](python-item-templates.md)引用所述，选项包括空的 Python 文件、Python 类、单元测试以及与 Web 应用程序相关的各种文件。 可使用测试项目研究这些选项以了解所用 Visual Studio 版本中可用的选项。

每个 Python 项目都有一个分配的启动文件，均以粗体显示在解决方案资源管理器中  。 开始调试（F5  或“调试”   > “开始调试”  ）时，或在交互  窗口中运行项目（Shift  +Alt  +F5  或“调试”   > “在 Python 交互中执行项目”  ）时，启动文件便是要运行的文件。 若要对其进行更改，请右键单击新文件并选择“设置为启动项”  （或者在较旧版本的 Visual Studio 中，选择“设置为启动文件”）  。

> [!Tip]
> 如果从项目中删除选定的启动文件且不选定新文件，那么，在你尝试运行该项目时，Visual Studio 不知道要启动哪个 Python 文件。 在这种情况下，Visual Studio 2017 版本 15.6 和更高版本将显示错误，早期版本将打开一个运行着 Python 解释器的输出窗口，或者显示输出窗口后几乎立即消失。 如果遇到以上任一行为，请检查你是否拥有分配的启动文件。
>
> 此外，如果出于任何原因想使输出窗口保持打开状态，请右键单击你的项目，选择“属性”  ，选择“调试”  选项卡，然后将 `-i` 添加到**解释器参数**字段。 此参数会使解释器在程序完成后进入交互模式，从而使窗口保持打开状态，直到按 Ctrl+Z > Enter 退出为止    。

::: moniker range="vs-2017"
新项目将始终与默认全局 Python 环境相关联。 若要将项目与其他环境（包括虚拟环境）相关联，请右键单击项目中的“Python 环境”  节点，选择“添加/删除 Python 环境”  ，然后选择所需的环境。
::: moniker-end
::: moniker range=">=vs-2019"
新项目将始终与默认全局 Python 环境相关联。 若要将项目与其他环境（包括虚拟环境）相关联，请右键单击项目中的“Python 环境”  节点，选择“添加环境”  ，然后选择所需的环境。 还可以使用工具栏上的环境下拉列表框控件选择环境或将其他环境添加到项目。

![Python 工具栏上的“添加环境”命令](media/environments/environments-toolbar-2019.png)
::: moniker-end

若要更改活动的环境，请在“解决方案资源管理器”  中右键单击所需的环境，并选择“激活环境”，如下所示  。 有关详细信息，请参阅[选择项目环境](selecting-a-python-environment-for-a-project.md)。

![激活 Python 项目的环境](media/projects-activate-environment.png)

<a name="project-types"></a>

## <a name="project-templates"></a>项目模板

Visual Studio 提供多种方法用于从零开始，或根据现有代码设置 Python 项目。 要使用模板，请选择“文件” > “新建” > “项目”菜单命令，或右键单击解决方案资源管理器中的解决方案，选择“添加” > “新建项目”，这两种方法都会打开下方的“新建项目”对话框        。 若要查看特定于 Python 的模板，请搜索“Python”或选择“已安装”   > “Python”  节点：

![Python 的新建项目对话框模板](media/projects-new-project-dialog.png)

下表总结了 Visual Studio 2017 及更高版本中提供的模板（并非以前的所有版本都提供了这些模板）：

| 模板 | 说明 |
| --- | --- |
| [**根据现有 Python 代码**](#create-project-from-existing-files) | 从文件夹结构中的现有 Python 代码创建 Visual Studio 项目。  |
| **Python 应用程序** | 新 Python 应用程序的基本项目结构具有一个空的源文件。 默认情况下，项目在默认全局环境的控制台解释器中运行，通过[分配其他环境](selecting-a-python-environment-for-a-project.md)可以更改环境。 |
| [**Azure 云服务**](python-azure-cloud-service-project-template.md) | 使用 Python 编写的 Azure 云服务项目。 |
| [**Web 项目**](python-web-application-project-templates.md) | 基于各种框架（包括 Bottle、Django 和 Flask）的 Web 应用项目。 |
| **IronPython 应用程序** | 与 Python 应用程序模板类似，但使用 IronPython 时，默认启用 .NET 互操作并通过 .NET 语言进行混合模式调试。 |
| **IronPython WPF 应用程序** | 将 IronPython 和 Windows Presentation Foundation XAML 文件配合使用以获得应用程序的用户界面的项目结构。 Visual Studio 提供 XAML UI 设计器，在 Python 中可以编写代码隐藏，以及运行应用程序时不显示控制台。 |
| **IronPython Silverlight 网页** | 在使用 Silverlight 的浏览器中运行的 IronPython 项目。 应用程序的 Python 代码作为脚本包含在网页中。 样本脚本标记会拉取一些 JavaScript 代码，这些代码会初始化在 Silverlight 中运行的 IronPython，Python 代码以此可与 DOM 交互。 |
| **IronPython Windows 窗体应用程序** | 将 IronPython 与在 Windows 窗体中使用代码创建的 UI 配合使用的项目结构。 应用程序运行时不显示控制台。 |
| **后台应用程序 (IoT)** | 支持部署 Python 项目，将其作为设备上的后台服务运行。 有关详细信息，请访问[Windows IoT 开发人员中心](https://dev.windows.com/en-us/iot)。 |
| **Python 扩展模块** | 如果随 Visual Studio 2017 或更高版本中的 Python 工作负载一起安装了 Python 本机开发工具，则此模板会显示在 Visual C++ 下（请参阅[安装](installing-python-support-in-visual-studio.md)）  。 它为 C++ 扩展 DLL 提供核心结构，类似于[创建适用于 Python 的 C++ 扩展](working-with-c-cpp-python-in-visual-studio.md)中所述的内容。 |

> [!Note]
> 由于 Python 是解释型语言，因此 Visual Studio 中的 Python 项目不会生成类似其他编译型语言项目（例如 C#）的独立可执行文件。 有关详细信息，请参阅[问题和解答](overview-of-python-tools-for-visual-studio.md#questions-and-answers)。

<a name="create-project-from-existing-files"></a>

### <a name="create-a-project-from-existing-files"></a>根据现有文件创建项目

> [!Important]
> 此处所述的过程不移动或复制原始源文件。 如果要使用副本，请先复制文件夹。

[!INCLUDE[project-from-existing](includes/project-from-existing.md)]

## <a name="linked-files"></a>链接文件

链接文件是指放入项目，但通常位于应用程序项目文件夹外的文件。 这些文件在“解决方案资源管理器”中显示为普通文件，具有重叠的快捷方式图标  ：![链接文件图标](media/projects-linked-file-icon.png)

链接文件通过 `<Compile Include="...">` 元素在 .pyproj 文件中指定  。 如果链接文件使用目录结构之外的相对路径，则为隐式链接文件，如果使用解决方案资源管理器内的路径，则为显式链接文件  ：

```xml
<Compile Include="..\test2.py">
    <Link>MyProject\test2.py</Link>
</Compile>
```

在以下任何情况下，会忽略链接文件：

- 链接文件包含链接元数据，并且在 Include 特性中指定的路径存在于项目目录中
- 链接文件复制存在于项目层次结构中的文件
- 链接文件包含链接元数据，并且链接路径是项目层次结构外的相对路径
- 链接路径是根路径

### <a name="work-with-linked-files"></a>使用链接文件

要将现有项添加为链接，请右键单击项目中要添加文件所在的文件夹，然后选择“添加” > “退出项”   。 在出现的对话框中，选择一个文件，然后从“添加”按钮上的下拉列表中选择“添加为链接”   。 如果没有冲突文件，此命令会在所选文件夹中创建一个链接。 但是，如果已存在具有相同名称的文件或项目中已存在该文件的链接，将不会添加链接。

如果尝试链接到项目文件夹中已存在的文件，会添加该文件作为普通文件而不是作为链接。 要将文件转换为链接，请选择“文件” > “另存为”，将文件保存到项目层次结构外的位置；Visual Studio 会自动将其转换为链接   。 同样，通过使用“文件” > “另存为”将文件保存在项目层次结构内的某个位置，可以将链接转换回文件   。

如果在解决方案资源管理器中移动链接文件，则链接会移动，但实际文件不会受到影响  。 同样，删除链接仅会删除该链接，而不会影响文件。

不能重命名链接文件。

## <a name="references"></a>reference

Visual Studio 项目支持将引用添加到项目和扩展，添加的引用将显示在解决方案资源管理器中的“引用”节点下   ：

![Python 项目中的扩展引用](media/projects-extension-references.png)

扩展引用通常指示项目之间的依赖项，在设计时用于提供 IntelliSense，在编译时用于提供链接。 Python 项目以类似的方式使用引用，但由于 Python 的动态特性，引用主要用于在设计时提供改进的 IntelliSense。 此外，还可以用于部署到 Microsoft Azure 以安装其他依赖项。

### <a name="extension-modules"></a>扩展模块

对 .pyd 文件的引用可为生成的模块启用 IntelliSense  。 Visual Studio 会将 .pyd 文件加载到 Python 解释器并检查其类型和函数  。 它还将尝试分析函数的文档字符串以提供签名帮助。

如果磁盘上更新了扩展模块，Visual Studio 会在后台重新分析模块。 此操作对运行时行为没有任何影响，但分析完成之前，某些完成功能不可用。

你可能还需要将[搜索路径](search-paths.md)添加到包含该模块的文件夹。

### <a name="net-projects"></a>.NET 项目

使用 IronPython 时，可以向 .NET 程序集添加引用，启用 IntelliSense。 对于解决方案中的 .NET 项目，请右键单击 Python 项目中的“引用”  节点，选择“添加引用”  ，选择“项目”  选项卡，然后浏览到所需项目。 对于已单独下载的 DLL，请改为选择“浏览”  选项卡，然后浏览到所需的 DLL。

因为只有调用 `clr.AddReference('<AssemblyName>')` 才可以使用 IronPython 中的引用，因此还需要将相应的 `clr.AddReference` 调用添加到程序集，通常位于代码的开头。 例如，在 Visual Studio 中通过“IronPython Windows 窗体应用程序”项目模板创建的代码在文件顶部包含两个调用： 

```python
import clr
clr.AddReference('System.Drawing')
clr.AddReference('System.Windows.Forms')

from System.Drawing import *
from System.Windows.Forms import *

# Other code omitted
```

### <a name="webpi-projects"></a>WebPI 项目

可以向 WebPI 产品条目添加引用以部署到 Microsoft Azure 云服务，可在其中通过 WebPI 源安装其他组件。 默认情况下，显示的源特定于 Python，包括 Django、CPython和其他核心组件。 还可以选择自己的源，如下所示。 发布到 Microsoft Azure 时，安装任务将安装所有引用的产品。

> [!IMPORTANT]
> WebPI 项目在 Visual Studio 2017 或 Visual Studio 2019 中不可用。

![WebPI 引用](media/projects-webPI-components.png)
