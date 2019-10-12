---
title: 本地化菜单命令 |Microsoft Docs
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
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b2b42143c2971bcbb172958b8da42a1e887e4699
ms.sourcegitcommit: 3e94d9fb6dc56fa8b23fbacd5d11cf8d6e7e18f1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/10/2019
ms.locfileid: "72252642"
---
# <a name="localize-menu-commands"></a>"本地化" 菜单命令

可以通过为 VSPackage 创建本地化的 *.vsct*文件和本地化的 *.resx*文件，然后更新项目文件以合并这些更改，为菜单和工具栏命令提供本地化的文本。

有关如何本地化安装体验的信息，请参阅[本地化 VSIX 包](../extensibility/localizing-vsix-packages.md)。

## <a name="localize-command-names"></a>本地化命令名称

在 Vspackage 中，将在 *.vsct*文件中定义菜单命令和工具栏按钮。

1. 在**解决方案资源管理器**中，将 *.vsct*文件的名称从 *.vsct*更改为 *.vsct*。

2. 为每种本地化语言的 *.vsct*副本。

    为每个副本命名*文件名 {Locale}. .vsct*，其中 *{Locale}* 是特定的区域性名称。 有关区域性名称值的列表，请参阅[Microsoft 分配的区域设置 id](/windows/uwp/publish/supported-languages)。

    这些*文件名.Vsct*文件将包含包的本地化菜单文本。

3. 打开每个*文件名。* 用于本地化文本的 .vsct 文件。

   1. 根据特定语言修改[ButtonText](../extensibility/buttontext-element.md)元素值。

   2. 如果你将提供本地化的图标，请修改[位图](../extensibility/bitmap-element.md)值以指向目标文件。

      下面的示例演示命令的英语和西班牙语按钮文本，用于打开系列树资源管理器工具窗口。

      [*FamilyTree.en-US.vsct*]

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

除命令名称外的文本资源在资源（ *.resx*）文件中定义。

1. 将*VSPackage*重命名为*VSPackage*。

2. 为每种本地化语言创建*VSPackage*文件的副本。

     为每个副本命名*VSPackage。 {Locale} .resx*，其中 *{Locale}* 是特定的区域性名称。

3. 将*资源 .resx*重命名为*资源. en-us*。

4. 为每种本地化语言的*en-us*文件创建一个副本。

     命名每个复制*资源。 {Locale} .resx*，其中 *{Locale}* 是特定的区域性名称。

5. 打开每个 *.resx*文件以根据特定语言和区域性修改字符串值。 下面的示例演示工具窗口标题栏的本地化资源定义。

     [*Resources.en-US.resx*]

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

必须修改*assemblyinfo.cs*文件和项目文件以合并已本地化的资源。

1. 在**解决方案资源管理器**的 "**属性**" 节点中，在编辑器中打开*assemblyinfo.cs*或*assemblyinfo* 。

2. 添加以下条目。

    ```csharp
    [assembly: NeutralResourcesLanguage("en-US", UltimateResourceFallbackLocation.Satellite)]
    ```

     这会将美国英语设置为默认语言。

3. 卸载项目。

4. 在编辑器中打开项目文件。

5. 在根 `Project` 元素中，添加一个具有与您的默认语言相匹配的 `UICulture` 元素的 @no__t 元素。

    ```xml
    <PropertyGroup>
      <UICulture>en-US</UICulture>
    </PropertyGroup>
    ```

     这会将美国英语设置为 Windows Presentation Foundation （WPF）控件的默认 UI 区域性。

6. 找到包含 @no__t 元素的 @no__t 0 元素。

7. 在调用*VSPackage*的 @no__t 0 元素中，将 `ManifestResourceName` 元素替换为设置为 `VSPackage.en-US.Resources` 的 @no__t 元素，如下所示：

    ```xml
    <EmbeddedResource Include="VSPackage.en-US.resx">
      <MergeWithCTO>true</MergeWithCTO>
      <LogicalName>VSPackage.en-US.Resources</LogicalName>
    </EmbeddedResource>
    ```

8. 对于每种本地化语言，请复制 @no__t 的 @no__t 0 元素，并将副本的**Include**属性和**LogicalName**元素设置为目标区域设置。

9. 对于每个本地化 @no__t 0 元素，添加一个指向 `Menus.ctmenu` 的 @no__t 元素，如下面的示例中所示：

    ```xml
    <ItemGroup>
      <VSCTCompile Include="LocalizedPackage.es-ES.vsct">
        <ResourceName>Menus.ctmenu</ResourceName>
      </VSCTCompile>
    </ItemGroup>
    ```

10. 保存项目文件，然后重新加载项目。

11. 生成项目。

     这会为每种语言创建主程序集和资源程序集。 有关本地化部署过程的信息，请参阅[本地化 VSIX 包](../extensibility/localizing-vsix-packages.md)

## <a name="see-also"></a>请参阅
- [扩展菜单和命令](../extensibility/extending-menus-and-commands.md)
- [MenuCommands 与OleMenuCommands](../extensibility/menucommands-vs-olemenucommands.md)
- [全球化和本地化应用程序](../ide/globalizing-and-localizing-applications.md)
