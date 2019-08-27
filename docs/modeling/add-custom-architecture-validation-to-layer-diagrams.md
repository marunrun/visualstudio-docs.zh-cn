---
title: 向依赖项关系图添加自定义体系结构验证
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- dependency diagrams, adding custom validation
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 743337777677b61661da53446f9717cad14ff9ed
ms.sourcegitcommit: 6a19c5ece38a70731496a38f2ef20676ff18f8a4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/09/2019
ms.locfileid: "65476673"
---
# <a name="add-custom-architecture-validation-to-dependency-diagrams"></a>向依赖项关系图添加自定义体系结构验证

在 Visual Studio 中，用户可以验证对照层模型项目中的源代码，以便他们可以验证源代码符合对依赖项关系图的依赖项。 有标准的验证算法，但你可以定义自己的验证扩展。

当用户选择**验证体系结构**命令在依赖项关系图中，调用标准验证方法时后, 跟任意验证扩展已安装的。

> [!NOTE]
> 在依赖项关系图中，验证的主要用途是将关系图与解决方案的其他部分中的程序代码进行比较。

你可以将层验证扩展打包到 Visual Studio 集成扩展 (VSIX) 中，以便将其分发给其他 Visual Studio 用户。 你可以通过其自身将你的验证程序放入 VSIX 中，也可以作为其他扩展在同一 VSIX 中组合使用。 应在其自身的 Visual Studio 项目中编写验证程序的代码，而不是在与其他扩展相同的项目中编写。

