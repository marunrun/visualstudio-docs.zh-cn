---
title: 工具窗口中显示配置 |Microsoft Docs
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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68186398"
---
# <a name="tool-window-display-configuration"></a>工具窗口显示配置
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可选值中指定了当 VSPackage 注册为工具窗口中，默认位置、 大小、 停靠样式和其他可见性信息。 工具窗口注册的详细信息，请参阅[工具 Windows 注册表中](../extensibility/tool-windows-in-the-registry.md)  
  
## <a name="window-display-information"></a>窗口显示信息  
 工具窗口的基本显示配置存储在最多六个可选值：  
  
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
  
|名称|类型|数据|描述|  
|----------|----------|----------|-----------------|  
|名称|REG_SZ|"此处显示短名称"|描述的工具窗口的短名称。 仅用于在注册表中的引用。|  
|Float|REG_SZ|"X1，Y1，X2，Y2"|四个逗号分隔的值。 X1，Y1 是工具窗口的左上角的坐标。 X2，Y2 是右下角的坐标。 所有值都均以屏幕坐标。|  
|样式|REG_SZ|"MDI"<br /><br /> "浮动"<br /><br /> "链接"<br /><br /> "选项卡式"<br /><br /> "AlwaysFloat"|关键字指定初始显示工具窗口的状态。<br /><br /> "MDI"= 与 MDI 窗口停靠在一起。<br /><br /> "浮动"= 浮动。<br /><br /> "链接"= 与另一个窗口 （在窗口中的项中指定） 链接。<br /><br /> "选项卡式"= 与另一个工具窗口结合使用。<br /><br /> "AlwaysFloat"= 不固定。<br /><br /> 有关详细信息，请参阅下面的注释部分。|  
|窗口|REG_SZ|*\<GUID>*|到工具窗口可以链接或选项卡式窗口的 GUID。 GUID 可能属于一个你自己的 windows 或 windows 中的一个[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]IDE。|  
|方向|REG_SZ|"Left"<br /><br /> "右"<br /><br /> "Top"<br /><br /> "底部"|请参阅下面的注释部分。|  
|DontForceCreate|REG_DWORD|0 或 1|此条目存在后，其值不为零，窗口加载，但不是会立即显示。|  
  
### <a name="comments"></a>注释  
 方向项定义工具窗口将双击标题栏时停靠的位置。 位置是相对于窗口中的项中指定的窗口。 如果样式条目设置为"链接"，则方向项可以是"Left"、"Right"、"Top"或"底部"。 如果样式条目为"选项卡式"、 方向条目可以"保留"右"并指定选项卡添加的位置。 如果样式项是"浮动"，工具窗口浮动第一次。 双击标题栏时，方向和窗口项适用，并且窗口使用"选项卡式"样式。 如果"AlwaysFloat"样式项，则不能固定工具窗口。 如果"MDI"样式项，则工具窗口链接到 MDI 区域中，并忽略窗口中的项。  
  
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
 可选的可见性子项中的值确定工具窗口的可见性设置。 值的名称用于存储需要窗口的可见性的命令的 Guid。 如果执行该命令时，IDE 可保证工具窗口创建并使其可见。  
  
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
  
|name|类型|数据|描述|  
|----------|----------|----------|-----------------|  
|(默认)|REG_SZ|None|将保留为空。|  
|*\<GUID>*|REG_DWORD 或 REG_SZ|0 或描述性字符串。|可选。 项的名称必须是命令的需要可见性的 GUID。 值只保留一个信息性的字符串。 通常情况下，值是`reg_dword`设置为 0。|  
  
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
  
## <a name="see-also"></a>请参阅  
 [VSPackage 要点](../misc/vspackage-essentials.md)
