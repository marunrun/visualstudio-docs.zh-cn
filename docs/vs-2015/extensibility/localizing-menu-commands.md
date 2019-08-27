---
title: 本地化菜单命令 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- localize
- localization
- vsct
- menu commands
- localize visual studio
- localize vsct
ms.assetid: b04ee0f6-82ea-47e6-853a-72382267d6da
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: c879072b55729e249b1aecd665d6f470f4138a75
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65686126"
---
# <a name="localizing-menu-commands"></a>本地化菜单命令
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

您可以本地化的文本的菜单和工具栏命令通过创建本地化的.vsct 文件和你的 VSPackage，以及然后更新项目文件所做的更改将合并为本地化.resx 文件。  
  
 有关如何将本地化安装体验的信息，请参阅[本地化 VSIX 包](../extensibility/localizing-vsix-packages.md)。  
  
## <a name="localizing-command-names"></a>本地化的命令名称  
 在 Vspackage 中，菜单命令和工具栏按钮定义在.vsct 文件中。  
  
1. 在**解决方案资源管理器**，将从.vsct 文件的名称更改*filename*到.vsct*文件名*.en US.vsct。  
  
2. 制作一份*文件名*.en US.vsct 为每个本地化语言。  
  
    命名每个副本*文件名*。*区域设置*.vsct，其中*区域设置*是特定区域性名称。 有关区域性名称值的列表，请参阅[由 Microsoft 分配的区域设置 Id](https://msdn.microsoft.com/library/windows/apps/jj657969.aspx)。  
  
    这些*文件名*。*区域设置*.vsct 文件将包含包的本地化的菜单文本。  
  
3. 打开每个*文件名*。*区域设置*.vsct 文件将文本本地化。  
  
   1. 修改[ButtonText](../extensibility/buttontext-element.md)值以适合特定语言元素。  
  
   2. 如果将提供本地化的图标，修改[位图](../extensibility/bitmap-element.md)值以指向目标文件。  
  
      下面的示例显示了英语和西班牙语按钮文本命令，以打开家族树资源管理器工具窗口。  
  
      [FamilyTree.en-US.vsct]  
  
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
  
    [FamilyTree.es-ES.vsct]  
  
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
  
## <a name="localizing-other-text-resources"></a>本地化文本的其他资源  
 资源 (.resx) 文件中定义了文本资源而不是命令名称。  
  
1. 重命名 VSPackage.en US.resx VSPackage.resx。  
  
2. 请为每种本地化语言 VSPackage.en US.resx 文件的副本。  
  
     命名每个副本的 VSPackage。*区域设置*.resx，其中*区域设置*是特定区域性名称。  
  
3. 将 Resources.resx 重命名为 Resources.en-us.resx。  
  
4. 请为每种本地化语言 Resources.en-us.resx 文件的副本。  
  
     命名每个副本的资源。*区域设置*.resx，其中*区域设置*是特定区域性名称。  
  
5. 打开每个.resx 文件修改为适合于特定的语言和区域性的字符串值。 下面的示例显示了一个工具窗口的标题栏的已本地化的资源定义。  
  
     [Resources.en-US.resx]  
  
    ```xml  
    <data name="ToolWindowTitle" xml:space="preserve">  
      <value>Family Tree Explorer</value>  
    </data>  
    ```  
  
     [Resources.es-ES.resx]  
  
    ```xml  
    <data name="ToolWindowTitle" xml:space="preserve">  
      <value>Explorador del arbol genealogico</value>  
    </data>  
  
    ```  
  
## <a name="incorporating-localized-resources-into-the-project"></a>将本地化的资源合并到项目  
 必须修改 assemblyinfo.cs 文件和要合并的本地化的资源的项目文件。  
  
1. 从**属性**中的节点**解决方案资源管理器**，在编辑器中打开 assemblyinfo.cs 或 assemblyinfo.vb。  
  
2. 添加以下条目。  
  
    ```csharp  
    [assembly: NeutralResourcesLanguage("en-US", UltimateResourceFallbackLocation.Satellite)]  
    ```  
  
     这将为默认语言设置美国英语。  
  
3. 卸载项目。  
  
4. 在编辑器中打开项目文件。  
  
5. 找到`ItemGroup`元素，其中包含`EmbeddedResource`元素。  
  
6. 在`EmbeddedResource`调用 VSPackage.en-US.resx 的元素替换`ManifestResourceName`具有元素`LogicalName`元素中，将设置为`VSPackage.en-US.Resources`，按如下所示。  
  
    ```xml  
    <EmbeddedResource Include="VSPackage.en-US.resx">  
      <MergeWithCTO>true</MergeWithCTO>  
      <LogicalName>VSPackage.en-US.Resources</LogicalName>  
    </EmbeddedResource>  
    ```  
  
7. 对于每种本地化语言，复制`EmbeddedResource`VsPackage.en 美国，并将设置的元素**Include**属性和**LogicalName**元素复制到目标区域设置，如以下所示示例。  
  
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
 [扩展菜单和命令](../extensibility/extending-menus-and-commands.md)   
 [MenuCommands 与OleMenuCommands](../misc/menucommands-vs-olemenucommands.md)   
 [全球化和本地化](https://msdn.microsoft.com/library/9a59696b-d89b-45bd-946d-c75da4732d02)
