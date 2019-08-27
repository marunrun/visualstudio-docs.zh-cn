---
title: 域特定语言入门 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
ms.assetid: 024392a2-2c04-404f-a27b-7273553c3b60
caps.latest.revision: 18
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: ca90a90d476acc0bdbc1df426b981d98207bbd28
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65687251"
---
# <a name="getting-started-with-domain-specific-languages"></a>域特定语言入门
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本主题说明中定义和使用用于 Visual Studio 的建模 SDK 创建的特定于域的语言 (DSL) 的基本概念。  
  
 如果你是 Dsl，我们建议您通过**DSL 工具实验室**，可以在此站点中找到：[初学者和建模 SDK](http://go.microsoft.com/fwlink/?LinkID=186128)  
  
## <a name="what-can-you-do-with-a-domain-specific-language"></a>使用域特定语言，您可以做什么？  
 特定于域的语言是一个符号，通常为图形，用于为特定目的而设计。 与此相反，如 UML 的语言是通用的。 在 DSL 中，您可以定义模型元素和它们之间的关系，以及如何在屏幕上显示的类型。  
  
 当您已设计 DSL 时，可以将其作为 Visual Studio 集成扩展 (VSIX) 包的一部分进行分发。 用户使用在 DSL [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]:  
  
 ![家族树关系图、 工具箱和资源管理器](../modeling/media/familyt-instance.png "FamilyT_Instance")  
  
 表示法是仅的 DSL 的一部分。 表示法，以及 VSIX 包包括工具，用户可以应用以帮助他们编辑，并从其模型生成材料。  
  
 Dsl 的主体应用程序之一是生成程序代码、 配置文件和其他项目。 特别是在大型项目和产品系列，其中将创建产品的多个变量，从 Dsl 生成多个可变方面可以大幅增加中提供可靠性和快速响应需求的更改。  
  
 本概述的其余部分是一个演练，介绍了创建和使用中的域特定语言的基本操作[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]。  
  
## <a name="prerequisites"></a>系统必备  
 若要定义 DSL，必须安装以下组件：  
  
|||  
|-|-|  
|[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]|[http://go.microsoft.com/fwlink/?LinkId=185579](http://go.microsoft.com/fwlink/?LinkId=185579)|  
|[!INCLUDE[vssdk_current_short](../includes/vssdk-current-short-md.md)]|[http://go.microsoft.com/fwlink/?LinkId=185580](http://go.microsoft.com/fwlink/?LinkId=185580)|  
|Visual Studio 的建模 SDK|[下载 MSDK](https://www.microsoft.com/download/details.aspx?id=48148)|  
  
## <a name="creating-a-dsl-solution"></a>创建 DSL 解决方案  
 若要创建新的域特定语言，创建一个新[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]解决方案通过使用域特定语言项目模板。  
  
#### <a name="to-create-a-dsl-solution"></a>创建 DSL 解决方案  
  
1. 在 **“文件”** 菜单上，指向 **“新建”** ，然后单击 **“项目”** 。  
  
2. 下**项目类型**，展开**其他项目类型**节点，然后单击**扩展性**。  
  
3. 单击**域特定语言设计器**。  
  
    ![创建 DSL 对话框](../modeling/media/create-dsldialog.png "Create_DSLDialog")  
  
4. 在中**名称**框中，键入**FamilyTree**。 单击 **“确定”** 。  
  
    **域特定语言向导**将打开，并显示模板 DSL 解决方案的列表。  
  
    单击每个模板以说明，请参阅  
  
    模板是很有用起点。 每个提供完整的有效 DSL，可编辑以满足您的需要。 通常，您可以选择最接近您想要创建的模板。  
  
5. 对于本演练中，选择**最小语言**模板。  
  
6. 在相应的向导页中输入 DSL 的文件扩展名。 这是包含 DSL 的实例的文件将使用的扩展名。  
  
   - 选择与您的计算机，或想要安装 DSL 的任何计算机中的任何应用程序都不关联的扩展。 例如， **docx**并**htm**将不可接受的文件扩展名。  
  
   - 如果你输入的扩展名已用作 DSL，则该向导将向你发出警告。 请考虑使用不同的文件扩展名。 还可以重置 Visual Studio SDK 实验实例以清除旧的实验设计器。 单击**启动**，单击**所有程序**， **Microsoft Visual Studio 2010 SDK**，**工具**，，然后**重置 MicrosoftVisual Studio 2010 实验实例**。  
  
7. 检查其他页，然后单击**完成**。  
  
    一种解决方案会生成包含两个项目。 它们被命名为 Dsl 和 DslPackage。 关系图文件，它是打开命名的 DslDefinition.dsl。  
  
   > [!NOTE]
   > 你可以在两个项目中的文件夹中看到的代码大部分是从 DslDefinition.dsl 生成的。 出于此原因，对你的 DSL 的大多数修改都会在此文件中。  
  
   用户界面现在类似于下图。  
  
   ![DSL 设计器](../modeling/media/dsl-designer.png "dsl_designer")  
  
   此解决方案将定义域特定语言。 有关详细信息，请参阅[域特定语言工具用户界面的概述](../modeling/overview-of-the-domain-specific-language-tools-user-interface.md)。  
  
## <a name="the-important-parts-of-the-dsl-solution"></a>DSL 解决方案的重要部分  
 请注意，新的解决方案的以下方面。  
  
- **Dsl\DslDefinition.dsl**这是创建 DSL 解决方案时看到的文件。 此文件中，从生成解决方案中的几乎所有代码和此处所做的大部分对 DSL 定义所做的更改。 有关详细信息，请参阅使用[使用 DSL 定义关系图](../modeling/working-with-the-dsl-definition-diagram.md)。  
  
- **Dsl 项目**此项目包含用于定义特定于域的语言代码。  
  
- **DslPackage 项目**此项目包含允许的打开和编辑 DSL 实例的代码[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]。  
  
## <a name="Debugging"></a> 运行 DSL  
 一旦您已创建，可以运行 DSL 解决方案。 更高版本，您可以修改 DSL 定义逐渐，每次更改后再次运行该解决方案。  
  
#### <a name="to-experiment-with-the-dsl"></a>尝试使用 DSL  
  
1. 单击**转换所有模板**解决方案资源管理器工具栏中。 此时将重新生成大部分 DslDefinition.dsl 中的源代码。  
  
   > [!NOTE]
   > 只要您更改 DslDefinition.dsl，必须单击**转换所有模板**重新生成解决方案之前。 可以自动化执行此步骤。 有关详细信息，请参阅[如何自动执行转换所有模板](https://msdn.microsoft.com/b63cfe20-fe5e-47cc-9506-59b29bca768a)。  
  
2. 按 F5，或在**调试**菜单上，单击**开始调试**。  
  
    DSL 生成并已安装在实验实例中的[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]。  
  
    此时将启动 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 的实验实例。 实验实例中将其设置从单独的子树的注册表中，其中[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]扩展注册以便进行调试。 正常实例[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]不具有访问的已那里注册的扩展。  
  
3. 在实验实例中的[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]，打开名为的模型文件**测试**从**解决方案资源管理器**。  
  
    \- 或 -  
  
    右键单击调试项目，指向**外**，然后单击**项**。 在中**添加项**对话框中，选择你的 DSL 的文件类型。  
  
    作为一个空白图表打开模型文件。  
  
    工具箱中打开并显示适用于关系图类型的工具。  
  
4. 使用这些工具在关系图上创建的形状和连接线。  
  
   1. 若要创建形状，将从该示例形状工具拖动到关系图。  
  
   2. 若要连接两个形状，单击示例连接器工具，单击第一个形状，然后单击第二个形状。  
  
5. 单击形状，以更改它们的标签。  
  
   在实验性[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]将类似于下面的示例：  
  
   ![](../modeling/media/dsl-min.png "DSL_min")  
  
### <a name="the-content-of-a-model"></a>模型的内容  
 调用是 DSL 的实例的文件的内容*模型*。 该模型包含*模型元素*并*链接*元素之间。 DSL 定义中指定哪些类型的模型元素，并可以存在于模型中的链接。 例如，在最小语言模板创建的 DSL，没有一种类型的模型元素和一个类型的链接。  
  
 DSL 定义中可以指定模型关系图上的显示方式。 您可以选择使用不同的形状和连接线的样式。 您可以指定某些形状出现在其他形状内。  
  
 可以查看模型中的树形**资源管理器**查看编辑模型时。 形状添加到关系图时，在资源管理器还显示模型元素。 可以使用资源管理器中，即使没有关系图。  
  
 如果您不能看到的调试实例中的资源管理器[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]，然后在**视图**菜单中的指向**其他 Windows**，然后单击 *\<Your 语言>* **资源管理器**。  
  
### <a name="the-api-of-your-dsl"></a>你的 DSL 的 API  
 你的 DSL 生成的 API，可用于读取和更新 DSL 实例模型。 一个应用程序的 api 是从模型生成的文本文件。 有关详细信息，请参阅[使用 T4 文本模板生成设计时代码](../modeling/design-time-code-generation-by-using-t4-text-templates.md)。  
  
 在调试解决方案中，使用扩展".tt"中打开模板文件。 这些示例演示如何从模型中，生成文本，并可用于测试你的 DSL 的 API。 其中一个示例用[!INCLUDE[vbprvb](../includes/vbprvb-md.md)]，则在其他[!INCLUDE[csprcs](../includes/csprcs-md.md)]。  
  
 在每个模板文件是它将生成的文件。 展开模板文件在解决方案资源管理器，并打开生成的文件。  
  
 模板文件包含简短的一段代码，它列出了在模型中的所有元素。  
  
 生成的文件包含结果。  
  
 当您更改模型文件时，重新生成文件后，会看到生成的文件中的相应更改。  
  
##### <a name="to-regenerate-text-files-after-you-change-the-model-file"></a>若要更改模型文件后，重新生成文本文件  
  
1. 在实验实例中的[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]，保存该模型文件。  
  
2. 请确保每个.tt 文件中的文件名称参数引用用于试验的模型文件。 保存.tt 文件。  
  
3. 单击**转换所有模板**中的工具栏**解决方案资源管理器**。  
  
    \- 或 -  
  
    右键单击你想要重新生成，然后单击模板**运行自定义工具**。  
  
   可以将任意数量的文本模板文件添加到项目。 每个模板生成一个结果文件。  
  
> [!NOTE]
> 当您更改 DSL 定义中时，示例文本模板代码才会生效，更新它。  
  
 有关详细信息，请参阅[从域特定语言生成代码](../modeling/generating-code-from-a-domain-specific-language.md)并[编写代码以自定义域特定于域的语言](../modeling/writing-code-to-customise-a-domain-specific-language.md)。  
  
## <a name="customizing-the-dsl"></a>自定义 DSL  
 当你想要修改 DSL 定义中时，关闭实验实例并更新主定义[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]实例。  
  
> [!NOTE]
> 已修改 DSL 定义后，可能会丢失已使用早期版本创建的测试模型中的信息。  例如，调试解决方案包含名为示例，其中包含一些形状和连接线的文件。 在开始开发你的 DSL 定义后，它们将不可见，并保存文件时它们将会丢失。  
  
 您可以对你的 DSL 各种各样的扩展。 下面的示例将为您提供展示了可能的值。  
  
 每个更改后，保存 DSL 定义中，单击**转换所有模板**中**解决方案资源管理器**，然后按**F5**尝试使用已更改的 DSL。  
  
### <a name="rename-the-types-and-tools"></a>重命名类型和工具  
 重命名现有的域类和关系。 例如，从最小语言模板创建的 Dsl 定义开始，你可以执行以下重命名操作，以使表示家族树的 DSL。  
  
##### <a name="to-rename-domain-classes-relationships-and-tools"></a>若要重命名域类、 关系和工具  
  
1. DslDefinition 关系图中，在重命名**ExampleModel**到**FamilyTreeModel**， **ExampleElement**到**人员**， **目标**到**父级**，和**源**到**子级**。 您可以单击每个标签来对其进行更改。  
  
     ![DSL 定义关系图&#45;家族树模型](../modeling/media/familyt-person.png "FamilyT_Person")  
  
2. 重命名的元素和连接器工具。  
  
    1. 通过在解决方案资源管理器下单击选项卡中打开 DSL 资源管理器窗口。 如果看不到它，在**视图**菜单中的指向**其他 Windows** ，然后单击**DSL 资源管理器**。 仅当 DSL 定义关系图是活动窗口时，DSL 资源管理器是可见的。  
  
    2. 打开属性窗口并将其置于，以便可以同时看到 DSL 资源管理器和属性。  
  
    3. 在 DSL 资源管理器，展开**编辑器**，**工具箱选项卡**，  *\<DSL >* ，然后**工具**。  
  
    4. 单击**ExampleElement**。 这是用于创建元素的工具箱项。  
  
    5. 在属性窗口中更改**名称**属性设置为**人员**。  
  
         请注意，**标题**属性也会更改。  
  
    6. 在相同的方式中的名称更改**ExampleConnector**工具到**ParentLink**。 Alter**标题**属性，以便它不是 Name 属性的副本。 例如，输入**父链接**。  
  
3. 重新生成 DSL。  
  
    1. 将 DSL 定义文件。  
  
    2. 单击**转换所有模板**的工具栏中的解决方案资源管理器  
  
    3. 按 F5。 等到的实验实例[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]出现。  
  
4. 在实验实例中的调试解决方案中[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]，打开测试模型文件。 从工具箱拖放到它的元素。 请注意工具隐藏式字幕和 DSL 资源管理器中的类型名称已更改。  
  
5. 保存模型文件。  
  
6. 打开一个.tt 文件和旧类型和属性名称的匹配项替换为新名称。  
  
7. 请确保在.tt 文件中指定的文件名称指定测试模型。  
  
8. 保存.tt 文件。 打开生成的文件，以查看在.tt 文件中运行代码的结果。 验证正确。  
  
### <a name="add-domain-properties-to-classes"></a>将域属性添加到类  
 将属性添加到域类，例如要表示年的出生和死亡的人员。  
  
 若要使新属性关系图上可见，必须添加*修饰器*为显示模型元素的形状。 此外必须将属性映射到修饰器。  
  
##### <a name="to-add-properties-and-display-them"></a>若要添加的属性并将其显示  
  
1. 添加属性。  
  
   1. 在 DSL 定义关系图中，右键单击**Person**域类中，依次指向**添加**，然后单击**域属性**。  
  
   2. 键入一系列新的属性名称，如**出生**并**死亡**。 按**Enter**后每个。  
  
2. 添加将在形状中显示的属性的修饰器。  
  
   1. 按照从 Person 域类延伸到关系图的另一端的灰色线条。 这是关系图元素映射。 它链接到形状类的域类。  
  
   2. 右键单击此形状类、 指向**外**，然后单击**文本修饰器**。  
  
   3. 添加两个具有名称的修饰器，例如**BirthDecorator**并**DeathDecorator**。  
  
   4. 选择每个新的修饰器，并在属性窗口中设置**位置**字段。 这可确定将在形状中显示域属性值。 例如，设置**InnerBottomLeft**并**InnerBottomRight**。  
  
        ![隔离舱形状定义](../modeling/media/familyt-compartment.png "FamilyT_Compartment")  
  
3. 将修饰器映射到属性。  
  
   1. 打开 DSL 详细信息窗口中。 它通常是在输出窗口的旁边的选项卡。 如果看不到它，在**视图**菜单，依次指向**其他 Windows**，然后单击**DSL 详细信息**。  
  
   2. 在 DSL 定义关系图中，单击连接的连线**人员**到形状类的域类。  
  
   3. 在中**DSL 详细信息**，然后在**修饰器映射**选项卡上，单击上未映射的修饰器的复选框。 在中**显示属性**，选择要其映射的域属性。 例如，映射**BirthDecorator**到**出生**。  
  
4. 保存 DSL 中，单击转换所有模板，并按 F5。  
  
5. 在示例模型关系图中，验证你现在可以单击所选的位置并向其中键入值。 此外，选择**人员**形状，属性窗口显示出生和死亡的新属性。  
  
6. 在.tt 文件中，可以添加代码可用于获取每个 person 的属性。  
  
   ![家族树关系图、 工具箱和资源管理器](../modeling/media/familyt-instance.png "FamilyT_Instance")  
  
### <a name="define-new-classes"></a>定义新类  
 可以向模型添加域类和关系。 例如，可以创建一个新类来表示城市分类，以及新的关系来表示一个人惊叹闪亮登场。  
  
 若要使不同的类型在模型关系图上不同，可以对不同类型的形状，或使用不同的几何图形和颜色的形状映射的域类。  
  
##### <a name="to-add-and-display-a-new-domain-class"></a>若要添加并显示新的域类  
  
1. 添加域类，并使其模型根的子级。  
  
    1. 在 DSL 定义关系图中，单击**嵌入关系**工具中，单击根类**FamilyTreeModel**，然后单击关系图的空白部分。  
  
         新的域类将出现，连接到与嵌入关系 FamilyTreeModel。  
  
         设置其名称，例如**城镇**。  
  
        > [!NOTE]
        > 除了根模型的每个域类必须至少一个嵌入关系的目标或它必须继承自目标的一个嵌入的类。 出于此原因，它是通常比较方便使用的嵌入关系工具创建域类。  
  
    2. 将域属性添加到新类，例如**名称**。  
  
2. 添加人员和城市之间的引用关系。  
  
    1. 单击**引用关系**工具中，单击人员，然后单击城镇。  
  
         ![DSL 定义片段： 家谱根目录](../modeling/media/familyt-root.png "FamilyT_Root")  
  
        > [!NOTE]
        > 引用关系到另一个从模型树的一部分表示交叉引用。  
  
3. 添加形状以表示城市分类模型关系图上。  
  
    1. 拖动**几何形状**从工具箱拖到关系图并进行重命名，例如**TownShape**。  
  
    2. 在属性窗口中设置新的形状，如填充颜色和几何图形的外观字段。  
  
    3. 添加要显示的城市名称的修饰器，并将其重命名 NameDecorator。 设置其位置属性。  
  
4. 映射到 TownShape 城镇域类。  
  
    1. 单击**关系图元素映射**工具，然后单击城镇域类，然后 TownShape 形状类。  
  
    2. 在中**修饰器映射**选项卡**DSL 详细信息**所选窗口与地图连接器、 检查 NameDecorator 并设置**显示属性**为名称。  
  
5. 创建连接器，以显示 Person 和城市分类之间的关系。  
  
    1. 将连接线从工具箱拖到关系图。 将其重命名并设置其外观属性。  
  
    2. 使用**关系图元素映射**工具，用于将新连接符链接到 Person 和城市之间的关系。  
  
         ![添加了形状映射的家谱定义](../modeling/media/familyt-shapemap.png "FamilyT_ShapeMap")  
  
6. 创建进行新建城镇元素工具。  
  
    1. 在中**DSL 资源管理器**，展开**编辑器**然后**工具箱选项卡**。  
  
    2. 右键单击 *\<DSL >* ，然后单击**添加新元素工具**。  
  
    3. 设置**名称**属性的新工具，并设置其**类**城镇属性。  
  
    4. 设置**工具箱图标**属性。 单击 **[...]** 然后在**文件名**字段中，选择一个图标文件。  
  
7. 创建连接符工具使城市分类与人之间的链接。  
  
    1. 右键单击 *\<DSL >* ，然后单击**添加新的连接器工具**。  
  
    2. 设置新的工具的名称属性。  
  
    3. 在中**ConnectionBuilder**属性中，选择包含 Person-town 关系的名称的生成器。  
  
    4. 设置**工具箱图标**。  
  
8. 保存 DSL 定义中，单击**转换所有模板**，然后按**F5**。  
  
9. 在实验实例中的[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]，打开测试模型文件。 使用新工具来创建城镇和城镇和人员之间的链接。 请注意，只能创建正确类型的元素之间的链接。  
  
10. 创建代码，其中列出了在其中每个人员所在的城镇。 文本模板是一种在其上运行此类代码的位置。 例如，可以修改调试解决方案中的现有 Sample.tt 文件，使其包含以下代码：  
  
    ```  
    <#@ template inherits="Microsoft.VisualStudio.TextTemplating.VSHost.ModelingTextTransformation" debug="true" #>  
    <#@ output extension=".txt" #>  
    <#@ FamilyTree processor="FamilyTreeDirectiveProcessor" requires="fileName='Sample.ftree'" #>  
  
    <#  
      foreach (Person person in this.FamilyTreeModel.People)  
      {  
    #>  
        <#= person.Name #><#if (person.Town != null) {#> of <#= person.Town.Name #> <#}#>  
  
    <#  
          foreach (Person child in person.Children)  
      {  
    #>  
                <#= child.Name #>  
    <#  
      }  
      }  
    #>  
  
    ```  
  
     当保存 *.tt 文件时，它将创建一个包含的人员和其派驻服务列表的附属文件。 有关详细信息，请参阅[从域特定语言生成代码](../modeling/generating-code-from-a-domain-specific-language.md)。  
  
## <a name="validation-and-commands"></a>验证和命令  
 可以通过添加验证约束来开发此 DSL 进一步。 这些约束是可以定义，请确保在模型处于正确状态的方法。 例如，您可以子级的出生日期晚于其父项的定义一个约束以确保。 验证功能显示警告，如果 DSL 用户尝试保存模型，可断开的任何约束。 有关详细信息，请参阅[特定于域的语言中的验证](../modeling/validation-in-a-domain-specific-language.md)。  
  
 此外可以定义用户可调用的菜单命令。 命令可以修改模型。 此外可以与其他模型中进行交互它们[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]和与外部资源。 有关详细信息，请参阅[如何：修改标准的菜单命令](../modeling/how-to-modify-a-standard-menu-command-in-a-domain-specific-language.md)。  
  
## <a name="deploying-the-dsl"></a>部署 DSL  
 若要允许其他用户使用域特定语言，你将分发[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]扩展 (VSIX) 文件。 生成 DSL 解决方案时，这被创建。  
  
 你的解决方案的 bin 文件夹中找到的.vsix 文件。 将其复制到要安装它的计算机。 在该计算机中，双击 VSIX 文件。 可在所有情况下的 DSL[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]该计算机上。  
  
 可以使用相同的过程，以便无需使用的实验实例中在你自己的计算机上安装 DSL [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]。  
  
 有关详细信息，请参阅[部署域特定语言解决方案](../modeling/deploying-domain-specific-language-solutions.md)。  
  
## <a name="Reset"></a> 删除旧的实验性 Dsl  
 如果你已创建实验性 Dsl，你不希望再，则可以从您的计算机通过删除重置[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]实验实例。  
  
 这将从计算机中删除所有实验性 Dsl 和其他试验性[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]扩展。 这些是在调试模式下执行的扩展。  
  
 此过程不会删除 Dsl 或其他[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]已经通过执行 VSIX 文件的完全安装的扩展。  
  
#### <a name="to-reset-the-visual-studio-experimental-instance"></a>若要重置 Visual Studio 实验实例  
  
1. 单击**启动**，单击**所有程序**， **Microsoft Visual Studio 2010 SDK**，**工具**，，然后**重置 MicrosoftVisual Studio 2010 实验实例**。  
  
2. 重新生成任何实验性 Dsl 或其他实验性[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]仍想要使用的扩展。  
  
## <a name="see-also"></a>请参阅  
 [了解模型、 类和关系](../modeling/understanding-models-classes-and-relationships.md)   
 [如何定义特定于域的语言](../modeling/how-to-define-a-domain-specific-language.md)   
 [初学者和建模 SDK](http://go.microsoft.com/fwlink/?LinkID=186128)
