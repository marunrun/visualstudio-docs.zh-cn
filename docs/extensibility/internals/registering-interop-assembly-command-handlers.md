---
title: 注册互操作程序集命令处理程序 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- interop assemblies, command handlers
- command handling with interop assemblies, registering
ms.assetid: 303cd399-e29d-4ea1-8abe-5e0b59c12a0c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7e2ab6389f1e0d369dd095290d12c97431c44155
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80705864"
---
# <a name="registering-interop-assembly-command-handlers"></a>注册互操作程序集命令处理程序
VSPackage 必须注册，[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]以便集成开发环境 （IDE） 正确路由其命令。

 注册表可以通过手动编辑或使用注册器 （.rgs） 文件进行更新。 有关更多信息，请参见 [Creating Registrar Scripts](/cpp/atl/creating-registrar-scripts)。

 托管包框架 （MPF） 通过<xref:Microsoft.VisualStudio.Shell.ProvideMenuResourceAttribute>类提供此功能。

- [命令表格式 参考](https://msdn.microsoft.com/library/09e9c6ef-9863-48de-9483-d45b7b7c798f)资源位于非托管的卫星 UI dlls 中。

## <a name="command-handler-registration-of-a-vspackage"></a>命令处理程序 VS 包注册
 VSPackage 充当基于用户界面 （UI） 的命令的处理程序需要以 VSPackage`GUID`命名的注册表项。 此注册表项指定 VSPackage 的 UI 资源文件的位置以及该文件中的菜单资源。 注册表项本身位于HKEY_LOCAL_MACHINE\软件\微软_VisualStudio\\*\<版本>* \Menus 下，*\<其中版本>* 是[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]，例如 9.0。

> [!NOTE]
> HKEY_LOCAL_MACHINE_SOFTWARE_Microsoft_VisualStudio\\*\<版本>* 的根路径可以在初始化[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]shell 时用备用根覆盖。 有关根路径的详细信息，请参阅[使用 Windows 安装程序安装 VS 包](../../extensibility/internals/installing-vspackages-with-windows-installer.md)。

### <a name="the-ctmenu-resource-registry-entry"></a>CTMENU 资源注册表项
 注册表项的结构是：

```
HKEY_LOCAL_MACHINE\Software\VisualStudio\<Version>\
  Menus\
    <GUID> = <Resource Information>
```

 \<*GUID*>`GUID`是表格 [XXXXXX-XXXX-XXXX-XXXX-XXXXXXXXX]中的 VS 包。

 资源信息>由三个用逗号分隔的元素组成。 * \<* 这些元素按以下顺序排列：

 \<*资源 DLL*>、\<*菜单资源 ID* \<>、*菜单版本的路径*>

 下表描述了\<*资源信息*>字段。

| 元素 | 描述 |
|---------------------------| - |
| \<*资源 DLL 的路径*> | 这是包含菜单资源的资源 DLL 的完整路径，或者该路径留空，指示将使用 VSPackage 的资源 DLL（如注册 VSPackage 本身的包子键中指定）。<br /><br /> 通常将此字段留空。 |
| \<*菜单资源 ID*> | 这是`CTMENU`资源的资源 ID，其中包含从[.vsct](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)文件编译的 VSPackage 的所有 UI 元素。 |
| \<*菜单版本*> | 这是用作`CTMENU`资源版本的数字。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]使用此值确定是否需要将`CTMENU`资源的内容与其所有`CTMENU`资源的缓存重新合并。 通过执行 devenv 设置命令触发重新合并。<br /><br /> 此值最初应设置为 1，并在`CTMENU`资源中的每一次更改后和重新合并发生之前递增。 |

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
