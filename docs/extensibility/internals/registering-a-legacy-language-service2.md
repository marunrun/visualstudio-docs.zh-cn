---
title: 注册传统语言服务2 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- registration, language services
- language services, registry information
- registry, language services
ms.assetid: ca312aa3-f9f1-4572-8553-89bf3a724deb
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2d9d13f301f6c04c0f7b14cc8c685f08b072ef84
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80705890"
---
# <a name="registering-a-legacy-language-service"></a>注册旧版语言服务
以下各节提供了 中[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]提供的各种语言服务选项的注册表项列表。

 在下面的注册表项列表中 *，VS Reg Root*等于HKEY_LOCAL_MACHINE_SOFTWARE_Microsoft_VisualStudio\\*X.Y*，其中*X.Y*是[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]版本号。

## <a name="registry-entries-for-language-service-options"></a>语言服务选项的注册表项
 *VS Reg 根*\语言\\\语言服务*语言名称*键可以包含以下值。

|名称|类型|范围|描述|
|----------|----------|-----------|-----------------|
|（默认值）|REG_SZ|*\<GUID>*|语言服务的 GUID。|
|朗雷斯ID|REG_DWORD|0x0-0xff|语言的本地化文本名称的字符串资源标识符 （ResID）。|
|程序包|REG_SZ|*\<GUID>*|VS 包的 GUID。|
|显示完成|REG_DWORD|0-1|指定是否启用了"**选项**"对话框中的 **"语句完成**"选项。|
|显示智能缩进|REG_DWORD|0-1|指定是否启用了在 **"选项**"对话框中选择 **"智能**缩进"的选项。|
|请求库存颜色|REG_DWORD|0-1|指定自定义颜色还是默认颜色用于为关键字着色。|
|显示 HotURL|REG_DWORD|0-1|指定用户是否可以单击 URL。|
|默认为非热 URL|REG_DWORD|0-1|在 **"选项"** 对话框中指定启用 **"启用一键 URL 导航**"选项的初始设置。|
|默认插入空格|REG_DWORD|0-1|指定语言服务是否具有"插入空格"作为其默认选项卡选项。|
|显示向下放置栏选项|REG_DWORD|0-1|启用或禁用"**选项**"对话框中的**导航栏**选项，该对话框显示或隐藏**导航栏**。|
|仅限单代码窗口|REG_DWORD|0-1|在**语言服务的"窗口"** 菜单中启用或禁用 **"新建窗口**"选项。|
|启用高级会员选项|REG_DWORD|0-1|启用或禁用"**隐藏高级成员"****的选项**对话框设置。|
|支持CF_HTML|REG_DWORD|0-1|指定编辑器是否启用 HTML 数据的复制和粘贴。|
|启用线编号选项|REG_DWORD|0-1|指定是否为语言服务启用"**选项**"对话框中的 **"行号"** 选项。|
|隐藏高级成员按默认值|REG_DWORD|0-1|指定高级成员（如专用字段）是否隐藏在完成列表中。|
|显示布雷斯完成|REG_DWORD|0-1|指定是否启用"**选项**"对话框中的 **"大括号完成**"选项。|

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
 *VS Reg 根*[语言]\\语言服务*语言名称*\\[调试器语言*GUID*] 键可以包含以下值。

