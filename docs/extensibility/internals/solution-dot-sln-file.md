---
title: 解决方案 （.Sln）文件
ms.date: 03/15/2019
ms.topic: conceptual
helpviewer_keywords:
- sln files, VSPackages
- solutions, .sln files
- .sln files, VSPackages
ms.assetid: 7d7ef539-2e4b-4637-b853-8ec7626609df
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9f4eee1f0a5e8371d239b3c33d10e1d9d7998095
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80705333"
---
# <a name="solution-sln-file"></a>解决方案 （.sln） 文件

解决方案是用于在 Visual Studio 中组织项目的结构。 该解决方案在两个文件中维护项目的状态信息：

- .sln 文件（基于文本的共享）

- .suo 文件（二进制、特定于用户的解决方案选项）

有关 .suo 文件的详细信息，请参阅[解决方案用户选项 （。Suo） 文件](../../extensibility/internals/solution-user-options-dot-suo-file.md)。

如果 VSPackage 是在 .sln 文件中引用的结果加载的，则环境将调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.ReadSolutionProps%2A>.sln 文件中读取。

.sln 文件包含环境用于查找和加载持久化数据和它引用的项目 VS包的名称值参数的基于文本的信息。 当用户打开解决方案时，环境会循环浏览`preSolution``Project`.sln`postSolution`文件中的信息以加载解决方案、解决方案中的项目以及附加到解决方案的任何持久化信息。

每个项目的文件都包含环境读取的其他信息，以便使用该项目的项填充层次结构。 层次结构数据持久性由项目控制。 数据通常不存储在 .sln 文件中，尽管如果您选择这样做，则可以有意将项目信息写入 .sln 文件。 有关持久性的详细信息，请参阅[项目持久性](../../extensibility/internals/project-persistence.md)以及[打开和保存项目项](../../extensibility/internals/opening-and-saving-project-items.md)。

## <a name="file-header"></a>文件头

.sln 文件的标头如下所示：

::: moniker range="vs-2017"

```
Microsoft Visual Studio Solution File, Format Version 12.00
# Visual Studio 15
VisualStudioVersion = 15.0.26730.15
MinimumVisualStudioVersion = 10.0.40219.1
```

### <a name="definitions"></a>定义

`Microsoft Visual Studio Solution File, Format Version 12.00`\
定义文件格式版本的标准标头。

`# Visual Studio 15`\
主要版本的 Visual Studio（最近）保存了此解决方案文件。 此信息控制解决方案图标中的版本号。

`VisualStudioVersion = 15.0.26730.15`\
完整版本的 Visual Studio（最近）保存了解决方案文件。 如果解决方案文件由具有相同主版本的较新版本的 Visual Studio 保存，则不会更新此值，以减少解决方案文件中的改动。

`MinimumVisualStudioVersion = 10.0.40219.1`\
可以打开此解决方案文件的可视化工作室的最小（最旧）版本。

::: moniker-end

::: moniker range=">=vs-2019"

```
Microsoft Visual Studio Solution File, Format Version 12.00
# Visual Studio Version 16
VisualStudioVersion = 16.0.28701.123
MinimumVisualStudioVersion = 10.0.40219.1
```

### <a name="definitions"></a>定义

`Microsoft Visual Studio Solution File, Format Version 12.00`\
定义文件格式版本的标准标头。

`# Visual Studio Version 16`\
主要版本的 Visual Studio（最近）保存了此解决方案文件。 此信息控制解决方案图标中的版本号。

`VisualStudioVersion = 16.0.28701.123`\
完整版本的 Visual Studio（最近）保存了解决方案文件。 如果解决方案文件由具有相同主版本的较新版本的 Visual Studio 保存，则不会更新此值，以减少文件中的改动。

`MinimumVisualStudioVersion = 10.0.40219.1`\
可以打开此解决方案文件的可视化工作室的最小（最旧）版本。

::: moniker-end

## <a name="file-body"></a>文件正文

.sln 文件的主体由标记`GlobalSection`的几个部分组成，如下所示：

```
Project("{F184B08F-C81C-45F6-A57F-5ABD9991F28F}") = "Project1", "Project1.vbproj", "{8CDD8387-B905-44A8-B5D5-07BB50E05BEA}"
EndProject
Global
  GlobalSection(SolutionNotes) = postSolution
  EndGlobalSection
  GlobalSection(SolutionConfiguration) = preSolution
       ConfigName.0 = Debug
       ConfigName.1 = Release
  EndGlobalSection
  GlobalSection(ProjectDependencies) = postSolution
  EndGlobalSection
  GlobalSection(ProjectConfiguration) = postSolution
   {8CDD8387-B905-44A8-B5D5-07BB50E05BEA}.Debug.ActiveCfg = Debug|x86
   {8CDD8387-B905-44A8-B5D5-07BB50E05BEA}.Debug.Build.0 = Debug|x86
   {8CDD8387-B905-44A8-B5D5-07BB50E05BEA}.Release.ActiveCfg = Release|x86
   {8CDD8387-B905-44A8-B5D5-07BB50E05BEA}.Release.Build.0 = Release|x86
  EndGlobalSection
  GlobalSection(ExtensibilityGlobals) = postSolution
  EndGlobalSection
  GlobalSection(ExtensibilityAddIns) = postSolution
  EndGlobalSection
EndGlobal
```

