---
title: 请参阅之间的依赖关系C++源文件和头文件
ms.date: 05/16/2018
ms.topic: conceptual
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3904ff08496257d18589e36e5878f49404bbdf7c
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62422153"
---
# <a name="code-maps-for-c-projects"></a>代码图的C++项目

如果要创建更多 C++ 项目的完整代码图，请在这些项目上设置浏览信息编译器选项 (**/FR**)。 否则，将出现一条消息并提示你设置此选项。 如果选择“确定” ，就只会为当前代码图设置选项。 可以选择隐藏所有之后的代码图的信息。

打开包含 Visual C++ 项目的解决方案时，可能需要花一些时间来更新 IntelliSense 数据库。 在此期间，您可能不能创建标头的代码图 (*.h*或`#include`) 文件，直到 IntelliSense 数据库完成更新。 你可在 Visual Studio 状态栏中监视更新进度。

- 若要查看所有源代码文件和你的解决方案中的标头文件之间的依赖关系，请选择**体系结构** > **生成包含文件的关系图**。

   ![本机代码的依赖项关系图](../modeling/media/dependencygraphgeneral_nativecode.png)

- 若要查看当前打开文件和相关的源文件以及头文件之间的依赖关系，请打开相关的源文件或头文件。 在文件内的任何地方打开文件快捷菜单。 选择“生成包含文件的关系图” 。

   ![.h 文件的第一级依赖项关系图](../modeling/media/dependencygraph_native_firstlevel.png)

## <a name="troubleshoot-code-maps-for-c-and-c-code"></a>对于 C 的故障排除代码图和C++代码

C 和 C++ 代码不支持这些项：

- 基类型不会显示在包含父层次结构的图中。

- 大多数“显示”  菜单项不适用于 C 和 C++ 代码。

为 C 创建代码图时，可能会出现这些问题和C++代码：

|**问题**|**可能的原因**|**解决方法**|
|-|-|-|
|未能生成代码图。|解决方案中没有项目成功生成过。|修复出现的生成错误，然后重新生成代码图。|
|当你尝试生成从代码图时，visual Studio 停止响应**体系结构**菜单。|程序数据库 (.pdb) 文件可能已损坏。<br /><br /> pdb 文件将存储调试信息，例如，类型、方法和源文件信息。|重新生成解决方案，然后重试。|
|禁用 IntelliSense 浏览器数据库的某些设置。|可能会在 Visual Studio 中禁用某些 IntelliSense 设置**选项**对话框。|打开设置以启用它们。<br /><br /> 请参阅[选项，文本编辑器，C /C++的高级](../ide/reference/options-text-editor-c-cpp-advanced.md)。|
|消息“未知方法”  将出现在方法节点上。<br /><br /> 由于无法解析方法的名称，导致出现此问题。|二进制文件可能没有基重定位表。|在链接器中打开 **/FIXED:NO** 选项。|
||无法生成程序数据库 (.pdb) 文件。<br /><br /> pdb 文件将存储调试信息，例如，类型、方法和源文件信息。|在链接器中打开 **/DEBUG** 选项。|
||无法在预期位置打开或找到 .pdb 文件。|确保 .pdb 文件位于预期位置。|
||已从 .pdb 文件中去除调试信息。|如果链接器中已使用 **/PDBSTRIPPED** 选项，则改为包含完整的 .pdb 文件。|
||调用方不是函数，它是二进制文件中的形式转换 (thunk) 或数据节中的指针。|当调用方是形式转换 (thunk) 时，尝试使用 `_declspec(dllimport)` 以避免形式转换 (thunk)。|

## <a name="see-also"></a>请参阅

- [使用代码映射来映射依赖项](../modeling/map-dependencies-across-your-solutions.md)