|名称|类型|范围|描述|
|----------|----------|-----------|-----------------|
|（默认值）|REG_SZ|text|默认值可用于记录语言的名称。 此键的名称是表达式赋值器的 GUID，该表达式赋值器在*\<VS Reg 根>*[AD7Metrics_表达式赋值器》中具有相应的条目。|

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
 您可以在属性页和属性节点的 EditorToolsOptions 键下添加注册表项。 这些键及其值标识用于配置语言服务**的选项**对话框（**在"工具**"菜单上）中的属性页。 在下面的示例中，*页面名称*是属性页的名称，*节点名称*是 **"选项"** 对话框中树中的节点的名称。 页面条目和节点条目必须单独指定。

|名称|类型|范围|描述|
|----------|----------|-----------|-----------------|
|（默认值）|REG_SZ|渣 油|此选项页的本地化显示名称。 名称可以是文本文本，或 *`nnn`，其中`nnn`是指定 VSPackage 的附属 DLL 中的字符串资源 ID。|
|程序包|REG_SZ|*Guid*|实现此选项页的 VS 包的 GUID。|
|页|REG_SZ|*Guid*|属性页的 GUID 通过调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetPropertyPage%2A>方法从 VSPackage 请求。 如果不存在此注册表项，注册表项将描述节点，而不是页面。|

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

## <a name="registry-entries-for-file-name-extension-options"></a>文件名扩展选项的注册表项
 文件扩展名的条目应包括前导期间，例如".myext"。

|名称|类型|范围|描述|
|----------|----------|-----------|-----------------|
|（默认值）|REG_SZ|*Guid*|此文件名扩展名类型的默认语言服务服务 GUID。|

### <a name="example"></a>示例

```
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp\
  Languages\
    File Extensions\
      .cpp\
        (Default) = {B2F072B0-ABC1-11D0-9D62-00C04FD9DFD9}
```

## <a name="registry-entries-for-editor-options"></a>编辑器选项的注册表项
 *VS Reg 根*\编辑器密钥可以包含以下值：

|名称|类型|范围|描述|
|----------|----------|-----------|-----------------|
|（默认值）|REG_SZ|""|未使用;您可以将您的姓名放在此处进行文档记录。|
|DefaultToolboxTab|REG_SZ|""|工具箱选项卡的名称，用于在编辑器处于活动状态时进行默认值。|
|DisplayName|REG_SZ|渣 油|要在 **"打开使用"** 对话框中显示的名称。 名称是字符串资源 ID 或标准格式的名称。|
|排除文本编辑器|REG_DWORD|0-1|用于**打开"随"** 菜单命令。 如果不想在特定文件类型的可用编辑器列表中列出默认文本编辑器，则将此值设置为 1。|
|链接编辑器|REG_SZ|*\<GUID>*|用于任何可以打开具有代码页支持的文件的语言服务。 例如，当您使用**Open With**命令打开 .txt 文件时，将提供用于使用源代码编辑器的选项，无论是否使用编码。<br /><br /> 子键名称中指定的 GUID 用于代码页编辑器工厂;在此特定注册表项中指定的链接 GUID 用于常规编辑器工厂。 此条目的目的是，如果 IDE 不使用默认编辑器打开文件，IDE 将尝试使用列表中的下一个编辑器。 下一个编辑器不应是代码页编辑器工厂，因为此编辑器工厂与失败的编辑器工厂基本相同。|
|程序包|REG_SZ|*\<GUID>*|显示名称的 ResID 的 VS 包装 GUID。|

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
 *VS Reg 根*\\\*编辑器 GUI>*_LogicViews 键可以包含以下值。

|名称|类型|范围|描述|
|----------|----------|-----------|-----------------|
|（默认值）|REG_SZ||未使用。|
|*\<GUID>*|REG_SZ|""|受支持的逻辑视图的键。 你可以有尽可能多的这些，你需要。 注册表项的名称是重要的，而不是值，它始终是一个空字符串。|

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
 *VS Reg 根*\\\*编辑器 GUID*_扩展键可以包含以下值。 文件名扩展名不包括前导期间。

|名称|类型|范围|描述|
|----------|----------|-----------|-----------------|
|（默认值）|REG_SZ||未使用。|
|*\<分机>*|REG_DWORD|0-0xffffff|扩展的相对优先级。 如果两种或多种语言共享同一扩展名，则选择优先级较高的语言。|

 \\此外，当前用户对编辑器的默认选择存储在HKEY_Current_User_软件\VisualStudio*X.Y*=默认编辑器\\*分机*。所选语言服务的 GUID 位于"自定义"条目中。 这优先适用于当前用户。

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
 以下注册表项特定于托管包框架 （MPF） 语言服务类。 这些注册表项表示对各种 IntelliSense 功能和其他高级编辑功能的语言服务的支持。

 这些注册表项通过<xref:Microsoft.VisualStudio.Package.LanguagePreferences>类访问。

|名称|类型|范围|描述|
|----------|----------|-----------|-----------------|
|代码感知|REG_DWORD|0-1|支持 IntelliSense 操作。|
|匹配支架|REG_DWORD|0-1|支持匹配的语言对，如大括号、括号和括号。|
|QuickInfo|REG_DWORD|0-1|支持"感知快速信息"操作。|
|显示匹配支架|REG_DWORD|0-1|支持在状态栏中显示匹配的语言对。|
|匹配支架AtCaret|REG_DWORD|0-1|支持显示匹配的语言对，通常通过突出显示这两个元素。|
|最大错误消息|REG_DWORD|0-n|可在 **"错误列表"** 窗口中显示的最大错误数。|
|代码感知延迟|REG_DWORD|0-n|启动 IntelliSense 操作的任何背景分析之前要延迟的毫秒数。|
|启用同步完成|REG_DWORD|0-1|支持后台分析。|
|启用注释|REG_DWORD|0-1|支持注释出选定的文本块，还意味着支持未注释的选定文本。|
|启用格式选择|REG_DWORD|0-1|支持格式化文本，如自动缩进或调整大括号的位置。|
|自动退出|REG_DWORD|0-1|支持大纲（可折叠的区域）。|
|最大区域|REG_DWORD|0-n|每个文件的最大隐藏区域数。|

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

## <a name="see-also"></a>请参阅
- [开发旧版语言服务](../../extensibility/internals/developing-a-legacy-language-service.md)
