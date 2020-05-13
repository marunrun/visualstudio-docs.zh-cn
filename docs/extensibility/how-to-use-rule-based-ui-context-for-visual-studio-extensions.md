---
title: 操作方式：将基于规则的 UI 上下文用于可视化工作室扩展 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 8dd2cd1d-d8ba-49b9-870a-45acf3a3259d
author: acangialosi
ms.author: anthc
ms.workload:
- vssdk
ms.openlocfilehash: de1a1e0a2022482433f81b0b2810b0d201ab7b8f
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80710598"
---
# <a name="how-to-use-rule-based-ui-context-for-visual-studio-extensions"></a>操作方式：将基于规则的 UI 上下文用于可视化工作室扩展

当激活某些已知<xref:Microsoft.VisualStudio.Shell.UIContext>组件时，Visual Studio 允许加载 VS 包。 但是，这些 UI 上下文不是细粒度的，这使得扩展作者别无选择，只能选择一个可用的 UI 上下文，该上下文在真正希望 VSPackage 加载的点之前激活。 有关已知 UI 上下文的列表，请参阅<xref:Microsoft.VisualStudio.Shell.KnownUIContexts>。

加载包可能会对性能产生影响，并且加载它们的时间不是最佳做法。 Visual Studio 2015 引入了基于规则的 UI 上下文的概念，该机制允许扩展作者定义激活 UI 上下文并加载关联的 VS 包的确切条件。

## <a name="rule-based-ui-context"></a>基于规则的 UI 上下文

"规则"由新的 UI 上下文 （GUID） 和布尔表达式组成，这些表达式引用一个或多个"术语"，并结合逻辑"和"，"或"，"不"操作。 "术语"在运行时动态计算，每当表达式的任何术语发生更改时，都会重新评估表达式。 当表达式计算为 true 时，关联的 UI 上下文将激活。 否则，UI 上下文将取消激活。

基于规则的 UI 上下文可通过多种方式使用：

1. 指定命令和工具窗口的可见性约束。 您可以隐藏命令/工具窗口，直到满足 UI 上下文规则。

2. 作为自动加载约束：仅在满足规则时自动加载包。

3. 作为延迟任务：延迟加载，直到指定间隔过去，并且仍满足规则。

   任何视觉工作室扩展都可以使用该机制。

## <a name="create-a-rule-based-ui-context"></a>创建基于规则的 UI 上下文
 假设您有一个名为 TestPackage 的扩展名，它提供了一个菜单命令，该命令仅适用于具有 *.config*扩展名的文件。 在 VS2015 之前，最佳选项是在激活 UI<xref:Microsoft.VisualStudio.Shell.KnownUIContexts.SolutionExistsAndFullyLoadedContext%2A>上下文时加载测试包。 以这种方式加载 TestPackage 效率不高，因为加载的解决方案可能甚至不包含 *.config*文件。 这些步骤演示如何仅在选择*具有 .config*扩展名的文件时才使用基于规则的 UI 上下文来激活 UI 上下文，并在激活该 UI 上下文时加载 TestPackage。

1. 定义新的 UIContext GUID 并添加到 VSPackage <xref:Microsoft.VisualStudio.Shell.ProvideAutoLoadAttribute> <xref:Microsoft.VisualStudio.Shell.ProvideUIContextRuleAttribute>类和 。

    例如，假设要添加新的 UIContext"UIContextGuid"。 创建的 GUID（您可以通过单击 **"工具** > **创建 GUID"创建 GUID）** 是"8B40D5E2-5626-42AE-99EF-3DD1EFF46E7B"。 然后，在包类中添加以下声明：

   ```csharp
   public const string UIContextGuid = "8B40D5E2-5626-42AE-99EF-3DD1EFF46E7B";
   ```

    对于属性，添加以下值：（稍后将介绍这些属性的详细信息）

   ```csharp
   [ProvideAutoLoad(TestPackage.UIContextGuid)]
   [ProvideUIContextRule(TestPackage.UIContextGuid,
       name: "Test auto load",
       expression: "DotConfig",
       termNames: new[] { "DotConfig" },
       termValues: new[] { "HierSingleSelectionName:.config$" })]
   ```

    这些元数据定义了新的 UIContext GUID （8B40D5E2-5626-42AE-99EF-3DD1EFF46E7B） 和一个引用单个术语"DotConfig"的表达式。 当活动层次结构中的当前选择具有与正则表达式模式".config$"（\\以 .config 结尾）的名称匹配时，"DotConfig"项将 *.config*计算为 true。 （默认）值为可用于调试的规则定义可选名称。

    属性的值将添加到生成期间生成的 pkgdef 中。

