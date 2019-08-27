---
title: 解决方案 (。Sln) 文件
ms.date: 03/15/2019
ms.topic: conceptual
helpviewer_keywords:
- sln files, VSPackages
- solutions, .sln files
- .sln files, VSPackages
ms.assetid: 7d7ef539-2e4b-4637-b853-8ec7626609df
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 30b0e0b09b12dca964958d5d7b35c6b0d83906fa
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66322610"
---
# <a name="solution-sln-file"></a>解决方案 (.sln) 文件

一种解决方案是用于组织项目在 Visual Studio 中的结构。 该解决方案维护两个文件中的项目的状态信息：

- .sln 文件基于文本的 （共享）

- .suo 文件 （二进制、 用户特定的解决方案选项）

有关.suo 文件的详细信息，请参阅[解决方案用户选项 (。Suo) 文件](../../extensibility/internals/solution-user-options-dot-suo-file.md)。

如果由于所引用的.sln 文件中加载你的 VSPackage，则环境在调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.ReadSolutionProps%2A>.sln 文件中读取。

.Sln 文件包含在环境中使用查找和加载持久化的数据和它所引用的 Vspackage 的项目的名称-值参数的基于文本的信息。 当用户打开一个解决方案时，在环境中循环`preSolution`， `Project`，和`postSolution`.sln 文件，若要加载的解决方案中的信息在解决方案中项目和任何保留的该信息附加到该解决方案。

每个项目的文件包含要填充与该项目的项的层次结构的环境所读取的其他信息。 由项目控制层次结构数据暂留。 尽管数据是不通常存储在.sln 文件中，您可以故意项目信息写入.sln 文件如果你选择这样做。 有关持久性的详细信息，请参阅[项目持久性](../../extensibility/internals/project-persistence.md)并[打开和保存项目项](../../extensibility/internals/opening-and-saving-project-items.md)。

## <a name="file-header"></a>文件标头

.Sln 文件的标头如下所示：

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
（最近） 保存此解决方案文件的 Visual Studio 主版本。 此信息控制的解决方案图标中的版本号。

`VisualStudioVersion = 15.0.26730.15`\
完整 （最近） 保存解决方案文件的 Visual Studio 版本。 如果有相同的主版本的 Visual Studio 的较新版本保存解决方案文件，则此值不会更新以便降低解决方案文件中的改动。

`MinimumVisualStudioVersion = 10.0.40219.1`\
最小 （最旧） 版本的 Visual Studio 可以打开此解决方案文件。

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
（最近） 保存此解决方案文件的 Visual Studio 主版本。 此信息控制的解决方案图标中的版本号。

`VisualStudioVersion = 16.0.28701.123`\
完整 （最近） 保存解决方案文件的 Visual Studio 版本。 如果有相同的主版本的 Visual Studio 的较新版本保存解决方案文件，则此值不会更新以降低文件中的改动。

`MinimumVisualStudioVersion = 10.0.40219.1`\
最小 （最旧） 版本的 Visual Studio 可以打开此解决方案文件。

::: moniker-end

## <a name="file-body"></a>文件正文

.Sln 文件的正文标记的几个部分组成`GlobalSection`，如下所示：

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

若要加载一个解决方案，该环境，请执行以下一系列任务：

1. 在环境中读取的.sln 文件的全局部分并处理标记的所有部分`preSolution`。 在此示例文件中，还有一个此类语句：

   ```
   GlobalSection(SolutionConfiguration) = preSolution
        ConfigName.0 = Debug
        ConfigName.1 = Release
   ```

   当在环境中读取`GlobalSection('name')`标记，它将名称映射到使用注册表的 VSPackage。 密钥名称应存在注册表中 [HKLM\\< 应用程序 ID 注册表根\>\SolutionPersistence\AggregateGUIDs]。 密钥的默认值为编写了项的 VSPackage 的包 GUID (REG_SZ)。

2. 在环境加载 VSPackage，调用`QueryInterface`上的 VSPackage<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps>接口，并调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.ReadSolutionProps%2A>使 VSPackage 能够存储数据的部分中的数据的方法。 环境会为每个重复此过程`preSolution`部分。

3. 项目持久性块循环访问环境。 在这种情况下，没有一个项目。

   ```
   Project("{F184B08F-C81C-45F6-A57F-5ABD9991F28F}") = "Project1",
   "Project1.vbproj", "{8CDD8387-B905-44A8-B5D5-07BB50E05BEA}"
   EndProject
   ```

   此语句包含 GUID 的唯一项目和项目类型 GUID。 在环境使用此信息来查找的项目文件或属于该解决方案的文件和 VSPackage 所需的每个项目。 项目 GUID 传递给<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory>加载特定 VSPackage 项目相关，然后加载该项目是由 VSPackage。 在这种情况下，为此项目加载 VSPackage 是 Visual Basic。

   每个项目可以保留一个唯一的项目实例 ID，以便根据需要由解决方案中的其他项目进行访问。 理想情况下，如果解决方案和项目源代码管理下，项目的路径应相对于解决方案的路径。 首次加载解决方案时，项目文件不能为用户的计算机上。 通过采用相对于解决方案文件服务器上存储的项目文件，是要找出并复制到用户的计算机上的项目文件的相对简单。 然后，再将复制，并加载该项目所需的文件的其余部分。

4. 根据项目一部分的.sln 文件中包含的信息，环境将加载每个项目文件。 项目本身负责，然后填充项目层次结构，并加载任何嵌套的项目。

5. .Sln 文件的所有部分进行都处理后，解决方案将显示在解决方案资源管理器，并可供用户修改。

如果任何 VSPackage 实现项目解决方案中无法加载，<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.OnProjectLoadFailure%2A>调用方法和解决方案中的每个其他项目就会有机会以忽略在加载期间可能已做的更改。 如果出现分析错误，请尽可能多的信息保留使用的解决方案文件，并在环境显示一个对话框，警告用户该解决方案已损坏。

保存或关闭，解决方案时<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.QuerySaveSolutionProps%2A>方法调用并传递给层次结构，以查看是否已对需要为其输入到.sln 文件的解决方案进行了更改。 Null 值，在传递给`QuerySaveSolutionProps`在<xref:Microsoft.VisualStudio.Shell.Interop.VSQUERYSAVESLNPROPS>，指示解决方案保留信息。 如果值不为 null，保持的信息是由指向指针的特定项目<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>接口。

如果没有要保存信息<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence>接口的指针调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.SaveSolutionProps%2A>方法。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.WriteSolutionProps%2A>环境，以检索从名称-值对然后调用方法`IPropertyBag`接口，并将信息写入到.sln 文件。

`SaveSolutionProps` 并`WriteSolutionProps`对象调用以检索从保存信息的环境以递归方式`IPropertyBag`接口之前的所有更改都已都输入到.sln 文件。 这样一来，可以确保信息就会保存解决方案并打开解决方案时可用的下一次。

枚举每个加载的 VSPackage 以查看是否有任何内容将保存到.sln 文件。 它是仅在加载时，查询注册表项。 因为它们是在保存解决方案时在内存中，则环境知道有关所有已加载的包。

只有.sln 文件包含中的条目`preSolution`和`postSolution`部分。 不相似的节中有.suo 文件由于解决方案需要此信息才能正确加载。 .Suo 文件包含特定于用户的选项，如不应被共享或放置在源代码管理下的私人的便笺。

## <a name="see-also"></a>请参阅

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps>
- [解决方案用户选项 (.Suo) 文件](../../extensibility/internals/solution-user-options-dot-suo-file.md)
- [解决方案](../../extensibility/internals/solutions-overview.md)