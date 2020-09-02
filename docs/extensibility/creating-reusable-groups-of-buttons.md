---
title: 创建可重用的按钮组 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- button groups, creating in VSPackages
- VSPackages, creating reusable button groups
- buttons, creating reusable groups
ms.assetid: 0c561617-fb86-476d-8bd1-c6e5e7464c65
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 477014ed77b60821ad191ba6842999be6f528fee
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "85903649"
---
# <a name="create-reusable-groups-of-buttons"></a>创建可重用的按钮组
命令组是始终在菜单或工具栏上一起显示的命令的集合。 可以通过在 *.vsct* 文件的 CommandPlacements 节中将命令组分配给不同的父菜单来重新使用该命令组。

 命令组通常包含按钮，但也可以包含其他菜单或组合框。

## <a name="to-create-a-reusable-group-of-buttons"></a>创建可重用的按钮组

1. 创建一个名为的 VSIX 项目 `ReusableButtons` 。 有关详细信息，请参阅 [使用菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)。

2. 当项目打开时，添加一个名为 **ReusableCommand**的自定义命令项模板。 在**解决方案资源管理器**中，右键单击项目节点，然后选择 "**添加**  >  **新项**"。 在 "**添加新项**" 对话框中，选择 " **Visual c #**  >  **扩展性**" 并选择 "**自定义命令**"。 在窗口底部的 " **名称** " 字段中，将命令文件名更改为 *ReusableCommand.cs*。

3. 在 *.vsct* 文件中，请参阅符号部分，并查找包含项目的组和命令的 GuidSymbol 元素。 它应命名为 guidReusableCommandPackageCmdSet。

4. 为将添加到组中的每个按钮添加一个 IDSymbol，如以下示例中所示。

    ```xml
    <GuidSymbol name="guidReusableCommandPackageCmdSet" value="{7f383b2a-c6b9-4c1d-b4b8-a26dc5b60ca1}">
        <IDSymbol name="MyMenuGroup" value="0x1020" />
        <IDSymbol name="ReusableCommandId" value="0x0100" />
        <IDSymbol name="SecondReusableCommandId" value="0x0200" />
    </GuidSymbol>
    ```

     默认情况下，命令项模板会创建一个名为 **MyMenuGroup** 的组，以及一个具有你提供的名称的按钮，以及每个名称的 IDSymbol 项。

5. 在 "组" 部分中，创建一个组元素，该元素具有与 "符号" 部分中指定的 GUID 和 ID 属性相同的 GUID 和 ID 属性。 你还可以使用现有组，或使用命令模板提供的条目，如以下示例中所示。 此组显示在 " **工具** " 菜单上

    ```xml
    <Groups>
        <Group guid="guidReusableCommandPackageCmdSet" id="MyMenuGroup" priority="0x0600">
              <Parent guid="guidSHLMainMenu" id="IDM_VS_MENU_TOOLS"/>
        </Group>
    </Groups>
    ```

## <a name="to-create-a-group-of-buttons-for-reuse"></a>创建一组用于重用的按钮

1. 您可以通过在命令或菜单的定义中使用该组作为父项，或通过使用 CommandPlacements 部分将命令或菜单放入组，来将命令或菜单放入组。

     在 "按钮" 部分中，定义一个将组作为其父项的按钮，或使用由包模板提供的按钮，如以下示例中所示。

    ```xml
    <Button guid="guidReusableCommandPackageCmdSet" id="ReusableCommandId" priority="0x0100" type="Button">
        <Parent guid="guidReusableCommandPackageCmdSet" id="MyMenuGroup" />
        <Icon guid="guidImages" id="bmpPic1" />
        <Strings>
            <ButtonText>Invoke ReusableCommand</ButtonText>
        </Strings>
    </Button>
    ```

2. 如果按钮必须出现在多个组中，请在 "CommandPlacements" 部分为其创建一个条目，该部分必须位于命令部分之后。 设置 CommandPlacement 元素的 GUID 和 ID 属性，使其与要定位的按钮相匹配，然后将其父元素的 GUID 和 ID 设置为目标组中的元素，如下面的示例中所示。

    ```xml
    <CommandPlacements>
        <CommandPlacement guid="guidReusableCommandPackageCmdSet" id="SecondReusableCommandId" priority="0x105">
          <Parent guid="guidReusableCommandPackageCmdSet" id="MyMenuGroup" />
        </CommandPlacement>
    </CommandPlacements>
    ```

    > [!NOTE]
    > "优先级" 字段的值决定了命令在新命令组中的位置。 在 CommandPlacement 元素中设置的优先级将覆盖项定义中的这些设置。 具有较低优先级值的命令将显示在具有较高优先级值的命令之前。 允许使用重复的优先级值，但无法保证具有相同优先级值的命令的相对位置，因为 **devenv/setup** 命令从注册表创建最终接口的顺序可能不一致。

## <a name="to-put-a-reusable-group-of-buttons-on-a-menu"></a>在菜单上放置一组可重用的按钮

1. 在部分中创建一个条目 `CommandPlacements` 。 将元素的 GUID 和 ID 设置为组的 GUID 和 ID `CommandPlacement` ，并将父 GUID 和 id 设置为目标位置的 guid 和 id。

    应将 CommandPlacements 节放置在命令部分之后：

   ```xml
   <CommandTable>
   ...
     <Commands>... </Commands>
     <CommandPlacements>... </CommandPlacements>
   ...
   </CommandTable>
   ```

    命令组可以包含在多个菜单上。 父菜单可以是你创建的菜单， [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] (如 *.Vsct* 或 *SharedCmdDef*) 中所述，或在另一个 VSPackage 中定义的菜单。 只要父菜单最终连接到 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 或 VSPackage 显示的快捷菜单，则父层的数目不受限制。

    下面的示例将 **解决方案资源管理器** 工具栏上的组放在其他按钮的右侧。

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