> [!WARNING]
> 创建验证项目之后，请复制本主题末尾的 [示例代码](#example) ，然后根据自己的需要进行编辑。

## <a name="requirements"></a>要求

请参阅 [要求](../modeling/extend-layer-diagrams.md#requirements)。

## <a name="defining-a-layer-validator-in-a-new-vsix"></a>在新的 VSIX 中定义层验证程序

创建验证程序最快的方法就是使用项目模板。 这会将代码和 VSIX 清单置于同一项目中。

### <a name="to-define-an-extension-by-using-a-project-template"></a>若要使用项目模板定义扩展

1. 创建一个新**层设计器验证扩展**项目。

    该模板将创建包含一个小型示例的项目。

   > [!WARNING]
   > 若要使模板正常工作：
   >
   > - 编辑对 `LogValidationError` 的调用，以删除可选参数 `errorSourceNodes` 和 `errorTargetNodes`。
   > - 如果使用自定义属性，应用更新中所述[将自定义属性添加到依赖项关系图](../modeling/add-custom-properties-to-layer-diagrams.md)。

2. 编辑代码以定义验证。 有关详细信息，请参阅 [验证编程](#programming)。

3. 若要测试此扩展，请参阅 [调试层验证](#debugging)。

   > [!NOTE]
   > 将仅在特定情况下调用你的方法，且断点将不会自动工作。 有关详细信息，请参阅 [调试层验证](#debugging)。

::: moniker range="vs-2017"

4. 若要安装该扩展的 Visual Studio 中，或在另一台计算机上的主实例中，找到 *.vsix*中的文件*bin*目录。 将此文件复制到想在其上安装它的计算机，然后双击它。 若要卸载它，请选择**扩展和更新**上**工具**菜单。

::: moniker-end

::: moniker range=">=vs-2019"

4. 若要安装该扩展的 Visual Studio 中，或在另一台计算机上的主实例中，找到 *.vsix*中的文件*bin*目录。 将此文件复制到想在其上安装它的计算机，然后双击它。 若要卸载它，请选择**管理扩展**上**扩展**菜单。

::: moniker-end

## <a name="adding-a-layer-validator-to-a-separate-vsix"></a>向单独的 VSIX 添加层验证程序

如果要创建一个包含层验证程序、命令和其他扩展的 VSIX，建议创建一个项目来定义该 VSIX，并分隔项目和处理程序。

### <a name="to-add-layer-validation-to-a-separate-vsix"></a>向单独的 VSIX 添加层验证

1. 创建新的“类库”项目  。 此项目将包含层验证类。

2. 查找或创建**VSIX 项目**解决方案中。 VSIX 项目包含名为 **source.extension.vsixmanifest**的文件。

3. 在中**解决方案资源管理器**，在 VSIX 项目的右键单击菜单，选择**设为启动项目**。

4. 在 **source.extension.vsixmanifest**中的“资产”  下，将层验证项目添加为 MEF 组件：

    1. 选择 **“新建”** 。

    2. 在“添加新资产”  对话框中，进行如下设置：

         **类型** = **Microsoft.VisualStudio.MefComponent**

          = **当前解决方案中的项目** 

         **项目** = *你的验证程序项目*

5. 还必须将其添加为层验证：

    1. 选择 **“新建”** 。

    2. 在“添加新资产”  对话框中，进行如下设置：

         **类型** = **Microsoft.VisualStudio.ArchitectureTools.Layer.Validator**。 这并不是下拉列表中的选项。 必须从键盘输入。

          = **当前解决方案中的项目** 

         **项目** = *你的验证程序项目*

6. 返回层验证项目，并添加以下项目引用：

    |**引用**|**允许执行的操作**|
    |-|-|
    |Microsoft.VisualStudio.GraphModel.dll|读取体系结构图|
    |Microsoft.VisualStudio.ArchitectureTools.Extensibility.CodeSchema.dll|读取与层关联的代码 DOM|
    |Microsoft.VisualStudio.ArchitectureTools.Extensibility.Layer.dll|读取层模型|
    |Microsoft.VisualStudio.ArchitectureTools.Extensibility|读取并更新形状和关系图。|
    |System.ComponentModel.Composition|使用 Managed Extensibility Framework (MEF) 定义验证组件|
    |Microsoft.VisualStudio.Modeling.Sdk.[版本号]|定义建模扩展|

7. 将本主题末的示例代码复制到验证程序库项目中的类文件中，以包含验证的代码。 有关详细信息，请参阅 [验证编程](#programming)。

8. 若要测试此扩展，请参阅 [调试层验证](#debugging)。

    > [!NOTE]
    > 将仅在特定情况下调用你的方法，且断点将不会自动工作。 有关详细信息，请参阅 [调试层验证](#debugging)。

9. 若要安装的 Visual Studio 中，或在另一台计算机上的主实例中的 VSIX，查找 **.vsix**中的文件**bin** VSIX 项目的目录。 将此文件复制到想在其上安装 VSIX 的计算机。 在 Windows 资源管理器中双击该 VSIX 文件。

## <a name="programming"></a> 验证编程

若要定义层验证扩展，可以定义一个具有以下特征的类：

- 声明的大体形式如下：

  ```csharp
  using System.ComponentModel.Composition;
  using Microsoft.VisualStudio.ArchitectureTools.Extensibility.CodeSchema;
  using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Layer;
  using Microsoft.VisualStudio.GraphModel;
  ...
   [Export(typeof(IValidateArchitectureExtension))]
    public partial class Validator1Extension :
                    IValidateArchitectureExtension
    {
      public void ValidateArchitecture(Graph graph)
      {
         GraphSchema schema = graph.DocumentSchema;
        ...
    } }
  ```

- 如果发现错误，可以使用 `LogValidationError()`进行报告。

  > [!WARNING]
  > 不要使用 `LogValidationError`的可选参数。

用户调用“验证体系结构”  菜单命令时，层运行时系统将分析层及其项目以生成图形。 图形包含四个部分：

- 表示为节点和关系图中的链接层模型的 Visual Studio 解决方案。

- 代码、项目项、解决方案中定义的表示为节点的其他项目，以及表示由分析过程发现的依赖项的链接。

- 从层节点到代码项目节点的链接。

- 表示由验证程序发现的错误的节点。

构造图形后，将调用标准验证方法。 完成此操作后，将以未指定的顺序调用已安装的任何扩展验证方法。 该图形会传递给每个 `ValidateArchitecture` 方法，以便扫描图形并报告找到的任何错误。

> [!NOTE]
> 这不是可以在域特定语言中使用的验证过程相同。

验证方法不应更改正在验证的层模型或代码。

在 <xref:Microsoft.VisualStudio.GraphModel>中定义了图形模型。 其主体类为 <xref:Microsoft.VisualStudio.GraphModel.GraphNode> 和 <xref:Microsoft.VisualStudio.GraphModel.GraphLink>。

每个节点和每个链接都有一个或多个指定元素类型或其表示的关系的类别。 典型图形的节点具有以下类别：

- Dsl.LayerModel

- Dsl.Layer

- Dsl.Reference

- CodeSchema_Type

- CodeSchema_Namespace

- CodeSchema_Type

- CodeSchema_Method

- CodeSchema_Field

- CodeSchema_Property

代码中从层到元素的链接具有“Represents”类别。

## <a name="debugging"></a> 调试验证

若要调试你的层验证扩展，请按 Ctrl + F5。 这将打开一个 Visual Studio 实验实例。 在本例中，将打开或创建一个层模型。 此模型必须与代码相关联，并且必须具有至少一个依赖项。

### <a name="test-with-a-solution-that-contains-dependencies"></a>使用包含依赖项的解决方案进行测试

除非出现以下特征，否则不执行验证：

- 依赖项关系图上没有至少一个依赖项链接。

- 模型中存在于代码元素相关联的层。

启动测试验证扩展，Visual Studio 的实验实例第一次打开或创建具有以下特征的解决方案。

### <a name="run-clean-solution-before-validate-architecture"></a>在验证体系结构之前运行清理解决方案

每当你更新验证代码时，请先在实验解决方案中的“生成”  菜单上使用“清理解决方案”  命令，然后再测试“验证”命令。 这是必要的，因为将缓存验证的结果。 如果未更新测试依赖项关系图或其代码，将不会执行验证方法。

### <a name="launch-the-debugger-explicitly"></a>显式启动调试器

验证在单独的进程中运行。 因此，不会触发验证方法中的断点。 验证开始后，必须将调试器显式附加到进程。

若要将调试器附加到验证进程，请在验证方法的开头插入一个对 `System.Diagnostics.Debugger.Launch()` 的调用。 当出现调试对话框中，选择 Visual Studio 的主实例。

或者，可以插入一个对 `System.Windows.Forms.MessageBox.Show()`的调用。 消息框出现时，请转到主实例的 Visual Studio 并在**调试**菜单上，单击**附加到进程**。 选择名为 **Graphcmd.exe**的进程。

始终通过按 Ctrl + F5（“开始执行(不调试)”  ）启动实验实例。

### <a name="deploying-a-validation-extension"></a>部署验证扩展

若要在安装了适当版本的 Visual Studio 的计算机上安装验证扩展，请打开目标计算机上的 VSIX 文件。

## <a name="example"></a> Example code

```csharp
using System;
using System.ComponentModel.Composition;
using System.Globalization;
using System.Linq;
using System.Text.RegularExpressions;
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.CodeSchema;
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Layer;
using Microsoft.VisualStudio.GraphModel;

namespace Validator3
{
    [Export(typeof(IValidateArchitectureExtension))]
    public partial class Validator3Extension : IValidateArchitectureExtension
    {
        /// <summary>
        /// Validate the architecture
        /// </summary>
        /// <param name="graph">The graph</param>
        public void ValidateArchitecture(Graph graph)
        {
            if (graph == null) throw new ArgumentNullException("graph");

            // Uncomment the line below to debug this extension during validation
            // System.Windows.Forms.MessageBox.Show("Attach 2 to GraphCmd.exe with process id " + System.Diagnostics.Process.GetCurrentProcess().Id);

            // Get all layers on the diagram
            foreach (GraphNode layer in graph.Nodes.GetByCategory("Dsl.Layer"))
            {
                System.Threading.Thread.Sleep(100);
                // Get the required regex property from the layer node
                string regexPattern = "^[a-zA-Z]+$"; //layer[customPropertyCategory] as string;
                if (!string.IsNullOrEmpty(regexPattern))
                {
                    Regex regEx = new Regex(regexPattern);

                    // Get all referenced types in this layer including those from nested layers so each
                    // type is validated against all containing layer constraints.
                    foreach (GraphNode containedType in layer.FindDescendants().Where(node => node.HasCategory("CodeSchema_Type")))
                    {
                        // Check the type name against the required regex
                        CodeGraphNodeIdBuilder builder = new CodeGraphNodeIdBuilder(containedType.Id, graph);
                        string typeName = builder.Type.Name;
                        if (!regEx.IsMatch(typeName))
                        {
                            // Log an error
                            string message = string.Format(CultureInfo.CurrentCulture, Resources.InvalidTypeNameMessage, typeName);
                            this.LogValidationError(graph, typeName + "TypeNameError", message, GraphErrorLevel.Error, layer);
                        }
                    }
                }

            }

        }
    }
}
```

## <a name="see-also"></a>请参阅

- [扩展依赖项关系图](../modeling/extend-layer-diagrams.md)
