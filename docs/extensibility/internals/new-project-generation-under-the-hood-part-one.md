---
title: 新项目生成：在引擎盖下，第一部分 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio], new project dialog
- projects [Visual Studio], new project generation
ms.assetid: 66778698-0258-467d-8b8b-c351744510eb
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: aca35e85e57a07a2b411a23d81b99cff9983b9c2
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707056"
---
# <a name="new-project-generation-under-the-hood-part-one"></a>生成新项目：揭秘，第 1 部分
曾经考虑过如何创建自己的项目类型？ 想知道创建新项目时实际会发生什么情况？ 让我们看看引擎盖下，看看到底发生了什么。

 Visual Studio 为您协调了几个任务：

- 它显示所有可用项目类型的树。

- 它显示每个项目类型的应用程序模板列表，并允许您选择一个模板。

- 它收集应用程序的项目信息，如项目名称和路径。

- 它将此信息传递给项目工厂。

- 它在当前解决方案中生成项目项和文件夹。

## <a name="the-new-project-dialog-box"></a>新项目对话框
 当您为新项目选择项目类型时，一切就开始了。 让我们首先单击 **"文件**"菜单上的 **"新项目**"。 此时将显示 **"新项目**"对话框，如下所示：

 ![“新建项目”对话框](../../extensibility/internals/media/newproject.gif "NewProject")

 接下来将更详细地介绍。 "**项目类型"** 树列出了您可以创建的各种项目类型。 当您选择项目类型（如**Visual C# Windows）** 时，您将看到一个应用程序模板列表来帮助您入门。 **Visual Studio 安装的模板**由 Visual Studio 安装，可供计算机的任何用户使用。 您创建或收集的新模板可以添加到 **"我的模板"中**，并且仅对您可用。

 当您选择像 Windows**应用程序**这样的模板时，应用程序类型的说明将显示在对话框中;但是，在对话框中，将显示应用程序类型的说明。在这种情况下，**用于使用 Windows 用户界面创建应用程序的项目**。

 在 **"新项目"** 对话框的底部，您将看到几个收集详细信息的控件。 您看到的控件取决于项目类型，但通常包括项目**名称**文本框、**位置**文本框和相关 **"浏览"** 按钮，以及**解决方案名称**文本框和**解决方案的相关"创建目录**"复选框。

## <a name="populating-the-new-project-dialog-box"></a>填充新项目对话框
 **新项目**对话框从何处获取其信息？ 这里有两种机制在起作用，其中一种是弃用的。 "**新项目**"对话框合并并显示从这两个机制获得的信息。

 较旧的（已弃用）方法使用系统注册表项和 .vsdir 文件。 此机制在可视化工作室打开时运行。 较新的方法使用 .vstemplate 文件。 此机制在可视化工作室初始化时运行，例如，通过运行

```
devenv /setup
```

 或

```
devenv /installvstemplates
```

### <a name="project-types"></a>项目类型
 **Project 类型**根节点（如**Visual C#** **和其他语言**）的位置和名称由系统注册表项确定。 子节点（如**数据库**和**智能设备**）的组织镜像包含相应 .vstemplate 文件的文件夹的层次结构。 让我们先看一下根节点。

#### <a name="project-type-root-nodes"></a>项目类型根节点
 初始[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]化时，它将遍历系统注册表项HKEY_LOCAL_MACHINE_SOFTWARE_Microsoft_VisualStudio_14.0_NewProjectTemplates_TemplateDirs 的子键，以生成和命名**项目类型**树的根节点。 此信息将缓存供以后使用。 查看模板 Dirs\\[FAE04EC1-301F-11D3-BF4B-00C04F79EFBC]\\/1 键。 每个条目都是 VSPackage GUID。 子键 （/1） 的名称将被忽略，但其存在表明这是**项目类型**根节点。 根节点可能又具有多个子键，这些子键控制其在**Project 类型**树中的外观。 让我们来看看其中的一些。

