---
title: How to Define a Domain-Specific Language | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
f1_keywords:
- vs.dsltools.dsldesigner.domainrelationship
- vs.dsltools.dsldesigner.domainclass
- vs.dsltools.dsldesigner.domaintype
helpviewer_keywords:
- Domain-Specific Language, domain class
- Domain-Specific Language, external types
- Domain-Specific Language, relationships
- Domain-Specific Language, domain properties
ms.assetid: d1772463-0eb1-40a5-b7c0-9a008bc76760
caps.latest.revision: 45
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: b4bcd1f1f023c9e439fb870c9e31f07aa5be215d
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74299556"
---
# <a name="how-to-define-a-domain-specific-language"></a>如何定义域特定语言
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

若要定义域特定语言 (DSL)，请从模板创建 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 解决方案。 解决方案的重要组成部分是 DSL 定义关系图，它存储在 DslDefinition.dsl 中。 DSL 定义将定义 DSL 的类和形状。 在进行修改并将所做修改添加到这些元素后，可以添加程序代码以更详细地自定义 DSL。

 If you are new to DSLs, we recommend that you work through the **DSL Tools Lab**, which you can find in this site: [Visualizaton and Modeling SDK](https://go.microsoft.com/fwlink/?LinkID=186128)

## <a name="templates"></a> Selecting a Template Solution
 若要定义 DSL，必须安装以下组件：

|||
|-|-|
|[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]|[http://go.microsoft.com/fwlink/?LinkId=185579](https://go.microsoft.com/fwlink/?LinkId=185579)|
|[!INCLUDE[vssdk_current_short](../includes/vssdk-current-short-md.md)]|[http://go.microsoft.com/fwlink/?LinkId=185580](https://go.microsoft.com/fwlink/?LinkId=185580)|
|Visual Studio 可视化和建模 SDK|[http://go.microsoft.com/fwlink/?LinkID=186128](https://go.microsoft.com/fwlink/?LinkID=186128)|

 若要创建新的域特定语言，请使用域特定语言项目模板创建新的 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 解决方案。

#### <a name="to-create-a-dsl-solution"></a>创建 DSL 解决方案

1. Create a solution with the **Domain-Specific Language** template, which can be found under **Other Project Types/Extensibility** in the **New Project** dialog box.

    ![Create DSL dialog](../modeling/media/create-dsldialog.png "Create_DSLDialog")

    When you click **OK**, the **Domain-Specific Language Wizard** opens and displays a list of template DSL solutions.

2. 单击每个模板以查看说明。 选择最近似你想要创建的解决方案。

    每个 DSL 模板都将定义一种基本工作 DSL。 你将编辑此 DSL 来符合你自己的要求。

    单击每个示例以获取详细信息。

   - Select **Task Flow** to create a DSL that has swimlanes. 泳道是关系图的垂直或水平分区。

   - Select **Component Models** to create a DSL that has ports. 端口是较大形状边缘上的较小形状。

   - Select **Class Diagrams** to define a DSL that has compartment shapes. 隔离舱形状包含项列表。

   - Select **Minimal Language** in other cases, or if you are uncertain.

       > [!NOTE]
       > 如果想要创建类图或组件图，请考虑使用 UML 模型。 UML 建模工具提供了一组围绕单个模型集成的关系图。 这些关系图是可扩展的，并且可以使用 ModelBus 与你的 DSL 集成。 For more information, see [Create models for your app](../modeling/create-models-for-your-app.md).

   - Select **Minimal WinForm Designer** or **Minimal WPF Designer** to create a DSL that is displayed on a Windows Forms or WPF surface. 必须编写代码，才能定义编辑器。 有关更多信息，请参见下列主题：

        [创建基于 Windows 窗体的域特定语言](../modeling/creating-a-windows-forms-based-domain-specific-language.md)

        [创建基于 WPF 的域特定语言](../modeling/creating-a-wpf-based-domain-specific-language.md)

3. 在相应的向导页中输入 DSL 的文件扩展名。 这是包含 DSL 的实例的文件将使用的扩展名。

   - 选择不与你的计算机（或想要在其中安装 DSL 的任何计算机）中的任何应用程序关联的文件扩展名。 For example, **docx** and **htm** would be unacceptable file name extensions.

   - 如果你输入的扩展名已用作 DSL，则该向导将向你发出警告。 请考虑使用不同的文件扩展名。 还可以重置 Visual Studio SDK 实验实例以清除旧的实验设计器。 Click **Start**, click **All Programs**, **Microsoft Visual Studio 2010 SDK**, **Tools**, and then **Reset the Microsoft Visual Studio 2010 Experimental instance**.

4. 可以调整其他页面上的设置，或保留默认值。

5. 单击 **“完成”** 。

    该向导将创建包含两个或三个项目的解决方案，并从 DSL 定义生成代码。

   用户界面现在类似于下图。

   ![dsl 设计器](../modeling/media/dsl-designer.png "dsl_designer")

   此解决方案将定义域特定语言。 For more information, see [Overview of the Domain-Specific Language Tools User Interface](../modeling/overview-of-the-domain-specific-language-tools-user-interface.md).

### <a name="test-the-solution"></a>测试解决方案
 模板解决方案提供了一个工作 DSL，你可以对其进行修改或按原样使用。

 若要测试解决方案，请按 F5 或 CTRL+F5。 一个新的 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 实例将以实验模式打开。

 在新的 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 实例中，在“解决方案资源管理器”中，打开“Sample”文件。 它将打开为关系图，并带有一个工具箱。

 If you run a solution that you have created from the **Minimal Language** template, your experimental [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] will resemble the following example:

 ![](../modeling/media/dsl-min.png "DSL_min")

 试验这些工具。 创建元素并连接它们。

 关闭 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 的实验实例。

> [!NOTE]
> 已修改 DSL 后，你将不再能够查看“Sample”测试文件上的形状。 但是，将能够创建新元素。

### <a name="modifying-the-template-dsl"></a>修改模板 DSL
 重命名并保留模板 DSL 定义中的某些或全部域类和形状类。 新的类名应为有效的 CLR 名称，不带有空格或标点。

 它在保留以下类时将尤其有用：

- The root class appears at the upper-left of the DSL Definition diagram, under **Classes and Relationships**. 将它重命名为与 DSL 不同的名称。 For example, a DSL named **MusicLibrary** might have a root class named **Music**.

- The diagram class appears at the lower right of the DSL Definition diagram, in the **Diagram Elements** column. 可能必须滚动到右侧才能看到它。 It is typically named _YourDsl_**Diagram**.

- If you used the **Task Flow** template and you want to create diagrams with swimlanes, keep and rename the Actor domain class and ActorSwimlane shape.

  删除或重命名其他类以满足你的要求。

## <a name="patterns"></a> Patterns for Defining a DSL
 建议通过一次添加或调整一个或两个功能来开发 DSL。 添加功能、运行 DSL 并对其进行测试，然后再多添加一个或两个功能。 你的 DSL 的典型功能可能是：

- 域类、将元素连接到模型的嵌入关系、在关系图上显示该类的元素所需的形状，以及允许用户创建元素的元素工具。

- 域类的域属性和在形状上显示它们的修饰器。

- 引用关系和在关系图上显示它的连接符，以及允许用户创建链接的连接符工具。

- 需要程序代码的自定义，例如验证约束或菜单命令。

  以下部分将介绍如何构造几种最有用的 DSL 功能。 存在许多可以用来构造 DSL 的其他模式，但这些模式是最常用的。

> [!NOTE]
> After adding a feature, do not forget to click **Transform All Templates** in the toolbar of Solution Explorer before you build and running your DSL.

 下图显示了用作本主题中的示例的 DSL 的类和关系部分。

 ![Embedding and Reference relationships](../modeling/media/music-classes.png "Music_Classes")

 下图是此 DSL 的示例模型：

 ![Instance model of generated DSL](../modeling/media/music-instance.png "Music_Instance")

> [!NOTE]
> “模型”是指用户创建的 DSL 的实例，并且通常显示为关系图。 本主题讨论了 DSL 定义关系图和在使用 DSL 时显示的模型关系图。

## <a name="classes"></a> Defining Domain Classes
 域类表示 DSL 的概念。 The instances are *model elements*. For example in a **MusicLibrary** DSL you might have Domain Classes named **Album** and **Song**.

 To create a domain class, you can drag from the **Named Domain Class** tool to the diagram, and then rename the class.

 For more information, see [Properties of Domain Classes](../modeling/properties-of-domain-classes.md).

### <a name="create-an-embedding-relationship-for-each-domain-class"></a>为每个域类创建嵌入关系
 每个域类（根类除外）都必须至少是一个嵌入关系的目标，或必须继承自作为嵌入关系目标的类。

 在模型中，每个模型元素都是嵌入关系的单个树中的节点。 嵌入关系的源和目标通常称为父级和子级。

 域类的父级的选择取决于你希望其元素的生存期如何取决于其他元素。 如果删除树的节点，则通常也将删除其子树。 因此，独立存在的元素的类将直接嵌入在根类下。

 通常，如果将一个元素显示在另一个元素内，则你希望指示所有者关系。 在这种情况下，最合适的父类是容器的类。 当你在容器内看到的项实际只是指向独立元素的引用链接时除外。 在这种情况下，删除容器将删除引用但不删除其目标。

 在本主题所述的 DSL 定义的模式中，将假设当删除容器时也将删除显示在容器内的元素。 可以使用更为复杂的架构，并且可以通过定义规则来实现这些架构。

|元素的显示方式|父（嵌入）类|DSL 解决方案模板中的示例|
|------------------------------|--------------------------------|--------------------------------------|
|关系图上的形状。<br /><br /> 泳道。|DSL 的根类。|最小语言。<br /><br /> 任务流：Actor 类。|
|泳道中的形状。|显示为泳道的元素的域类。|任务流：Task 类。|
|形状中的列表中的项，其中项会随着容器的删除被一并删除。<br /><br /> 形状边缘上的端口。|映射到容器形状的域类。|类图：Attribute 类。<br /><br /> 组件图：Port 类。|
|列表中的项，删除容器时并不会删除项。|DSL 的根类。<br /><br /> 该列表将显示引用链接。||
|不直接显示。|由类作为一部分所组成的类。||

 在“音乐库”示例中，Album 将显示为在其中列出 Song 的标题的矩形。 因此，Album 的父级是根类 Music，而 Song 的父级是 Album。

 To create a domain class and its embedding at the same time, click the **Embedding Relationship** tool, then click the parent class, and then click on a blank part of the diagram.

 通常不必调整嵌入关系及其角色的名称，因为它们将自动跟踪类名。

 For more information, see [Properties of Domain Relationships](../modeling/properties-of-domain-relationships.md) and [Properties of Domain Roles](../modeling/properties-of-domain-roles.md).

> [!NOTE]
> 嵌入与继承不同。 嵌入关系中的子级不会从其父级继承功能。

### <a name="add-domain-properties-to-each-domain-class"></a>将域属性添加到每个域类
 域属性存储值。 示例为：Name、Title、Publication Date。

 Click **Domain Properties** in the class, press the ENTER key, and then type the name of a property. 域属性的默认类型是 String。 If you want to change the type, select the domain property, and set the **Type** in the **Properties** window. If the type that you want is not in the drop-down list, see [Adding Property Types](#addTypes).

 **Set an Element Name property.** Select a domain property that can be used to identify elements in the language explorer. 例如，在 Song 域类中可以选择 Title 域属性。 In the **Properties** window, set **Is Element Name** to `true`.

### <a name="create-derived-domain-classes"></a>创建派生的域类
 如果希望域类具有继承其属性和关系的变量，则创建从它派生的类。 例如，Album 可能具有派生类 WMA 和 MP3。

 Create the derived class using the **Domain Class** tool.

 Click the **Inheritance** tool, click the derived class, and then click the base class.

 Consider setting the **Inheritance Modifier** of the base class to **abstract**. 如果你认为可能需要基类的实例，则请考虑为它们创建单独的派生类。

 派生类继承其基类的属性和角色。

### <a name="tidy-the-dsl-definition-diagram"></a>整理 DSL 定义关系图
 在添加关系时，某些类将显示在多个地方。 To reduce the number of appearances and make the diagram wider, right-click the target class of a relationship, and then click **Bring Tree Here**. For the opposite effect, right-click the target class of a relationship and click **Split Tree**. 如果未看见这些菜单命令，则确保只选中域类。

 使用 CTRL+Up 和 CTRL+Down 来移动域类和形状类。

### <a name="test-the-domain-classes"></a>测试域类

##### <a name="to-test-the-new-domain-classes"></a>测试新的域类

1. **Click Transform All Templates** in the toolbar of Solution Explorer, to generate the DSL designer code. 可以自动化执行此步骤。 For more information, see [How to Automate Transform All Templates](https://msdn.microsoft.com/b63cfe20-fe5e-47cc-9506-59b29bca768a).

2. **Build and run the DSL.** Press F5 or CTRL+F5 to run a new instance of [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] in experimental mode. 在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 的实验实例中，打开或创建具有 DSL 的文件扩展名的文件。

3. **Open the Explorer.** At the side of the diagram is the language explorer window, which is usually named *YourLanguage* Explorer. 如果未看见此窗口，则它可能位于“解决方案资源管理器”下方的选项卡上。 If you cannot find it, on the **View** menu, point to **Other Windows**, and then click _YourLanguage_**Explorer**.

     资源管理器将呈现模型的树视图。

4. **Create new elements.** Right-click the root node at the top, and then click **Add New**_YourClass_.

     类的新实例显示在语言资源管理器中。

5. 在创建新实例时验证每个实例是否都具有不同名称。 This will occur only if you have set the **Is Element Name** flag on a domain property.

6. **Examine the domain properties. With an instance of your class selected,** inspect the Properties window. 它应显示在此域类上定义的域属性。

7. **Save the file, close it, and re-open it**. 在展开节点后，你创建的所有实例都应在资源管理器中可见。

## <a name="shapes"></a> Defining Shapes on the Diagram
 可以将显示在关系图上的元素的类定义为矩形、椭圆或图标。

#### <a name="to-define-a-class-of-elements-that-appear-as-shapes-on-a-diagram"></a>定义显示为关系图上的形状的元素的类

1. **Define and test a domain class as described in**  [Defining Domain Classes](#classes) **.**

   - 该类的父级应为根类。 即根类和新域类之间应存在嵌入关系。

   - 如果关系图具有泳道，则父级可以是映射到泳道的域类。 Before continuing with this procedure, see [Defining a DSL that has Swimlanes](#swimlanes).

2. **Add a shape class** to represent the elements on the model diagram. 从以下工具之一拖到 DSL 定义关系图上：

   - **Geometry Shape** provides a rectangle or ellipse.

   - **Image Shape** displays an image that you provide.

   - **Compartment Shape** is a rectangle that contains one or more lists of items.

     重命名形状类，它将显示在“形状”和“连接符”下的 DSL 定义关系图的右侧。

3. **Define an image, if you created an image shape**.

   1. 创建任意大小的图像文件。 支持 BMP、JPEG、GIF 和 EMF 格式。

   2. 在“解决方案资源管理”中，将文件添加到 Dsl\Resources 下的解决方案。

   3. 返回到 DSL 定义关系图，然后选择新的图像形状类。

   4. In the Properties window, click the **Image** property.

   5. In the **Select Image** dialog box, click the drop-down menu under **File name**, and select the image.

4. **Add text decorators to the shape, to display the domain properties.**

    若要显示模型元素的名称或标题，将可能需要至少一个文本修饰器。

    Right-click the header of the shape class, point to **Add**, and then click **Text Decorator**. Set the name of the decorator, and in the Properties window set its **Position**.

5. **Connect each shape with a Diagram Element Map to the domain class that it should display**.

    Click the **Diagram Element Map** tool, then click the domain class, then click the shape class.

6. **Map the properties to the text decorators.**

   1. 选中域类和形状类之间表示关系图元素映射的灰色线。

   2. In the **DSL Details** window, click the **Decorator Maps** tab. If you do not see the **DSL Details** window, on the **View** menu, point to **Other Windows** and then click **DSL Details**. 通常需要提升此窗口的顶部以查看它的所有内容。

   3. 选择修饰器的名称。 Under **Display property**, select the name of a property of the domain class. 为每个修饰器重复此过程。

       If you want to display a property of a related element, click the drop-down tree navigator under **Path to display property**.

   4. 确保复选标记出现在每个修饰器名称旁边。

      ![Shape Mappings and DSL Details window](../modeling/media/dsldetailswindow.png "DslDetailsWindow")

7. **Make a toolbox item for creating elements of the domain class.**

   1. In **DSL Explorer**, expand the **Editor** node and all its sub-nodes.

   2. Right-click the node under **Toolbox Tabs** that has the same name as your DSL, for example MusicLibrary. Click **Add Element Tool**.

       > [!NOTE]
       > If you right-click the **Tools** node, you will not see **Add Element Tool**. 应改为单击其上方的节点。

   3. In the Properties window with the new element tool selected, set **Class** to the domain class that you have recently added.

   4. Set **Caption** and **Tooltip**.

   5. Set **Toolbox Icon** to an icon that will appear in the toolbox. 可以将它设置为新图标或已用于其他工具的图标。

        To create a new icon, open Dsl\Resources in **Solution Explorer**. 复制并粘贴现有元素工具 BMP 文件之一。 重命名粘贴的副本，然后双击以对其进行编辑。

        Return to the DSL Definition diagram, select the tool, and in the Properties window click **[...]** in **Toolbox Icon**. In the **Select Bitmap** dialog box, select your .BMP file from the drop-down menu.

   For more information, see [Properties of Geometry Shapes](../modeling/properties-of-geometry-shapes.md) and [Properties of Image Shapes](../modeling/properties-of-image-shapes.md).

#### <a name="to-test-shapes"></a>测试形状

1. **Click Transform All Templates** in the toolbar of Solution Explorer, to generate the DSL designer code.

2. **Build and run the DSL.** Press F5 or CTRL+F5 to run a new instance of [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] in experimental mode. 在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 的实验实例中，打开或创建具有 DSL 的文件扩展名的文件。

3. **Verify that the element tools appear on the toolbox.**

4. **Create shapes** by dragging from a tool onto the model diagram.

5. **Verify that each text decorator appears,** and that:

   1. You can edit it, unless you have set the **Is UI Read Only** flag on the domain property.

   2. 当在“属性”窗口或在修饰器中编辑属性时，将更新其他视图。

   在首次测试形状后，你可能想要调整它的某些属性并添加一些更高级的功能。 For more information, see [Customizing and Extending a Domain-Specific Language](../modeling/customizing-and-extending-a-domain-specific-language.md).

## <a name="references"></a> Defining Reference Relationships
 可以在任何源域类和任何目标域类之间定义引用关系。 引用关系通常在关系图上显示为连接符，它们是形状之间的线条。

 例如，如果音乐 Album 和 Artist 在关系图上显示为形状，则可以定义名为 ArtistsAppearedOnAlbums 的关系，该关系可将 Artist 链接到所参与的 Album。 请参阅图中的示例。

 ![Instance model of generated DSL](../modeling/media/music-instance.png "Music_Instance")

 引用关系还可以链接相同类型的元素。 例如，在表示家族树的 DSL 中，父级及其子级之间的关系是从 Person 到 Person 的关系。

### <a name="define-a-reference-relationship"></a>定义引用关系
 单击“引用关系”工具、单击该关系的源域类，然后单击目标域类。 目标类可以与源类相同。

 每个关系具有两个角色，这些角色由关系框两侧上的线条表示。 可以选择每个角色并在“属性”窗口中设置其属性。

 **Consider renaming the roles**. 例如，在 Person 和 Person 之间的关系中，你可能想要将默认名称更改为 Parents 和 Children、Manager 和 Subordinates、Teacher 和 Student 等等。

 **Adjust the multiplicities of each role**, if it is necessary. 如果希望每个 Person 最多只有一个 Manager，则将显示在关系图上的 Manager 标签下的重数设置为 0..1。

 **Add domain properties to the relationship.** In the figure, the Artist-Album relationship has a property of role.

 **Set the Allows Duplicates property of the relationship,** if more than one link of the same class can exist between the same pair of model elements. 例如，可以允许 Teacher 向相同的 Student 教授多个 Subject。

 ![Shape maps for connectors](../modeling/media/music-connector.png "Music_Connector")

 For more information, see [Properties of Domain Relationships](../modeling/properties-of-domain-relationships.md) and [Properties of Domain Roles](../modeling/properties-of-domain-roles.md).

### <a name="define-a-connector-to-display-the-relationship"></a>定义连接符以显示关系
 连接符将在模型关系图上的两个形状之间显示一个线条。

 Drag the **Connector** tool onto the DSL definition diagram.

 如果想要在连接符上显示标签，则添加文本修饰器。 设置其位置。 To let the user move a text decorator, set its **Is Moveable** property.

 Use the **Diagram Element Map** tool to link the connector to the reference relationship.

 With the diagram element map selected, open the **DSL Details** window, and open the **Decorator Maps** tab.

 Select each **Decorator** and set **Display property** to the correct domain property.

 Make sure that a check mark appears next to each item in the **Decorators** list.

### <a name="define-a-connection-builder-tool"></a>定义“连接生成器”工具
 In the **DSL Explorer** window, expand the **Editor** node and all its subnodes.

 Right-click the node that has the same name as your DSL, and then click **Add New Connection Tool**.

 在新工具处于选中状态的同时，请在“属性”窗口中执行以下操作：

- Set the **Caption** and **Tooltip**.

- Click **Connection Builder** and select the appropriate builder for the new relationship.

- Set **Toolbox Icon** to the icon that you want to appear in the toolbox. 可以将它设置为新图标或已用于其他工具的图标。

     To create a new icon, open Dsl\Resources in **Solution Explorer**. 复制并粘贴现有元素工具 BMP 文件之一。 重命名粘贴的副本，然后双击以对其进行编辑。

     Return to the DSL Definition diagram, select the tool, and in the Properties window click **[...]** in **Toolbox Icon**. In the **Select Bitmap** dialog box, select your .BMP file from the drop-down menu.

##### <a name="to-test-a-reference-relationship-and-connector"></a>测试引用关系和连接符

1. **Click Transform All Templates** in the toolbar of Solution Explorer, to generate the DSL designer code.

2. **Build and run the DSL.** Press F5 or CTRL+F5 to run a new instance of [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] in experimental mode. 在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 的实验实例中，打开或创建具有 DSL 的文件扩展名的文件。

3. **Verify that the connection tool appears on the toolbox.**

4. **Create shapes** by dragging from a tool onto the model diagram.

5. **Create connections** between the shapes. 依次单击连接符工具、形状，然后单击另一个形状。

6. **Verify that you cannot create connections between inappropriate classes.** For example, if your relationship is between Albums and Artists, verify that you cannot link Artists to Artists.

7. **Verify that the multiplicities are correct. For example, verify that you cannot connect a Person to more than one manager.**

8. **Verify that each text decorator appears,** and that:

   1. You can edit it, unless you have set the **Is UI Read Only** flag on the domain property.

   2. 当在“属性”窗口或在修饰器中编辑属性时，将更新其他视图。

   在首次测试连接符后，你可能想要调整它的某些属性并添加一些更高级的功能。 For more information, see [Customizing and Extending a Domain-Specific Language](../modeling/customizing-and-extending-a-domain-specific-language.md).

## <a name="compartments"></a> Defining Shapes that Contain Lists: Compartment Shapes
 隔离舱形状包含一个或多个项列表。 例如，在“音乐库”DSL 中，可以使用隔离舱形状来表示音乐 Album。 在每个 Album 中，存在一个 Song 列表。

 ![Compartment Shape](../modeling/media/compartmentshape.png "CompartmentShape")

 采用在 DSL 定义中实现此效果的最简单方法，为容器定义一个域类，并为每个列表定义一个域类。 将容器类映射到隔离舱形状。

 ![Shape map](../modeling/media/music-mapcomp.png "Music_MapComp")

 For more information, see [Properties of Compartment Shapes](../modeling/properties-of-compartment-shapes.md).

#### <a name="to-define-a-compartment-shape"></a>定义隔离舱形状

1. **Create the container domain class**. Click the **Embedding Relationship** tool, click the root class of the model, and then click a blank part of the DSL definition diagram. 这将创建在示例图中名为 Album 的域类。

     另外，你可以将容器嵌入在映射到泳道的域类中，而不是嵌入在根域中。

     Add a domain property such as Name to the class, and set its **Is Element Name** flag in the Properties window.

2. **Create the list item domain class**. Click the **Embedding Relationship** tool, click the container class (Album) and then click a blank part of the diagram. 这将创建在示例图中名为 Song 的域类。

     Add a domain property such as Title to the class, and set its **Is Element Name** flag.

     添加其他域属性。

     为想要显示的每个列表添加其他列表项域类。

3. **To mix several types of item in the list**, create classes that inherit from the list class. Make the list class abstract by setting its **Inheritance Modifier**.

     例如，如果希望古典音乐按作曲家而不是艺术家进行排序，则可以创建 Song 的两个子类：ClassicalSong 和 NonClassicalSong。

4. **Create the compartment shape**. Drag from the **Compartment Shape** tool onto the DSL definition diagram.

     添加文本修饰器并设置其名称。

     添加隔离舱并设置其名称。

5. To let the user hide the list compartments, right-click the compartment shape class, point to **Add**, and then click **Expand/Collapse Decorator**. 在“属性”窗口中，设置修饰器的位置。

6. Click the **Diagram Element Map** tool, click the container domain class, and then click the compartment shape.

7. 选中域类和形状之间的关系图元素映射链接。 In the **DSL Details** window:

    1. Click the **Decorators** tab. Click the name of the decorator and then select the appropriate item under **Display Property**. 确保复选标记出现在修饰器的名称旁边。

    2. Click the **Compartment Maps** tab.

         单击隔离舱的名称。

         Under **Displayed elements collection path**, navigate to the list element class (Song). 单击下拉箭头以使用导航器工具。

         Under **Display Property**, select the property that should be displayed in the list. 在该示例中，此属性是 Title。

> [!NOTE]
> 通过使用“修饰器映射和隔离舱”映射字段中的“路径”字段，可以在域类和隔离舱形状之间建立更复杂的关系。

#### <a name="to-define-a-tool-for-creating-the-shape"></a>定义用于创建形状的工具

1. **Make a toolbox item for creating elements of the domain class.**

2. In **DSL Explorer**, expand the **Editor** node and all its sub-nodes.

3. Right-click the node under **Toolbox Tabs** that has the same name as your DSL, for example MusicLibrary. Click **Add Element Tool**.

    > [!NOTE]
    > If you right-click the **Tools** node, you will not see **Add Element Tool**. 应改为单击其上方的节点。

4. In the Properties window with the new element tool selected, set **Class** to the domain class that you have recently added.

5. Set **Caption** and **Tooltip**.

6. Set **Toolbox Icon** to an icon that will appear in the toolbox. 可以将它设置为新图标或已用于其他工具的图标。

     To create a new icon, open Dsl\Resources in **Solution Explorer**. 复制并粘贴现有元素工具 .BMP 文件之一。 重命名粘贴的副本，然后双击以对其进行编辑。

     Return to the DSL Definition diagram, select the tool, and in the Properties window click **[...]** in **Toolbox Icon**. In the **Select Bitmap** dialog box, select your BMP file from the drop-down menu.

#### <a name="to-test-a-compartment-shape"></a>测试隔离舱形状

1. **Click Transform All Templates** in the toolbar of Solution Explorer, to generate the DSL designer code.

2. **Build and run the DSL.** Press F5 or CTRL+F5 to run a new instance of [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] in experimental mode. 在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 的实验实例中，打开或创建具有 DSL 的文件扩展名的文件。

3. **Verify that the tool appears on the toolbox.**

4. 将工具拖到模型关系图上。 随即创建一个形状。

    验证是否显示元素的名称并且是否将其自动设置为默认值。

5. Right-click the header of the new shape, and then click Add *Your List Item.* 在该示例中，该命令是“添加 Song”。

    验证项是否显示在列表中以及是否具有新名称。

6. 单击其中一个列表项，然后检查“属性”窗口。 应看到列表项的属性。

7. 打开语言资源管理器。 验证是否可以看到内部具有列表项节点的容器节点。

   ![Generated explorer of DSL](../modeling/media/music-explorer.png "Music_Explorer")

   在首次测试隔离舱形状后，你可能想要调整它的某些属性并添加一些更高级的功能。 For more information, see [Customizing and Extending a Domain-Specific Language](../modeling/customizing-and-extending-a-domain-specific-language.md).

### <a name="displaying-a-reference-link-in-a-compartment"></a>在隔离舱中显示引用链接
 通常，在隔离舱中显示的元素是由隔离舱形状表示的元素的子级。 但是有时你可能想要显示使用引用关系链接到它的元素。

 例如，可以将第二个隔离舱添加到 AlbumShape，它将显示链接到 Album 的 Artist 列表。

 在这种情况下，隔离舱应显示链接而不是引用的元素。 这是因为当用户选中隔离舱中的项并按 DELETE 时，你会希望删除链接而不是引用的元素。

 然而，你可以使引用的元素的名称显示在隔离舱中。

 以下过程假设你已创建域类、引用关系、隔离舱形状和关系图元素映射，如本部分前面所述。

##### <a name="to-display-a-reference-link-in-a-compartment"></a>在隔离中显示引用链接

1. **Add a compartment to the compartment shape**. On the DSL Definition diagram, right-click the compartment shape class, point to **Add**, and then click **Compartment**.

2. Set **Displayed elements collection path** to navigate to the link, instead of its target element. 单击下拉菜单并使用树视图来选择引用关系而不是其目标。 In the example, the relationship is **ArtistAppearedOnAlbums**.

3. Set **Path to Display Property** to navigate from the link to the target element. In the example, this is **Artist**.

4. Set **Display Property** to the appropriate property of the target element, for example **Name**.

5. **Transform All Templates**, build and run the DSL, and open a test model.

6. 在模型关系图中，创建形状的相应类、设置它们的名称并在它们之间创建链接。 在隔离舱形状中，应显示链接元素的名称。

7. 在隔离舱形状中选择链接或项。 链接和项都应消失。

## <a name="ports"></a> Defining Ports on the Boundary of another Shape
 端口是位于另一个形状的边界上的形状。

 端口可以用于在另一个形状上提供固定连接点，用户可以将连接符绘制到端口。 在这种情况下，可以使端口形状变为透明。

 To see an example that uses ports, select the **Component Diagram** template when you create a new DSL solution. 此示例显示在定义端口时可以考虑的主要几点：

- 存在一个表示端口的容器的域类：`Component`。

- 存在一个表示端口的域类。 在该示例中，此域类是 `ComponentPort`。

- 存在一个从容器域类到端口域类的嵌入关系。 For more information, see [Defining Domain Classes](#classes).

- 如果你想要将不同类型的端口混合在同一容器上，则可以创建端口域类的子类。 在该示例中，`InPort` 和 `OutPort` 继承自 `ComponentPort`。

- 容器域类可以映射到任何类型的形状。 在该示例中，它是 `ComponentShape`。 For more information, see [Defining Shapes](#shapes).

- 端口域类可映射到端口形状。 可以将派生类映射到单独的端口形状类，或将基类映射到一个端口形状类。

  In other respects, port shapes behave as described in [Defining Shapes](#shapes).

  For more information, see [Properties of Port Shapes](../modeling/properties-of-port-shapes.md).

## <a name="swimlanes"></a> Defining a DSL that has Swimlanes
 泳道是关系图中的水平或垂直分区。 每个泳道都对应于一个模型元素。 DSL 定义需要一个用于泳道元素的域类。

 创建具有泳道的 DSL 的最佳方式是创建新 DSL 解决方案并选择“任务流”解决方案模板。 在 DSL 定义中，Actor 类是映射到泳道的域类。 重命名此类和其他类以符合你的项目。

 若要添加将显示为泳道内的形状的类，请在泳道类和新类之间创建嵌入关系。 用户能够将元素从一个泳道拖到另一个泳道，但每个元素都将始终位于特定泳道内。 在“任务流”解决方案模板中，FlowElement 是泳道类的子级。

 若要添加将显示为独立于泳道的形状的类，请在根类和新类之间创建嵌入关系。 用户能够将这些形状放置在关系图上的任意位置，包括跨泳道的边界和在泳道之外。 在“任务流”解决方案模板中，Comment 是根类的子级。

 For more information, see [Properties of Swimlanes](../modeling/properties-of-swimlanes.md).

## <a name="addTypes"></a> Adding Property Types

### <a name="domain-enumerations-and-literals"></a>域枚举和文本
 域枚举是具有多种文本值的类型。

 To add a domain enumeration, right-click the root of the model in the **DSL Explorer** and then click **Add New Domain Enumeration**. The element will appear in the **DSL Explorer** under the **Domain Types** node. 此元素不会显示在关系图上。

 To add enumeration literals to the domain enumeration, right-click the domain enumeration in the **DSL Explorer** and then click **Add New Enumeration Literal**.

 默认情况下，一次只能将具有枚举类型的属性设置为一个枚举值。 If you want users and programmers to be able to set any combination of values - a "bit field" - set the **IsFlags** property of the Enumeration.

### <a name="external-types"></a>外部类型
 When you set the type of a domain property, if you do not find the type you want in the **Type** drop-down list, you can add an external type. For example, you could add the **System.Drawing.Color** type to the list.

 To add a type, right-click the root of the model in DSL Explorer, and then click **Add New External Type**. In the Properties window, set the name to **Color** and the namespace to **System.Drawing**. This type now appears in DSL Explorer under **Domain Types**. 无论何时设置域属性的类型，你都可以选择此类型。

## <a name="custom"></a> Customizing the DSL
 使用本主题中所述的技术，可以通过关系图表示法、可读 XML 格式以及生成代码和其他项目所需的基础工具快速创建 DSL。

 有两种扩展 DSL 定义的方法：

1. 使用 DSL 定义的更多功能微调 DSL。 例如，你可以生成可创建多种类型的连接符的单个连接符工具，也可以通过删除一个元素也将删除相关元素的方式来控制规则。 这些技术主要通过在 DSL 定义中设置值来实现，而有些技术则需要几行程序代码。

     For more information, see [Customizing and Extending a Domain-Specific Language](../modeling/customizing-and-extending-a-domain-specific-language.md).

2. 通过使用程序代码扩展模型工具以实现更高级的效果。 例如，你可以创建可更改模型的菜单命令，也可以创建集成两个或多个 DSL 的工具。 VMSDK 专门用于轻松将扩展和从 DSL 定义生成的代码相集成。  For more information, see [Writing Code to Customise a Domain-Specific Language](../modeling/writing-code-to-customise-a-domain-specific-language.md).

### <a name="changing-the-dsl-definition"></a>更改 DSL 定义
 当在 DSL 定义中创建任何项时，将自动设置许多默认值。 设置完这些值后，你可以更改它们。 这将简化 DSL 的开发，同时仍允许强大的自定义。

 例如，在将形状映射到元素时，将根据域类的嵌入关系自动设置映射的“父元素路径”。 但是，如果之后更改了嵌入关系，则父元素路径将不会进行自动更改。

 因此请注意，更改 DSL 定义中的某些关系后，如果你保存了该定义或“转换所有模板”，则收到错误报告可能很正常。 大多数错误都易于修复。 双击错误报告来查看错误的位置。

 See also [How to: Change the Namespace of a Domain-Specific Language](../modeling/how-to-change-the-namespace-of-a-domain-specific-language.md).

## <a name="trouble"></a> Troubleshooting
 下表列出了在设计 DSL 时遇到的一些最常见问题，以及其解决方案的建议。 More advice is available on the [Visualization Tools Extensibililty Forum](https://go.microsoft.com/fwlink/?LinkId=186074).

|问题|建议|
|-------------|----------------|
|在 DSL 定义文件中进行的更改不起作用。|Click **Transform All Templates** in the toolbar above Solution Explorer, and then rebuild the solution.|
|形状显示了修饰器的名称而不是属性值。|设置修饰器映射。 在 DSL 定义关系图上，单击“关系图元素映射”，它是域类和形状类之间的灰色线条。<br /><br /> Open the **DSL Details** window. If you cannot see it, on the View menu, point to **Other Windows**, and then click **DSL Details**.<br /><br /> Click the **Decorator Maps** tab. Select the name of the decorator. 确保选中它旁边的框。 Under **Display property**, select the name of a domain property.<br /><br /> For more information, see [Shapes on the Diagram](#shapes).|
|在 DSL 资源管理器中，无法添加到集合。 例如，当右键单击“工具”时，菜单中没有“添加工具”命令。<br /><br /> 在 DSL 的资源管理器中，无法将元素添加到列表。|右键单击你正在尝试的节点上方的项。 当你想要添加到列表中时，“添加”命令不在列表节点中，而在其所有者中。|
|已创建域类，但无法在语言资源管理器中创建实例。|每个域类（根除外）都必须是嵌入关系的目标。|
|在 DSL 的资源管理器中，只显示元素及其类型名称。|In the DSL Definition, select a domain property of the class and in the Properties window, set **Is Element Name** to true.|
|始终在 XML 编辑器中打开 DSL。|发生这种情况是由于在读取文件的同时出现一个错误。 但是，即使在修复该错误后，也必须显式将该编辑器重置为 DSL 设计器。<br /><br /> Right-click the project item, click **Open With** and select _YourLanguage_**Designer (Default)** .|
|在更改程序集名称后，不会显示 DSL 的工具箱。|Inspect and update **DslPackage\GeneratedCode\Package.tt** For more information, see [How to: Change the Namespace of a Domain-Specific Language](../modeling/how-to-change-the-namespace-of-a-domain-specific-language.md).|
|不会显示 DSL 的工具箱，但并未更改程序集名称。<br /><br /> 或者，显示一个报告加载扩展失败的消息框。|重置实验实例，并重新生成解决方案。<br /><br /> 1.  At the Windows Start menu, under **All Programs**, expand [!INCLUDE[vssdk_current_long](../includes/vssdk-current-long-md.md)], then **Tools**, and then click **Reset the Microsoft Visual Studio Experimental Instance**.<br />2.  On the [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]**Build** menu, click **Rebuild Solution**.|

## <a name="see-also"></a>请参阅
 [Getting Started with Domain-Specific Languages](../modeling/getting-started-with-domain-specific-languages.md) [Creating a Windows Forms-Based Domain-Specific Language](../modeling/creating-a-windows-forms-based-domain-specific-language.md) [Creating a WPF-Based Domain-Specific Language](../modeling/creating-a-wpf-based-domain-specific-language.md)
