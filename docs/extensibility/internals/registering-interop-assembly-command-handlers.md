---
title: 注册互操作程序集命令处理程序 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- interop assemblies, command handlers
- command handling with interop assemblies, registering
ms.assetid: 303cd399-e29d-4ea1-8abe-5e0b59c12a0c
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: cbc0d162a11df034bec4d1f357ef8abd106da401
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72724691"
---
# <a name="registering-interop-assembly-command-handlers"></a>注册互操作程序集命令处理程序
VSPackage 必须注册到 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]，以便集成开发环境（IDE）正确路由其命令。

 可以通过手动编辑或使用注册机构（.rgs）文件来更新注册表。 有关详细信息，请参阅 [Creating Registrar Scripts](/cpp/atl/creating-registrar-scripts)。

 托管包框架（MPF）通过 <xref:Microsoft.VisualStudio.Shell.ProvideMenuResourceAttribute> 类提供此功能。

- [命令表格式引用](https://msdn.microsoft.com/library/09e9c6ef-9863-48de-9483-d45b7b7c798f)资源位于非托管附属 UI dll 中。

## <a name="command-handler-registration-of-a-vspackage"></a>命令处理程序注册 VSPackage
 作为基于用户界面（UI）的命令的处理程序的 VSPackage 要求在 VSPackage `GUID` 后面命名一个注册表项。 此注册表项指定 VSPackage 的 UI 资源文件的位置以及该文件中的菜单资源。 注册表项本身位于 HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio \\ *\<Version >* \Menus，其中 *\<Version >* 是 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 的版本，例如9.0。

> [!NOTE]
> 初始化 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] shell 时，可以使用备用根覆盖 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio \\ *\<Version >* 的根路径。 有关根路径的详细信息，请参阅[安装带有 Windows Installer 的 vspackage](../../extensibility/internals/installing-vspackages-with-windows-installer.md)。

### <a name="the-ctmenu-resource-registry-entry"></a>CTMENU 资源注册表项
 注册表项的结构是：

```
HKEY_LOCAL_MACHINE\Software\VisualStudio\<Version>\
  Menus\
    <GUID> = <Resource Information>
```

 *GUID*> \< 是 VSPackage 的 `GUID`，格式为 {XXXXXX-XXXXXXXXX}。

 *\<Resource 信息 >* 包含以逗号分隔的三个元素。 这些元素按顺序排列：

 \< > 的*资源 DLL 的路径*，\<*菜单资源 ID*>，\<*菜单版本*>

 下表描述了 \<*资源信息*> 的字段。

| 元素 | 描述 |
|---------------------------| - |
| \<*资源 DLL 的路径*> | 这是包含菜单资源的资源 DLL 的完整路径，或留空，这表示将使用 VSPackage 的资源 DLL （在 VSPackage 本身注册到的 "包" 子项中指定）。<br /><br /> 建议将此字段留空。 |
| \<*菜单资源 ID* > | 这是 `CTMENU` 资源的资源 ID，其中包含 VSPackage 的所有 UI 元素，这些元素是从[.vsct](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)文件编译而来的。 |
| \<*菜单版本*> | 这是用作 `CTMENU` 资源的版本的数字。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 使用此值来确定是否需要将 `CTMENU` 资源的内容与所有 `CTMENU` 资源的缓存更正。 通过执行 devenv 安装命令触发更正。<br /><br /> 此值最初应设置为1，并在每次更改 `CTMENU` 资源后和发生更正之前递增。 |

### <a name="example"></a>示例
 下面是几个资源条目的示例：

```
HKEY_LOCAL_MACHINE\Software\VisualStudio\9.0Exp\
  Menus\
    {019971D6-4685-11D2-B48A-0000F87572EB} = ,1, 10
    {1b027a40-8f43-11d0-8d11-00a0c91bc942} = , 10211, 3
```

## <a name="see-also"></a>请参阅
- [VSPackage 如何添加用户界面元素](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [使用互操作程序集的命令和菜单](../../extensibility/internals/commands-and-menus-that-use-interop-assemblies.md)