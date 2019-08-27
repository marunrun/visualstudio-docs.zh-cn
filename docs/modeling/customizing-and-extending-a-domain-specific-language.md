---
title: 自定义和扩展域特定语言
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language Tools, creating solutions
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ebbb18e37356c1ef6ccc47f18afe4736a418c0c3
ms.sourcegitcommit: 6a19c5ece38a70731496a38f2ef20676ff18f8a4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/09/2019
ms.locfileid: "65476583"
---
# <a name="customize-and-extend-a-domain-specific-language"></a>自定义和扩展域特定语言

Visual Studio 建模和可视化效果 SDK (VMSDK) 提供了可以在其中定义建模工具的多个级别：

1. 定义使用 DSL 定义关系图的特定于域的语言 (DSL)。 关系图表示法、 可读的 XML 格式，与生成代码和其他项目所需的基本工具，可以快速创建 DSL。 有关详细信息，请参阅[如何定义特定于域的语言](../modeling/how-to-define-a-domain-specific-language.md)。

2. 使用 DSL 定义的更高级的功能来微调 DSL。 例如，可以使其他用户创建的元素时，将显示的链接。 这些技术主要实现在 DSL 定义中，并且某些需要少量的程序代码行。

3. 通过使用程序代码来扩展你的建模工具。 VMSDK 专门用于轻松将扩展和从 DSL 定义生成的代码相集成。 有关详细信息，请参阅[编写代码以自定义特定于域的语言](../modeling/writing-code-to-customise-a-domain-specific-language.md)。

> [!NOTE]
> 更新 DSL 定义文件后，不要忘记单击**转换所有模板**中的工具栏**解决方案资源管理器**之前重新生成解决方案。

## <a name="article-reference"></a>项目引用

