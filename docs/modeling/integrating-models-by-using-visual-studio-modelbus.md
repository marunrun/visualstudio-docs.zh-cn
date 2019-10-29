---
title: 使用 Modelbus 集成模型
ms.date: 11/04/2016
ms.topic: conceptual
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9b5a0ad18c7b1472e8c08ccc2902cade7714f2b9
ms.sourcegitcommit: dcbb876a5dd598f2538e62e1eabd4dc98595b53a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2019
ms.locfileid: "72985270"
---
# <a name="integrate-models-by-using-visual-studio-modelbus"></a>使用 Visual Studio Modelbus 集成模型

Visual Studio ModelBus 提供了一种方法，用于在模型和其他工具之间创建链接到模型。 例如，可以链接域特定语言（DSL）模型和 UML 模型。 可以创建一组集成 DSL。

ModelBus 允许你创建对模型或模型中特定元素的唯一引用。 此引用可存储在该模型外部，例如另一个模型的元素中。 在随后的场合中，当工具想要获取对元素的访问权限时，模型总线基础结构将加载相应的模型并返回元素。 如果需要，可以向用户显示该模型。 如果不能在其以前的位置中访问该文件，则 ModelBus 将要求用户查找该文件。 如果用户找到该文件，则 ModelBus 将修复所有对该文件的引用。

> [!NOTE]
> 在 ModelBus 的当前 Visual Studio 实现中，链接模型必须是同一 Visual Studio 解决方案中的项。

有关其他信息和示例代码，请参阅：

- [如何：添加拖放处理程序](../modeling/how-to-add-a-drag-and-drop-handler.md)

- [Visual Studio 的建模 SDK](https://www.microsoft.com/download/details.aspx?id=48148)

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]

## <a name="provide"></a>提供对 DSL 的访问
 在可以创建对模型或其元素的 ModelBus 引用之前，必须定义用于 DSL 的 ModelBusAdapter。 执行此操作的最简单方法是使用 Visual Studio 模型总线扩展，该扩展将命令添加到 DSL 设计器。

### <a name="expose"></a>向模型总线公开 DSL 定义

1. 打开 DSL 定义文件。 右键单击设计图面，然后单击 "**启用 Modelbus**"。

2. 在对话框中，选择 **"我想要向 ModelBus 公开此 DSL"** 。 如果希望此 DSL 同时公开其模型并使用对其他 DSL 的引用，则可选择这两个选项。

3. 单击“确定”。 新项目“ModelBusAdapter”随即添加到 DSL 解决方案中。

4. 如果要从文本模板访问 DSL，则必须修改新项目中的 AdapterManager.tt。 如果要从其他代码（例如命令和事件处理程序）访问 DSL，则忽略此步骤。 有关详细信息，请参阅[在文本模板中使用 Visual Studio ModelBus](../modeling/using-visual-studio-modelbus-in-a-text-template.md)。

   1. 将 AdapterManagerBase 的基类更改为[VsTextTemplatingModelingAdapterManager](/previous-versions/ee844317(v=vs.140))。

   2. 在文件末尾附近，将此附加特性插入到类 AdapterManager 的前面：

       `[Microsoft.VisualStudio.Modeling.Integration.HostSpecific(HostName)]`

   3. 在 ModelBusAdapter 项目的引用中，添加**VisualStudio**。

      如果要同时从文本模板和其他代码访问 DSL，则需要两个适配器：一个已经过修改，另一个未经过修改。

5. 单击 "**转换所有模板**"。

6. 重新生成解决方案。

   现在 ModelBus 可以打开此 DSL 的实例。

   文件夹 `ModelBusAdapters\bin\*` 包含由 `Dsl` 项目和 `ModelBusAdapters` 项目生成的程序集。 若要从另一个 DSL 引用此 DSL，应导入这些程序集。

### <a name="ensure-that-elements-can-be-referenced"></a>确保可以引用元素

