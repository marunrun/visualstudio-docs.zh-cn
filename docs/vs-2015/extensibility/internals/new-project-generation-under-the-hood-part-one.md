---
title: 生成新项目：实质上，第 1 部分 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio], new project dialog
- projects [Visual Studio], new project generation
ms.assetid: 66778698-0258-467d-8b8b-c351744510eb
caps.latest.revision: 30
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 6f26c093f09cd5b7b99f00ee69a81be99c769e2e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68184151"
---
# <a name="new-project-generation-under-the-hood-part-one"></a>生成新项目：揭秘，第 1 部分
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

有关如何创建您自己的项目类型有没有想过吗？ 想知道实际情况时创建新的项目？ 让我们了解一下实质上，了解实际情况。  
  
 有几个 Visual Studio 协调为你的任务：  
  
- 它将显示所有可用的项目类型的树。  
  
- 它显示每个项目类型的应用程序模板的列表，并可让你选择其中一个。  
  
- 它收集应用程序，如项目名称和路径的项目信息。  
  
- 它将此信息传递到项目工厂。  
  
- 它生成当前解决方案中的项目项和文件夹。  
  
## <a name="the-new-project-dialog-box"></a>新建项目对话框  
 所有它开始时选择新的项目的项目类型。 首先，通过单击**新的项目**上**文件**菜单。 **新的项目**对话框随即出现，外观如下所示：  
  
 ![新建项目对话框](../../extensibility/internals/media/newproject.gif "新建项目")  
  
 让我们更详细地介绍。 **项目类型**树列出了可以创建的各种项目类型。 当选择项目类型，例如**Visual C# Windows**，您将看到一系列应用程序模板帮助你入门。 **Visual Studio 已安装的模板**由 Visual Studio 安装并可供您的计算机的任何用户。 创建或收集的新模板可以添加到**我的模板**并且仅提供给你。  
  
 当选择一个与模板**Windows 应用程序**，应用程序类型的说明将显示在对话框中; 在本例中为**使用 Windows 用户界面创建应用程序的项目**。  
  
 在底部**新的项目**对话框中，您将看到收集的详细信息的多个控件。 您看到的控件依赖于项目类型，但它们通常包含一个项目**名称**文本框中**位置**文本框及相关**浏览**按钮，然后**解决方案名称**文本框中，相关**创建解决方案目录**复选框。  
  
## <a name="populating-the-new-project-dialog-box"></a>填充新建项目对话框  
 其中 does**新的项目**对话框获取从其信息？ 在工作在这里，不推荐使用的其中一个有两种机制。 **新的项目**对话框组合，并显示从这两种机制获取的信息。  
  
 较旧 （已弃用） 方法使用系统注册表项和.vsdir 文件。 Visual Studio 打开时，将运行此机制。 较新的方法使用.vstemplate 文件。 此机制在 Visual Studio 在初始化时，例如，通过运行时运行  
  
```  
devenv /setup  
```  
  
 或  
  
```  
devenv /installvstemplates  
```  
  
### <a name="project-types"></a>项目类型  
 位置和名称**项目类型**根节点，如**Visual C#** 并**其他语言**，由系统注册表项。 组织子节点，如**数据库**并**智能设备**，镜像包含相应的.vstemplate 文件的文件夹的层次结构。 让我们看一下根节点第一次。  
  
#### <a name="project-type-root-nodes"></a>项目类型的根节点  
 当[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]是初始化，遍历系统注册表项 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\14.0\NewProjectTemplates\TemplateDirs 来生成，并命名的根节点的子项**项目类型**树。 此信息进行缓存以供将来使用。 看一看 TemplateDirs\\{FAE04EC1-301F-11D3-BF4B-00C04F79EFBC} \\ /1 键。 每个条目是 VSPackage 的 GUID。 该子项的名称 （/ 1） 将被忽略，但它的存在指示这是**项目类型**根节点。 根节点可能有多个控件中的外观的子项**项目类型**树。 让我们看一下其中一些。  
  