##### <a name="default"></a>（默认值）
 这是命名根节点的本地化字符串的资源 ID。 字符串资源位于 VSPackage GUID 选择的卫星 DLL 中。

 在此示例中，VS 包 GUID 是

 [FAE04EC1-301F-11D3-BF4B-00C04F79EFBC]

 根节点 （/1） 的资源 ID（默认值）#2345

 如果在附近的"包"键中查找 GUID 并检查 SatelliteDll 子键，则可以找到包含字符串资源的程序集的路径：

 \<视觉工作室安装路径>_VC_VCS 包\1033\csprojui.dll

 要验证这一点，请打开文件资源管理器并将 csprojui.dll 拖动到可视化工作室目录中。 字符串表显示资源#2345具有 Visual **C#** 的标题。

##### <a name="sortpriority"></a>排序优先级
 这将确定根节点在**项目类型**树中的位置。

 排序优先级REG_DWORD 0x00000014 （20）

 优先级的数量越低，树中的位置越高。

##### <a name="developeractivity"></a>开发人员活动
 如果存在此子键，则根节点的位置由"开发人员设置"对话框控制。 例如，

 开发人员活动REG_SZ VC#

 指示如果为[!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)]开发设置了 Visual Studio，则 Visual C++ 将成为根节点。 否则，它将是**其他语言**的子节点。

##### <a name="folder"></a>Folder
 如果存在此子键，则根节点将成为指定文件夹的子节点。 该键下将显示可能的文件夹列表

 HKEY_LOCAL_MACHINE_SOFTWARE_微软_VisualStudio_11.0\新项目模板\伪文件夹

 例如，数据库项目条目具有与伪文件夹中的"其他项目类型"条目匹配的文件夹键。 因此，在**项目类型**树中，**数据库项目**将是**其他项目类型的**子节点。

#### <a name="project-type-child-nodes-and-vstdir-files"></a>项目类型 子节点和 .vstdir 文件
 **"项目类型"** 树中的子节点的位置遵循 ProjectTemplates 文件夹中文件夹的层次结构。 对于机器模板 **（Visual Studio 安装的模板**），典型位置是 [程序文件]微软可视化工作室 14.0\Common7_IDE_ProjectTemplates]和用户模板（**我的模板**），典型位置是 [我的文档]Visual Studio 14.0_模板\项目模板\\。 合并这两个位置的文件夹层次结构以创建**项目类型**树。

 对于具有 C# 开发人员设置的可视化工作室，**项目类型**树如下所示：

 ![项目类型](../../extensibility/internals/media/projecttypes.png "项目类型")

 相应的 ProjectTemplates 文件夹如下所示：

 ![项目模板](../../extensibility/internals/media/projecttemplates.png "项目模板")

 打开 **"新项目**"对话框时，[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]遍历 ProjectTemplates 文件夹，并在 **"项目类型**"树中重新创建其结构，并进行一些更改：

- **项目类型**树中的根节点由应用程序模板确定。

- 节点名称可以本地化，可以包含特殊字符。

- 可以更改排序顺序。

##### <a name="finding-the-root-node-for-a-project-type"></a>查找项目类型的根节点
 当 Visual Studio 遍历 ProjectTemplates 文件夹时，它会打开所有 .zip 文件并提取任何 .vstemplate 文件。 .vstemplate 文件使用 XML 来描述应用程序模板。 有关详细信息，请参阅[新项目生成：在罩下，第二部分](../../extensibility/internals/new-project-generation-under-the-hood-part-two.md)。

 项目\<类型>标记确定应用程序的项目类型。 例如，[CSharp]智能设备\WindowsCE_1033_WindowsCE-emptyProject.zip 文件包含一个 EmptyProject.vstemplate 文件，该文件具有以下标记：

