---
title: 自定义文件存储和 XML 序列化
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.dsltools.dsldesigner.xmlbehavior
helpviewer_keywords:
- Domain-Specific Language, serialization
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 27d8672ea94cf2a1547904f313ac36509f111462
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72748459"
---
# <a name="customize-file-storage-and-xml-serialization"></a>自定义文件存储和 XML 序列化

当用户在 Visual Studio 中保存特定于域的语言（DSL）的实例或*模型*时，将创建或更新 XML 文件。 可以重新加载该文件以在应用商店中重新创建该模型。

可以通过在 DSL 资源管理器中调整**Xml 序列化行为**下的设置，自定义序列化方案。 对于每个域类、属性和关系， **Xml 序列化行为**下有一个节点。 关系位于其源类下。 还有对应于形状、连接符和关系图类的节点。

你还可以编写程序代码以进行更高级的自定义。

> [!NOTE]
> 如果要以特定格式保存模型，但不需要从该窗体中重新加载它，请考虑使用文本模板从模型生成输出，而不是使用自定义序列化方案。 有关详细信息，请参阅[从域特定语言生成代码](../modeling/generating-code-from-a-domain-specific-language.md)。

## <a name="model-and-diagram-files"></a>模型和关系图文件

每个模型通常保存在两个文件中：

- 模型文件具有一个名称，例如**Model1. mydsl**。 它存储模型元素和关系及其属性。 文件扩展名（如**mydsl** ）由 DSL 定义中**编辑器**节点的**FileExtension**属性确定。

- 关系图文件具有一个名称，例如**Model1. mydsl**。 它存储形状、连接符及其位置、颜色、线条粗细和关系图外观的其他详细信息。 如果用户删除某个**关系图**文件，则模型中的基本信息不会丢失。 仅会丢失关系图的布局。 打开模型文件时，将创建一组默认的形状和连接线。

### <a name="to-change-the-file-extension-of-a-dsl"></a>更改 DSL 的文件扩展名

1. 打开 DSL 定义。 在 DSL 资源管理器中，单击 "编辑器" 节点。

2. 在属性窗口中，编辑**FileExtension**属性。 不要包含文件扩展名的初始 "."。

3. 在解决方案资源管理器中，更改**DslPackage\ProjectItemTemplates**中两个项模板文件的名称。 这些文件的名称遵循以下格式：

     `myDsl.diagram`

     `myDsl.myDsl`

## <a name="the-default-serialization-scheme"></a>默认序列化方案

若要创建本主题的示例，请使用以下 DSL 定义。

