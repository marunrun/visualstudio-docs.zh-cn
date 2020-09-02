---
title: 工具窗口显示配置 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- tool windows, configuring
- tool windows, appearance
ms.assetid: 502a4926-bb83-473e-94e2-8e833c5f8b53
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 1af78bd58c42cf1312e36621011802e908c9e919
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68186398"
---
# <a name="tool-window-display-configuration"></a>工具窗口显示配置
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

当 VSPackage 注册工具窗口时，默认位置、大小、停靠样式和其他可见性信息将在可选值中指定。 有关工具窗口注册的详细信息，请参阅 [注册表中的工具窗口](../extensibility/tool-windows-in-the-registry.md)  
  
## <a name="window-display-information"></a>窗口显示信息  
 工具窗口的基本显示配置存储在多达六个可选值中：  
  
```  
HKEY_LOCAL_MACHINE\  
  Software\  
    Microsoft\  
      VisualStudio\  
        <Version>\  
          ToolWindows\  
            <Tool Window GUID>\  
              (Default)       = reg_sz: <Package GUID>Name            = reg_sz: <name of tool window>Float           = reg_sz: <position>Style           = reg_sz: <dock style>Window          = reg_sz: <window GUID>Orientation     = reg_sz: <orientation>DontForceCreate = reg_dword: 0x00000000  
```  
  
|名称|类型|数据|说明|  
|----------|----------|----------|-----------------|  
|名称|REG_SZ|"此处为短名称"|描述工具窗口的短名称。 仅用于注册表中的引用。|  
|Float|REG_SZ|"X1，Y1，X2，Y2"|四个逗号分隔值。 X1，Y1 是工具窗口左上角的坐标。 X2，Y2 是右下角的坐标。 所有值都以屏幕坐标表示。|  
|Style|REG_SZ|@<br /><br /> Float<br /><br /> 链表<br /><br /> 键<br /><br /> "AlwaysFloat"|一个关键字，指定工具窗口的初始显示状态。<br /><br /> "MDI" = 与 MDI 窗口停靠。<br /><br /> "Float" = 浮动。<br /><br /> "链接" = 与其他窗口链接 () 的窗口项中指定。<br /><br /> "选项卡" = 与其他工具窗口结合。<br /><br /> "AlwaysFloat" 不能停靠。<br /><br /> 有关详细信息，请参阅下面的 "注释" 部分。|  
|窗口|REG_SZ|*\<GUID>*|可以链接到工具窗口或选项卡式的窗口的 GUID。 GUID 可以属于您自己的一个窗口或 IDE 中的一个窗口 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 。|  
|方向|REG_SZ|左中<br /><br /> 然后<br /><br /> 热门<br /><br /> 最终|请参阅下面的 "备注" 部分。|  
|DontForceCreate|REG_DWORD|0 或 1|如果此项存在并且其值不为零，则会加载窗口，但不会立即显示。|  
  
### <a name="comments"></a>注释  
 方向项用于定义双击标题栏时工具窗口停靠的位置。 位置相对于在窗口项中指定的窗口。 如果样式项设置为 "链接"，则方向项可以是 "左"、"右"、"顶部" 或 "底部"。 如果样式项为 "选项卡式"，则方向项可以是 "左" 或 "右"，并指定添加选项卡的位置。 如果样式项为 "Float"，则工具窗口将首先浮动。 双击标题栏后，将应用方向和窗口项，并使用 "选项卡式" 样式。 如果样式条目为 "AlwaysFloat"，则无法停靠工具窗口。 如果样式项为 "MDI"，则工具窗口将链接到 MDI 区域，并且忽略窗口项。  
  
### <a name="example"></a>示例  
  
```  
HKEY_LOCAL_MACHINE\  
  Software\  
    Microsoft\  
      VisualStudio\  
        8.0Exp\  
          ToolWindows\  
            {A0C5197D-0AC7-4B63-97CD-8872A789D233}\  
              (Default)       = reg_sz: {DA9FB551-C724-11D0-AE1F-00A0C90FFFC3}  
              DontForceCreate = reg_dword: 0x00000000  
              Float           = reg_sz: 100,100,450,300  
              Name            = reg_sz: Bookmarks  
              Orientation     = reg_sz: Left  
              Style           = reg_sz: Tabbed  
              Window          = reg_sz: {34E76E81-EE4A-11D0-00A0C90FFFC3}  
```  
  
## <a name="tool-window-visibility"></a>工具窗口可见性  
 可选的可见性子项中的值确定工具窗口的可见性设置。 值的名称用于存储需要窗口可见性的命令的 Guid。 如果执行了命令，IDE 将保证创建工具窗口并使其可见。  
  
```  
HKEY_LOCAL_MACHINE\  
  Software\  
    Microsoft\  
      VisualStudio\  
        <Version>\  
          ToolWindows\  
            <Tool Window GUID>\  
              Visibility\  
                (Default) = reg_sz:  
                <GUID>    = reg_dword:  
                <GUID>    = reg_dword:  
                <GUID>    = reg_sz:  
```  
  
|名称|类型|数据|说明|  
|----------|----------|----------|-----------------|  
|（默认值）|REG_SZ|无|留空。|  
|*\<GUID>*|REG_DWORD 或 REG_SZ|0或描述性字符串。|可选。 条目的名称必须是需要可见性的命令的 GUID。 值仅保存信息性字符串。 通常情况下，该值 `reg_dword` 设置为0。|  
  
### <a name="example"></a>示例  
  
```  
HKEY_LOCAL_MACHINE\  
  Software\  
    Microsoft\  
      VisualStudio\  
        8.0Exp\  
          ToolWindows\  
            {EEFA5220-E298-11D0-8F78-00A0C9110057}\  
              Visibility\  
                (Default) = reg_sz:  
                {93694fa0-0397-11d1-9f4e-00a0c911004f} = reg_dword: 0x00000000  
                {9DA22B82-6211-11d2-9561-00600818403B} = reg_dword: 0x00000000  
                {adfc4e66-0397-11d1-9f4e-00a0c911004f} = reg_dword: 0x00000000  
```  
  
## <a name="see-also"></a>另请参阅  
 [VSPackage 要点](../misc/vspackage-essentials.md)