##### <a name="default"></a>(默认)  
 这是名称的根节点的本地化字符串的资源 ID。 字符串资源位于附属 DLL 选择的 VSPackage 的 GUID。  
  
 在示例中，VSPackage GUID 是  
  
 {FAE04EC1-301F-11D3-BF4B-00C04F79EFBC}  
  
 根节点的资源 ID （默认值） 和 （/ 1） 是 # 2345年  
  
 如果您查找附近的包项中的 GUID，并检查 SatelliteDll 子项，您可以找到包含字符串资源的程序集的路径：  
  
 \<Visual Studio 安装路径 > \VC#\VCSPackages\1033\csprojui.dll  
  
 若要验证这一点，打开文件资源管理器，并将 csprojui.dll 拖入 Visual Studio 目录... 字符串表显示了资源 # 2345年具有标题**Visual C#** 。  
  
##### <a name="sortpriority"></a>SortPriority  
 这将确定中的根节点的位置**项目类型**树。  
  
 SortPriority REG_DWORD 0x00000014 (20)  
  
 优先级越低数在树中的更高版本的位置。  
  
##### <a name="developeractivity"></a>DeveloperActivity  
 如果存在此子项，则由开发人员设置对话框控制的根节点的位置。 例如，应用于对象的  
  
 DeveloperActivity REG_SZVC#  
  
 指示 Visual C# 为根节点是否 Visual Studio 设置为[!INCLUDE[vcprvc](../../includes/vcprvc-md.md)]开发。 否则，它将为的子节点**其他语言**。  
  
##### <a name="folder"></a>文件夹  
 如果存在此子项，则根节点将成为指定的文件夹的子节点。 可能的文件夹的列表将显示在项下  
  
 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\11.0\NewProjectTemplates\PseudoFolders  
  
 例如，数据库项目项具有文件夹匹配的键的 PseudoFolders 中的其他项目类型条目。 因此，在**项目类型**树中，**数据库项目**将作为子节点的**其他项目类型**。  
  
#### <a name="project-type-child-nodes-and-vstdir-files"></a>项目类型的子节点和.vstdir 文件  
 中的子节点的位置**项目类型**树遵循 ProjectTemplates 文件夹中文件夹的层次结构。 对于机模板 (**Visual Studio 已安装的模板**)，典型位置是 Visual Studio 14.0\Common7\IDE\ProjectTemplates\ \Program Files\Microsoft 和用户模板 (**我模板**)，典型位置是 documents\visual Studio 14.0\Templates\ProjectTemplates\\。 从这两个位置的文件夹层次结构合并以创建**项目类型**树。  
  
 对于 C# 开发人员设置，Visual Studio**项目类型**树类似如下：  
  
 ![项目类型](../../extensibility/internals/media/projecttypes.png "ProjectTypes")  
  
 如下所示的相应 ProjectTemplates 文件夹中：  
  
 ![项目模板](../../extensibility/internals/media/projecttemplates.png "ProjectTemplates")  
  
 时**新的项目**对话框将打开，[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]遍历 ProjectTemplates 文件夹，并重新创建其结构处于**项目类型**树中的一些更改：  
  
- 中的根节点**项目类型**树由应用程序模板。  
  
- 节点名称可本地化，并可包含特殊字符。  
  
- 可以更改排序顺序。  
  
##### <a name="finding-the-root-node-for-a-project-type"></a>查找根节点的项目类型  
 当 Visual Studio 遍历 ProjectTemplates 文件夹时，打开所有的.zip 文件，并提取任何.vstemplate 文件。 .Vstemplate 文件使用 XML 来描述应用程序模板。 有关详细信息，请参阅[生成新项目：实质上，第二部分](../../extensibility/internals/new-project-generation-under-the-hood-part-two.md)。  
  
 \<ProjectType > 标记确定该应用程序的项目类型。 例如，\CSharp\SmartDevice\WindowsCE\1033\WindowsCE-EmptyProject.zip 文件包含具有此标记的 EmptyProject.vstemplate 文件：  
  
```  
<ProjectType>CSharp</ProjectType>  
```  
  
 \<ProjectType > 标记中，并且不在 ProjectTemplates 文件夹中，子文件夹确定中的应用程序的根节点**项目类型**树。 在示例中，Windows CE 应用程序将显示下**Visual C#** 根节点，即使您打算将 WindowsCE 文件夹移动到 VisualBasic 文件夹，Windows CE 应用程序仍会显示在**Visual C#** 根节点。  
  