默认情况下，Visual Studio ModelBus 适配器使用元素的 guid 来标识它。 因此这些标识符必须保留在模型文件中。

若要确保保持元素 Id，请执行以下操作：

1. 打开 DslDefinition.dsl。

2. 在 DSL 资源管理器中，依次展开 " **Xml 序列化行为**" 和 "**类数据**"。

3. 对于想要为其创建模型总线引用的每个类：

    单击 "类" 节点，然后在 "属性窗口中，确保**序列化 ID**设置为 `true`。

   或者，如果要使用元素名称来标识元素而不是 Guid，则可以重写生成的适配器的各个部分。 在适配器类中重写以下方法：

- 重写 `GetElementId` 以返回要使用的标识符。 在创建引用时将调用此方法。

- 重写 `ResolveElementReference` 以从模型总线引用中查找正确元素。

## <a name="editRef"></a>从另一个 DSL 访问 DSL

你可以将模型总线引用存储在 DSL 的域属性中，也可以编写使用它们的自定义代码。 还可以允许用户通过选取模型文件和其中的元素来创建模型总线引用。

若要允许 DSL 使用对其他 DSL 的引用，你应该首先使其成为模型总线引用的*使用者*。

### <a name="to-enable-a-dsl-to-consume-references-to-an-exposed-dsl"></a>允许 DSL 使用对公开的 DSL 的引用

1. 在 DSL 定义关系图中，右键单击关系图的主要部分，然后单击 "**启用 Modelbus**"。

2. 在对话框中，选择 "**我想要启用此模型以使用模型总线引用**"。

3. 在使用 DSL 的 DSL 项目中，将以下程序集添加到项目引用。 你将在公开的 DSL 的 ModelBusAdapter\bin \\ * 目录中找到这些程序集（.dll 文件）。

    - 公开的 DSL 程序集，例如**FamilyTree**

    - 公开的模型总线适配器程序集，例如**FamilyTree. ModelBusAdapter**

4. 将以下 .NET 程序集添加到使用 DSL 项目的项目引用。

    1. **VisualStudio. 11.0. 11.0。**

    2. **VisualStudio..... e。**

### <a name="to-store-a-model-bus-reference-in-a-domain-property"></a>将模型总线引用存储在域属性中

1. 在使用 DSL 的 DSL 定义中，将域属性添加到域类并设置其名称。

2. 在 "属性窗口" 中，选择 "域" 属性，将 "**类型**" 设置为 `ModelBusReference`。

   在此阶段，程序代码可设置属性值，但在“属性”窗口中该值为只读。

   可以允许用户使用专用 ModelBus 引用编辑器设置属性。 此编辑器或*选择器*有两个版本：一个允许用户选择模型文件，另一个则允许用户选择模型文件和模型中的元素。

### <a name="to-allow-the-user-to-set-a-model-bus-reference-in-a-domain-property"></a>允许用户在域属性中设置模型总线引用

1. 右键单击 "域" 属性，然后单击 "**编辑 ModelBusReference 特定属性**"。 这将打开一个对话框。 这是*模型总线选取器*。

2. 选择适当**的 ModelBusReference 类型**：对模型或模型中的元素。

3. 在文件对话框筛选器字符串中，输入字符串（如 `Family Tree files |*.ftree`）。 替换公开 DSL 的文件扩展名。

4. 如果选择引用模型中的元素，则可添加用户可选择的类型（例如 Company.FamilyTree.Person）的列表。

5. 单击 **"确定**"，然后单击 "**解决方案资源管理器**" 工具栏中的 "**转换所有模板**"。

    > [!WARNING]
    > 如果未选择有效的模型或实体，则“确定”按钮将不起作用，即使它可能显示为“已启用”也是如此。

6. 如果指定了目标类型（如 Company.FamilyTree.Person）的列表，则必须将程序集引用添加到 DSL 项目，从而引用目标 DSL 的 DLL（例如 Company.FamilyTree.Dsl.dll）