![DSL 定义关系&#45;图系列树模型](../modeling/media/familyt_person.png)

此 DSL 用于创建在屏幕上具有以下外观的模型。

![家谱关系图、工具箱和资源管理器](../modeling/media/familyt_instance.png)

已保存此模型，然后在 XML 文本编辑器中将其重新打开：

```xml
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

请注意有关序列化模型的以下几点：

- 每个 XML 节点都具有与域类名称相同的名称，只不过初始字母为小写。 例如，`familyTreeModel` 和 `person`。

- 诸如 Name 和 BirthYear 之类的域属性将作为 XML 节点中的属性进行序列化。 同样，将属性名称的初始字符转换为小写。

- 每个关系都序列化为嵌套在关系的源端内的 XML 节点。 该节点与源角色属性同名，但使用的是小写的初始字符。

     例如，在 DSL 定义中，名为 "**人员**" 的角色来源于**FamilyTree**类。  在 XML 中，这由嵌套在 `familyTreeModel` 节点内名为 `people` 的节点表示。

- 每个嵌入关系的目标端均序列化为在关系下嵌套的节点。 例如，"`people`" 节点包含多个 `person` 节点。

- 每个引用关系的目标端均序列化为*标记*，这将对目标元素的引用进行编码。

     例如，在 `person` 节点下，可以有 `children` 的关系。 此节点包含如下所示的名字对象：

    ```xml
    <personMoniker name="/f817b728-e920-458e-bb99-98edc469d78f/Elizabeth I" />
    ```

## <a name="understand-monikers"></a>了解名字对象

名字对象用于表示在模型和关系图文件的不同部分之间进行交叉引用。 它们还用于在 `.diagram` 文件中引用模型文件中的节点。 名字对象有两种形式：

- *Id 名字对象*引用目标元素的 GUID。 例如:

    ```xml
    <personShapeMoniker Id="f79734c0-3da1-4d72-9514-848fa9e75157" />
    ```

- *限定键名字对象*通过称为 "名字对象" 键的指定域属性的值识别目标元素。 目标元素的名字对象在嵌入关系树中以其父元素的名字对象为前缀。

     下面的示例来自一个 DSL，其中有一个名为 "唱片集" 的域类，它与名为 Song 的域类具有嵌入关系：

    ```xml
    <albumMoniker title="/My Favorites/Jazz after Teatime" />
    <songMoniker title="/My Favorites/Jazz after Teatime/Hot tea" />
    ```

     如果目标类的域属性的域属性的选项为 "**名字对象密钥**"，则将使用限定密钥名字对象，在**Xml 序列化行为**中将其设置为 `true`。 在此示例中，为域类 "唱片集" 和 "歌曲" 中名为 "Title" 的域属性设置了此选项。

限定密钥名字对象比 ID 名字对象更易于读取。 如果你想要将模型文件的 XML 作为人员读取，请考虑使用限定的密钥名字。 但是，用户可以将多个元素设置为具有相同的名字对象密钥。 重复键可能导致文件无法正确地重新加载。 因此，如果您定义使用限定密钥名字对象引用的域类，则应考虑阻止用户保存具有重复名字对象的文件的方法。

### <a name="to-set-a-domain-class-to-be-referenced-by-id-monikers"></a>设置由 ID 名字对象引用的域类

1. 请确保为类及其基类中的每个域属性都 `false`**为名字对象密钥**。

    1. 在 "DSL 资源管理器" 中，展开 " **Xml 序列化 Behavior\Class data \\ \<the 域类 > \Element 数据**"。

    2. 验证是否为每个域属性 `false` 为**名字对象密钥**。

    3. 如果域类有一个基类，请重复此类中的过程。

2. 设置域类的**序列化 Id**  =  `true`。

     此属性可在 " **Xml 序列化行为**" 下找到。

### <a name="to-set-a-domain-class-to-be-referenced-by-qualified-key-monikers"></a>设置由限定的键名字对象引用的域类

- Set 是现有域类的域属性的**名字对象密钥**。 属性的类型必须为 `string`。

    1. 在 "DSL 资源管理器" 中，展开 " **Xml 序列化 Behavior\Class data \\ \<the 域类 > \Element data**"，然后选择 "域" 属性。

    2. 在属性窗口中，set**是名字对象键**以 `true`。

- \- 或 -

     使用**命名域类**工具创建新的域类。

     此工具创建一个新类，该类具有名为 Name 的域属性。 **是元素名称**，并且是此域属性的**名字对象键**属性将初始化为 `true`。

- \- 或 -

     创建从域类到具有名字对象键属性的另一个类的继承关系。

### <a name="avoid-duplicate-monikers"></a>避免重复的名字对象

如果使用限定的键名字对象，则用户模型中的两个元素可能在键属性中具有相同的值。 例如，如果 DSL 具有具有属性名称的类人员，则用户可以将两个元素的名称设置为相同的名称。 虽然可以将模型保存到文件，但它不会正确地重新加载。

有多种方法可帮助避免这种情况：

- 对于键域属性，设置**为元素名称** =  `true`。 选择 DSL 定义关系图上的 "域" 属性，然后在 "属性窗口中设置值。

     当用户创建类的新实例时，此值将导致自动为域属性分配不同的值。 默认行为向类名的末尾添加一个数字。 这不会阻止用户将该名称更改为重复的名称，但在保存模型之前，用户不设置该值时，这会有所帮助。

- 启用 DSL 验证。 在 DSL 资源管理器中，选择 "编辑器 \ 验证"，并将 "**使用 ...** " 属性设置为 `true`。

     自动生成的验证方法会检查歧义。 方法位于 `Load` 验证类别中。 这可以确保用户将收到警告，指出可能无法重新打开文件。

     有关详细信息，请参阅[以域特定语言进行验证](../modeling/validation-in-a-domain-specific-language.md)。

### <a name="moniker-paths-and-qualifiers"></a>名字对象路径和限定符

限定的密钥名字对象以名字对象密钥结尾，并在嵌入树中以其父对象的名字对象为前缀。 例如，如果唱片集的名字对象为：

```xml
<albumMoniker title="/My Favorites/Jazz after Teatime" />
```

然后，该唱片集中的一首歌曲可能为：

```xml
<songMoniker title="/My Favorites/Jazz after Teatime/Hot tea" />
```

但是，如果按 ID 引用唱集，则名字对象将如下所示：

```xml
<albumMoniker Id="77472c3a-9bf9-4085-976a-d97a4745237c" />
<songMoniker title="/77472c3a-9bf9-4085-976a-d97a4745237c/Hot tea" />
```

请注意，由于 GUID 是唯一的，因此永远不会被其父级的名字对象作为前缀。

如果你知道某个特定域属性在模型中始终具有唯一值，则可以将该属性的**名字对象限定符**设置为 `true`。 这将导致它作为限定符使用，而无需使用父级的名字对象。 例如，如果您设置了两个都**是名字对象限定符**，并且是唱集类的 Title domain 属性的**名字对象键**，则不会在唱片集及其嵌入子级的名字对象中使用该模型的名称或标识符：

```xml
<albumMoniker name="Jazz after Teatime" />
<songMoniker title="/Jazz after Teatime/Hot tea" />
```

## <a name="customize-the-structure-of-the-xml"></a>自定义 XML 的结构

若要进行以下自定义，请在 DSL 资源管理器中展开 " **Xml 序列化行为**" 节点。 在域类下，展开元素数据节点以查看此类中的属性和关系的列表。 选择关系并调整其在属性窗口中的选项。

- 将**省略元素**设置为 true 可省略源角色节点，只留下目标元素的列表。 如果源类和目标类之间存在多个关系，则不应设置此选项。

    ```xml
    <familyTreeModel ...>
      <!-- The following node is omitted by using Omit Element: -->
      <!-- <people> -->
        <person name="Henry VIII" .../>
        <person name="Elizabeth I" .../>
      <!-- </people> -->
    </familyTreeModel>
    ```

- 设置 "**使用完整窗体**" 将目标节点嵌入表示关系实例的节点中。 将域属性添加到域关系时，将自动设置此选项。

    ```xml
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

- @No__t_1**元素**中设置**表示形式**，以将域属性另存为元素而不是属性值。

    ```xml
    <person name="Elizabeth I" birthYear="1533">
      <deathYear>1603</deathYear>
    </person>
    ```

- 若要更改属性和关系的序列化顺序，请右键单击 "元素数据" 下的某个项，然后使用 "**上移** **" 或 "下移"** 菜单命令。

## <a name="major-customization-using-program-code"></a>使用程序代码进行重大自定义

可以替换部分或全部序列化算法。

建议你在**Dsl\Generated Code\Serializer.cs**和**SerializationHelper.cs**中研究代码。

### <a name="to-customize-the-serialization-of-a-particular-class"></a>自定义特定类的序列化

1. 对于**Xml 序列化行为**，此类的节点中的 Set**是 Custom** 。

2. 转换所有模板，生成解决方案，并调查生成的编译错误。 每个错误附近的注释解释了必须提供的代码。

### <a name="to-provide-your-own-serialization-for-the-whole-model"></a>为整个模型提供自己的序列化

1. 重写 Dsl\GeneratedCode\SerializationHelper.cs 中的方法

## <a name="options-in-xml-serialization-behavior"></a>Xml 序列化行为中的选项

在 DSL 资源管理器中，Xml 序列化行为节点包含每个域类、关系、形状、连接符和关系图类的子节点。 在每个节点下，都列出了源自该元素的属性和关系。 关系在其自身的权限和源类下都表示。

下表汇总了可在 DSL 定义的此部分中设置的选项。 在每种情况下，在 DSL 资源管理器中选择一个元素，并设置属性窗口中的选项。

### <a name="xml-class-data"></a>Xml 类数据

这些元素可在 DSL 资源管理器中的 " **Xml 序列化 Behavior\Class 数据**" 下找到。

|||
|-|-|
|Property|描述|
|具有自定义元素架构|如果为 True，则指示域类具有自定义元素架构|
|为自定义|如果要为此域类编写自己的序列化和反序列化代码，请将此值设置为**True** 。<br /><br /> 构建解决方案并调查错误以发现详细说明。|
|域类|此类数据节点适用的域类。 只读。|
|元素名称|此类的元素的 Xml 节点名称。 默认值为域类名称的小写形式。|
|名字对象特性名称|用于包含引用的名字对象元素中的属性的名称。 如果为空，则使用键属性或 id 的名称。<br /><br /> 在此示例中，为 "name"： `<personMoniker name="/Mike Nash"/>`|
|名字对象元素名称|用于引用此类的元素的名字对象的 xml 元素的名称。<br /><br /> 默认值是类名以 "名字对象" 作为后缀的小写形式。 例如 `personMoniker`。|
|名字对象类型名称|为此类的元素的名字对象生成的 xsd 类型的名称。 XSD 位于 Dsl\Generated 的**代码 \\ \*Schema .xsd**|
|序列化 Id|如果为 True，则元素 GUID 包含在文件中。 如果没有标记**为名字对象键**的属性，并且 DSL 定义了此类的引用关系，则必须为 true。|
|类型名称|在指定域类的 xsd 中生成的 xml 类型的名称。|
|注意|与此元素关联的非正式说明|

### <a name="xml-property-data"></a>Xml 属性数据

Xml 属性节点位于类节点下。

|||
|-|-|
|Property|描述|
|域属性|Xml 序列化配置数据应用到的属性。 只读。|
|是名字对象键|如果为 True，则将属性用作创建引用此域类的实例的名字对象的键。|
|是名字对象限定符|如果为 True，则该属性用于在名字对象中创建限定符。 如果为 false，并且对于此域类，如果 SerializeId 不为 true，则名字对象由嵌入树中父元素的名字对象限定。|
|表达|如果特性，则将属性序列化为 xml 特性;如果为元素，则序列化为元素;如果为 Ignore，则不序列化。|
|Xml 名称|用于表示属性的 xml 特性或元素的名称。 默认情况下，这是域属性名称的小写形式。|
|注意|与此元素关联的非正式说明|

### <a name="xml-role-data"></a>Xml 角色数据

角色数据节点可在源类节点下找到。

|Property|描述|
|-|-|
|具有自定义名字对象|如果要提供自己的代码来生成和解析遍历此关系的名字对象，请将此值设置为 true。<br /><br /> 有关详细说明，请生成解决方案，然后双击错误消息。|
|域关系|指定应用这些选项的关系。 只读。|
|省略元素|如果为 true，则从架构中省略对应于源角色的 XML 节点。<br /><br /> 如果源类和目标类之间存在多个关系，此角色节点将区分属于这两个关系的链接。 因此，建议您不要在这种情况下设置此选项。|
|角色元素名称|指定从源角色派生的 XML 元素的名称。 默认值为角色属性名称。|
|使用完整形式|如果为 true，则每个目标元素或名字对象都包含在表示关系的 XML 节点中。 如果关系具有其自己的域属性，则应将其设置为 true。|

## <a name="see-also"></a>请参阅

- [在程序代码中导航和更新模型](../modeling/navigating-and-updating-a-model-in-program-code.md)
- [从域特定语言生成代码](../modeling/generating-code-from-a-domain-specific-language.md)