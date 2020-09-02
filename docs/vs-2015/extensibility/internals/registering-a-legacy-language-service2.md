---
title: 注册旧版语言 Service2 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- registration, language services
- language services, registry information
- registry, language services
ms.assetid: ca312aa3-f9f1-4572-8553-89bf3a724deb
caps.latest.revision: 25
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 07d70bb1d77dc3022b06c4036317e31692307f98
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68188839"
---
# <a name="registering-a-legacy-language-service"></a>注册旧版语言服务
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

以下部分提供中提供的各种语言服务选项的注册表项列表 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 。  
  
 在以下注册表项列表中， *VS Reg Root*等于 HKEY_LOCAL_MACHINE \software\microsoft\visualstudio \\ *X. y*，其中， *x*是 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 版本号。  
  
## <a name="registry-entries-for-language-service-options"></a>语言服务选项的注册表项  
 *VS Reg Root*\Languages\Language Services \\ *Language Name* key 可以包含以下值。  
  
|名称|类型|范围|说明|  
|----------|----------|-----------|-----------------|  
|（默认值）|REG_SZ|*\<GUID>*|语言服务的 GUID。|  
|LangResID|REG_DWORD|0x0-0xffff|字符串资源标识符 (语言的本地化文本名称的 Resid 标识) 。|  
|包|REG_SZ|*\<GUID>*|VSPackage 的 GUID。|  
|ShowCompletion|REG_DWORD|0-1|指定是否在 "**选项**" 对话框中启用**语句完成**选项。|  
|ShowSmartIndent|REG_DWORD|0-1|指定是否在 "**选项**" 对话框中启用选择**智能**缩进的选项。|  
|RequestStockColors|REG_DWORD|0-1|指定是否使用自定义或默认颜色来为关键字着色。|  
|ShowHotURLs|REG_DWORD|0-1|指定用户是否可以单击 "Url"。|  
|默认为非热 Url|REG_DWORD|0-1|指定 "**选项**" 对话框中的 "**启用一键式 URL" 导航**选项的初始设置。|  
|DefaultToInsertSpaces|REG_DWORD|0-1|指定语言服务是否将 "插入空格" 作为其默认选项卡选项。|  
|ShowDropdownBarOption|REG_DWORD|0-1|启用或禁用显示或隐藏**导航栏**的 "**选项**" 对话框中的 "**导航栏**" 选项。|  
|仅限单一代码窗口|REG_DWORD|0-1|在语言服务的 "**窗口**" 菜单中启用或禁用**新窗口**选项。|  
|EnableAdvancedMembersOption|REG_DWORD|0-1|启用或禁用用于**隐藏高级成员**的 "**选项**" 对话框设置。|  
|支持 CF_HTML|REG_DWORD|0-1|指定编辑器是否启用 HTML 数据的复制和粘贴。|  
|EnableLineNumbersOption|REG_DWORD|0-1|指定是否为语言服务启用了 "**选项**" 对话框中的 "**行号**" 选项。|  
|HideAdvancedMembersByDefault|REG_DWORD|0-1|指定是否在完成列表中隐藏高级成员，如私有字段。|  
|ShowBraceCompletion|REG_DWORD|0-1|指定是否启用了 "**选项**" 对话框中的**大括号完成**选项。|  
  
### <a name="example"></a>示例  
  
```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp\  
  Languages\  
    Language Services\  
      C/C++\  
        (Default)             = reg_sz:{B2F072B0-ABC1-11D0-9D62-00C04FD9DFD9}  
        LangResID             = reg_dword:0x00000000  
        Package               = reg_sz:{8C2EA640-ABC1-11D0-9D62-00C04FD9DFD9}  
        ShowCompletion        = reg_dword:0x00000001  
        ShowSmartIndent       = reg_dword:0x00000001  
        ShowDropdownBarOption = reg_dword:0x00000001  
```  
  
## <a name="registry-entries-for-debugger-languages-options"></a>调试器语言选项的注册表项  
 *VS Reg Root*\Languages\Language Services \\ *Language Name \Debugger Language* \\ *GUID*key 可以包含以下值。  
  
|名称|类型|范围|说明|  
|----------|----------|-----------|-----------------|  
|（默认值）|REG_SZ|文本|默认值可用于记录语言的名称。 此密钥的名称是在 \AD7Metrics\Expression 计算器中具有相应条目的表达式计算器的 GUID *\<VS Reg Root>* 。|  
  
### <a name="example"></a>示例  
  
```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp\  
  Languages\  
    Language Services\  
      C/C++\  
        Debugger Languages\  
          {3A12D0B7-C26C-11D0-B442-00A0244A1DD2}\  
            (Default) = reg_sz:C++  
```  
  
## <a name="registry-entries-for-editor-tools-options"></a>编辑器工具选项的注册表项  
 可以在属性页和属性节点的 EditorToolsOptions 项下添加注册表项。 这些键及其值在 "选项" 对话框中 ("**工具**" 菜单上的 "**选项**" 对话框中，) 用于配置语言服务。 在下面的示例中， *Page name* 是属性页的名称， *节点名称* 是 " **选项** " 对话框中的树中的节点名称。 页面输入和节点条目必须单独指定。  
  
