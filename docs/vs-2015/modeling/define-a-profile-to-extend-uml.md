---
title: Define a profile to extend UML | Microsoft Docs
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
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: bdb6620f8d73bf7fae7b7dbb1b92af38e71345b6
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74295677"
---
# <a name="define-a-profile-to-extend-uml"></a>定义用于扩展 UML 的配置文件
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

You can define a *UML profile* to customize the standard model elements for specific purposes. A profile defines one or more *UML stereotypes*. 构造型可用于标记类型以表示一种特定对象。 构造型还可以扩展元素的属性列表。

 多个配置文件与受支持版本的 Visual Studio 一起安装。 若要查看支持此功能的 Visual Studio 的版本，请参阅 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)。 For more information about those profiles and about how to apply stereotypes, see [Customize your model with profiles and stereotypes](../modeling/customize-your-model-with-profiles-and-stereotypes.md).

 你可以定义自己的配置文件，以采用 UML 并将其扩展到自己的业务范围或体系结构。 例如:

- 如果需要经常定义网站，则可以定义自己的配置文件，其中提供可应用到类图中的类的 «网页» 构造型。 然后可以使用类图规划网站。 每个 «网页» 类都会具有页面内容、样式等的额外属性。

- 如果需要开发银行软件，则可以定义一个提供 «帐户» 构造型的配置文件。 然后可以使用类图定义不同类型的帐户并显示这些帐户之间的关系。

  你可以将自己的配置文件分发给你的团队。 每个团队成员都可以安装你的配置文件。 这样一来，团队成员便可以编辑和创建使用其构造型的模型。

> [!NOTE]
> 如果你在自己所编辑的模型中应用某个配置文件的构造型，然后与他人共享该模型，则他们应在其自己的计算机上安装同一配置文件。 否则，他们将无法看到你使用的构造型。

 A profile is often part of a larger [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] extension. 例如，你可以定义用于将模型的某些部件转换为代码的命令。 你可以定义用户必须应用到他们想要转换的包的配置文件。 您将在单个 [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] 扩展中分发您的新命令和该配置文件。

 你还可以定义配置文件的本地化变体。 加载你的扩展的用户可以看到适合他们自己的区域性的变体。

## <a name="DefineProfile"></a> How to Define a Profile

#### <a name="to-define-a-uml-profile"></a>定义 UML 配置文件

1. 创建具有文件扩展名 `.profile` 的新 XML 文件。

