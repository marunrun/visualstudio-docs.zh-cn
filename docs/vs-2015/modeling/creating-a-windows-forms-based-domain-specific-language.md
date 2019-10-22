---
title: 创建基于 Windows 窗体的域特定语言 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
ms.assetid: 452318ff-8ecf-46d0-8ca0-4013d0cdafaf
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: cea3b76575e1da2e846e230580c6cfa50ef9b207
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72651268"
---
# <a name="creating-a-windows-forms-based-domain-specific-language"></a>创建基于 Windows 窗体的域特定语言
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

您可以使用 Windows 窗体来显示域特定语言（DSL）模型的状态，而不是使用 DSL 关系图。 本主题演示如何使用 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 可视化和建模 SDK 将 Windows 窗体绑定到 DSL。

 ![DSL&#45;Wpf&#45;2](../modeling/media/dsl-wpf-2.png "DSL-Wpf-2")DSL 实例，显示 Windows 窗体 UI 和模型资源管理器。

## <a name="creating-a-windows-forms-dsl"></a>创建 Windows 窗体 DSL
 **最小 WinForm 设计器**DSL 模板会创建最小的 DSL，你可以根据自己的要求进行修改。

#### <a name="to-create-a-minimal-winforms-dsl"></a>创建最小的 WinForms DSL

1. 使用**最小 WinForm 设计器**模板创建 DSL。

    在本演练中，假定以下名称：

   |                       |                 |
   |-----------------------|-----------------|
   | 解决方案和 DSL 名称 |     FarmApp     |
   |       Namespace       | FarmApp |

2. 试验模板提供的初始示例：

   1. 转换所有模板。

   2. 生成并运行示例（**CTRL + F5**）。

   3. 在 Visual Studio 的实验实例中，打开调试项目中的 `Sample` 文件。

        请注意，它显示在 Windows 窗体控件中。

        您还可以在资源管理器中查看模型的元素。

        在窗体或资源管理器中添加一些元素，并注意它们显示在另一个显示中。

   在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 的主实例中，请注意 DSL 解决方案的以下几点：

- `DslDefinition.dsl` 不包含任何关系图元素。 这是因为不会使用 DSL 关系图来查看此 DSL 的实例模型。 相反，将 Windows 窗体绑定到模型，窗体上的元素将显示该模型。

- 除了 `Dsl` 和 `DslPackage` 项目，解决方案还包含一个名为 `UI.`**UI**项目的第三个项目，其中包含 Windows 窗体控件的定义。 `DslPackage` 依赖于 `UI`，`UI` 依赖于 `Dsl`。

- 在 `DslPackage` 项目中，`UI\DocView.cs` 包含显示 `UI` 项目中定义的 Windows 窗体控件的代码。

- @No__t_0 项目包含绑定到 DSL 的窗体控件的工作示例。 但是，在更改 DSL 定义后，它将不起作用。 @No__t_0 项目包含：

  - 名为 `ModelViewControl` Windows 窗体类。

  - 一个名为 `DataBinding.cs` 的文件，其中包含 `ModelViewControl` 的其他部分定义。 若要查看其内容，请在**解决方案资源管理器**中打开该文件的快捷菜单，然后选择 "**查看代码**"。

### <a name="about-the-ui-project"></a>关于 UI 项目
 当你更新 DSL 定义文件以定义你自己的 DSL 时，必须更新 `UI` 项目中的控件以显示你的 DSL。 与 `Dsl` 和 `DslPackage` 项目不同，示例 `UI` 项目不是从 `DslDefinitionl.dsl` 生成的。 如果需要，你可以添加 tt 文件以生成代码，但本演练中并未涉及到。

## <a name="updating-the-dsl-definition"></a>更新 DSL 定义
 此演练中使用了以下 DSL 定义。

 ![DSL&#45;Wpf&#45;1](../modeling/media/dsl-wpf-1.png "DSL-Wpf-1")

#### <a name="to-update-the-dsl-definition"></a>更新 DSL 定义

1. 在 DSL 设计器中打开 Dsldefinition.dsl。

2. 删除**ExampleElement**

3. 将**位于 examplemodel.store**域类重命名为 `Farm`。

     向其授予类型为**Int32**的 `Size` 的其他域属性和类型为**Boolean**的 `IsOrganic`。

    > [!NOTE]
    > 如果删除根域类，然后创建新的根，则必须重置编辑器的根类属性。 在**DSL 资源管理器**中，选择 "**编辑器**"。 然后在属性窗口中，将**根类**设置为 `Farm`。

4. 使用**指定的域类**工具创建以下域类：

    - `Field` –为此添加一个名为 `Size` 的其他域属性。

    - `Animal` –在属性窗口中，将 "**继承修饰符**" 设置为 "**抽象**"。

5. 使用**域类**工具创建以下类：

    - `Sheep`

    - `Goat`

6. 使用**继承**工具可以从 `Animal` 继承 `Goat` 和 `Sheep`。

7. 使用**嵌入**工具嵌入 `Farm` 下的 `Field` 和 `Animal`。

8. 您可能想要整理关系图。 若要减少重复元素的数目，请使用叶元素的快捷菜单上的 "将**子树置于此处**" 命令。

9. 转换解决方案资源管理器的工具栏中的**所有模板**。

10. 构建**Dsl**项目。

    > [!NOTE]
    > 在此阶段，其他项目不会生成任何错误。 但是，我们希望构建 Dsl 项目，使其程序集可用于数据源向导。

## <a name="updating-the-ui-project"></a>更新 UI 项目
 现在，你可以创建一个新的用户控件，该控件将显示 DSL 模型中存储的信息。 将用户控件连接到模型的最简单方法是通过数据绑定。 名为**ModelingBindingSource**的数据绑定适配器类型专门用于将 dsl 连接到非 VMSDK 接口。

#### <a name="to-define-your-dsl-model-as-a-data-source"></a>将 DSL 模型定义为数据源

1. 在 "**数据**" 菜单上，选择 "**显示数据源**"。

     “数据源”窗口随即打开。

     选择 "**添加新数据源**"。 “数据源配置”向导随即打开。

2. 选择 "**对象**"，"**下一步**"。

     展开 " **Dsl**"、" **FarmApp**"，然后选择 "**服务器场**"，它是模型的根类。 选择“完成”。

     在解决方案资源管理器中， **UI**项目现在包含**Properties\DataSources\Farm.datasource**

     模型类的属性和关系将显示在 "数据源" 窗口中。

     ![DslWpf&#45;3](../modeling/media/dslwpf-3.png "DslWpf-3")

#### <a name="to-connect-your-model-to-a-form"></a>将模型连接到窗体

1. 在**UI**项目中，删除所有现有的 .cs 文件。

2. 向**UI**项目添加一个名为 `FarmControl` 的新**用户控件**文件。

3. 在 "**数据源**" 窗口中的 "**服务器场**" 下拉菜单上，选择 "**详细信息**"。

    保留其他属性的默认设置。

4. 在 "设计" 视图中打开 FarmControl.cs。

    将**场**从 "数据源" 窗口拖到 "FarmControl"。

    将显示一组控件，每个属性对应一个控件。 关系属性不生成控件。

5. 删除**farmBindingNavigator**。 此方法也会在 `FarmControl` 设计器中自动生成，但对于此应用程序则无效。

6. 使用 "工具箱" 创建两个**DataGridView**实例，并将它们命名为 "`AnimalGridView`" 和 "`FieldGridView`"。

   > [!NOTE]
   > 另一步是将 "动物" 和 "字段" 项从 "数据源" 窗口拖到控件上。 此操作会自动创建网格视图和数据源之间的数据网格和绑定。 但是，此绑定不适用于 Dsl。 因此，最好手动创建数据网格和绑定。

7. 如果工具箱中不包含**ModelingBindingSource**工具，请添加它。 在 "**数据**" 选项卡的快捷菜单上，选择 "**选择项**"。 在 "**选择工具箱项**" 对话框中，从 " **.NET Framework" 选项卡**中选择 " **ModelingBindingSource** "。

8. 使用 "工具箱" 创建两个**ModelingBindingSource**实例，并将它们命名为 `AnimalBinding` 和 `FieldBinding`。

9. 将每个**ModelingBindingSource**的**DataSource**属性设置为**farmBindingSource**。

     将**DataMember**属性设置为**动物**或**字段**。

10. 将 `AnimalGridView` 的**数据源**属性设置为 `AnimalBinding`，并将 `FieldGridView` 设置为 `FieldBinding`。

11. 根据自己的喜好调整场控件的布局。

    **ModelingBindingSource**是一种适配器，它执行特定于 dsl 的多个函数：

- 它在 VMSDK 存储事务中包装更新。

   例如，当用户从数据视图网格中删除某行时，常规绑定将导致事务异常。

- 它可确保在用户选择某一行时，属性窗口显示相应模型元素的属性，而不是显示数据网格行。

  ![DslWpf4](../modeling/media/dslwpf4.png "DslWpf4")数据源和视图之间的链接架构。

#### <a name="to-complete-the-bindings-to-the-dsl"></a>完成到 DSL 的绑定

1. 在**UI**项目的单独代码文件中添加以下代码：

    ```csharp
    using System.ComponentModel;
    using Microsoft.VisualStudio.Modeling;
    using Microsoft.VisualStudio.Modeling.Design;

    namespace Company.FarmApp
    {
      partial class FarmControl
      {
        public IContainer Components { get { return components; } }

        /// <summary>Binds the WinForms data source to the DSL model.
        /// </summary>
        /// <param name="nodelRoot">The root element of the model.</param>
        public void DataBind(ModelElement modelRoot)
        {
          WinFormsDataBindingHelper.PreInitializeDataSources(this);
          this.farmBindingSource.DataSource = modelRoot;
          WinFormsDataBindingHelper.InitializeDataSources(this);
        }
      }
    }
    ```

2. 在**DslPackage**项目中，编辑**DslPackage\DocView.tt**以更新以下变量定义：

    ```csharp
    string viewControlTypeName = "FarmControl";
    ```

## <a name="testing-the-dsl"></a>测试 DSL
 现在，可以生成并运行 DSL 解决方案，但以后可能需要添加更多改进。

#### <a name="to-test-the-dsl"></a>测试 DSL

1. 生成和运行解决方案。

2. 在 Visual Studio 的实验实例中，打开**示例**文件。

3. 在**FarmApp 资源管理器**中，打开**场**根节点上的快捷菜单，然后选择 "**添加新 Goat**"。

     `Goat1` 显示在 "**动物**" 视图中。

    > [!WARNING]
    > 必须使用**场**节点上的快捷菜单，而不是 "**动物**" 节点。

4. 选择**场**根节点并查看其属性。

     在窗体视图中，更改场的**名称**或**大小**。

     离开窗体中的每个字段时，相应的属性更改属性窗口中。

## <a name="enhancing-the-dsl"></a>增强 DSL

#### <a name="to-make-the-properties-update-immediately"></a>使属性立即更新

1. 在 FarmControl.cs 的 "设计" 视图中，选择 "名称"、"大小" 或 "IsOrganic" 等简单字段。

2. 在属性窗口中 **，展开 "** databinding" 并打开 " **（高级）** "。

     在 "**格式设置和高级绑定**" 对话框的 "**数据源更新模式**" 下，选择 " **OnPropertyChanged**"。

3. 生成和运行解决方案。

     验证在更改字段内容时，场模型的相应属性会立即更改。

#### <a name="to-provide-add-buttons"></a>提供 "添加" 按钮

1. 在 FarmControl.cs 的 "设计" 视图中，使用 "工具箱" 来创建窗体上的按钮。

    编辑按钮的 "名称" 和 "文本"，例如 "`New Sheep`"。

2. 打开按钮后的代码（例如，通过双击来打开代码）。

    按如下所示对其进行编辑：

   ```csharp
   private void NewSheepButton_Click(object sender, EventArgs e)
   {
     using (Transaction t = farm.Store.TransactionManager.BeginTransaction("Add sheep"))
     {
       elementOperations.MergeElementGroup(farm,
         new ElementGroup(new Sheep(farm.Partition)));
       t.Commit();
     }
   }

   // The following code is shared with other add buttons:
   private ElementOperations operationsCache = null;
   private ElementOperations elementOperations
   {
     get
     {
       if (operationsCache == null)
       {
         operationsCache = new ElementOperations(farm.Store, farm.Partition);
       }
       return operationsCache;
     }
   }
   private Farm farm
   {
     get { return this.farmBindingSource.DataSource as Farm; }
   }

   ```

    还需要插入以下指令：

   ```csharp

   using Microsoft.VisualStudio.Modeling;

   ```

3. 为 "Goats" 和 "字段" 添加类似的按钮。

4. 生成和运行解决方案。

5. 验证 "新建" 按钮是否添加项。 新项应同时出现在 "FarmApp 资源管理器" 和相应的数据网格视图中。

    您应该能够在数据网格视图中编辑元素的名称。 你还可以从此处删除它。

   ![DSL&#45;Wpf&#45;2](../modeling/media/dsl-wpf-2.png "DSL-Wpf-2")

### <a name="about-the-code-to-add-an-element"></a>关于要添加元素的代码
 对于新元素按钮，以下替代代码稍微简单一些。

```csharp
private void NewSheepButton_Click(object sender, EventArgs e)
{
  using (Transaction t = farm.Store.TransactionManager.BeginTransaction("Add sheep"))
  {
    farm.Animals.Add(new Sheep(farm.Partition)); ;
    t.Commit();
  }
}

```

 但是，此代码不会设置新项的默认名称。 它不会运行你可能在 DSL 的**元素合并指令**中定义的任何自定义的合并，并且它不会运行可能已定义的任何自定义合并代码。

 因此，我们建议使用 <xref:Microsoft.VisualStudio.Modeling.ElementOperations> 来创建新元素。 有关详细信息，请参阅[自定义元素创建和移动](../modeling/customizing-element-creation-and-movement.md)。

## <a name="see-also"></a>请参阅
 [如何定义域特定语言](../modeling/how-to-define-a-domain-specific-language.md)[编写代码以为 Visual Studio 提供特定于域的语言](../modeling/writing-code-to-customise-a-domain-specific-language.md)[建模 SDK-特定于域](../modeling/modeling-sdk-for-visual-studio-domain-specific-languages.md)的语言