2. 在测试包命令的 VSCT 文件中，将"动态可见性"标志添加到相应的命令：

   ```xml
   <CommandFlag>DynamicVisibility</CommandFlag>
   ```

3. 在 VSCT 的可见性部分中，将适当的命令与#1中定义的新 UIContext GUID 进行连接：

   ```xml
   <VisibilityConstraints>
       <VisibilityItem guid="guidTestPackageCmdSet" id="TestId"  context="UIContextGuid"/>
   </VisibilityConstraints>
   ```

4. 在"符号"部分中，添加 UIContext 的定义：

   ```xml
   <GuidSymbol name="UIContextGuid" value="{8B40D5E2-5626-42AE-99EF-3DD1EFF46E7B}" />
   ```

    现在，*\*仅当*解决方案资源管理器中的选定项为 *.config*文件且在选择其中一个命令之前不会加载包时，.config 文件的上下文菜单命令才会可见。

   接下来，使用调试器确认包仅在预期加载时加载。 要调试测试包：

5. 在<xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A>方法中设置断点。

6. 生成测试包并开始调试。

7. 创建项目或打开项目。

8. 选择扩展*名以外的任何*文件。不应命中断点。

9. 选择*App.Config*文件。

   测试包在断点加载和停止。

## <a name="add-more-rules-for-ui-context"></a>为 UI 上下文添加更多规则
 由于 UI 上下文规则是布尔表达式，因此可以为 UI 上下文添加更多受限制的规则。 例如，在上面的 UI 上下文中，可以指定规则仅在加载具有项目的解决方案时才适用。 这样，如果将 *.config*文件作为独立文件而不是作为项目的一部分打开，则命令不会显示。

```csharp
[ProvideAutoLoad(TestPackage.UIContextGuid)]
[ProvideUIContextRule(TestPackage.UIContextGuid,
    name: "Test auto load",
    expression: "(SingleProject | MultipleProjects) & DotConfig",
    termNames: new[] { "SingleProject", "MultipleProjects","DotConfig" },
    termValues: new[] { VSConstants.UICONTEXT_SolutionHasSingleProject_string , VSConstants.UICONTEXT_SolutionHasMultipleProjects_string , "HierSingleSelectionName:.config$" })]
```

 现在表达式引用三个术语。 前两个术语"单一项目"和"多项目"是指其他知名 UI 上下文（由其 GUID）。 第三个术语"DotConfig"是本文前面定义的基于规则的 UI 上下文。

## <a name="delayed-activation"></a>延迟激活
 规则可以具有可选的"延迟"。 延迟以毫秒为单位指定。 如果存在，则延迟会导致规则的 UI 上下文的激活或停用延迟到该时间间隔。 如果规则在延迟间隔之前更改回来，则没有任何反应。 此机制可用于"错开"初始化步骤 - 尤其是一次性初始化，而无需依赖计时器或注册空闲通知。

 例如，您可以指定测试负载规则具有 100 毫秒的延迟：

```csharp
[ProvideAutoLoad(TestPackage.UIContextGuid)]
[ProvideUIContextRule(TestPackage.UIContextGuid,
    name: "Test auto load",
    expression: "DotConfig",
    termNames: new[] { "DotConfig" },
    termValues: new[] { "HierSingleSelectionName:.config$" },
    delay: 100)]
```

## <a name="term-types"></a>术语类型

以下是支持的各种术语类型：