### <a name="to-test-a-model-bus-reference"></a>测试模型总线引用

1. 同时生成公开的 DSL 和使用的 DSL。

2. 通过按 F5 或 CTRL+F5，在实验模式下运行一个 DSL。

3. 在 Visual Studio 的实验实例中的调试项目中，添加作为每个 DSL 的实例的文件。

    > [!NOTE]
    > Visual Studio ModelBus 只能解析对属于同一 Visual Studio 解决方案中的项的模型的引用。 例如，你无法创建对位于文件系统另一部分中的模型文件的引用。

4. 在公开的 DSL 的实例中创建一些元素和链接，并将其保存。

5. 打开使用的 DSL 的实例，并选择一个具有模型总线引用属性的模型元素。

6. 在“属性”窗口中，双击模型总线引用属性。 这将打开选取器对话框。

7. 单击 "**浏览**" 并选择公开的 DSL 的实例。

     如果你指定了特定于元素类型的模型总线引用，选取器还将允许你选择模型中的项。

## <a name="creating-references-in-program-code"></a>在程序代码中创建引用

当你想要存储对模型或模型内的元素的引用时，请创建 `ModelBusReference`。 有两种 `ModelBusReference`：模型引用和元素引用。

若要创建模型引用，需要 AdapterManager 的模型为其实例的 DSL，以及该模型的文件名或 Visual Studio 项目项。

若要创建元素引用，你需要用于模型文件的适配器，以及要引用的元素。

> [!NOTE]
> 在 Visual Studio ModelBus 中，你只能创建对同一 Visual Studio 解决方案中的项的引用。

### <a name="import-the-exposed-dsl-assemblies"></a>导入公开的 DSL 程序集

在使用的项目中，将项目引用添加到 DSL 和公开的 DSL 的 ModelBusAdapter 程序集。

例如，假设要将 ModelBus 引用存储在 MusicLibrary DSL 的元素中。 ModelBus 引用将引用 FamilyTree DSL 的元素。 在 MusicLibrary 解决方案的 `Dsl` 项目中，在“引用”节点中，将引用添加到以下程序集：

- Fabrikam.FamilyTree.Dsl.dll - 公开的 DSL。

- Fabrikam.FamilyTree.ModelBusAdapters.dll - 公开的 DSL 的 ModelBus 适配器。

- Microsoft.VisualStudio.Modeling.Sdk.Integration.11.0

- Microsoft.VisualStudio.Modeling.Sdk.Integration.Shell.11.0

  可在 `ModelBusAdapters` 下的公开 DSL 的 `bin\*` 项目中找到这些程序集。

  在将创建引用所在的代码文件中，通常必须导入这些命名空间：

```csharp
// The namespace of the DSL you want to reference:
using Fabrikam.FamilyTree;  // Exposed DSL
using Fabrikam.FamilyTree.ModelBusAdapters;
using Microsoft.VisualStudio.Modeling.Integration;
using System.Linq;
...
```

### <a name="to-create-a-reference-to-a-model"></a>创建对模型的引用

若要创建模型引用，请访问公开的 DSL 的 AdapterManager，并将其用于创建对该模型的引用。 可以指定文件路径或 `EnvDTE.ProjectItem`。

你可以从 AdapterManager 中获取一个适配器，该适配器提供了对模型中各个元素的访问权限。

> [!NOTE]
> 你必须在使用完适配器后将其公开。 实现此目的的最简便方式是使用 `using` 语句。 下面的示例阐释了这一点。

