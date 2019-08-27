---
title: 如何：使用 Visual Studio 扩展的基于规则的 UI 上下文 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 8dd2cd1d-d8ba-49b9-870a-45acf3a3259d
author: madskristensen
ms.author: madsk
ms.workload:
- vssdk
ms.openlocfilehash: c3075ca5092dd1b8a69aa4b34c0e507505cf7123
ms.sourcegitcommit: 16bcaca215de75479695738d3c2d703c78c3500e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/21/2019
ms.locfileid: "67309681"
---
# <a name="how-to-use-rule-based-ui-context-for-visual-studio-extensions"></a>如何：用于 Visual Studio 扩展的基于规则的 UI 上下文

Visual Studio 允许加载 Vspackage 时某些已知<xref:Microsoft.VisualStudio.Shell.UIContext>s 被激活。 但是，这些 UI 上下文不是精细粒度，使扩展创建者无选择，但选择可用的 UI 上下文的点之前激活它们真正想要加载的 VSPackage。 有关的已知用户界面上下文中的列表，请参阅<xref:Microsoft.VisualStudio.Shell.KnownUIContexts>。

加载包可能会影响性能并不是需要更快地加载它们不是最佳做法。 Visual Studio 2015 引入了基于规则的 UI 上下文，一种机制，允许扩展创建者定义的精确条件在其下 UI 上下文被激活并加载相关联的 Vspackage 的概念。

## <a name="rule-based-ui-context"></a>基于规则的 UI 上下文

"规则"包括新的 UI 上下文 (GUID) 和引用一个或多个"条款"的布尔表达式结合使用逻辑"and"、"，"not"操作。 "条款"在运行时动态计算，只要任何其条款更改将被重新计算该表达式。 表达式的计算结果为 true，将激活关联的 UI 上下文。 否则，为取消激活 UI 上下文。

可以多种方式使用基于规则的 UI 上下文：

1. 指定命令和工具窗口的可见性的限制。 满足 UI 上下文规则之前，您可以隐藏 windows 命令/工具。

2. 为自动加载约束： 仅当满足规则，自动加载包。

3. 作为延迟的任务： 延迟加载之前指定的时间间隔已过，是否仍满足该规则。

   可以通过任何 Visual Studio 扩展中使用的机制。

## <a name="create-a-rule-based-ui-context"></a>创建基于规则的 UI 上下文
 假设具有名为 TestPackage 扩展，它提供了菜单命令，仅适用于使用的文件 *.config*扩展。 在 VS2015 之前, 的最佳选择是加载 TestPackage 时<xref:Microsoft.VisualStudio.Shell.KnownUIContexts.SolutionExistsAndFullyLoadedContext%2A>UI 上下文已激活。 以这种方式加载 TestPackage 不是有效，因为即使不能包含加载的解决方案 *.config*文件。 以下步骤演示了如何基于规则的 UI 上下文可用于激活的 UI 上下文使用的文件时仅 *.config*扩展已选中，然后加载 TestPackage 时激活该 UI 上下文。

1. 定义新的 UIContext GUID，并将添加到 VSPackage 类<xref:Microsoft.VisualStudio.Shell.ProvideAutoLoadAttribute>和<xref:Microsoft.VisualStudio.Shell.ProvideUIContextRuleAttribute>。

    例如，假设新 UIContext"UIContextGuid"是要添加。 创建的 GUID (可以通过单击来创建一个 GUID**工具** > **创建 GUID**) 是"8B40D5E2-5626-42AE-99EF-3DD1EFF46E7B"。 然后在包类中添加以下声明：

   ```csharp
   public const string UIContextGuid = "8B40D5E2-5626-42AE-99EF-3DD1EFF46E7B";
   ```

    对于属性，添加以下值：（这些属性的详细信息将稍后介绍）

   ```csharp
   [ProvideAutoLoad(TestPackage.UIContextGuid)]
   [ProvideUIContextRule(TestPackage.UIContextGuid,
       name: "Test auto load",
       expression: "DotConfig",
       termNames: new[] { "DotConfig" },
       termValues: new[] { "HierSingleSelectionName:.config$" })]
   ```

    这些元数据定义新 UIContext GUID (8B40D5E2-5626-42AE-99EF-3DD1EFF46E7B) 和单个字词，"DotConfig"引用的表达式。 "DotConfig"一词计算结果为 true，只要在活动的层次结构中当前所选内容具有与正则表达式模式匹配的名称"\\.config$"(结尾 *.config*)。 （默认值） 值定义可用于调试的规则的可选名称。

    属性的值将添加到 pkgdef 之后尽早的时间生成过程中生成。