```
<ProjectType>CSharp</ProjectType>
```

 ProjectType>\<标记（而不是 ProjectTemplates 文件夹中的子文件夹）确定 **"项目类型**"树中的应用程序的根节点。 在此示例中，Windows CE 应用程序将显示在 Visual **C++** 根节点下，即使您要将 WindowsCE 文件夹移动到 VisualBasic 文件夹，Windows CE 应用程序仍将显示在**Visual C++** 根节点下。

##### <a name="localizing-the-node-name"></a>本地化节点名称
 当 Visual Studio 遍历 ProjectTemplates 文件夹时，它会检查它找到的任何 .vstdir 文件。 .vstdir 文件是一个 XML 文件，用于控制项目类型在 **"新项目"** 对话框中的外观。 在 .vstdir 文件中，使用\<本地化名称>标记来命名**项目类型**节点。

 例如，[CSharp]数据库_模板索引.vstdir 文件包含此标记：

```
<LocalizedName Package="{462b036f-7349-4835-9e21-bec60e989b9c}" ID="4598"/>
```

 这将确定命名根节点的本地化字符串的附属 DLL 和资源 ID，在这种情况下，**为数据库**。 本地化名称可以包含不适用于文件夹名称的特殊字符，例如 **.NET**。

 如果不存在\<本地化名称>标记，则项目类型由文件夹本身**称为 SmartPhone2003**。

##### <a name="finding-the-sort-order-for-a-project-type"></a>查找项目类型的排序顺序
 要确定项目类型的排序顺序，.vstdir 文件使用\<SortOrder> 标记。

 例如，[CSharp]Windows_Windows.vstdir 文件包含此标记：

```
<SortOrder>5</SortOrder>
```

 [CSharp]数据库_模板索引.vstdir 文件具有具有较大值的标记：

```
<SortOrder>5000</SortOrder>
```

 "SortOrder"> 标记中的数字越低，树中的位置越高，因此**Windows**节点看起来高于**项目类型**树中的数据库节点。 **Database** \<

 如果未\<为项目类型指定 SortOrder>标记，则它按字母顺序显示，遵循包含\<SortOrder>规范的任何项目类型。

 请注意，"我的文档（**我的模板**）"文件夹中没有 .vstdir 文件。 用户应用程序项目类型名称未本地化，按字母顺序显示。

#### <a name="a-quick-review"></a>快速回顾
 让我们修改 **"新项目**"对话框并创建新的用户项目模板。

1. 将 MyProjectNode 子文件夹添加到 [程序文件]微软可视化工作室 14.0_Common7_IDE_ProjectTemplates_CSharp 文件夹。

2. 使用任何文本编辑器在 MyProjectNode 文件夹中创建 MyProject.vstdir 文件。

3. 将这些行添加到 .vstdir 文件：

   ```
   <TemplateDir Version="1.0.0">
       <SortOrder>6</SortOrder>
   </TemplateDir>
   ```

4. 保存并关闭 .vstdir 文件。

5. 使用任何文本编辑器在 MyProjectNode 文件夹中创建 MyProject.vstemplate 文件。

6. 将这些行添加到 .vstemplate 文件：

   ```
   <VSTemplate Version="2.0.0" Type="Project" xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
       <TemplateData>
           <ProjectType>CSharp</ProjectType>
       </TemplateData>
   </VSTemplate>
   ```

7. 保存.vstemplate 文件并关闭编辑器。

8. 将 .vstemplate 文件发送到新的压缩 MyProjectNode_MyProject.zip 文件夹。

9. 从可视化工作室命令窗口中，键入：

    ```
    devenv /installvstemplates
    ```

   打开 Visual Studio。

10. 打开 **"新项目**"对话框并展开可视化**C#** 项目节点。

    ![MyProjectNode](../../extensibility/internals/media/myprojectnode.png "MyProjectNode")

    **MyProjectNode**显示为 Windows 节点下的 Visual C++ 的子节点。

## <a name="see-also"></a>请参阅
- [生成新项目：揭秘，第 2 部分](../../extensibility/internals/new-project-generation-under-the-hood-part-two.md)
