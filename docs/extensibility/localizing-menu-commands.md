---
title: 本地化菜单命令 |微软文档
ms.date: 10/08/2019
ms.topic: conceptual
helpviewer_keywords:
- localize
- localization
- vsct
- menu commands
- localize visual studio
- localize vsct
ms.assetid: b04ee0f6-82ea-47e6-853a-72382267d6da
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d363b495eb84dc3bfeabd7bf7c5d05fabcbc4d36
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80702947"
---
# <a name="localize-menu-commands"></a>本地化菜单命令

您可以通过为 VSPackage 创建本地化*的 .vsct*文件和本地化的 *.resx*文件，然后更新项目文件以合并更改，为菜单和工具栏命令提供本地化文本。

有关如何本地化安装体验的信息，请参阅[本地化 VSIX 包](../extensibility/localizing-vsix-packages.md)。

## <a name="localize-command-names"></a>本地化命令名称

在 VSPackages 中，菜单命令和工具栏按钮在 *.vsct*文件中定义。

1. 在**解决方案资源管理器中**，将 *.vsct*文件的名称从*filename.vsct*更改为*filename.en-US.vsct*。

2. 为每个本地化语言创建*文件名.en-US.vsct*的副本。

    命名每个副本*文件名。区域设置\.vsct*，其中 *[区域设置]* 是特定的区域性名称。 有关区域性名称值的列表，请参阅[Microsoft 分配的区域设置。](/windows/uwp/publish/supported-languages)

    这些文件*名。区域设置.vsct*文件将包含包的本地化菜单文本。

3. 打开每个*文件名。区域设置.vsct*文件以本地化文本。

   1. 根据需要修改针对特定语言的[ButtonText](../extensibility/buttontext-element.md)元素值。

   2. 如果要提供本地化图标，请修改[Bitmap](../extensibility/bitmap-element.md)值以指向目标文件。

      下面的示例显示打开"家谱资源管理器"工具窗口的命令的英语和西班牙语按钮文本。

      [*家庭树.en-US.vsct*]

   ```xml
   <Button guid="guidLocalizedPackageCmdSet" id="cmdidFamilyTree" priority="0x0100" type="Button">
     <Parent guid="guidSHLMainMenu" id="IDG_VS_WNDO_OTRWNDWS1"/>
     <Icon guid="guidImages" id="bmpPic2" />
     <Strings>
       <CommandName>cmdidFamilyTree</CommandName>
       <ButtonText>Family Tree Explorer</ButtonText>
     </Strings>
   </Button>
   ```

    [*FamilyTree.es-ES.vsct*]

   ```xml
   <Button guid="guidLocalizedPackageCmdSet" id="cmdidFamilyTree" priority="0x0100" type="Button">
     <Parent guid="guidSHLMainMenu" id="IDG_VS_WNDO_OTRWNDWS1"/>
     <Icon guid="guidImages" id="bmpPic2" />
     <Strings>
       <CommandName>cmdidFamilyTree</CommandName>
       <ButtonText>Explorar el arbol genealogico</ButtonText>
     </Strings>
   </Button>
   ```

## <a name="localize-other-text-resources"></a>本地化其他文本资源

命令名称以外的文本资源在资源 （*.resx*） 文件中定义。

1. 重命名*VSPackage.resx*到*VSPackage.en-US.resx*。

2. 为每个本地化语言复制*VSPackage.en-US.resx*文件。

     命名每个副本*VSPackage。区域设置\.resx*，其中 *[区域设置]* 是特定的区域性名称。

3. 重命名*资源.resx*到*资源.en-US.resx*。

4. 为每个本地化语言复制*参考资料.en-US.resx*文件。

     命名每个副本*资源。区域设置\.resx*，其中 *[区域设置]* 是特定的区域性名称。

5. 打开每个 *.resx*文件以修改特定语言和区域性的字符串值。 下面的示例显示了工具窗口的标题栏的本地化资源定义。

     [*资源.en-US.resx*]

    ```xml
    <data name="ToolWindowTitle" xml:space="preserve">
      <value>Family Tree Explorer</value>
    </data>
    ```

     [*Resources.es-ES.resx*]

    ```xml
    <data name="ToolWindowTitle" xml:space="preserve">
      <value>Explorador del arbol genealogico</value>
    </data>
    ```

## <a name="incorporate-localized-resources-into-the-project"></a>将本地化资源合并到项目中

您必须修改*assemblyinfo.cs*文件和项目文件以合并本地化的资源。

1. 从**解决方案资源管理器**中的 **"属性"** 节点中，在编辑器中打开*assemblyinfo.cs*或*assemblyinfo.vb。*

2. 添加以下条目。

    ```csharp
    [assembly: NeutralResourcesLanguage("en-US", UltimateResourceFallbackLocation.Satellite)]
    ```

     这将美国英语设置为默认语言。

3. 卸载项目。

4. 在编辑器中打开项目文件。

5. 在根`Project`元素中`PropertyGroup`，添加具有与默认语言`UICulture`匹配的元素的元素。

    ```xml
    <PropertyGroup>
      <UICulture>en-US</UICulture>
    </PropertyGroup>
    ```

     这将美国英语集为 Windows 演示文稿基础 （WPF） 控件的默认 UI 区域性。

6. 找到包含`ItemGroup``EmbeddedResource`元素的元素。

7. 在`EmbeddedResource`调用*VSPackage.en-US.resx*的元素中，将`ManifestResourceName`元素替换为`LogicalName`设置为`VSPackage.en-US.Resources`的元素，如下所示：

    ```xml
    <EmbeddedResource Include="VSPackage.en-US.resx">
      <MergeWithCTO>true</MergeWithCTO>
      <LogicalName>VSPackage.en-US.Resources</LogicalName>
    </EmbeddedResource>
    ```

8. 对于每个本地化`EmbeddedResource`语言，复制 的元素`VsPackage.en-US`，并将副本的 **"包括"** 属性和**逻辑名称**元素设置为目标区域设置。

9. 到每个本地化`VSCTCompile`元素，添加指向`ResourceName``Menus.ctmenu`的元素，如以下示例所示：

    ```xml
    <ItemGroup>
      <VSCTCompile Include="LocalizedPackage.es-ES.vsct">
        <ResourceName>Menus.ctmenu</ResourceName>
      </VSCTCompile>
    </ItemGroup>
    ```

10. 保存项目文件并重新加载项目。

11. 生成项目。

     这将为每个语言创建主程序集和资源程序集。 有关本地化部署过程的信息，请参阅[本地化 VSIX 包](../extensibility/localizing-vsix-packages.md)

## <a name="see-also"></a>请参阅

- [扩展菜单和命令](../extensibility/extending-menus-and-commands.md)
- [全球化和本地化应用程序](../ide/globalizing-and-localizing-applications.md)
