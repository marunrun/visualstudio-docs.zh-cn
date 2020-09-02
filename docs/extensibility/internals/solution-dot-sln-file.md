---
title: 解决方案 (。.Sln) 文件
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80705333"
---
# <a name="solution-sln-file"></a>解决方案 ( .sln) 文件

解决方案是在 Visual Studio 中组织项目的结构。 解决方案维护两个文件中的项目的状态信息：

- .sln 文件 (基于文本的共享) 

- .suo 文件 (二进制，特定于用户的解决方案选项) 

有关 .suo 文件的详细信息，请参阅 [解决方案用户选项 (。.Suo) 文件](../../extensibility/internals/solution-user-options-dot-suo-file.md)。

如果由于在 .sln 文件中引用了 VSPackage，则环境将调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.ReadSolutionProps%2A> 以在 .sln 文件中读取。

.Sln 文件包含基于文本的信息，环境使用该信息查找并加载持久数据的名称-值参数和它引用的项目 Vspackage。 当用户打开解决方案时，环境会循环遍历 `preSolution` `Project` `postSolution` .sln 文件中的、和信息，以加载解决方案、解决方案中的项目以及附加到解决方案的任何持久性信息。

每个项目的文件都包含环境读取的其他信息，以使用该项目的项填充层次结构。 层次结构数据持久性由项目控制。 数据通常不会存储在 .sln 文件中，但如果您选择这样做，您可以有意地将项目信息写入 .sln 文件。 有关持久性的详细信息，请参阅 [项目持久性](../../extensibility/internals/project-persistence.md) 和 [打开和保存项目项](../../extensibility/internals/opening-and-saving-project-items.md)。

## <a name="file-header"></a>文件头

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
 (最近) 保存此解决方案文件的 Visual Studio 的主要版本。 此信息控制解决方案图标中的版本号。

`VisualStudioVersion = 15.0.26730.15`\
 (最近) 保存解决方案文件的 Visual Studio 的完整版本。 如果解决方案文件是由较新版本的 Visual Studio （具有相同的主版本）保存的，则不会更新此值，以减少解决方案文件中的更改。

`MinimumVisualStudioVersion = 10.0.40219.1`\
可以打开此解决方案文件的最早) 版本的 Visual Studio (。

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
 (最近) 保存此解决方案文件的 Visual Studio 的主要版本。 此信息控制解决方案图标中的版本号。

`VisualStudioVersion = 16.0.28701.123`\
 (最近) 保存解决方案文件的 Visual Studio 的完整版本。 如果解决方案文件是由较新版本的 Visual Studio （具有相同的主版本）保存的，则不会更新此值，以减少文件中的更改。

`MinimumVisualStudioVersion = 10.0.40219.1`\
可以打开此解决方案文件的最早) 版本的 Visual Studio (。

::: moniker-end

## <a name="file-body"></a>文件正文

.Sln 文件的主体由若干部分标记 `GlobalSection` ，如下所示：

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

若要加载解决方案，环境将执行以下任务序列：

1. 环境将读取 .sln 文件的全局部分，并处理标记的所有部分 `preSolution` 。 在此示例文件中，有一个这样的语句：

   ```
   GlobalSection(SolutionConfiguration) = preSolution
        ConfigName.0 = Debug
        ConfigName.1 = Release
   ```

   当环境读取标记时 `GlobalSection('name')` ，它将使用注册表将名称映射到 VSPackage。 注册表项名称应存在于 [HKLM \\<APPLICATION ID Registry Root \SolutionPersistence\AggregateGUIDs] 下的注册表中 \> 。 密钥的默认值是写入条目的 VSPackage REG_SZ) 的包 GUID (。

2. 环境加载 VSPackage，对接口调用 `QueryInterface` VSPackage， <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps> 并 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.ReadSolutionProps%2A> 通过节中的数据调用方法，以便 VSPackage 可以存储数据。 环境为每个部分重复此过程 `preSolution` 。

3. 环境循环访问项目持久性块。 在这种情况下，有一个项目。

   ```
   Project("{F184B08F-C81C-45F6-A57F-5ABD9991F28F}") = "Project1",
   "Project1.vbproj", "{8CDD8387-B905-44A8-B5D5-07BB50E05BEA}"
   EndProject
   ```

   此语句包含唯一项目 GUID 和项目类型 GUID。 环境使用此信息来查找项目文件或属于解决方案的文件，以及每个项目所需的 VSPackage。 项目 GUID 传递到 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory> 以加载与项目相关的特定 VSPackage，然后由 VSPackage 加载项目。 在这种情况下，为此项目加载的 VSPackage Visual Basic。

   每个项目都可以保留唯一的项目实例 ID，以便可以根据解决方案中的其他项目的需要对其进行访问。 理想情况下，如果解决方案和项目处于源代码管理下，则项目的路径应相对于解决方案的路径。 首次加载解决方案时，项目文件不能在用户的计算机上。 通过将项目文件与解决方案文件相关，将项目文件存储在服务器上，可以找到项目文件并将其复制到用户的计算机。 然后，它会复制并加载项目所需的其他文件。

4. 根据 .sln 文件的 "项目" 部分中包含的信息，环境将加载每个项目文件。 然后，项目本身负责填充项目层次结构并加载任何嵌套的项目。

5. 处理 .sln 文件的所有部分后，解决方案将显示在 "解决方案资源管理器中，并可供用户修改。

如果在解决方案中实现项目的任何 VSPackage 都无法加载，则会 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.OnProjectLoadFailure%2A> 调用方法，并且解决方案中的每个项目都有机会忽略在加载过程中可能已进行的更改。 如果发生分析错误，解决方案文件中将保留尽可能多的信息，并且环境会显示一个对话框，警告用户解决方案已损坏。

保存或关闭解决方案时，将 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.QuerySaveSolutionProps%2A> 调用方法并将其传递给层次结构，以查看是否已对需要输入 .sln 文件的解决方案进行了更改。 传入的中的 null 值 `QuerySaveSolutionProps` 指示该 <xref:Microsoft.VisualStudio.Shell.Interop.VSQUERYSAVESLNPROPS> 解决方案的信息是持久的。 如果值不为 null，则保留的信息针对特定项目，由指向接口的指针确定 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> 。

如果有要保存的信息，则 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence> 使用指向方法的指针调用接口 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.SaveSolutionProps%2A> 。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.WriteSolutionProps%2A>然后，环境将调用方法，以从接口检索名称/值对 `IPropertyBag` ，并将信息写入 .sln 文件。

`SaveSolutionProps` 和 `WriteSolutionProps` 对象由环境以递归方式调用，以检索要从接口保存的信息， `IPropertyBag` 直到将所有更改都输入到 .sln 文件中为止。 通过这种方式，您可以确保信息将随解决方案一起保存，并且在下次打开解决方案时可用。

枚举每个加载的 VSPackage，以查看它是否有任何内容保存到 .sln 文件。 仅在加载时才对注册表项进行查询。 环境知道所有加载的包，因为这些包在保存解决方案时位于内存中。

只有 .sln 文件包含和节中的条目 `preSolution` `postSolution` 。 .Suo 文件中没有类似的部分，因为解决方案需要此信息才能正确加载。 .Suo 文件包含特定于用户的选项，如专用说明，这些选项不应在源代码管理下共享或放置。

## <a name="see-also"></a>另请参阅

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps>
- [解决方案用户选项 (.Suo) 文件](../../extensibility/internals/solution-user-options-dot-suo-file.md)
- [解决方案](../../extensibility/internals/solutions-overview.md)