```csharp
// The file path of a model instance of the FamilyTree DSL:
string targetModelFile = "TudorFamilyTree.ftree";
// Get the ModelBus service:
IModelBus modelBus =
    this.Store.GetService(typeof(SModelBus)) as IModelBus;
// Get an adapterManager for the target DSL:
FamilyTreeAdapterManager manager =
    (modelbus.GetAdapterManager(FamilyTreeAdapter.AdapterId)
     as FamilyTreeAdapterManager;
// or: (modelBus.FindAdapterManagers(targetModelFile).First())
// or could provide an EnvDTE.ProjectItem

// Create a reference to the target model:
// NOTE: the target model must be a file in this project.
ModelBusReference modelReference =
     manager.CreateReference(targetModelFile);
// or can use an EnvDTE.ProjectItem instead of the filename

// Get the root element of this model:
using (FamilyTreeAdapter adapter =
     modelBus.CreateAdapter(modelReference) as FamilyTreeAdapter)
{
  FamilyTree modelRoot = adapter.ModelRoot;
  // Access elements under the root in the usual way:
  foreach (Person p in modelRoot.Persons) {...}
  // You can create adapters for individual elements:
  ModelBusReference elementReference =
     adapter.GetElementReference(person);
  ...
} // Dispose adapter
```

如果希望以后可以使用 `modelReference`，可将它存储在具有外部类型 `ModelBusReference` 的域属性中：

```csharp
using Transaction t = this.Store.TransactionManager
    .BeginTransaction("keep reference"))
{
  artist.FamilyTreeReference = modelReference;
  t.Commit();
}
```

