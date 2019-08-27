---
title: 定义用于扩展 UML 的配置文件 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- profiles, UML
- stereotypes, UML
- UML, profiles and stereotypes
- UML - extending, defining profiles
- UML, customizing
- UML, profiles
ms.assetid: 776589cb-f89d-48d5-aafa-04a4c074b0d6
caps.latest.revision: 44
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: b256971cd327098e22b243a1c171b0c9e82d32bc
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63433134"
---
# <a name="define-a-profile-to-extend-uml"></a>定义用于扩展 UML 的配置文件
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

您可以定义*UML 配置文件*以针对特定目的自定义标准模型元素。 配置文件定义一个或多个*UML 构造型*。 构造型可用于标记类型以表示一种特定对象。 构造型还可以扩展元素的属性列表。  
  
 多个配置文件与受支持版本的 Visual Studio 一起安装。 若要查看支持此功能的 Visual Studio 的版本，请参阅 [体系结构和建模工具的版本支持](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)。 有关这些配置文件以及如何应用构造型的详细信息，请参阅[自定义模型使用配置文件和构造型](../modeling/customize-your-model-with-profiles-and-stereotypes.md)。  
  
 你可以定义自己的配置文件，以采用 UML 并将其扩展到自己的业务范围或体系结构。 例如：  
  
- 如果需要经常定义网站，则可以定义自己的配置文件，其中提供可应用到类图中的类的 «网页» 构造型。 然后可以使用类图规划网站。 每个 «网页» 类都会具有页面内容、样式等的额外属性。  
  
- 如果需要开发银行软件，则可以定义一个提供 «帐户» 构造型的配置文件。 然后可以使用类图定义不同类型的帐户并显示这些帐户之间的关系。  
  
  你可以将自己的配置文件分发给你的团队。 每个团队成员都可以安装你的配置文件。 这样一来，团队成员便可以编辑和创建使用其构造型的模型。  
  
> [!NOTE]
> 如果你在自己所编辑的模型中应用某个配置文件的构造型，然后与他人共享该模型，则他们应在其自己的计算机上安装同一配置文件。 否则，他们将无法看到你使用的构造型。  
  
 一个配置文件通常是更大一部分[!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)]扩展。 例如，你可以定义用于将模型的某些部件转换为代码的命令。 你可以定义用户必须应用到他们想要转换的包的配置文件。 您将在单个 [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] 扩展中分发您的新命令和该配置文件。  
  
 你还可以定义配置文件的本地化变体。 加载你的扩展的用户可以看到适合他们自己的区域性的变体。  
  
## <a name="DefineProfile"></a> 如何定义配置文件  
  
#### <a name="to-define-a-uml-profile"></a>定义 UML 配置文件  
  
1. 创建具有文件扩展名 `.profile` 的新 XML 文件。  
  
