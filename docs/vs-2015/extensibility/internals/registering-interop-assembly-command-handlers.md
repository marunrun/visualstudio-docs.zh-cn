---
title: 注册互操作程序集命令处理程序 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- interop assemblies, command handlers
- command handling with interop assemblies, registering
ms.assetid: 303cd399-e29d-4ea1-8abe-5e0b59c12a0c
caps.latest.revision: 20
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 9d2822e9eef36806f5c251813925fb4244242519
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65705810"
---
# <a name="registering-interop-assembly-command-handlers"></a>注册互操作程序集命令处理程序
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

VSPackage 必须向注册， [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 使集成开发环境 (IDE) 正确路由其命令。  
  
 可以通过手动编辑或使用注册器 () 文件来更新注册表。 有关更多信息，请参见 [Creating Registrar Scripts](https://msdn.microsoft.com/library/cbd5024b-8061-4a71-be65-7fee90374a35)。  
  
 托管包框架 (MPF) 通过类提供此功能 <xref:Microsoft.VisualStudio.Shell.ProvideMenuResourceAttribute> 。  
  
 [命令表格式引用](https://msdn.microsoft.com/09e9c6ef-9863-48de-9483-d45b7b7c798f) 资源位于非托管附属 UI dll 中。  
  
## <a name="command-handler-registration-of-a-vspackage"></a>命令处理程序注册 VSPackage  
 用作用户界面 (UI) 命令的处理程序的 VSPackage 需要名为 VSPackage 的注册表项 `GUID` 。 此注册表项指定 VSPackage 的 UI 资源文件的位置以及该文件中的菜单资源。 注册表项本身位于 HKEY_LOCAL_MACHINE \Software\Microsoft\VisualStudio \\ *\<Version>* \Menus 下，其中 *\<Version>* 是的版本 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ，例如9.0。  
  
> [!NOTE]
> \\ *\<Version>* 初始化 shell 时，可以使用备用根替换 HKEY_LOCAL_MACHINE \software\microsoft\visualstudio 的根路径 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 。 有关根路径的详细信息，请参阅 [安装带有 Windows Installer 的 vspackage](../../extensibility/internals/installing-vspackages-with-windows-installer.md)。  
  
### <a name="the-ctmenu-resource-registry-entry"></a>CTMENU 资源注册表项  
 注册表项的结构是：  
  
```  
HKEY_LOCAL_MACHINE\Software\VisualStudio\<Version>\  
  Menus\  
    <GUID> = <Resource Information>  
```  
  
 \<*GUID*> 是 VSPackage 的，格式为 {XXXXXX-xxxx- `GUID` XXXXXXXXX}。  
  
 *\<Resource Information>* 由以逗号分隔的三个元素组成。 这些元素按顺序排列：  
  
 \<*Path to Resource DLL*>, \<*Menu Resource ID*>, \<*Menu Version*>  
  
 下表对的字段进行了说明 \<*Resource Information*> 。  
  
|元素|说明|  
|-------------|-----------------|  
|\<*Path to Resource DLL*>|这是包含菜单资源的资源 DLL 的完整路径，或留空，这表示将使用 VSPackage 的资源 DLL， (在 VSPackage 本身) 注册到的 "包" 子项中指定。<br /><br /> 建议将此字段留空。|  
|\<*Menu Resource ID*>|这是资源的资源 ID `CTMENU` ，其中包含 VSPackage 的所有 UI 元素，这些元素是从 [.vsct](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md) 文件编译而来的。|  
|\<*Menu Version*>|此值用作资源的版本 `CTMENU` 。 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 使用此值来确定是否需要将资源的内容更正到 `CTMENU` 其所有资源的缓存中 `CTMENU` 。 通过执行 devenv 安装命令触发更正。<br /><br /> 此值最初应设置为1，并在资源中每次更改之后 `CTMENU` 和发生更正之前递增。|  
  
### <a name="example"></a>示例  
 下面是几个资源条目的示例：  
  
```  
HKEY_LOCAL_MACHINE\Software\VisualStudio\9.0Exp\  
  Menus\  
    {019971D6-4685-11D2-B48A-0000F87572EB} = ,1, 10  
    {1b027a40-8f43-11d0-8d11-00a0c91bc942} = , 10211, 3  
```  
  
## <a name="see-also"></a>另请参阅  
 [Vspackage 如何添加用户界面元素](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)   
 [使用互操作程序集的命令和菜单](../../extensibility/internals/commands-and-menus-that-use-interop-assemblies.md)