|若要实现此效果|请参阅本主题|
|-|-|
|允许用户设置形状的颜色和样式属性。|右键单击形状或连接符类、 指向**公开添加**，单击的项目。|
|不同的模型元素的类在关系图中，共享属性，如初始高度和宽度、 颜色、 工具提示类似。|使用形状或连接符类之间的继承。 派生的形状和派生的域类之间的映射继承父项的映射详细的信息。<br /><br /> 或者，将不同的域类映射到相同的形状类。|
|通过不同的形状上下文可显示的模型元素的类。|将多个形状类映射到同一个域类。 生成解决方案时，遵循错误报告，并提供请求的代码来决定要使用哪些形状。|
|形状的颜色或字体等其他功能指示当前状态。|请参阅[更新形状和连接线以反映模型](../modeling/updating-shapes-and-connectors-to-reflect-the-model.md)。<br /><br /> 创建更新的公开的属性的规则。 请参阅[规则在模型内部传播更改](../modeling/rules-propagate-changes-within-the-model.md)。<br /><br /> 或者，使用 OnAssociatedPropertyChanged() 更新非公开功能，如链接箭头或字体。|
|形状更改来指示状态的图标。|在 DSL 详细信息窗口中设置的可见性的修饰器映射。 找到多个图像修饰器上的相同位置。 请参阅[更新形状和连接线以反映模型](../modeling/updating-shapes-and-connectors-to-reflect-the-model.md)。<br /><br /> 或者，重写`ImageField.GetDisplayImage()`。 中的示例，请参阅<xref:Microsoft.VisualStudio.Modeling.Diagrams.ImageField>。|
|任何形状上设置背景图像|重写 InitializeInstanceResources() 添加锚定的 ImageField。|
|任何深度的嵌套形状|设置嵌入树的递归。 定义 BoundsRules 包含形状。|
|将元素的边界上的固定位置的连接器连接。|定义嵌入的终端元素，表示关系图上的小端口。 BoundsRules 用于修复中的位置的端口。 请参阅在电路图示例[可视化和建模 SDK](http://go.microsoft.com/fwlink/?LinkID=186128)。|
|文本字段将显示与其他值派生的值。|将文本修饰器映射到 Calculated 或自定义存储域属性。 有关详细信息，请参阅[计算和自定义存储属性](../modeling/calculated-and-custom-storage-properties.md)。|
|更改模型元素之间的或形状之间传播|请参阅[特定于域的语言中的验证](../modeling/validation-in-a-domain-specific-language.md)。|
|将更改传播到资源，例如 store 外的其他 Visual Studio 扩展。|请参阅[事件处理程序模型外部传播更改](../modeling/event-handlers-propagate-changes-outside-the-model.md)。|
|属性窗口中显示相关元素的属性。|设置属性转发。 请参阅[自定义属性窗口](../modeling/customizing-the-properties-window.md)。|
|属性类别|属性窗口划分到各类别中。 设置**类别**的域属性。 具有相同的类别名称的属性将显示在同一部分。 您还可以设置**类别**的关系角色。|
|控制用户对域属性访问|设置**是可浏览**为 false，则禁止在运行时在属性窗口中显示域属性。 你仍可以将其映射到文本修饰器。<br /><br /> **是一个 UI 只读选项**防止用户更改域属性。<br /><br /> 程序可以访问域属性不受影响。|
|更改名称、 图标和你的 DSL 模型资源管理器中的节点的可见性。|请参阅[自定义模型资源管理器](../modeling/customizing-the-model-explorer.md)。|
|启用复制、 剪切和粘贴|设置**启用复制粘贴**的属性**编辑器**DSL 资源管理器中的节点。|
|每当复制元素时，将复制引用链接和它们的目标。 例如，将复制的项附加备注。|设置**传播复制**（由在 DSL 定义关系图中的域关系的一侧的行） 的源角色的属性。<br /><br /> 编写代码以覆盖 ProcessOnCopy 以实现更复杂的效果。<br /><br /> 请参阅[自定义复制行为](../modeling/customizing-copy-behavior.md)。|
|删除、 重新设置父级，或删除元素时重新链接相关的元素。|设置**传播删除**关系角色的值。 对于更复杂的影响，重写`ShouldVisitRelationship`并`ShouldVisitRolePlayer`中的方法`MyDslDeleteClosure`类，如**DomainModel.cs**。|
|保留形状布局和外观上复制和拖放。|将形状和连接线添加到复制`ElementGroupPrototype`。 重写的最简便方法是 `ElementOperations.CreateElementGroupPrototype()`<br /><br /> 请参阅[自定义复制行为](../modeling/customizing-copy-behavior.md)。|
|在所选位置（例如当前光标位置）粘贴形状。|重写`ClipboardCommandSet.ProcessOnCopy()`若要使用特定于位置的新版`ElementOperations.Merge().`请参阅[自定义复制行为](../modeling/customizing-copy-behavior.md)。|
|在粘贴上创建其他链接|Override ClipboardCommandSet.ProcessOnPasteCommand()|
|启用从拖放此关系图中，其他 Dsl 和 Windows 元素|请参阅[如何：添加拖放句柄](../modeling/how-to-add-a-drag-and-drop-handler.md)|
|允许的形状或工具拖放到子形状，例如端口，如同已拖动到父级上。|元素合并指令在类上定义目标对象，将转发到父级的拖放的对象。 请参阅[自定义元素创建和移动](../modeling/customizing-element-creation-and-movement.md)。|
|允许的形状或工具拖动到形状上，并让其他链接或创建的对象。 例如，若要允许拖放到它是要链接的项的注释。|在目标域类上定义元素合并指令，定义要生成的链接。 在复杂的情况下，可以添加自定义代码。 请参阅[自定义元素创建和移动](../modeling/customizing-element-creation-and-movement.md)。|
|使用一种工具创建一的组元素。 例如，具有一组固定的端口组件。|重写 ToolboxHelper.cs 中的工具箱初始化方法。 创建包含元素和其关系链接元素组原型 (EGP)。 请参阅[自定义工具和工具箱](../modeling/customizing-tools-and-the-toolbox.md)。<br /><br /> 中 EGP，包括主体和端口形状，或者定义 BoundsRules EGP 实例化时定位端口形状。|
|使用一个连接工具将实例化几种类型的关系。|将链接连接指令 (LCD) 添加到该工具由调用连接生成器。 LCDs 确定两个元素的类型中的关系类型。 若要使这取决于元素的状态，可以添加自定义代码。 请参阅[自定义工具和工具箱](../modeling/customizing-tools-and-the-toolbox.md)。|
|粘滞工具-用户可以双击任何工具连续创建多个形状或连接符。|在 DSL 资源管理器中选择`Editor`节点。 在属性窗口中设置**使用粘滞工具箱项**。|
|定义菜单命令|请参阅[如何：修改标准菜单命令](../modeling/how-to-modify-a-standard-menu-command-in-a-domain-specific-language.md)|
|约束具有验证规则的模型|请参阅[域特定语言中的验证](../modeling/validation-in-a-domain-specific-language.md)|
|从 DSL 中生成代码、 配置文件或文档。|[从域特定语言生成代码](../modeling/generating-code-from-a-domain-specific-language.md)|
|自定义模型的方式保存到文件。|请参阅[自定义文件存储和 XML 序列化](../modeling/customizing-file-storage-and-xml-serialization.md)|
|将模型保存到数据库或其他媒体。|重写*YourLanguage*DocData<br /><br /> 请参阅[自定义文件存储和 XML 序列化](../modeling/customizing-file-storage-and-xml-serialization.md)|
|将多个 Dsl 集成，使它们作为一个应用程序的一部分工作。|请参阅[通过使用 Visual Studio Modelbus 集成模型](../modeling/integrating-models-by-using-visual-studio-modelbus.md)。|
|允许由第三方扩展 DSL 和控制扩展。|[使用 MEF 扩展 DSL](../modeling/extend-your-dsl-by-using-mef.md)<br /><br /> [使用 DSL 库在 DSL 之间共享类](../modeling/sharing-classes-between-dsls-by-using-a-dsl-library.md)<br /><br /> [定义锁定策略以创建只读段](../modeling/defining-a-locking-policy-to-create-read-only-segments.md)|

## <a name="see-also"></a>请参阅

- [如何定义域特定语言](../modeling/how-to-define-a-domain-specific-language.md)
- [编写代码以自定义特定于域的语言](../modeling/writing-code-to-customise-a-domain-specific-language.md)
- [Visual Studio 的建模 SDK - 特定于域的语言](../modeling/modeling-sdk-for-visual-studio-domain-specific-languages.md)

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]