2. 添加构造型定义中所述指南 》 中提及[配置文件的结构](#Schema)。  
  
3. 将配置文件添加到 Visual Studio 扩展中（`.vsix` 文件）。 你可以为配置文件创建新扩展，也可以将配置文件添加到现有扩展中。  
  
     请参阅下一部分中，[如何将一个配置文件添加到 Visual Studio 扩展](#AddProfile)。  
  
4. 在你的计算机上安装扩展。  
  
    1. 双击扩展文件，该文件的文件扩展名为 `.vsix`。  
  
    2. 重新启动 Visual Studio。  
  
5. 确认已安装配置文件。  
  
    1. 在 UML 资源管理器中选择模型。  
  
    2. 在属性窗口中，单击**配置文件**属性。 此时配置文件将在菜单中显示。 设置配置文件旁边的复选标记。  
  
    3. 选择一个你的配置文件为其定义构造型的元素。 在属性窗口中，单击**构造型**属性。 此时你的构造型将在列表中显示。 设置其中一个构造型的复选标记。  
  
    4. 如果你的配置文件为此构造型定义了附加属性，则可以展开构造型属性进行查看。  
  
6. 将扩展文件发送给 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 的其他用户，以将该文件安装到他们的计算机上。  
  
## <a name="AddProfile"></a> 如何将一个配置文件添加到 Visual Studio 扩展  
 要安装某个配置文件并允许你将其发送给其他用户，必须将该配置文件添加到 Visual Studio 扩展中。 有关详细信息，请参阅[部署 Visual Studio 扩展](http://go.microsoft.com/fwlink/?LinkId=160780)。  
  
#### <a name="to-define-a-profile-in-a-new-visual-studio-extension"></a>在新 Visual Studio 扩展中定义配置文件  
  
1. 创建 Visual Studio 扩展项目。  
  
   > [!NOTE]
   > 必须安装 [!INCLUDE[vsipsdk](../includes/vsipsdk-md.md)] 才能使用此过程。  
  
   1. 在 **“文件”** 菜单上，指向 **“新建”**，然后单击 **“项目”**。  
  
   2. 在中**新的项目**对话框中的**已安装的模板**，展开**Visual C#**，单击**扩展性**，然后单击**VSIX 项目**。 设置项目名称，然后单击**确定**。  
  
2. 将你的配置文件添加到项目中。  
  
   - 在解决方案资源管理器，右键单击项目，指向**外**，然后单击**现有项**。 在对话框中找到你的配置文件。  
  
3. 设置该配置文件**复制到输出**属性。  
  
   1. 在解决方案资源管理器，右键单击该配置文件，然后依次**属性**。  
  
   2. 在属性窗口中设置**复制到输出目录**属性设置为**始终复制**。  
  
4. 在解决方案资源管理器中，打开 `source.extension.vsixmanifest`。  
  
    文件将在扩展清单编辑器中打开。  
  
5. 上**资产**页上，添加一行来描述该配置文件：  
  
   - 单击“新建” 。 设置中的字段**添加新资产**，如下所示的对话框。  
  
   - 设置**类型**到 `Microsoft.VisualStudio.UmlProfile`  
  
        这不是一个下拉式选择。 使用键盘输入此名称。  
  
   - 单击**在文件系统上的文件**并选择你的配置文件的名称，例如 `MyProfile.profile`  
  
6. 生成项目。  
  
7. **若要调试配置文件**，按 F5。  
  
    这将打开一个 Visual Studio 实验实例。 在此实例中，打开建模项目。 在 UML 资源管理器中，选择模型的根元素，并在“属性”窗口中选择配置文件。 然后选择模型中的元素，并设置已为其定义的构造型。  
  
8. **若要提取部署的 VSIX**  
  
   1. 在 Windows 资源管理器中，打开文件夹 **.\bin\Debug**或 **.\bin\Release**若要查找 **.vsix**文件。 此文件是 [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] 扩展文件。 可以在你的计算机上安装该文件，也可将其发送给其他 Visual Studio 用户。  
  
   2. 安装扩展：  
  
       1. 双击 `.vsix` 文件。 Visual Studio 扩展安装程序将启动。  
  
       2. 重启任何正在运行的 Visual Studio 实例。  
  
   如果尚未安装 [!INCLUDE[vsipsdk](../includes/vsipsdk-md.md)]，则可以使用以下替代过程进行小型扩展。  
  
#### <a name="to-define-a-profile-extension-without-using-visual-studio-sdk"></a>定义配置文件扩展而不使用 Visual Studio SDK  
  
1. 创建包含下列三个文件的 Windows 目录：  
  
    - *YourProfile* `.profile`  
  
    - `extension.vsixmanifest`  
  
    - `[Content_Types].xml` － 按照如下所示键入此名称，并将名称括在方括号中  
  
2. 编辑 `[Content_Types].xml` 以包含下面的文本。 请注意，每个文件扩展名在该文件中都有对应项。  
  
    ```  
    <?xml version="1.0" encoding="utf-8"?>  
    <Types xmlns="http://schemas.openxmlformats.org/package/2006/content-types">  
      <Default Extension="profile" ContentType="application/octet-stream" />  
      <Default Extension="vsixmanifest" ContentType="text/xml" />  
    </Types>  
    ```  
  
3. 复制现有 `extension.vsixmanifest` 并使用 XML 编辑器进行编辑。 更改“ID”、“名称”和“内容”节点。  
  
    - 可以在以下目录中找到 `extension.vsixmanifest` 的示例：  
  
         *驱动器* **: \Program Files\Microsoft Visual Studio [version] \Common7\IDE\Extensions\Microsoft\Architecture Tools\UmlProfiles**  
  
    - “内容”节点应如下所示：  
  
        ```  
        <Content>  
          <CustomExtension Type="Microsoft.VisualStudio.UmlProfile"  
          >YourProfile.Profile</CustomExtension>  
        </Content>  
        ```  
  
4. 将这三个文件压缩到一个压缩文件中。  
  
     在 Windows 资源管理器中选择的三个文件，右键单击，指向**发送到**，然后单击**压缩 (zipped) 文件夹**。  
  
5. 重命名该压缩文件，并将其文件扩展名从 `.zip` 更改为 `.vsix`。  
  
6. 要在具有适当 Visual Studio 版本的任何计算机上安装该配置文件，请双击 `.vsix` 文件。  
  
#### <a name="to-install-a-uml-profile-from-a-visual-studio-extension"></a>从 Visual Studio 扩展安装 UML 配置文件  
  
1. 在 Windows 资源管理器中双击 `.vsix` 文件，或在 Visual Studio 中打开该文件。  
  
2. 单击**安装**中出现的对话框。  
  
3. 若要卸载或临时禁用该扩展，打开**扩展和更新**从**工具**菜单。  
  
## <a name="Localized"></a> 如何定义本地化的配置文件  
 你可以为不同的区域性或语言定义不同的配置文件，并将所有配置文件打包到同一扩展中。 当用户加载你的扩展时，他们将会看到你为其区域性定义的配置文件。  
  
 必须始终提供默认配置文件。 如果没有为用户的区域性定义配置文件，则他们将看到该默认配置文件。  
  
#### <a name="to-define-a-localized-profile"></a>定义本地化的配置文件  
  
1. 创建配置文件，如前面各节中所述[如何定义配置文件](#DefineProfile)并[如何将一个配置文件添加到 Visual Studio 扩展](#AddProfile)。 这是默认配置文件，将在你未提供本地化的配置文件的任何安装中用到该配置文件。  
  
2. 在默认配置文件所在目录中添加一个新目录。  
  
    > [!NOTE]
    > 如果要使用 Visual Studio 扩展项目生成扩展，请使用解决方案资源管理器向该项目添加一个新文件夹。  
  
3. 将新目录的名称更改为本地化区域性所对应的 ISO 短代码，例如保加利亚语对应 `bg`，法语对应 `fr`。 应使用非特定区域性代码（通常为两个字母），而不应使用特定区域性代码（例如 `fr-CA`）。 有关区域性代码的详细信息，请参阅[CultureInfo.GetCultures 方法](http://go.microsoft.com/fwlink/?LinkId=160782)，提供区域性代码的完整列表。  
  
4. 将默认配置文件的副本添加到新目录中。 请不要更改其文件名。  
  
     一个示例[!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)]扩展文件夹，然后生成或压缩到`.vsix`文件中，将包含以下文件夹和文件：  
  
     `extension.vsixmanifest`  
  
     `MyProfile.profile`  
  
     `fr\MyProfile.profile`  
  
     `de\MyProfile.profile`  
  
    > [!NOTE]
    > 不应在 `extension.vsixmanifest` 中插入对配置文件的本地化版本的引用。 复制的配置文件必须与父文件夹中的配置文件同名。  
  
5. 编辑配置文件的新副本，将用户可见的所有部分（例如 `displayName` 特性）转换为目标语言。  
  
6. 可以根据需要为多个区域性创建附加区域性文件夹和本地化的配置文件。  
  
7. 通过生成扩展项目或压缩所有文件生成 Visual Studio 扩展，如前面的章节中所述。  
  
## <a name="Schema"></a> 配置文件结构  
 UML 配置文件的 XSD 文件可在下面的示例：[设置构造型和配置文件 XSD](http://go.microsoft.com/fwlink/?LinkID=213811)。 为帮助编辑配置文件，请在以下位置安装 `.xsd` 文件：  
  
 **%ProgramFiles%\Microsoft Visual Studio [version]\Xml\Schemas**  
  
 本节使用 C# 配置文件作为示例。 完整的配置文件定义位于：  
  
 *驱动器* **: \Program Files\Microsoft Visual Studio [version] \Common7\IDE\Extensions\Microsoft\Architecture Tools\UmlProfiles\CSharp.profile**  
  
 此路径的开头部分在你的安装中可能有所不同。  
  
 有关.NET 配置文件的详细信息，请参阅[UML 模型的标准构造型](../modeling/standard-stereotypes-for-uml-models.md)。  
  
### <a name="main-sections-of-the-uml-profile-definition"></a>UML 配置文件定义的主要部分  
 每个配置文件都包含以下内容：  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<profile dslVersion="1.0.0.0"   
       name="CSharpProfile" displayName="C# Profile"   
       xmlns="http://schemas.microsoft.com/UML2.1.2/ProfileDefinition">  
  <stereotypes>...</stereotypes>  
  <metaclasses>...</metaclasses>  
  <propertyTypes>...</propertyTypes>  
</profile>  
```  
  
> [!NOTE]
> 称为 `name` 的特性不能包含空格或标点。 在用户界面中显示的特性 `displayName` 应为有效的 XML 字符串。  
  
 每个配置文件都包含三个主要部分。 按照相反顺序，这三个部分如下所示：  
  
- `<propertyTypes>` － 用于构造型部分中定义的属性的类型列表。  
  
- `<metaclasses>` － 此配置文件中的构造型应用到的模型元素类型列表，例如 IClass、IInterface、IOperation 和 IDependency。  
  
- `<stereotypes>` － 构造型定义。 每个定义都包括添加到目标模型元素中的属性的名称和类型。  
  
#### <a name="property-types"></a>属性类型  
 `<propertyTypes>`部分用于声明用于中的属性的类型的列表`<stereotypes>`部分。 属性类型有两种：外部和枚举。  
  
 外部类型声明标准 .NET 类型的完全限定名：  
  
```  
<externalType name="System.String" />  
```  
  
 枚举类型定义一组文本值：  
  
```  
<enumerationType name="PackageVisibility">  
  <enumerationLiterals>  
    <enumerationLiteral name="internal" displayName="internal"  />  
    <enumerationLiteral name="protectedinternal" displayName="protected internal" />  
  </enumerationLiterals>  
</enumerationType>  
```  
  
#### <a name="metaclasses"></a>元类  
 `<metaclasses>` 部分是此配置文件中的构造型可以定义为的模型元素类型的列表：  
  
```  
<metaclass   
      name="Microsoft.VisualStudio.Uml.Classes.IClass" />  
<metaclass  
      name="Microsoft.VisualStudio.Uml.Classes.IInterface" />  
<metaclass  
      name="Microsoft.VisualStudio.Uml.Components.IComponent" />  
```  
  
 有关可用作元类的模型元素和关系类型的完整列表，请参阅[模型元素类型](#Elements)。  
  
#### <a name="stereotype-definition"></a>构造型定义  
 `<stereotypes>` 部分包含一个或多个构造型定义：  
  
```  
<stereotype name="CSharpClass" displayName="C# Class"> ...  
```  
  
 每个构造型都列出了它可以应用到的一个或多个模型元素或关系类型。 你可以指定基类的名称，以包括其所有派生类型。 例如，如果指定 `Microsoft.VisualStudio.Uml.Classes.IType`，则构造型可以应用到元素的 `IClass`、`IInterface`、`IEnumeration` 以及多个其他类型。  
  
```  
<metaclasses>  
  <metaclassMoniker name=  
   "/CSharpProfile/Microsoft.VisualStudio.Uml.Classes.IClass" />  
</metaclasses>  
```  
  
 `name` 的 `metaclassMoniker` 特性是一个指向 `<metaClasses>` 部分中某个元素的链接。  
  
> [!NOTE]
> 名字对象的名称必须以 `/yourProfileName/` 开头，其中 `yourProfileName` 在配置文件（此示例中为“CSharpProfile”）的 `name` 特性中定义。 名字对象以元类部分中的某个项的名称结尾。  
  
 每个构造型都可以列出零个或多个属性，该构造型将这些属性添加到它所应用到的任何模型元素。 `<propertyType>`包含指向某个中定义的类型的`<propertyTypes>`部分。 该链接必须为用于引用 `<externalTypeMoniker>` 的 `<externalType>,`，或为用于引用 `<enumerationTypeMoniker>` 的 `<enumerationType>`。 再次强调，该链接以你的配置文件的名称开头。  
  
```  
  <properties>  
    <property name="IsStatic"   
            displayName="Is Static" defaultValue="false">  
      <propertyType>  
<externalTypeMoniker   
               name="/CSharpProfile/System.Boolean" />  
      </propertyType>  
    </property>  
    <property name="PackageVisibility"   
              displayName="Package Visibility"  
              defaultValue="internal">  
      <propertyType>  
        <enumerationTypeMoniker   
              name="/CSharpProfile/PackageVisibility"/>  
      </propertyType>  
    </property>  
  </properties>  
</stereotype>  
```  
  
## <a name="Elements"></a> 模型元素类型  
 中列出的类型可以为其定义构造型[UML 模型元素类型](../modeling/uml-model-element-types.md)。  
  
## <a name="troubleshooting"></a>疑难解答  
 我的构造型不显示我的 UML 模型。  
 必须在包或模型中选择配置文件。 然后，构造型将在包或模型内部的元素上显示。 有关详细信息，请参阅[添加构造型添加到 UML 模型元素](../modeling/add-stereotypes-to-uml-model-elements.md)。  
  
 当我打开 UML 模型时，将出现以下错误：**VS1707:无法加载以下配置文件，因为发生了序列化错误：MyProfile.profile**  
1. 验证 .profile 的基本 XML 语法是否正确。  
  
2. 确保每个名字对象名称的格式都为 /profileName/nodeName。 profileName 是根配置文件节点中的名称特性的值。 nodeName 是元类、externalType 或 enumerationType 的名称特性的值。  
  
3. 确保语法如下所述，和中所示_驱动器_**: \Program Files\Microsoft Visual Studio [version] \Common7\IDE\Extensions\Microsoft\Architecture Tools\UmlProfiles\\** .  
  
4. 卸载有错误的扩展。 在  “工具”菜单上，单击 “扩展和更新”。  
  
   - 如果未显示该扩展，请查看下一个项。  
  
5. 重新生成 VSIX 文件，然后在 Windows 资源管理器中打开该文件以将其重新安装。 重新启动 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]。  
  
   不显示该扩展在扩展管理器中，但当你尝试重新安装它，将显示以下消息：**该扩展已经安装到所有适用的产品。**  
   1. 一个子文件夹中删除扩展文件*LocalAppData*\Microsoft\VisualStudio\\[version] \Extensions\  
  
   - 若要查看*LocalAppData*，必须在 Windows 资源管理器文件夹选项视图选项卡中设置显示隐藏的文件和文件夹。  
  
   - *LocalAppData*通常位于 C:\Users\\*用户名*\AppData\Local\  
  
6. 重新启动 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]。  
  
## <a name="see-also"></a>请参阅  
 [向 UML 模型元素添加构造型](../modeling/add-stereotypes-to-uml-model-elements.md)   
 [自定义模型使用配置文件和构造型](../modeling/customize-your-model-with-profiles-and-stereotypes.md)   
 [UML 模型的标准构造型](../modeling/standard-stereotypes-for-uml-models.md)   
 [示例：根据构造型的颜色 UML 元素](http://go.microsoft.com/fwlink/?LinkID=213841)   
 [示例：设置构造型、 配置文件 XSD](http://go.microsoft.com/fwlink/?LinkID=213811)