2. 在 VSCT 文件 TestPackage 的命令中，将"DynamicVisibility"标志添加到适当的命令：

   ```xml
   <CommandFlag>DynamicVisibility</CommandFlag>
   ```

3. 在 VSCT 可见性部分中，将绑定到新 UIContext GUID #1 中定义适当的命令：

   ```xml
   <VisibilityConstraints>
       <VisibilityItem guid="guidTestPackageCmdSet" id="TestId"  context="UIContextGuid"/>
   </VisibilityConstraints>
   ```

4. 在符号部分中，添加 UIContext 的定义：

   ```xml
   <GuidSymbol name="UIContextGuid" value="{8B40D5E2-5626-42AE-99EF-3DD1EFF46E7B}" />
   ```

    现在，上下文菜单命令 *\*.config*文件将显示在解决方案资源管理器中的选定的项时才 *.config*文件和包将不会加载到其中一个选择命令。

   接下来，使用调试程序确认包加载仅当您预期。 若要调试 TestPackage:

5. 中设置断点<xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A>方法。

6. 生成 TestPackage 并启动调试。

7. 创建项目或打开一个。

8. 而不选择任何文件扩展名 *.config*。应不会命中断点。

9. 选择*App.Config*文件。

   TestPackage 加载，并在断点处停止。

## <a name="add-more-rules-for-ui-context"></a>为 UI 上下文中添加更多的规则
 由于 UI 上下文规则都是布尔表达式，可以添加更受限制的规则的 UI 上下文。 例如，在上面的 UI 上下文中，可以指定该规则仅在加载与项目的解决方案时适用。 这样一来，命令不会显示是否打开 *.config*文件作为独立文件，而不是项目的一部分。

```csharp
[ProvideAutoLoad(TestPackage.UIContextGuid)]
[ProvideUIContextRule(TestPackage.UIContextGuid,
    name: "Test auto load",
    expression: "(SingleProject | MultipleProjects) & DotConfig",
    termNames: new[] { "SingleProject", "MultipleProjects","DotConfig" },
    termValues: new[] { VSConstants.UICONTEXT_SolutionHasSingleProject_string , VSConstants.UICONTEXT_SolutionHasMultipleProjects_string , "HierSingleSelectionName:.config$" })]
```

 现在该表达式引用了这三个术语。 前两个术语，"SingleProject"和"MultipleProjects"，请参阅其他的已知用户界面上下文中 （由其 Guid)。 第三个术语中，"DotConfig"是在本文前面定义的基于规则的 UI 上下文。

## <a name="delayed-activation"></a>延迟的激活
 规则可以具有可选的"延迟"。 以毫秒为单位指定延迟。 如果存在，延迟将导致激活或停用的规则的 UI 上下文会延迟由该时间间隔。 如果规则更改回之前的延迟间隔，则没有任何变化。 此机制可用于"错开"初始化步骤-尤其是一次性初始化而无需依赖于计时器或注册的空闲通知。

 例如，可以指定测试负载规则，以配置有 100 毫秒的延迟：

```csharp
[ProvideAutoLoad(TestPackage.UIContextGuid)]
[ProvideUIContextRule(TestPackage.UIContextGuid,
    name: "Test auto load",
    expression: "DotConfig",
    termNames: new[] { "DotConfig" },
    termValues: new[] { "HierSingleSelectionName:.config$" },
    delay: 100)]
```

## <a name="term-types"></a>字词类型

下面是术语的支持各种类型:

|术语|描述|
|-|-|
|{nnnnnnnn-nnnn-nnnn-nnnn-nnnnnnnnnnnn}|GUID 是指 UI 上下文。 只要 UI 上下文否则处于活动状态且 false 一词将为 true。|
|HierSingleSelectionName:\<模式 >|活动的层次结构中的选择是单个项或所选的项的名称与"pattern"提供的.Net 正则表达式匹配时，术语将为 true。|
|UserSettingsStoreQuery:\<query>|"查询"到用户设置存储中，计算结果必须为非零值表示的完整路径。 该查询拆分为"集合"和"属性名称"处的最后一个斜杠。|
|ConfigSettingsStoreQuery:\<query>|"查询"到配置设置存储中，计算结果必须为非零值表示的完整路径。 该查询拆分为"集合"和"属性名称"处的最后一个斜杠。|
|ActiveProjectFlavor:\<projectTypeGuid>|术语将为 true，每当当前选定的项目风格 （聚合） 和具有风格匹配给定的项目类型 GUID。|
|ActiveEditorContentType:\<contentType>|当所选的文档与给定内容类型的文本编辑器时，术语将为 true。|
|ActiveProjectCapability:\<Expression>|当活动项目功能与所提供的表达式匹配时，术语是，则返回 true。 表达式可以是类似于 VB 的内容&#124;CSharp。|
|SolutionHasProjectCapability:\<Expression>|解决方案中包含与表达式匹配任何加载的项目时，与上述相似，但一词是如此。|
|SolutionHasProjectFlavor:\<projectTypeGuid>|每当解决方案风格 （聚合） 的项目，并具有匹配给定的项目类型 GUID 的风格，术语将为 true。|
|ProjectAddedItem:\<pattern>| 术语"模式"匹配的文件添加到项目中打开 soluion 时，则返回 true。|
|ActiveProjectOutputType:\<outputType>|术语为 true 时输出类型完全匹配的活动项目。  OutputType 可能是一个整数或<xref:Microsoft.VisualStudio.Shell.Interop.__VSPROJOUTPUTTYPE>类型。|
|ActiveProjectBuildProperty:\<buildProperty>=\<regex>|当活动项目具有指定的生成属性和属性值与提供的正则表达式筛选器匹配时，术语是，则返回 true。 请参阅[MSBuild 项目文件中保存数据](internals/persisting-data-in-the-msbuild-project-file.md)适用于更多详细信息生成属性。|
|SolutionHasProjectBuildProperty:\<buildProperty>=\<regex>|解决方案已加载的项目与指定的生成属性和属性值与提供的正则表达式筛选器匹配时，术语是，则返回 true。|

## <a name="compatibility-with-cross-version-extension"></a>使用跨版本扩展的兼容性

基于规则的 UI 上下文是在 Visual Studio 2015 中的新功能，并将不能移植到更早版本。 不移植到更早版本创建面向多个版本的 Visual Studio/扩展包的问题。 这些版本必须进行自动加载在 Visual Studio 2013 及更早版本，但可以受益于基于规则的 UI 上下文，以防止正在自动加载 Visual Studio 2015 中。

为了支持此类包，AutoLoadPackages 注册表中的项现在可以提供其值字段，用于指示该条目应跳过，在 Visual Studio 2015 及更高版本中的标志。 这可以通过添加一个标志选项，到<xref:Microsoft.VisualStudio.Shell.PackageAutoLoadFlags>。 现在可以添加 Vspackage **SkipWhenUIContextRulesActive**选项设为其<xref:Microsoft.VisualStudio.Shell.ProvideAutoLoadAttribute>特性以指示应忽略该条目，在 Visual Studio 2015 及更高版本。
## <a name="extensible-ui-context-rules"></a>可扩展 UI 上下文规则

有时，包不能使用 UI 上下文的静态规则。 例如，假设有支持可扩展性，以便命令状态基于导入 MEF 提供程序支持的编辑器类型的包。 如果没有支持当前的编辑类型扩展会启用命令。 在这种情况下，包本身不能使用静态的 UI 上下文规则，因为条款将发生更改，具体取决于哪个 MEF 提供了扩展。

若要支持此类包，基于规则的 UI 上下文支持硬编码表达式"*"，该值指示所有以下条款将与联接或者。 这允许主包定义已知的基于规则的 UI 上下文并将绑定到此上下文其命令状态。 以后针对主包任何 MEF 扩展可以添加其条款它不会影响其他术语或主表达式支持的编辑器。

构造函数<xref:Microsoft.VisualStudio.Shell.ProvideExtensibleUIContextRuleAttribute.%23ctor%2A>文档显示了可扩展 UI 上下文规则的语法。