若要允许用户编辑此域属性，请将 `ModelReferenceEditor` 用作“编辑器”特性中的参数。 有关详细信息，请参阅[允许用户编辑引用](#editRef)。

### <a name="to-create-a-reference-to-an-element"></a>创建对元素的引用

为模型创建的适配器可用于创建和解析引用。

```csharp
// person is an element in the FamilyTree model:
ModelBusReference personReference =
  adapter.GetElementReference(person);
```

如果希望以后可以使用 `elementReference`，可将它存储在具有外部类型 `ModelBusReference` 的域属性中。 若要允许用户编辑它，请将 `ModelElementReferenceEditor` 用作“编辑器”特性中的参数。 有关详细信息，请参阅[允许用户编辑引用](#editRef)。

### <a name="resolving-references"></a>解析引用

如果你具有 `ModelBusReference` (MBR)，则可获取它所引用的模型或模型元素。 如果元素存在于关系图或其他视图上，则可打开视图，然后选择该元素。

可从 MBR 创建适配器。 你可以从适配器中获取模型的根。 还可解析引用模型内特定元素的 MBR。

```csharp
using Microsoft.VisualStudio.Modeling.Integration; ...
ModelBusReference elementReference = ...;

// Get the ModelBus service:
IModelBus modelBus =
    this.Store.GetService(typeof(SModelBus)) as IModelBus;
// Use a model reference or an element reference
// to obtain an adapter for the target model:
using (FamilyTreeAdapter adapter =
   modelBus.CreateAdapter(elementReference) as FamilyTreeAdapter)
   // or CreateAdapter(modelReference)
{
  // Get the root of the model:
  FamilyTree tree = adapter.ModelRoot;

  // Get a model element:
  MyDomainClass mel =
    adapter.ResolveElementReference<MyDomainClass>(elementReference);
  if (mel != null) {...}

  // Get the diagram or other view, if there is one:
  ModelBusView view = adapter.GetDefaultView();
  if (view != null)
  {
   view.Open();
   // Display the diagram:
   view.Show();
   // Attempt to select the shape that presents the element:
   view.SetSelection(elementReference);
  }
} // Dispose the adapter.
```

#### <a name="to-resolve-modelbus-references-in-a-text-template"></a>在文本模板中解析 ModelBus 引用

1. 要访问的 DSL 必须具有 ModelBus 适配器，已配置该适配器以供文本模板访问。 有关详细信息，请参阅[提供对 DSL 的访问](#provide)。

2. 通常，使用存储在源 DSL 中的模型总线引用 (MBR) 访问目标 DSL。 因此模板包括源 DSL 的指令，以及用于解析 MBR 的代码。 有关文本模板的详细信息，请参阅[从域特定语言生成代码](../modeling/generating-code-from-a-domain-specific-language.md)。

   ```
   <#@ template debug="true" hostspecific="true"
   inherits="Microsoft.VisualStudio.TextTemplating.Modeling.ModelBusEnabledTextTransformation" #>
   <#@ SourceDsl processor="SourceDslDirectiveProcessor" requires="fileName='Sample.source'" #>
   <#@ output extension=".txt" #>
   <#@ assembly name = "Microsoft.VisualStudio.Modeling.Sdk.Integration.11.0" #>
   <#@ assembly name = "System.Core" #>
   <#@ assembly name = "Company.CompartmentDragDrop.Dsl.dll" #>
   <#@ assembly name = "Company.CompartmentDragDrop.ModelBusAdapter.dll" #>
   <#@ import namespace="Microsoft.VisualStudio.Modeling.Integration" #>
   <#@ import namespace="System.Linq" #>
   <#@ import namespace="Company.CompartmentDragDrop" #>
   <#@ import namespace="Company.CompartmentDragDrop.ModelBusAdapters" #>
   <# // Get source root from directive processor:
     ExampleModel source = this.ExampleModel;
     // This DSL has a MBR in its root:
   using (ModelBusAdapter adapter = this.ModelBus.CreateAdapter(source.ModelReference) as ModelBusAdapter)
     {
     ModelBusAdapterManager manager = this.ModelBus.FindAdapterManagers(this.Host.ResolvePath("Sample.compDD1")).FirstOrDefault();
     ModelBusReference modelReference =
       manager.CreateReference(this.Host.ResolvePath("Sample.compDD1"));

     // Get the root element of this model:
     using (CompartmentDragDropAdapter adapter =
        this.ModelBus.CreateAdapter(modelReference) as CompartmentDragDropAdapter)
     {
       ModelRoot root = adapter.ModelRoot;
   #>
   [[<#= root.Name #>]]
   <#
     }
   #>
   ```

   有关详细信息和演练，请参阅[在文本模板中使用 Visual Studio ModelBus](../modeling/using-visual-studio-modelbus-in-a-text-template.md)

## <a name="serializing-a-modelbusreference"></a>序列化 ModelBusReference

如果想要以字符串的形式存储 `ModelBusReference` (MBR)，则可将其序列化：

```csharp
string serialized = modelBus.SerializeReference(elementReference);
// Store it anywhere, then get it back again:
ModelBusReference elementReferenceRestored =
    modelBus.DeserializeReference(serialized, null);
```

以这种方式序列化的 MBR 与上下文无关。 如果要使用简单的基于文件的模型总线适配器，则 MBR 将包含绝对文件路径。 如果实例模型文件永不移动，则这种做法已经足够。 但是，模型文件通常是 Visual Studio 项目中的项。 用户希望能够将整个项目移动到文件系统的不同部分。 他们还希望能够将项目保持在源代码管理之下并在不同的计算机上打开它。 因此应相对于包含文件的项目的位置对路径名称进行序列化。

### <a name="serializing-relative-to-a-specified-file-path"></a>相对于指定的文件路径进行序列化

`ModelBusReference` 包含 `ReferenceContext`，它是可将信息（例如应相对于其进行序列化的文件路径）存储在其中的字典。

相对于路径进行序列化：

```csharp
elementReference.ReferenceContext.Add(
   ModelBusReferencePropertySerializer.FilePathSaveContextKey,
   currentProjectFilePath);
string serialized = modelBus.SerializeReference(elementReference);
```

从字符串检索引用：

```csharp
ReferenceContext context = new ReferenceContext();
context.Add(ModelBusReferencePropertySerializer.FilePathLoadContextKey,
    currentProjectFilePath);
ModelBusReference elementReferenceRestored =
    modelBus.DeserializeReference(serialized, context);
```

### <a name="modelbusreferences-created-by-other-adapters"></a>由其他适配器创建的 ModelBusReferences
 如果想要创建自己的适配器，以下信息十分有用。

 `ModelBusReference` (MBR) 由两部分组成：由模型总线反序列化的 MBR 标头，以及由特定适配器管理器处理的特定于适配器的部分。 这允许你提供自己的适配器序列化格式。 例如，你可以引用数据库而不是文件，或者可以将附加信息存储在适配器引用中。 你自己的适配器可将附加信息放在 `ReferenceContext` 中。

 在反序列化 MBR 时，必须提供随后将存储在 MBR 对象中的 ReferenceContext。 在序列化 MBR 时，适配器将使用存储的 ReferenceContext 以帮助生成字符串。 反序列化的字符串不包含 ReferenceContext 中的所有信息。 例如，在简单的基于文件的适配器中，ReferenceContext 包含未存储在序列化的 MBR 字符串中的根文件路径。

 反序列化 MBR 分为两个阶段：

- `ModelBusReferencePropertySerializer` 是处理 MBR 标头的标准序列化程序。 它使用标准 DSL `SerializationContext` 属性包，该属性包使用键 `ReferenceContext` 存储在 `ModelBusReferencePropertySerializer.ModelBusLoadContextKey` 中。 具体而言，`SerializationContext` 应包含 `ModelBus` 的实例。

- ModelBus 适配器将处理 MBR 的特定于适配器的部分。 它可使用存储在 MBR 的 ReferenceContext 中的附加信息。 简单的基于文件的适配器使用 `FilePathLoadContextKey` 和 `FilePathSaveContextKey` 的密钥来保存根文件路径。

     仅当使用模型文件中的适配器引用时才对其进行反序列化。

## <a name="to-create-a-model"></a>创建模型

### <a name="creating-opening-and-editing-a-model"></a>创建、打开和编辑模型
 以下片段是从 VMSDK 网站上的状态机示例获取的。 它阐释了如何使用 ModelBusReferences 创建和打开模型，以及获取与该模型相关联的关系图。

 在此示例中，目标 DSL 的名称是 StateMachine。 可从该名称派生多个名称，例如模型类的名称和 ModelBusAdapter 的名称。

```csharp
using Fabrikam.StateMachine.ModelBusAdapters;
using Microsoft.VisualStudio.Modeling;
using Microsoft.VisualStudio.Modeling.Diagrams;
using Microsoft.VisualStudio.Modeling.Integration;
using Microsoft.VisualStudio.Modeling.Integration.Shell;
using Microsoft.VisualStudio.Modeling.Shell;
...
// Create a new model.
ModelBusReference modelReference =
   StateMachineAdapterManager    .CreateStateMachineModel(modelName, fileName);
//Keep reference of new model in this model.
using (Transaction t = ...)
{
  myModelElement.ReferenceProperty = modelReference;
  t.Commit();
}
// Get the ModelBus service from Visual Studio.
IModelBus modelBus = Microsoft.VisualStudio.Shell.Package.
    GetGlobalService(typeof(SModelBus)) as IModelBus;
// Get a modelbus adapter on the new model.
ModelBusAdapter modelBusAdapter;
modelBus.TryCreateAdapter(modelReference,
    this.ServiceProvider, out modelBusAdapter);
using (StateMachineAdapter adapter =
      modelBusAdapter as StateMachineAdapter)
{
    if (adapter != null)
    {
        // Obtain a Diagram from the adapter.
        Diagram targetDiagram =
           ((StandardVsModelingDiagramView)
                 adapter.GetDefaultView()
            ).Diagram;

        using (Transaction t =
             targetDiagram.Store.TransactionManager
                .BeginTransaction("Update diagram"))
        {
            DoUpdates(targetDiagram);
            t.Commit();
        }

        // Display the new diagram.
        adapter.GetDefaultView().Show();
    }
}
```

## <a name="validating-references"></a>验证引用
 BrokenReferenceDetector 测试可保留 ModelBusReferences 的“存储”中的所有域属性。 它将调用你提供的操作，并可在其中查找所有操作。 这对验证方法尤为有用。 以下验证方法将在尝试保存模型时测试存储，并在错误窗口中报告中断的引用：

```csharp
[ValidationMethod(ValidationCategories.Save)]
public void ValidateModelBusReferences(ValidationContext context)
{
  BrokenReferenceDetector.DetectBrokenReferences(this.Store,
    delegate(ModelElement element, // parent of property
             DomainPropertyInfo property, // identifies property
             ModelBusReference reference) // invalid reference
    {
      context.LogError(string.Format(INVALID_REF_FORMAT,
             property.Name,
             referenceState.Name,
             new ModelBusReferenceTypeConverter().
                 ConvertToInvariantString(reference)),
         "Reference",
         element);
      });
}}
private const string INVALID_REF_FORMAT =
    "The '{0}' domain property of ths ReferenceState instance "
  + "named '{1}' contains reference value '{2}' which is invalid";
```

## <a name="actions-performed-by-the-modelbus-extension"></a>由 ModelBus 扩展执行的操作

以下信息并不重要，但如果要大量使用 ModelBus，则可能十分有用。

ModelBus 扩展将在 DSL 解决方案中进行以下更改。

右键单击 DSL 定义关系图时，单击 "**启用 Modelbus**"，然后选择 "**启用此 DSL 以使用 Modelbus"** ：

- 在 DSL 项目中，将一个引用添加到了**VisualStudio**中。

- 在 DSL 定义中，外部类型引用将添加到：`Microsoft.VisualStudio.Modeling.Integration.ModelBusReference`。

   可以在**DSL 资源管理器**中的 "**域类型**" 下查看参考。 若要手动添加外部类型引用，请右键单击根节点。

- 将添加一个新的模板文件**Dsl\GeneratedCode\ModelBusReferencesSerialization.tt**。

将域属性的类型设置为 "ModelBusReference" 时，右键单击该属性，然后单击 "**启用 ModelBusReference 特定属性**"：

- 多个 CLR 特性已添加到域属性。 可在“属性”窗口的“自定义特性”字段中查看它们。 在**Dsl\GeneratedCode\DomainClasses.cs**中，可以在属性声明中查看属性：

  ```csharp
  [System.ComponentModel.TypeConverter(typeof(
  Microsoft.VisualStudio.Modeling.Integration.ModelBusReferenceTypeConverter))]
  [System.ComponentModel.Editor(typeof(
    Microsoft.VisualStudio.Modeling.Integration.Picker
    .ModelReferenceEditor // or ModelElementReferenceEditor
    ), typeof(System.Drawing.Design.UITypeEditor))]
  [Microsoft.VisualStudio.Modeling.Integration.Picker
    .SupplyFileBasedBrowserConfiguration
    ("Choose a model file", "Target model|*.target")]
  ```

右键单击 DSL 定义关系图时，单击 "**启用 ModelBus**"，然后选择 **"将此 DSL 公开到 ModelBus**：

- 新项目 `ModelBusAdapter` 已添加到解决方案。

- 对 `ModelBusAdapter` 的引用已添加到 `DslPackage` 项目。 `ModelBusAdapter` 具有对 `Dsl` 项目的引用。

- 在**DslPackage\source.extention.tt**中，`|ModelBusAdapter|` 添加为 MEF 组件。

## <a name="see-also"></a>请参阅

- [如何：在程序代码中从文件打开模型](../modeling/how-to-open-a-model-from-file-in-program-code.md)
- [如何：添加拖放处理程序](../modeling/how-to-add-a-drag-and-drop-handler.md)
- [在文本模板中使用 Visual Studio ModelBus](../modeling/using-visual-studio-modelbus-in-a-text-template.md)
