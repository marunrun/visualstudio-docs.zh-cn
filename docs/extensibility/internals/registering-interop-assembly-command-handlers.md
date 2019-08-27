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
ms.openlocfilehash: b3e90ffc6b065b6d69bbe09bfe1887764ccc9955
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66353324"
---
# <a name="registering-interop-assembly-command-handlers"></a>注册互操作程序集命令处理程序
VSPackage 必须使用注册[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]，以便在集成的开发环境 (IDE) 将正确路由命令。

 通过手动编辑或使用注册机构 (.rgs) 文件，可以更新注册表。 有关详细信息，请参阅 [Creating Registrar Scripts](/cpp/atl/creating-registrar-scripts)。

 托管包框架 (MPF) 提供此功能通过<xref:Microsoft.VisualStudio.Shell.ProvideMenuResourceAttribute>类。

- [命令表格式参考](https://msdn.microsoft.com/library/09e9c6ef-9863-48de-9483-d45b7b7c798f)资源位于非托管附属 UI dll 中。

## <a name="command-handler-registration-of-a-vspackage"></a>命令的 VSPackage 的处理程序注册
 VSPackage 充当用户界面 (UI) 的处理程序的基于的命令需要名为后 VSPackage 的注册表项`GUID`。 此注册表项指定 VSPackage 的用户界面资源文件和文件内的菜单资源的位置。 注册表项本身位于 HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\\ *\<版本>* \Menus，其中 *\<版本>* 是的版本[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]，例如 9.0。

> [!NOTE]
> HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio 的根路径\\ *\<版本 >* 可以重写使用备用根时[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]shell 进行初始化。 根路径的详细信息，请参阅[使用 Windows Installer 安装 Vspackage](../../extensibility/internals/installing-vspackages-with-windows-installer.md)。

### <a name="the-ctmenu-resource-registry-entry"></a>CTMENU 资源注册表项
 注册表项的结构为：

```
HKEY_LOCAL_MACHINE\Software\VisualStudio\<Version>\
  Menus\
    <GUID> = <Resource Information>
```

 \<*GUID*> 是`GUID`的 VSPackage 中窗体 {XXXXXX-XXXX-XXXX-XXXX-XXXXXXXXX}。

 *\<资源信息 >* 逗号分隔的三个元素组成。 这些元素按顺序是：

 \<*资源 DLL 路径*>， \<*菜单资源 ID*>， \<*菜单版本*>

 下表描述的字段\<*资源信息*>。

| 元素 | 描述 |
|---------------------------| - |
| \<*资源 DLL 路径*> | 这是包含该菜单资源 DLL 的资源的完整路径或此留空，指示，VSPackage 的资源 DLL 要使用 （如指定在其中注册自己的 VSPackage 的包子项中）。<br /><br /> 这也十分常见将此字段留空。 |
| \<*菜单资源 ID*> | 这是资源 ID `CTMENU` vspackage 包含的所有 UI 元素，如从编译的资源[.vsct](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)文件。 |
| \<*菜单版本*> | 这是一个数字作为版本使用`CTMENU`资源。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 使用此值来确定它是否需要重新合并的内容`CTMENU`具有其所有的缓存资源`CTMENU`资源。 通过执行 devenv 安装程序命令来触发重新合并。<br /><br /> 此值最初应设置为 1，在每次更改后递增`CTMENU`资源并重新合并发生之前。 |

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