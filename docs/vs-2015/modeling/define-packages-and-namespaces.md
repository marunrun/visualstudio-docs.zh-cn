---
title: 定义包和命名空间 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- UML model, namespaces
- UML, namespaces
- UML, packages
- UML model, packages
ms.assetid: 79147068-02d5-4b70-933d-f647c1da3829
caps.latest.revision: 22
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 863df1da686e56a8b38c0652baf0aafab7436d08
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63434359"
---
# <a name="define-packages-and-namespaces"></a>定义包和命名空间
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在 Visual Studio 中，*包*是 UML 类、 用例和组件等元素的定义的容器。 包还可以包含其他包。  
  
 在 UML 模型资源管理器中，包内的所有定义都嵌套在包的下方。 UML 模型是一种包，用于构成树的根。  
  
 若要查看支持此功能的 Visual Studio 的版本，请参阅 [体系结构和建模工具的版本支持](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)。  
  
## <a name="in-this-topic"></a>本主题内容  
 [命名空间](#Namespaces)  
  
 [创建和查看包](#Packages)  
  
 [创建包内的模型元素](#Elements)  
  
 [将元素移入或移出包](#Moving)  
  
 [将元素粘贴到包](#Pasting)  
  
 [导入包之间的关系](#Import)  
  
 [从一个 Namespace 到另一个引用](#References)  
  
 [包的属性](#Properties)  
  
## <a name="Namespaces"></a> 命名空间  
 包对于将工作分隔为不同的区域十分有用。 每个包定义一个命名空间，以便在不同的包中定义的名称不会相互冲突。  
  
 每个元素的限定名属性就是其所属包的限定名，后跟该元素自己的名称。 例如，如果你有一个名为 `MyPackage` 的包，则该包中的类将拥有类似于 `MyPackage::MyClass` 的限定名。 由于每个元素都包含在模型中，每个限定名都以模型的名称开头。  
  
 模型也定义命名空间，因此模型中每个元素的限定名都以模型的名称开头。  
  
 其他模型元素也定义命名空间。 例如，一个操作属于其父类定义的命名空间，因此其限定名将类似于 `MyModel ::MyPackage ::MyClass ::MyOperation`。 同样，操作属于其父活动定义的命名空间。  
  
 包是容器。 如果移动或删除包，则包内定义的类、包及其他元素也会被移动或删除。 此规则对于其他定义命名空间的元素同样适用。  
  
## <a name="Packages"></a> 创建和查看包  
 可以在 UML 类图或 UML 模型资源管理器中创建包。  
  
#### <a name="to-create-a-package-in-a-uml-class-diagram"></a>在 UML 类图中创建包  
  
1. 打开一个 UML 类图或创建一个新的 UML 类图。  
  
2. 单击**包**工具。  
  
3. 在关系图上的任意位置单击。 此时将显示一个新的包的形状。  
  
     可以在现有包中单击，以将一个包嵌套到另一个包中。  
  
4. 为该包键入新名称。  
  
#### <a name="to-create-a-package-in-uml-model-explorer"></a>在 UML 模型资源管理器中创建包  
  
1. 打开**UML 模型资源管理器**。 上**体系结构**菜单，依次指向**Windows**，然后单击**UML 模型资源管理器**。  
  
2. 右键单击想要向其中添加新包的包或模型。  
  
   > [!NOTE]
   > 可以将一个包嵌套到另一个包中。  
  
3. 指向**外**，然后单击**包**。  
  
    此时模型中将显示新包。  
  
4. 为该包键入新名称。  
  
   如果已在 UML 模型资源管理器中创建了包，则可以让它在 UML 类图中显示。 还可以让包在多个 UML 类图中显示。  
  
#### <a name="to-show-an-existing-package-on-a-uml-class-diagram"></a>在 UML 类图中显示现有包  
  
- 将包从 UML 模型资源管理器拖动到类图中。  
  
    > [!NOTE]
    > 此操作会在该关系图中创建包的视图， 但不一定会在关系图中显示包中包含的所有元素。 要确保能看到包中的所有内容，请在 UML 模型资源管理器中进行查看。  
  
## <a name="Elements"></a> 创建包内的模型元素  
 可以通过以下四种方法将模型元素放置到包中：  
  
- 在 UML 模型资源管理器中将新元素添加到包中。  
  
- 在 UML 类图中将类和其他类型添加到包中。  
  
- 设置**LinkedPackage**关系图的属性，以便在关系图上创建新元素放置到您指定的包。 可以通过这种方式将类图、组件图和用例图链接到包。  
  
- 在 UML 模型资源管理器中将元素移入或移出包。  
  
  在 UML 模型资源管理器中，包中的元素将在包的下方显示，且其限定名以包的限定名开头。 若要查看的任何元素的限定的名称，右键单击该元素，然后依次**属性**。 **限定名**属性将出现在**属性**窗口。  
  
#### <a name="to-create-an-element-in-a-package-in-uml-model-explorer"></a>在 UML 模型资源管理器中创建包中的元素  
  
1. 打开**UML 模型资源管理器**。 上**视图**菜单，依次指向**其他 Windows**，然后单击**UML 模型资源管理器**。  
  
2. 右键单击想要向其中添加新元素的包或模型。  
  
3. 指向**添加**，然后单击你想要添加的元素的种类。  
  
     新元素将在包的下方显示。  
  
4. 为新元素键入名称。  
  
    > [!NOTE]
    > 新元素不会在任何关系图中显示。 要创建新元素的视图，可以将其从 UML 模型资源管理器拖动到关系图中。 该关系图必须为将显示此类元素的类型。  
  
#### <a name="to-create-an-element-in-a-package-on-a-uml-class-diagram"></a>在 UML 类图中创建包中的元素  
  
1. 打开其中会显示包的类图。  
  
    - 创建一个新包（如果尚未执行此操作）。  
  
    - 若要使现有类图上显示的包，可以将该包从**UML 模型资源管理器**拖动到类图上。  
  
2. 单击用于类、接口或枚举的工具，或单击包。  
  
3. 单击想要在其中放入新元素的包。  
  
     新元素将在包中显示。  
  
#### <a name="to-create-all-the-elements-of-a-diagram-in-a-specified-package"></a>在指定的包中创建关系图的所有元素  
  
1. 创建包（如果尚未执行此操作）。  
  
2. 打开组件图、用例图或 UML 类图。  
  
3. 打开关系图的属性。 在关系图的空白部分右键单击，然后单击**属性**。  
  
4. 在中**链接的包**属性中，选择你想要包含的关系图的内容的包。  
  
5. 在关系图中创建新元素。 这些元素将被放入包中。  
  
    - **限定名**的每个元素将以包的限定名开头。  
  
    - 在中**UML 模型资源管理器**，每个元素将显示在包的下方。  
  
## <a name="Moving"></a> 将元素移入和移出包  
 可以将一个或多个元素移入或移出包。  
  
 如果移动某个包，则其内部的所有内容都将随之一起移动。  
  
#### <a name="to-move-an-element-into-or-out-of-a-package"></a>将元素移入或移出包  
  
- 在 UML 模型资源管理器中，可以将元素拖入或拖出根为包的树。  
  
     元素的限定名将进行相应更改，以显示其所属的新包或新模型。  
  
     \- 或 -  
  
- 在类图中，将元素拖动到包的形状中。  
  
     元素的限定名将进行相应更改，以显示其所属的新包。  
  
    > [!NOTE]
    > 如果将一个元素从包中拖出，并将其放到关系图中的空白部分，那么其所属的包不会更改。 这样一来，你就可以绘制一个显示多个包中的元素，而不必显示包本身的关系图。  
  
## <a name="Pasting"></a> 将元素粘贴到包  
 可以将元素粘贴到包中。 如果将一组相关的元素粘贴到包中，那么这些元素之间的关系也会随之粘贴。  
  
#### <a name="to-paste-elements-into-a-package-on-a-uml-class-diagram"></a>在 UML 类图中将元素粘贴到包中  
  
1. 在 UML 类图中，选择想要复制的所有元素。 右键单击其中之一，然后单击**复制**。  
  
2. 右键单击包，然后单击**粘贴**。  
  
    > [!NOTE]
    > 包可以位于其他关系图上。  
  
## <a name="Import"></a> 导入包之间的关系  
 可以定义之间使用的包的导入关系**导入**工具。  
  
 导入意味着在导入的包中定义的元素（关系箭头端的元素）也会在导入包中进行有效定义。 其可见性定义为任何元素**包**将还在导入包中可见。  
  
 请避免在导入关系中创建循环。  
  
## <a name="References"></a> 从一个 Namespace 到另一个引用  
 如果要从一个包中引用另一个包中的元素，则必须使用该元素的限定名。  
  
 例如，假设包 `SalesCommon` 定义了类型 `CustomerAddress`。 在另一个包 `RestaurantSales` 中，你想要定义类型 `MealOrder`，该类型具有“客户地址”类型的一个特性。 你有两个选择：  
  
- 使用完全限定名 `SalesCommon::CustomerAddress` 指定特性的类型。 应执行此可以仅当`CustomerAddress`具有其**可见性**属性设置为**公共**。  
  
- 创建从 `RestaurantSales` 包到 `SalesCommon` 包的导入关系。 然后，可以直接使用 `CustomerAddress`，而无需使用其限定名。  
  
## <a name="Properties"></a> 包的属性  
 每个包都具有以下属性。 要查看的属性，右键单击关系图上或 UML 模型资源管理器中的程序包，然后单击**属性**。  
  
|属性|默认值|描述|  
|--------------|-------------------|-----------------|  
|**名称**|（新名称）|包名。 可以在关系图或“属性”窗口中更改该名称。|  
|**限定的名称**|*容器*::*包名称*|全名，以包含此包的包或模型的名称为前缀。 有关详细信息，请参阅[命名空间](#Namespaces)。|  
|**配置文件**|（空）|链接到此包的配置文件的列表。 这些配置文件提供可应用于包内元素的构造型。 有关详细信息，请参阅[自定义模型使用配置文件和构造型](../modeling/customize-your-model-with-profiles-and-stereotypes.md)。|  
|**可见性**|**Public**|包在其父包外部的可见性。|  
|**工作项**|（空）|已链接的工作项的列表。 有关详细信息，请参阅[链接模型元素和工作项](../modeling/link-model-elements-and-work-items.md)。|  
|**定义位置**|（名称）|存储包的详细信息的文件的名称。 这些文件位于**ModelDefinition**项目文件夹。 在进行源控制时这些信息十分有用。|  
|**说明**|（空）|对包的描述。|  
|**构造型**|（空）|应用于此包的构造型。 可用构造型的列表由你为此包以及包含此包的包选择的配置文件确定。 有关详细信息，请参阅[自定义模型使用配置文件和构造型](../modeling/customize-your-model-with-profiles-and-stereotypes.md)。|  
  
## <a name="how-packages-are-stored"></a>如何存储包  
 当创建新的包，一个新 **.uml**中创建文件**ModelDefinition**项目文件夹。 根模型，也是一个包，也存储在 **.uml**文件。  
  
 此外，每个关系图都存储在两个文件，其中一个表示关系图的形状和一个 **.layout**记录形状的位置的文件。  
  
## <a name="see-also"></a>请参阅  
 [编辑 UML 模型和关系图](../modeling/edit-uml-models-and-diagrams.md)   
 [UML 类关系图：引用](../modeling/uml-class-diagrams-reference.md)   
 [UML 类关系图：指导原则](../modeling/uml-class-diagrams-guidelines.md)   
 [管理版本控制下的模型和关系图](../modeling/manage-models-and-diagrams-under-version-control.md)
