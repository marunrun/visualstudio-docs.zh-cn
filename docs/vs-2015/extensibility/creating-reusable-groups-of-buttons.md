---
title: 创建可重用的按钮的组 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- button groups, creating in VSPackages
- VSPackages, creating reusable button groups
- buttons, creating reusable groups
ms.assetid: 0c561617-fb86-476d-8bd1-c6e5e7464c65
caps.latest.revision: 45
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 6ac1fd0dc242ae8b8979a3f420f5e1c4d837f62b
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63405720"
---
# <a name="creating-reusable-groups-of-buttons"></a>创建可重复使用的按钮组
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

命令组是始终一起出现的菜单或工具栏的命令的集合。 可以将其分配给不同的父菜单 CommandPlacements 节的.vsct 文件重新使用任何命令组。  
  
 命令组通常包含按钮，但它们还可以包含其他菜单或组合框。  
  
### <a name="to-create-a-reusable-group-of-buttons"></a>若要创建可重用的一组按钮  
  
1. 创建一个名为的 VSIX 项目`ReusableButtons`。 有关详细信息，请参阅[使用菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)。  
  
2. 项目打开后，添加名为的自定义命令项模板**ReusableCommand**。 在中**解决方案资源管理器**，右键单击项目节点并选择**添加 / 新项**。 在中**添加新项**对话框中，转到**Visual C# / 可扩展性**，然后选择**自定义命令**。 在中**名称**在窗口底部字段中，将命令文件名称更改为**ReusableCommand.cs**。  
  
3. 在.vsct 文件中，转到符号部分，并找到包含组和项目的命令的 GuidSymbol 元素。 它应命名 guidReusableCommandPackageCmdSet。  
  
4. 添加将添加到组，如以下示例所示的每个按钮 IDSymbol。  
  
    ```xml  
    <GuidSymbol name="guidReusableCommandPackageCmdSet" value="{7f383b2a-c6b9-4c1d-b4b8-a26dc5b60ca1}">  
        <IDSymbol name="MyMenuGroup" value="0x1020" />  
        <IDSymbol name="ReusableCommandId" value="0x0100" />  
        <IDSymbol name="SecondReusableCommandId" value="0x0200" />  
    </GuidSymbol>  
    ```  
  
     默认情况下，该命令项模板将创建一个名为组**MyGroup**和一个按钮，已提供，以及每个 IDSymbol 条目的名称。  
  
5. 在组部分中，创建一个具有相同的 GUID 和 ID 属性与符号部分中提供的组元素。 您还可以使用现有的组，或使用提供的命令模板，如以下示例所示的条目。 此组显示在**工具**菜单  
  
    ```xml  
    <Groups>  
        <Group guid="guidReusableCommandPackageCmdSet" id="MyMenuGroup" priority="0x0600">  
              <Parent guid="guidSHLMainMenu" id="IDM_VS_MENU_TOOLS"/>  
        </Group>  
    </Groups>  
    ```  
  
### <a name="to-create-a-group-of-buttons-for-reuse"></a>若要创建一组以供重复使用的按钮  
  
1. 通过使用组作为父定义中的命令或菜单中，或通过将命令或菜单组中置于使用 CommandPlacements 部分，可在组中将命令或菜单。  
  
     按钮部分中定义一个按钮，将组作为其父级，或使用由包模板提供的按钮，如下面的示例中所示。  
  
    ```xml  
    <Button guid="guidReusableCommandPackageCmdSet" id="ReusableCommandId" priority="0x0100" type="Button">  
        <Parent guid="guidReusableCommandPackageCmdSet" id="MyMenuGroup" />  
        <Icon guid="guidImages" id="bmpPic1" />  
        <Strings>  
            <ButtonText>Invoke ReusableCommand</ButtonText>  
        </Strings>  
    </Button>  
    ```  
  
2. 如果一个按钮必须出现在多个组，一个条目为其创建后的命令部分必须放置在 CommandPlacements 部分中。 设置 CommandPlacement 元素以匹配你想要放置，该按钮的 GUID 和 ID 属性，然后设置的 GUID 和其父元素的 ID 与目标组中，如下面的示例中所示。  
  
    ```xml  
    <CommandPlacements>  
        <CommandPlacement guid="guidReusableCommandPackageCmdSet" id="SecondReusableCommandId" priority="0x105">  
          <Parent guid="guidReusableCommandPackageCmdSet" id="MyMenuGroup" />  
        </CommandPlacement>  
    </CommandPlacements>  
    ```  
  
    > [!NOTE]
    > 优先级字段的值确定该命令在新的命令组中的位置。 在元素中的项定义设置会覆盖的 CommandPlacement 中设置优先级。 在具有较高优先级值的命令之前将显示具有较低优先级值的命令。 允许使用重复的优先级值，但不能保证具有相同的优先级值的命令的相对位置，因为依据的顺序**devenv /setup**命令从注册表中创建的最后一个接口可能不一致。  
  
### <a name="to-put-a-reusable-group-of-buttons-on-a-menu"></a>将在菜单上的一组可重用按钮  
  
1. 创建中的条目`CommandPlacements`部分。 设置的 GUID 和 ID`CommandPlacement`元素与你的组，并将父 GUID 和 ID 为的目标位置。  
  
     CommandPlacements 部分应放置命令节的后面：  
  
    ```xml  
    <CommandTable>  
    ...  
      <Commands>... </Commands>  
      <CommandPlacements>... </CommandPlacements>  
    ...   
    </CommandTable>  
    ```  
  
     命令组可以包含多个菜单上。 父菜单可以是你创建一个由提供[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]（按中所述 ShellCmdDef.vsct 或 SharedCmdDef.vsct），或在另一个 VSPackage 中定义的其中一个。 子女教养层数不受限制，只要父菜单最终连接到[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]或向显示的 vspackage 的快捷菜单。  
  
     下面的示例将此组放**解决方案资源管理器**工具栏右侧的其他按钮。  
  
    ```xml  
    <CommandPlacements>  
        <CommandPlacement guid="guidReusableCommandPackageCmdSet" id="MyMenuGroup" priority="0xF00">  
          <Parent guid="guidSHLMainMenu" id="IDM_VS_TOOL_PROJWIN"/>  
        </CommandPlacement>  
    </CommandPlacements>  
    ```  
  
    ```xml  
    <CommandPlacements>  
      <CommandPlacement guid="guidButtonGroupCmdSet" id="MyMenuGroup"   
          priority="0x605">  
        <Parent guid="guidSHLMainMenu" id="IDM_VS_MENU_TOOLS" />  
      </CommandPlacement>  
    </CommandPlacements>  
  
    ```