##### <a name="localizing-the-node-name"></a>本地化的节点名称  
 当 Visual Studio 遍历 ProjectTemplates 文件夹时，它会检查它找到的任何.vstdir 文件。 .Vstdir 文件是 XML 文件，用于控制中的项目类型的外观**新的项目**对话框。 在.vstdir 文件中，使用\<LocalizedName > 标记添加到名称**项目类型**节点。  
  
 例如，\CSharp\Database\TemplateIndex.vstdir 文件包含此标记：  
  
```  
<LocalizedName Package="{462b036f-7349-4835-9e21-bec60e989b9c}" ID="4598"/>  
```  
  
 这将确定在这种情况下，命名的根节点中，已本地化字符串的附属 DLL 和资源 ID**数据库**。 本地化的名称可包含特殊字符所不具备的文件夹名称，如 **.NET**。  
  
 如果没有\<LocalizedName > 标记存在，项目类型命名的文件夹本身**SmartPhone2003**。  
  
##### <a name="finding-the-sort-order-for-a-project-type"></a>查找项目类型的排序顺序  
 若要确定项目类型的排序顺序，.vstdir 文件使用\<SortOrder > 标记。  
  
 例如，\CSharp\Windows\Windows.vstdir 文件包含此标记：  
  
```  
<SortOrder>5</SortOrder>  
```  
  
 \CSharp\Database\TemplateIndex.vstdir 文件具有一个标记具有更大的值：  
  
```  
<SortOrder>5000</SortOrder>  
```  
  
 中的较小数字\<SortOrder > 标记、 更高版本的位置在树中，因此**Windows**节点将显示高于**数据库**中的节点**项目类型**树。  
  
 如果没有\<SortOrder > 标记指定的项目类型，它将显示以下包含任何项目类型的按字母顺序\<SortOrder > 规范。  
  
 请注意在我的文档中没有任何.vstdir 文件 (**我的模板**) 文件夹。 用户应用程序项目类型名称未本地化，且按字母顺序显示。  
  
#### <a name="a-quick-review"></a>快速查看  
 让我们修改**新的项目**对话框并创建一个新的用户项目模板。  
  
1. 将 MyProjectNode 子文件夹添加到 \Program Files\Microsoft Visual Studio 14.0\Common7\IDE\ProjectTemplates\CSharp 文件夹。  
  
2. 使用任何文本编辑器在 MyProjectNode 文件夹中创建 MyProject.vstdir 文件。  
  
3. 将以下行添加到.vstdir 文件：  
  
   ```  
   <TemplateDir Version="1.0.0">  
       <SortOrder>6</SortOrder>  
   </TemplateDir>  
   ```  
  
4. 保存并关闭.vstdir 文件。  
  
5. 使用任何文本编辑器在 MyProjectNode 文件夹中创建 MyProject.vstemplate 文件。  
  
6. 将以下行添加到.vstemplate 文件：  
  
   ```  
   <VSTemplate Version="2.0.0" Type="Project" xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">  
       <TemplateData>  
           <ProjectType>CSharp</ProjectType>  
       </TemplateData>  
   </VSTemplate>  
   ```  
  
7. 保存 the.vstemplate 文件并关闭编辑器。  
  
8. .Vstemplate 文件发送到新的压缩 MyProjectNode\MyProject.zip 文件夹。  
  
9. 从 Visual Studio 命令窗口中，键入：  
  
    ```  
    devenv /installvstemplates  
    ```  
  
   打开 Visual Studio。  
  
10. 打开**新的项目**对话框框中，展开**Visual C#** 项目节点。  
  
    ![MyProjectNode](../../extensibility/internals/media/myprojectnode.png "MyProjectNode")  
  
    **MyProjectNode**显示为子节点的 Visual C# Windows 节点的正下方。  
  
## <a name="see-also"></a>请参阅  
 [生成新项目：揭秘，第 2 部分](../../extensibility/internals/new-project-generation-under-the-hood-part-two.md)