要加载解决方案，环境将执行以下任务序列：

1. 环境读取 .sln 文件的全局部分，并处理标记`preSolution`的所有部分。 在此示例中文件中，有一个这样的语句：

   ```
   GlobalSection(SolutionConfiguration) = preSolution
        ConfigName.0 = Debug
        ConfigName.1 = Release
   ```

   当环境读取标记时`GlobalSection('name')`，它将名称映射到使用注册表的 VSPackage。 密钥名称应存在于注册表中[HKLM\\<应用程序 ID 注册表根\>[解决方案持久性]聚合 GUIDs]下。 键的默认值是写入条目的 VSPackage 的包 GUID（REG_SZ）。

2. 环境加载 VSPackage，调用`QueryInterface`<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps>接口的 VSPackage，并在节中使用数据调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.ReadSolutionProps%2A>该方法，以便 VSPackage 可以存储数据。 环境将为每个`preSolution`部分重复此过程。

3. 环境通过项目持久性块进行遍发。 在这种情况下，有一个项目。

   ```
   Project("{F184B08F-C81C-45F6-A57F-5ABD9991F28F}") = "Project1",
   "Project1.vbproj", "{8CDD8387-B905-44A8-B5D5-07BB50E05BEA}"
   EndProject
   ```

   此语句包含唯一的项目 GUID 和项目类型 GUID。 环境使用此信息查找属于解决方案的项目文件或文件，以及每个项目所需的 VSPackage。 项目 GUID 传递给以<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory>加载与项目相关的特定 VS 包，然后由 VSPackage 加载项目。 在这种情况下，为此项目加载的 VS 包是可视化基本。

   每个项目都可以保留一个唯一的项目实例 ID，以便解决方案中的其他项目可以根据需要访问它。 理想情况下，如果解决方案和项目处于源代码控制之下，则项目的路径应相对于解决方案的路径。 首次加载解决方案时，项目文件不能位于用户的计算机上。 通过将项目文件相对于解决方案文件存储在服务器上，找到项目文件并将其复制到用户的计算机相对简单。 然后，它复制并加载项目所需的其余文件。

4. 根据 .sln 文件的项目部分中包含的信息，环境将加载每个项目文件。 然后，项目本身负责填充项目层次结构并加载任何嵌套项目。

5. 处理 .sln 文件的所有部分后，解决方案将显示在解决方案资源管理器中，并可供用户修改。

如果实现解决方案中项目的任何 VSPackage 无法加载，则调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.OnProjectLoadFailure%2A>该方法，并且解决方案中的每个其他项目都有机会忽略它在加载过程中可能所做的更改。 如果发生分析错误，解决方案文件将保留尽可能多的信息，环境将显示一个对话框，警告用户解决方案已损坏。

保存或关闭解决方案时，<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.QuerySaveSolutionProps%2A>将调用该方法并将其传递给层次结构，以查看是否对需要输入到 .sln 文件中的解决方案进行了更改。 传入`QuerySaveSolutionProps`到 的<xref:Microsoft.VisualStudio.Shell.Interop.VSQUERYSAVESLNPROPS>null 值 表示正在为解决方案持久化信息。 如果值不为空，则持久化的信息适用于特定项目，由指向接口的<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>指针确定。

如果有要保存的信息，<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence>则使用指向 方法的<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.SaveSolutionProps%2A>指针调用接口。 然后<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.WriteSolutionProps%2A>，环境调用该方法，从`IPropertyBag`接口检索名称值对并将信息写入 .sln 文件。

`SaveSolutionProps`环境`WriteSolutionProps`递归地调用对象，以检索要从接口保存的信息，`IPropertyBag`直到所有更改都输入到 .sln 文件中。 通过这种方式，您可以确保信息将保留到解决方案中，并在下次打开解决方案时可用。

将枚举每个加载的 VSPackage 以查看它是否有要保存到 .sln 文件的东西。 只有在加载时查询注册表项。 环境知道所有加载的包，因为它们在保存解决方案时位于内存中。

只有 .sln 文件包含 和`preSolution``postSolution`节中的条目。 .suo 文件中没有类似的部分，因为解决方案需要此信息才能正确加载。 .suo 文件包含用户特定的选项，如专用注释，这些选项不打算共享或置于源代码控制之下。

## <a name="see-also"></a>请参阅

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps>
- [解决方案用户选项 (.Suo) 文件](../../extensibility/internals/solution-user-options-dot-suo-file.md)
- [解决方案](../../extensibility/internals/solutions-overview.md)
