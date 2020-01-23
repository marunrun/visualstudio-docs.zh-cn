---
title: DSL 的 VSIX 部署 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
ms.assetid: 6ce16f06-1978-4e19-8cdc-441ee65a3fb2
caps.latest.revision: 4
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: be9d3d44bfceaae1f2912086c3d20c90ce1e094b
ms.sourcegitcommit: 939407118f978162a590379997cb33076c57a707
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/13/2020
ms.locfileid: "75916550"
---
# <a name="vsix-deployment-of-a-dsl"></a>DSL 的 VSIX 部署
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以在自己的计算机或其他计算机上安装域特定语言。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 必须已安装在目标计算机上。

## <a name="Installing"></a>使用 VSX 安装和卸载 DSL
 此方法安装 DSL 后，用户可以从 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]中打开 DSL 文件，但无法从 Windows 资源管理器打开该文件。

#### <a name="to-install-a-dsl-by-using-the-vsix"></a>使用 VSIX 安装 DSL

1. 在计算机中，查找 DSL 包项目生成的 **.vsix**文件。

    1. 在**解决方案资源管理器**中，右键单击**DslPackage**项目，然后单击 "**在 Windows 资源管理器中打开文件夹**"。

    2. **\\\*\\** _项目_找到文件箱 **。DslPackage**

2. 将 **.vsix**文件复制到要安装 DSL 的目标计算机。 该计算机可以是自己的计算机或其他计算机。

    - 目标计算机必须具有在运行时支持 Dsl 的 [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] 版本之一。 有关详细信息，请参阅[支持的 Visual Studio 版本 & 建模 SDK](../modeling/supported-visual-studio-editions-for-visualization-amp-modeling-sdk.md)。

    - 目标计算机必须具有**DslPackage\source.extensions.manifest**中指定的其中一个 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 版本。

3. 在目标计算机上，双击 **.vsix**文件。

     “” 将会打开并安装扩展。

4. 启动或重启 [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)]。

5. 若要测试 DSL，请使用 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 创建新文件，该文件具有你为 DSL 定义的扩展。

#### <a name="to-uninstall-a-dsl-that-was-installed-by-using-vsx"></a>卸载使用 VSX 安装的 DSL

1. 在 "**工具**" 菜单上，单击 "**扩展管理器**"。

2. 展开“已安装的扩展”。

3. 选择在其中定义 DSL 的扩展，然后单击 "**卸载**"。

   在极少数情况下，有错误的扩展无法加载并在错误窗口中创建报告，但不显示在扩展管理器中。 在这种情况下，可以通过从以下位置删除文件来删除扩展：

   *LocalAppData* **\Microsoft\VisualStudio\10.0\Extensions**
