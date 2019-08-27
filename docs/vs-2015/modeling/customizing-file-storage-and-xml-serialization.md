---
title: 自定义文件存储和 XML 序列化 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
f1_keywords:
- vs.dsltools.dsldesigner.xmlbehavior
helpviewer_keywords:
- Domain-Specific Language, serialization
ms.assetid: 76c53ef1-e3b9-45da-b425-1bddb3c01395
caps.latest.revision: 19
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: b41f5f6a3d937f23db1039fdab5e1cf7e36960ef
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63433256"
---
# <a name="customizing-file-storage-and-xml-serialization"></a>自定义文件存储和 XML 序列化
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

当用户保存实例，或*模型*，域特定语言 (DSL) 中的[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]，创建或更新的 XML 文件。 可以重新加载该文件以重新创建该模型存储区中。  
  
 可以通过调整下的设置自定义序列化方案**Xml 序列化行为**在 DSL 资源管理器。 在某个节点**Xml 序列化行为**为每个域类、 属性和关系。 关系都位于其源类下。 另外还有对应形状、 连接器和关系图类的节点。  
  
 此外可以编写更多高级自定义的程序代码。  
  
> [!NOTE]
> 如果你想要将模型保存在特定的格式，但不是需要重新加载它从该窗体，请考虑使用文本模板从模型中，而不是自定义序列化方案生成的输出。 有关详细信息，请参阅[从域特定语言生成代码](../modeling/generating-code-from-a-domain-specific-language.md)。  
  
## <a name="model-and-diagram-files"></a>模型和关系图文件  
 每个模型通常保存在两个文件：  
  
- 模型文件具有一个名称，如**Model1.mydsl**。 它将存储模型元素和关系和其属性。 如的文件扩展名 **.mydsl**由**FileExtension**属性**编辑器**DSL 定义中的节点。  
  
- 关系图文件有一个名称，例如**Model1.mydsl.diagram**。 它将存储这些形状、 连接器和它们的位置、 颜色、 线条粗细和关系图的外观的其他详细信息。 如果用户删除 **.diagram**文件中，在模型中的基本信息不会丢失。 仅关系图的布局将丢失。 当打开模型文件时，一组默认的形状并将创建连接器。  
  
#### <a name="to-change-the-file-extension-of-a-dsl"></a>若要更改 DSL 的文件扩展名  
  
1. 打开 DSL 定义中。 在 DSL 资源管理器，单击编辑器节点。  
  
2. 在属性窗口中编辑**FileExtension**属性。 不包括在初始"。"的文件扩展名。  
  
3. 在解决方案资源管理器中的两个项模板文件的名称更改**DslPackage\ProjectItemTemplates**。 这些文件的名称遵循以下格式：  
  
     `myDsl.diagram`  
  
     `myDsl.myDsl`  
  
