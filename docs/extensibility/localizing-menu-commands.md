---
title: 本地化菜单命令 |Microsoft Docs
ms.date: 11/04/2016
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
ms.openlocfilehash: 62c6011d1a04b60d1bd0cc538e9560d8977f9799
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66344675"
---
# <a name="localize-menu-commands"></a>本地化菜单命令
您可以通过创建本地化提供菜单和工具栏命令的本地化的文本 *.vsct*文件，并本地化 *.resx*为你的 VSPackage，以及然后更新项目文件将合并的文件更改。

 有关如何将本地化安装体验的信息，请参阅[本地化 VSIX 包](../extensibility/localizing-vsix-packages.md)。

## <a name="localize-command-names"></a>本地化的命令名称
 在 Vspackage 中，菜单命令和工具栏按钮中定义 *.vsct*文件。

1. 在中**解决方案资源管理器**，更改的名称 *.vsct*从文件*filename.vsct*到*filename.en US.vsct*。

2. 制作一份*filename.en US.vsct*为每个本地化语言。

    命名每个副本*文件名。 {区域设置}.vsct*，其中 *{区域}* 是特定区域性名称。 有关区域性名称值的列表，请参阅[Microsoft 分配的区域设置 Id](/windows/uwp/publish/supported-languages)。

    这些*文件名。Locale.vsct*文件将包含包的本地化的菜单文本。

3. 打开每个*文件名。Locale.vsct*文件将文本本地化。

   1. 修改[ButtonText](../extensibility/buttontext-element.md)值以适合特定语言元素。

   2. 如果将提供本地化的图标，修改[位图](../extensibility/bitmap-element.md)值以指向目标文件。

      下面的示例显示了英语和西班牙语按钮文本命令，以打开家族树资源管理器工具窗口。

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

## <a name="localize-other-text-resources"></a>将其他文本资源本地化
 在资源中定义文本资源而不是命令名称 ( *.resx*) 文件。

1. 重命名*VSPackage.resx*到*VSPackage.en US.resx*。

2. 制作一份*VSPackage.en US.resx*文件为每个本地化语言。

     命名每个副本*VSPackage。 {区域设置}.resx*，其中 *{区域}* 是特定区域性名称。

3. 重命名*Resources.resx*到*Resources.en-us.resx*。

4. 制作一份*Resources.en-us.resx*文件为每个本地化语言。

     命名每个副本*资源。 {区域设置}.resx*，其中 *{区域}* 是特定区域性名称。

5. 打开每个 *.resx*文件若要修改的字符串值以适合特定的语言和区域性。 下面的示例显示了一个工具窗口的标题栏的已本地化的资源定义。

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

## <a name="incorporate-localized-resources-into-the-project"></a>将本地化的资源合并到项目
 必须修改*assemblyinfo.cs*文件和要合并的本地化的资源的项目文件。

1. 从**属性**中的节点**解决方案资源管理器**，打开*assemblyinfo.cs*或者*assemblyinfo.vb*在编辑器中。

2. 添加以下条目。

    ```csharp
    [assembly: NeutralResourcesLanguage("en-US", UltimateResourceFallbackLocation.Satellite)]
    ```

     这将为默认语言设置美国英语。

3. 卸载项目。

4. 在编辑器中打开项目文件。

5. 找到`ItemGroup`元素，其中包含`EmbeddedResource`元素。

6. 中`EmbeddedResource`调用的元素*VSPackage.en US.resx*，将为`ManifestResourceName`具有元素`LogicalName`元素中，将设置为`VSPackage.en-US.Resources`，按如下所示。

    ```xml
    <EmbeddedResource Include="VSPackage.en-US.resx">
      <MergeWithCTO>true</MergeWithCTO>
      <LogicalName>VSPackage.en-US.Resources</LogicalName>
    </EmbeddedResource>
    ```

7. 对于每种本地化语言，复制`EmbeddedResource`的元素`VsPackage.en-US`，并设置**Include**属性和**LogicalName**元素复制到目标区域设置，如以下所示示例。

8. 向每个本地化`VSCTCompile`元素中，添加`ResourceName`指向的元素`Menus.ctmenu`，如以下示例所示。

    ```xml
    <ItemGroup>
      <VSCTCompile Include="LocalizedPackage.es-ES.vsct">
        <ResourceName>Menus.ctmenu</ResourceName>
      </VSCTCompile>
    </ItemGroup>
    ```

9. 保存项目文件并重新加载项目。

10. 生成项目。

     这将创建主程序集，并为每种语言的资源程序集。 本地化的部署过程的信息，请参阅[本地化 VSIX 包](../extensibility/localizing-vsix-packages.md)

## <a name="see-also"></a>请参阅
- [扩展菜单和命令](../extensibility/extending-menus-and-commands.md)
- [MenuCommands 与OleMenuCommands](../extensibility/menucommands-vs-olemenucommands.md)
- [全球化和本地化应用程序](../ide/globalizing-and-localizing-applications.md)