2. Add stereotype definitions according to the guidelines described in [The Structure of a Profile](#Schema).

3. 将配置文件添加到 Visual Studio 扩展中（`.vsix` 文件）。 你可以为配置文件创建新扩展，也可以将配置文件添加到现有扩展中。

     See the next section, [How to Add a Profile to a Visual Studio Extension](#AddProfile).

4. 在你的计算机上安装扩展。

    1. 双击扩展文件，该文件的文件扩展名为 `.vsix`。

    2. 重新启动 Visual Studio。

5. 确认已安装配置文件。

    1. 在 UML 资源管理器中选择模型。

    2. In the Properties window, click the **Profiles** property. 此时配置文件将在菜单中显示。 设置配置文件旁边的复选标记。

    3. 选择一个你的配置文件为其定义构造型的元素。 In the Properties window, click the **Stereotypes** property. 此时你的构造型将在列表中显示。 设置其中一个构造型的复选标记。

    4. 如果你的配置文件为此构造型定义了附加属性，则可以展开构造型属性进行查看。

6. 将扩展文件发送给 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 的其他用户，以将该文件安装到他们的计算机上。

## <a name="AddProfile"></a> How to Add a Profile to a Visual Studio Extension
 要安装某个配置文件并允许你将其发送给其他用户，必须将该配置文件添加到 Visual Studio 扩展中。 For more information, see [Deploying Visual Studio Extensions](https://go.microsoft.com/fwlink/?LinkId=160780).

#### <a name="to-define-a-profile-in-a-new-visual-studio-extension"></a>在新 Visual Studio 扩展中定义配置文件

1. 创建 Visual Studio 扩展项目。

   > [!NOTE]
   > 必须安装 [!INCLUDE[vsipsdk](../includes/vsipsdk-md.md)] 才能使用此过程。

   1. 在 **“文件”** 菜单上，指向 **“新建”** ，然后单击 **“项目”** 。

   2. In the **New Project** dialog box, under **Installed Templates**, expand **Visual C#** , click **Extensibility**, and then click **VSIX project**. Set the project name and click **OK**.

2. 将你的配置文件添加到项目中。

   - In Solution Explorer, right-click the project, point to **Add**, and then click **Existing Item**. 在对话框中找到你的配置文件。

3. Set the profile file's **Copy to Output** property.

   1. In Solution Explorer, right-click the profile file, and then click **Properties**.

   2. In the Properties window, set the **Copy to Output Directory** property to **Copy Always**.

4. 在解决方案资源管理器中，打开 `source.extension.vsixmanifest`。

    文件将在扩展清单编辑器中打开。

5. On the **Assets** page, add a row describing the profile:

   - 单击“新建”。 Set the fields in the **Add New Asset** dialog as follows.

   - Set **Type** to `Microsoft.VisualStudio.UmlProfile`

        这不是一个下拉式选择。 使用键盘输入此名称。

   - Click **File on filesystem** and select the name of your profile file, for example `MyProfile.profile`

6. 生成项目。

7. **To debug the profile**, press F5.

    这将打开一个 Visual Studio 实验实例。 在此实例中，打开建模项目。 在 UML 资源管理器中，选择模型的根元素，并在“属性”窗口中选择配置文件。 然后选择模型中的元素，并设置已为其定义的构造型。

8. **To extract the VSIX for deployment**

   1. In Windows Explorer, open the folder **.\bin\Debug** or **.\bin\Release** to find the **.vsix** file. 此文件是 [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] 扩展文件。 可以在你的计算机上安装该文件，也可将其发送给其他 Visual Studio 用户。

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

         *drive* **:\Program Files\Microsoft Visual Studio [version]\Common7\IDE\Extensions\Microsoft\Architecture Tools\UmlProfiles**

    - “内容”节点应如下所示：

        ```
        <Content>
          <CustomExtension Type="Microsoft.VisualStudio.UmlProfile"
          >YourProfile.Profile</CustomExtension>
        </Content>
        ```

4. 将这三个文件压缩到一个压缩文件中。

     In Windows Explorer, select the three files, right-click, point to **Send To**, and then click **Compressed (zipped) folder**.

5. 重命名该压缩文件，并将其文件扩展名从 `.zip` 更改为 `.vsix`。

6. 要在具有适当 Visual Studio 版本的任何计算机上安装该配置文件，请双击 `.vsix` 文件。

#### <a name="to-install-a-uml-profile-from-a-visual-studio-extension"></a>从 Visual Studio 扩展安装 UML 配置文件

1. 在 Windows 资源管理器中双击 `.vsix` 文件，或在 Visual Studio 中打开该文件。

2. Click **Install** in the dialog box that appears.

3. To uninstall or temporarily disable the extension, open **Extensions and Updates** from the **Tools** menu.

## <a name="Localized"></a> How to Define Localized Profiles
 你可以为不同的区域性或语言定义不同的配置文件，并将所有配置文件打包到同一扩展中。 当用户加载你的扩展时，他们将会看到你为其区域性定义的配置文件。

 必须始终提供默认配置文件。 如果没有为用户的区域性定义配置文件，则他们将看到该默认配置文件。

#### <a name="to-define-a-localized-profile"></a>定义本地化的配置文件

1. Create a profile as described in the previous sections[How to Define a Profile](#DefineProfile) and [How to Add a Profile to a Visual Studio Extension](#AddProfile). 这是默认配置文件，将在你未提供本地化的配置文件的任何安装中用到该配置文件。

2. 在默认配置文件所在目录中添加一个新目录。

    > [!NOTE]
    > 如果要使用 Visual Studio 扩展项目生成扩展，请使用解决方案资源管理器向该项目添加一个新文件夹。

3. 将新目录的名称更改为本地化区域性所对应的 ISO 短代码，例如保加利亚语对应 `bg`，法语对应 `fr`。 应使用非特定区域性代码（通常为两个字母），而不应使用特定区域性代码（例如 `fr-CA`）。 For more information about culture codes, see [CultureInfo.GetCultures method](https://go.microsoft.com/fwlink/?LinkId=160782), which provides a complete list of culture codes.

4. 将默认配置文件的副本添加到新目录中。 请不要更改其文件名。

     A sample [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] Extension folder, before it is built or compressed into a `.vsix` file, would contain the following folders and files:

     `extension.vsixmanifest`

     `MyProfile.profile`

     `fr\MyProfile.profile`

     `de\MyProfile.profile`

    > [!NOTE]
    > 不应在 `extension.vsixmanifest` 中插入对配置文件的本地化版本的引用。 复制的配置文件必须与父文件夹中的配置文件同名。

5. 编辑配置文件的新副本，将用户可见的所有部分（例如 `displayName` 特性）转换为目标语言。

6. 可以根据需要为多个区域性创建附加区域性文件夹和本地化的配置文件。

7. 通过生成扩展项目或压缩所有文件生成 Visual Studio 扩展，如前面的章节中所述。

## <a name="Schema"></a> The Structure of a Profile
 The XSD file for UML profiles can be found in the following sample: [Setting Stereotypes and Profiles XSD](https://go.microsoft.com/fwlink/?LinkID=213811). 为帮助编辑配置文件，请在以下位置安装 `.xsd` 文件：

 **%ProgramFiles%\Microsoft Visual Studio [version]\Xml\Schemas**

 本节使用 C# 配置文件作为示例。 完整的配置文件定义位于：

 *drive* **:\Program Files\Microsoft Visual Studio [version]\Common7\IDE\Extensions\Microsoft\Architecture Tools\UmlProfiles\CSharp.profile**

 此路径的开头部分在你的安装中可能有所不同。

 For more information about the .NET profile, see [Standard stereotypes for UML models](../modeling/standard-stereotypes-for-uml-models.md).

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
 The `<propertyTypes>` section declares a list of types that are used for properties in the `<stereotypes>` section. 属性类型有两种：外部和枚举。

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

 For the full list of model element and relationship types that you can use as metaclasses, see [Model Element Types](#Elements).

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

 每个构造型都可以列出零个或多个属性，该构造型将这些属性添加到它所应用到的任何模型元素。 The `<propertyType>` contains a link to one of the types that are defined in the `<propertyTypes>` section. 该链接必须为用于引用 `<externalTypeMoniker>` 的 `<externalType>,`，或为用于引用 `<enumerationTypeMoniker>` 的 `<enumerationType>`。 再次强调，该链接以你的配置文件的名称开头。

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

## <a name="Elements"></a> Model Element Types
 The set of types for which you can define stereotypes is listed in [UML model element types](../modeling/uml-model-element-types.md).

## <a name="troubleshooting"></a>疑难解答
 我的构造型不显示我的 UML 模型。
必须在包或模型中选择配置文件。 然后，构造型将在包或模型内部的元素上显示。 For more information, see [Add stereotypes to UML model elements](../modeling/add-stereotypes-to-uml-model-elements.md).

 The following error appears when I open a UML model: **VS1707: The following profiles cannot be loaded because a serialization error occurred: MyProfile.profile**
1. 验证 .profile 的基本 XML 语法是否正确。

2. 确保每个名字对象名称的格式都为 /profileName/nodeName。 profileName 是根配置文件节点中的名称特性的值。 nodeName 是元类、externalType 或 enumerationType 的名称特性的值。

3. Ensure the syntax is as described here, and as demonstrated in _drive_ **:\Program Files\Microsoft Visual Studio [version]\Common7\IDE\Extensions\Microsoft\Architecture Tools\UmlProfiles\\** .

4. 卸载有错误的扩展。 在 “工具”菜单上，单击“扩展和更新”。

   - 如果未显示该扩展，请查看下一个项。

5. 重新生成 VSIX 文件，然后在 Windows 资源管理器中打开该文件以将其重新安装。 重新启动 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]。

   The extension does not appear in Extension Manager, but when you try to re-install it, the following message appears: **The extension is already installed to all applicable products.**
   1. Remove the extension file from a subfolder of *LocalAppData*\Microsoft\VisualStudio\\[version]\Extensions\

   - To see *LocalAppData*, you must set Show Hidden Files and Folders in the View tab of the Windows Explorer Folder Options.

   - *LocalAppData* is typically in C:\Users\\*userName*\AppData\Local\

6. 重新启动 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]。

## <a name="see-also"></a>请参阅
 [Add stereotypes to UML model elements](../modeling/add-stereotypes-to-uml-model-elements.md) [Customize your model with profiles and stereotypes](../modeling/customize-your-model-with-profiles-and-stereotypes.md) [Standard stereotypes for UML models](../modeling/standard-stereotypes-for-uml-models.md) [Sample: Color UML Elements by Stereotype](https://go.microsoft.com/fwlink/?LinkID=213841) [Sample: Setting Stereotypes, Profiles XSD](https://go.microsoft.com/fwlink/?LinkID=213811)