|名称|类型|范围|说明|  
|----------|----------|-----------|-----------------|  
|（默认值）|REG_SZ|Resid 标识|此选项页的本地化显示名称。 名称可以是文本文本或 # `nnn` ，其中 `nnn` 是指定 VSPackage 的附属 DLL 中的字符串资源 ID。|  
|包|REG_SZ|*GUID*|实现此选项页的 VSPackage 的 GUID。|  
|页面|REG_SZ|*GUID*|要通过调用方法从 VSPackage 请求的属性页的 GUID <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetPropertyPage%2A> 。 如果此注册表项不存在，则注册表项将描述一个节点，而不是页。|  
  
### <a name="example"></a>示例  
  
```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp\  
  Languages\  
    Language Services\  
      CSharp\  
        EditorToolsOptions\  
          Formatting\  
            (Default) = reg_sz:#242  
            Package   = reg_sz:{A066E284-DCAB-11D2-B551-00C04F68D4DB}  
            General\  
              (Default) = reg_sz:#255  
              Package   = reg_sz:{A066E284-DCAB-11D2-B551-00C04F68D4DB}  
              Page      = reg_sz:{3EB2CC0B-033E-4D75-B26A-B2362C25227E}  
            Indentation\  
              (Default) = reg_sz:#250  
              Package   = reg_sz:{A066E284-DCAB-11D2-B551-00C04F68D4DB}  
              Page      = reg_sz:{5E21D017-6D2A-4114-A1F1-C923F001CBBB}  
            Newlines\  
              (Default) = reg_sz:#253  
              Package   = reg_sz:{A066E284-DCAB-11D2-B551-00C04F68D4DB}  
              Page      = reg_sz:{607D8062-68D1-41E4-9A35-B5E7F14D0481}  
```  
  
## <a name="registry-entries-for-file-name-extension-options"></a>文件扩展名选项的注册表项  
 文件扩展名的条目应包含前导句点，例如 "myext"。  
  
|名称|类型|范围|说明|  
|----------|----------|-----------|-----------------|  
|（默认值）|REG_SZ|*GUID*|此文件扩展名类型的默认语言服务的服务 GUID。|  
  
### <a name="example"></a>示例  
  
```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp\  
  Languages\  
    File Extensions\  
      .cpp\  
        (Default) = {B2F072B0-ABC1-11D0-9D62-00C04FD9DFD9}  
```  
  
## <a name="registry-entries-for-editor-options"></a>编辑器选项的注册表项  
 *VS Reg Root*\Editors 键可以包含以下值：  
  
|名称|类型|范围|说明|  
|----------|----------|-----------|-----------------|  
|（默认值）|REG_SZ|""|用你可以在此处为文档输入名称。|  
|DefaultToolboxTab|REG_SZ|""|编辑器处于活动状态时的 "工具箱" 选项卡的名称。|  
|DisplayName|REG_SZ|Resid 标识|要在 " **打开方式** " 对话框中显示的名称。 名称是字符串资源 ID 或标准格式的名称。|  
|ExcludeDefTextEditor|REG_DWORD|0-1|用于 " **打开方式** " 菜单命令。 如果你不希望在特定文件类型的可用编辑器列表中列出默认文本编辑器，请将此值设置为1。|  
|LinkedEditorGUID|REG_SZ|*\<GUID>*|用于任何可以打开包含代码页支持的文件的语言服务。 例如，当你使用 " **打开方式** " 命令打开 .txt 文件时，提供的选项可用于在不使用编码的情况下使用源代码编辑器。<br /><br /> 子项名称中指定的 GUID 适用于代码页编辑器工厂;此特定注册表项中指定的链接 GUID 用于常规编辑器工厂。 此项的目的是，如果 IDE 不使用默认编辑器打开文件，IDE 将尝试使用列表中的下一个编辑器。 由于此编辑器工厂基本上与失败的编辑器工厂相同，因此下一个编辑器不应为代码页编辑器工厂。|  
|包|REG_SZ|*\<GUID>*|显示名称的 Resid 标识的 VSPackage GUID。|  
  
### <a name="example"></a>示例  
  
```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp\  
  \Editors\  
    {8281C572-2171-45AA-A642-7D8BC1662F1C}\  
      (Default)            = reg_sz:Html Editor with Encoding  
      DefaultToolboxTab    = reg_sz:HTML  
      DisplayName          = reg_sz:#20101  
      LinkedEditorGUID     = reg_sz:{C76D83F8-A489-11D0-8195-00A0C91BBEE3}  
      Package              = reg_sz:{1B437D20-F8FE-11D2-A6AE-00104BCC7269}  
```  
  
## <a name="registry-entries-for-logical-view-options"></a>逻辑视图选项的注册表项  
 *VS Reg Root*\EDITORS \\ *Editor GUI>* \LogicalViews 键可以包含以下值。  
  