|术语|描述|
|-|-|
|[nnnnnn-nnnn-nnnn-nnnn-nnnnnnnnnnnnnnnnnnnnnnnnnnnn]|GUID 引用 UI 上下文。 每当 UI 上下文处于活动状态且 false 否则，该术语将为 true。|
|Hier 单选名称\<：图案>|每当活动层次结构中的选择是单个项且所选项的名称与"pattern"给出的 .net 正则表达式匹配时，术语将为 true。|
|用户设置存储查询：\<查询>|"查询"表示进入用户设置存储的完整路径，该路径必须计算为非零值。 查询在最后一个斜杠上拆分为"集合"和"属性名称"。|
|配置设置存储查询：\<查询>|"查询"表示进入配置设置存储的完整路径，该路径必须计算为非零值。 查询在最后一个斜杠上拆分为"集合"和"属性名称"。|
|活动项目口味：\<项目类型>|每当当前选定的项目具有调味料（聚合），并且具有与给定项目类型 GUID 匹配的味道时，该术语将为 true。|
|活动编辑器内容类型：\<内容类型>|当所选文档是具有给定内容类型的文本编辑器时，术语将为 true。 注意：重命名所选文档时，在关闭并重新打开文件之前，此术语不会刷新。|
|活动项目功能：\<表达式>|当活动项目功能与提供的表达式匹配时，该术语为 true。 表达式可以是类似于 VB &#124; CSharp。|
|解决方案具有项目能力：\<表达式>|与上面类似，但当解决方案具有与表达式匹配的任何加载项目时，术语为 true。|
|解决方案HasProjectFlavor：\<项目类型>|每当解决方案具有具有调味料（聚合）且具有与给定项目类型 GUID 匹配的风味时，该术语将是正确的。|
|项目添加项目：\<模式>| 当将匹配"模式"的文件添加到打开的 soluion 中的项目中时，该术语为 true。|
|活动项目输出类型：\<输出类型>|当活动项目的输出类型完全匹配时，术语为 true。  输出类型可以是整数或<xref:Microsoft.VisualStudio.Shell.Interop.__VSPROJOUTPUTTYPE>类型。|
|活动项目构建属性：\<构建财产>\<= 正则>|当活动项目具有指定的生成属性和属性值与提供的 regex 筛选器匹配时，该术语为 true。 有关生成属性的更多详细信息，请参阅[MSBuild 项目文件中的持久数据](internals/persisting-data-in-the-msbuild-project-file.md)。|
|解决方案HasProjectBuild属性：\<构建财产>\<= 正则>|当解决方案具有与提供的 regex 筛选器匹配的加载项目且具有指定的生成属性和属性值匹配时，该术语为 true。|

## <a name="compatibility-with-cross-version-extension"></a>与跨版本扩展兼容

基于规则的 UI 上下文是 Visual Studio 2015 中的新功能，不会移植到早期版本。 不移植到早期版本会造成针对 Visual Studio 多个版本的扩展/包的问题。 这些版本必须在 Visual Studio 2013 和更早版本中自动加载，但可以从基于规则的 UI 上下文中获益，以防止在 Visual Studio 2015 中自动加载。

为了支持此类包，注册表中的 AutoLoadPackages 条目现在可以在其值字段中提供一个标志，以指示应在 Visual Studio 2015 及以上中跳过该条目。 这可以通过向 添加标志选项来实现<xref:Microsoft.VisualStudio.Shell.PackageAutoLoadFlags>。 VSPackages 现在可以将**SkipWhenUIContextRulesActive**选项<xref:Microsoft.VisualStudio.Shell.ProvideAutoLoadAttribute>添加到其属性中，以指示应在 Visual Studio 2015 及以上内容中忽略该条目。
## <a name="extensible-ui-context-rules"></a>可扩展的 UI 上下文规则

有时，包不能使用静态 UI 上下文规则。 例如，假设您有一个包支持可扩展性，以便命令状态基于导入的 MEF 提供程序支持的编辑器类型。 如果有支持当前编辑类型的扩展，则启用该命令。 在这种情况下，包本身不能使用静态 UI 上下文规则，因为术语会根据可用的 MEF 扩展而变化。

为了支持此类包，基于规则的 UI 上下文支持硬编码表达式"*"，该表达式指示其下的所有术语都将与 OR 联接。 这允许主包定义一个已知的基于规则的 UI 上下文，并将其命令状态绑定到此上下文。 之后，针对主包的任何 MEF 扩展都可以为其支持的编辑器添加其术语，而不会影响其他术语或主表达式。

构造函数<xref:Microsoft.VisualStudio.Shell.ProvideExtensibleUIContextRuleAttribute.%23ctor%2A>文档显示可扩展 UI 上下文规则的语法。