## <a name="the-default-serialization-scheme"></a>默认序列化方案  
 若要创建一个用于本主题的示例，请使用以下的 DSL 定义。  
  
 ![DSL 定义关系图&#45;家族树模型](../modeling/media/familyt-person.png "FamilyT_Person")  
  
 此 DSL 用于创建在屏幕具有以下外观的模型。  
  
 ![家族树关系图、 工具箱和资源管理器](../modeling/media/familyt-instance.png "FamilyT_Instance")  
  
 此模型进行保存，然后重新在 XML 文本编辑器中打开它：  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<familyTreeModel xmlns:dm0="http://schemas.microsoft.com/VisualStudio/2008/DslTools/Core" dslVersion="1.0.0.0" Id="f817b728-e920-458e-bb99-98edc469d78f" xmlns="http://schemas.microsoft.com/dsltools/FamilyTree">  
  <people>  
    <person name="Henry VIII" birthYear="1491" deathYear="1547" age="519">  
      <children>  
        <personMoniker name="/f817b728-e920-458e-bb99-98edc469d78f/Elizabeth I" />  
        <personMoniker name="/f817b728-e920-458e-bb99-98edc469d78f/Mary" />  
      </children>  
    </person>  
    <person name="Elizabeth I" birthYear="1533" deathYear="1603" age="477" />  
    <person name="Mary" birthYear="1515" deathYear="1558" age="495" />  
  </people>  
</familyTreeModel>  
  
```  
  
 请注意，序列化模型有关的以下几点：  
  
- 每个 XML 节点具有域类名称相同的名称，只是首字母为小写形式。 例如，`familyTreeModel` 和 `person`。  
  
- 域属性，如名称和出生年份扩展会序列化为的 XML 节点中的属性。 同样，属性名称的初始字符转换为小写。  
  
- 每个关系序列化为 XML 节点嵌套在关系的源端。 该节点具有相同名称，为源角色属性，但大小写的初始字符。  
  
     例如，在 DSL 定义中，名为的角色**人们**源于**FamilyTree**类。  在 XML 中，这由名为的节点`people`嵌套在`familyTreeModel`节点。  
  
- 每个嵌入关系目标端序列化为嵌套在此关系下一个节点。 例如，`people`节点包含多个`person`节点。  
  
- 每个引用关系的目标端序列化为*名字对象*，这对目标元素的引用进行编码。  
  
     例如，在`person`节点，可以有`children`关系。 此节点包含名字对象，例如：  
  
    ```  
    <personMoniker name="/f817b728-e920-458e-bb99-98edc469d78f/Elizabeth I" />  
    ```  
  
## <a name="understanding-monikers"></a>了解名字对象  
 名字对象用于表示的模型和关系图文件的不同部分之间的交叉引用。 中还使用`.diagram`文件以引用的模型文件中的节点。 有两种形式的名字对象：  
  
- *Id 名字对象*用引号括起来的目标元素的 GUID。 例如：  
  
  ```  
  <personShapeMoniker Id="f79734c0-3da1-4d72-9514-848fa9e75157" />  
  
  ```  
  
- *限定键的名字对象*通过一个名为的名字对象密钥的指定的域属性的值确定目标元素。 目标元素的名字对象由其父元素的嵌入关系树中的名字对象作为前缀。  
  
   下面的示例取自 DSL 中这是一个名为唱片集，具有到域类名为的 Song 的嵌入关系的域类：  
  
  ```  
  <albumMoniker title="/My Favorites/Jazz after Teatime" />  
  <songMoniker title="/My Favorites/Jazz after Teatime/Hot tea" />  
  
  ```  
  
   如果目标类具有为其域属性，则使用限定键的名字对象选项**名字对象键**设置为`true`中**Xml 序列化行为**。 在示例中，此选项设置为"唱片集"和"歌曲"的域类中名为"Title"域属性。  
  
  限定键的名字对象是易于阅读比 ID 名字对象。 如果你想要的人员无法读取模型文件的 XML，请考虑使用限定键的名字对象。 但是，它是用户可以设置多个元素具有相同的名字对象密钥。 重复的键可能会导致不正确地重新下载文件。 因此，如果你定义使用限定键的名字对象引用的域类，则应考虑种方法可以防止用户保存具有重复名字对象的文件。  
  
#### <a name="to-set-a-domain-class-to-be-referenced-by-id-monikers"></a>若要设置用于引用的 ID 名字对象的域类  
  
1. 请确保**名字对象键**是`false`类和其基类中的每个域属性。  
  
    1. 在 DSL 资源管理器，展开**Xml 序列化 Behavior\Class 数据\\**_\<域类 >_**\Element 数据**。  
  
    2. 确认**名字对象键**是`false`针对每个域属性。  
  
    3. 如果域类具有一个基类，重复在该类中的过程。  
  
2. 设置**序列化 Id**  =  `true`域类。  
  
     此属性可以下找到**Xml 序列化行为**。  
  
#### <a name="to-set-a-domain-class-to-be-referenced-by-qualified-key-monikers"></a>若要设置用于限定键的名字对象引用的域类  
  
- 设置**名字对象键**现有域类的域属性。 属性的类型必须为`string`。  
  
    1. 在 DSL 资源管理器，展开**Xml 序列化 Behavior\Class 数据\\**_\<域类 >_**\Element 数据**，然后选择域属性。  
  
    2. 在属性窗口中设置**名字对象键**到`true`。  
  
- \- 或 -  
  
     创建新的域类使用**名为域类**工具。  
  
     此工具创建具有一个名为名称的域属性的新类。 **元素名称**并**是名字对象密钥**此域属性的属性初始化为`true`。  
  
- \- 或 -  
  
     创建从域类与具有的名字对象密钥属性的另一个类继承关系。  
  
### <a name="avoiding-duplicate-monikers"></a>避免重复名字对象  
 如果使用限定键的名字对象，就可以在用户的模型中的两个元素可能在键属性具有相同的值。 例如，如果 DSL 具有类有一个属性名称的人员，用户可以设置的两个元素的名称相同。 尽管可能是该模型保存到文件，它将不重新加载正确。  
  
 有几种方法，可帮助避免这种情况：  
  
- 设置**元素名称** =  `true`关键域属性。 选择域属性上的 DSL 定义关系图，然后在属性窗口中设置值。  
  
     当用户创建类的新实例时，此值会导致域属性自动分配一个不同的值。 默认行为的类名的末尾添加一个数字。 这不会阻止用户的名称更改为重复，但它可帮助在这种情况时用户将模型保存之前未设置的值。  
  
- 启用对 DSL 的验证。 在 DSL 资源管理器，选择编辑器 \ 验证，并设置**使用...** 属性设置为`true`。  
  
     没有二义性检查的自动生成的验证方法。 该方法是在`Load`验证类别。 这可确保它可能无法重新打开该文件会警告用户。  
  
     有关详细信息，请参阅[特定于域的语言中的验证](../modeling/validation-in-a-domain-specific-language.md)。  
  
### <a name="moniker-paths-and-qualifiers"></a>名字对象路径和限定符  
 限定键的名字对象结尾的名字对象密钥，并将名字对象为嵌入树中其父级的作为前缀。 例如，如果相册的名字对象为：  
  
```  
<albumMoniker title="/My Favorites/Jazz after Teatime" />  
  
```  
  
 然后在该唱片集的歌曲之一就是：  
  
```  
<songMoniker title="/My Favorites/Jazz after Teatime/Hot tea" />  
```  
  
 但是，如果唱片集改为引用的 ID，将按如下所示是名字对象：  
  
```  
<albumMoniker Id="77472c3a-9bf9-4085-976a-d97a4745237c" />  
<songMoniker title="/77472c3a-9bf9-4085-976a-d97a4745237c/Hot tea" />  
```  
  
 请注意，GUID 是唯一的因为它永远不会作为前缀的名字对象的父级。  
  
 如果您知道特定域属性将始终具有一个模型内的唯一值，则可以设置**是名字对象限定符**到`true`该属性。 这会导致它要用作限定符，而无需使用的名字对象的父级。 例如，如果您同时设置**是名字对象限定符**并**是名字对象密钥**唱片集类的 Title 域属性，该模型的名称或标识符中不使用名字对象的唱片集和其嵌入子级：  
  
```  
<albumMoniker name="Jazz after Teatime" />  
<songMoniker title="/Jazz after Teatime/Hot tea" />  
  
```  
  
## <a name="customizing-the-structure-of-the-xml"></a>自定义 XML 的结构  
 若要进行以下自定义，展开**Xml 序列化行为**DSL 资源管理器中的节点。 下一个域类中，展开要查看的属性和关系来源于此类列表的元素数据节点。 选择一种关系，并调整其属性窗口中的选项。  
  
- 设置**省略元素**为 true，以忽略源角色节点，离开只是目标元素的列表。 如果源和目标类之间存在多个关系，不应设置此选项。  
  
    ```  
  
    <familyTreeModel ...>  
      <!-- The following node is omitted by using Omit Element: -->  
      <!-- <people> -->  
        <person name="Henry VIII" .../>  
        <person name="Elizabeth I" .../>  
      <!-- </people> -->  
    </familyTreeModel>  
  
    ```  
  
- 设置**使用完整的窗体**表示关系实例的节点中嵌入的目标节点。 将域属性添加到域关系时，将自动设置此选项。  
  
    ```  
  
    <familyTreeModel ...>  
      <people>  
        <!-- The following node is inserted by using Use Full Form: -->  
        <familyTreeModelHasPeople myRelationshipProperty="x1">  
          <person name="Henry VIII" .../>  
        </familyTreeModelHasPeople>  
        <familyTreeModelHasPeople myRelationshipProperty="x2">  
          <person name="Elizabeth I" .../>  
        </familyTreeModelHasPeople>  
      </people>  
    </familyTreeModel>  
  
    ```  
  
- 设置**表示形式** = **元素**具有另存为元素而不是属性值的域属性。  
  
    ```  
    <person name="Elizabeth I" birthYear="1533">  
      <deathYear>1603</deathYear>  
    </person>  
    ```  
  
- 若要更改在其中的属性和关系进行序列化的顺序，请右键单击某项下的数据元素，并使用**移**或**下移**菜单命令。  
  
## <a name="major-customization-using-program-code"></a>使用程序代码的主要自定义  
 您可以替换部分或全部的序列化算法。  
  
 我们建议你先研究中的代码**Dsl\Generated Code\Serializer.cs**并**SerializationHelper.cs**。  
  
#### <a name="to-customize-the-serialization-of-a-particular-class"></a>若要自定义特定类的序列化  
  
1. 设置**是自定义**中的节点，在该类**Xml 序列化行为**。  
  
2. 转换所有模板、 生成解决方案，并调查导致的编译错误。 附近的每个错误的注释说明你需要提供哪些代码。  
  
#### <a name="to-provide-your-own-serialization-for-the-whole-model"></a>若要提供您自己的整个模型的序列化  
  
1. Dsl\GeneratedCode\SerializationHelper.cs 中重写方法  
  
## <a name="options-in-xml-serialization-behavior"></a>Xml 序列化行为中的选项  
 在 DSL 资源管理器，Xml 序列化行为节点包含有关每个域类、 关系、 形状、 连接符和关系图类的子节点。 在每个这些节点是属性和关系来源于该元素的列表。 关系本身就和在其源类表示。  
  
 下表总结了可在 DSL 定义的此部分中设置的选项。 每种情况下，在 DSL 资源管理器中选择一个元素并在属性窗口中设置的选项。  
  
### <a name="xml-class-data"></a>Xml 类数据  
 在 DSL 资源管理器下找到这些元素**Xml 序列化 Behavior\Class 数据**。  
  
|||  
|-|-|  
|属性|描述|  
|具有自定义元素的架构|如果为 True，指示域类具有自定义元素架构|  
|为自定义|将此设置为 **，则返回 True**如果想要编写自己的序列化和反序列化的代码，为此域类。<br /><br /> 生成解决方案，并调查错误以了解详细的说明。|  
|域类|此类数据节点应用到的域类。 只读。|  
|元素名称|此类的元素的 Xml 节点名称。 默认值为域类名称的小写版本。|  
|名字对象属性名|使用名字对象元素中包含引用的属性的名称。 如果保留为空，则使用 id 的键属性的名称。<br /><br /> 在此示例中，它是"name":  `<personMoniker name="/Mike Nash"/>`|  
|名字对象元素名称|用于引用此类的元素的名字对象的 xml 元素的名称。<br /><br /> 默认值为"Moniker"作为后缀的类名称的小写形式。 例如 `personMoniker`。|  
|名字对象的类型名称|此类的元素的名字对象生成的 xsd 类型的名称。 XSD，该文件中**Dsl\Generated 代码\\\*Schema.xsd**|  
|序列化 Id|如果为 True，在文件中包含该元素的 GUID。 这必须是如果标记没有属性为 true**名字对象键**和 DSL 定义引用关系到此类。|  
|类型名称|在 xsd 中指定的域类生成的 xml 类型的名称。|  
|说明|与此元素相关联的非正式说明|  
  
### <a name="xml-property-data"></a>Xml 属性数据  
 类节点下可找到 Xml 属性节点。  
  
|||  
|-|-|  
|属性|描述|  
|域属性|Xml 序列化配置数据应用到的属性。 只读。|  
|是名字对象密钥|如果为 True，则该属性用作创建引用此域类的实例的名字对象密钥。|  
|是名字对象限定符|如果为 True，该属性用于创建限定符在名字对象中。 如果为 false，并且同时将 SerializeId 不是此域类，则返回 true，名字对象进行限定由嵌入树中父元素的名字对象。|  
|表示形式|如果特性，则属性序列化为 xml 特性;如果元素，它是序列化为元素;如果忽略，则不序列化。|  
|Xml 名称|用于 xml 特性或元素表示的属性名称。 默认情况下，这是域的属性名称的小写版本。|  
|说明|与此元素相关联的非正式说明|  
  
### <a name="xml-role-data"></a>Xml 角色的数据  
 源类节点下可找到角色数据节点。  
  
|属性|描述|  
|--------------|-----------------|  
|具有自定义名字对象|设置为 true，如果你想要提供自己的代码生成和解决遍历此关系的名字对象。<br /><br /> 有关详细说明，生成解决方案，，然后双击错误消息。|  
|域关系|指定这些选项适用的关系。 只读。|  
|省略元素|如果为 true，该架构中省略对应于源角色的 XML 节点。<br /><br /> 如果源和目标类之间存在多个关系，此角色节点可区分属于两个关系的链接。 因此，我们建议，不设置此选项在这种情况下。|  
|角色元素名称|指定派生自源角色的 XML 元素的名称。 默认值为角色属性名称。|  
|使用完整的窗体|如果为 true，每个目标元素或名字对象被括在表示此关系的 XML 节点。 这应设置为 true，如果关系具有其自己的域属性。|  
  
## <a name="see-also"></a>请参阅  
 [导航和更新程序代码中的模型](../modeling/navigating-and-updating-a-model-in-program-code.md)   
 [从域特定语言生成代码](../modeling/generating-code-from-a-domain-specific-language.md)