|名称|类型|范围|说明|  
|----------|----------|-----------|-----------------|  
|（默认值）|REG_SZ||未使用。|  
|*\<GUID>*|REG_SZ|""|支持的逻辑视图的键。 您可以根据需要使用任意数量的。 注册表项的名称是重要的，而不是值，该值始终为空字符串。|  
  
### <a name="example"></a>示例  
  
```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp\  
  \Editors\  
    {8281C572-2171-45AA-A642-7D8BC1662F1C}\  
      LogicalViews\  
       (Default) = reg_sz:  
       {7651a700-06e5-11d1-8ebd-00a0c90f26ea} = reg_sz:  
       {7651a701-06e5-11d1-8ebd-00a0c90f26ea} = reg_sz:  
       {7651a702-06e5-11d1-8ebd-00a0c90f26ea} = reg_sz:  
       {7651a703-06e5-11d1-8ebd-00a0c90f26ea} = reg_sz:  
```  
  
## <a name="registry-entries-for-editor-extension-options"></a>编辑器扩展选项的注册表项  
 *VS Reg Root*\EDITORS \\ *编辑器 GUID*\Extensions 键可以包含以下值。 文件扩展名不包含前导句点。  
  
|名称|类型|范围|说明|  
|----------|----------|-----------|-----------------|  
|（默认值）|REG_SZ||未使用。|  
|*\<ext>*|REG_DWORD|0-0xffffffff|扩展的相对优先级。 如果两种或多种语言共享同一扩展，则选择较高优先级的语言。|  
  
 此外，当前用户对编辑器的默认选择将存储在 HKEY_Current_User \Software\Microsoft\VisualStudio \\ *X.Y*\Default 编辑器 \\ *ext*中。所选语言服务的 GUID 位于自定义条目中。 这优先于当前用户。  
  
### <a name="example"></a>示例  
  
```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\9.0\  
  \Editors\  
    {8281C572-2171-45AA-A642-7D8BC1662F1C}\  
      Extensions\  
       (Default) = reg_sz:  
       *         = reg_dword:0x00000018  
       html      = reg_dword:0x00000027  
       shtm      = reg_dword:0x00000027  
       shtml     = reg_dword:0x00000027  
```  
  
## <a name="registry-entries-for-managed-package-framework-language-service-options"></a>托管包框架语言服务选项的注册表项  
 以下注册表项特定于管理包框架 (MPF) 语言服务类。 这些注册表项表示在语言服务中对各种 IntelliSense 功能和其他高级编辑功能的支持。  
  
 这些注册表项可通过类访问 <xref:Microsoft.VisualStudio.Package.LanguagePreferences> 。  
  
|名称|类型|范围|说明|  
|----------|----------|-----------|-----------------|  
|CodeSense|REG_DWORD|0-1|对 IntelliSense 操作的支持。|  
|MatchBraces|REG_DWORD|0-1|支持匹配语言对，如大括号、圆括号和方括号。|  
|QuickInfo|REG_DWORD|0-1|支持 IntelliSense 快速信息操作。|  
|ShowMatchingBrace|REG_DWORD|0-1|支持在状态栏中显示匹配的语言对。|  
|MatchBracesAtCaret|REG_DWORD|0-1|支持显示匹配的语言对，通常通过突出显示这两个元素。|  
|MaxErrorMessages|REG_DWORD|0-n|**错误列表**窗口中可显示的最大错误数。|  
|CodeSenseDelay|REG_DWORD|0-n|为 IntelliSense 操作启动任何后台分析之前延迟的毫秒数。|  
|EnableAsyncCompletion|REG_DWORD|0-1|支持后台分析。|  
|EnableCommenting|REG_DWORD|0-1|支持注释掉选定的文本块，同时也表示支持取消注释选定文本。|  
|EnableFormatSelection|REG_DWORD|0-1|支持设置文本格式，如自动缩进或调整大括号的位置。|  
|AutoOutlining|REG_DWORD|0-1|支持 (可以折叠) 的区域的大纲。|  
|MaxRegions|REG_DWORD|0-n|每个文件的最大隐藏区域数。|  
  
```  
ExampleHKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp\  
  Languages\  
    Language Services\  
      XML\  
        (Default)             = reg_sz:{f6819a78-a205-47b5-be1c-675b3c7f0b8e}  
        MatchBraces           = reg_dword:0x00000001  
        QuickInfo             = reg_dword:0x00000001  
        ShowMatchingBrace     = reg_dword:0x00000001  
        MatchBracesAtCaret    = reg_dword:0x00000000  
        MaxErrorMessages      = reg_dword:0x00000064  
        CodeSenseDelay        = reg_dword:0x000001f4  
        MaxRegions            = reg_dword:0x0000000a  
```  
  
## <a name="see-also"></a>另请参阅  
 [开发旧版语言服务](../../extensibility/internals/developing-a-legacy-language-service.md)
