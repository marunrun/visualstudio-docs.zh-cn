---
title: Vspackage 中的资源 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- managed VSPackages, resources in
- resources, managed VSPackages
- VSPackages, managed resources
ms.assetid: cc8c17a6-b190-4856-b001-0c1104f104b2
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 07e1e19f802203b9770764330ea894b7d0eb98b8
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72724160"
---
# <a name="resources-in-vspackages"></a>VSPackage 中的资源
可以将本地化的资源嵌入到本机附属 UI Dll、托管的附属 Dll 或托管的 VSPackage 本身中。

 无法在 Vspackage 中嵌入某些资源。 可以嵌入以下托管类型：

- 字符串

- 包加载键（也是字符串）

- 工具窗口图标

- 编译的命令表输出（CTO）文件

- CTO 位图

- 命令行帮助

- "关于" 对话框数据

  按资源 ID 选择管理包中的资源。 异常是 CTO 文件，必须将其命名为 CTMENU。 CTO 文件必须作为 `byte[]` 出现在资源表中。 所有其他资源项都按类型进行标识。

  您可以使用 <xref:Microsoft.VisualStudio.Shell.PackageRegistrationAttribute> 特性指示 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 托管资源可用。

  [!code-csharp[VSSDKResources#1](../../extensibility/internals/codesnippet/CSharp/resources-in-vspackages_1.cs)]
  [!code-vb[VSSDKResources#1](../../extensibility/internals/codesnippet/VisualBasic/resources-in-vspackages_1.vb)]

  以这种方式设置 <xref:Microsoft.VisualStudio.Shell.PackageRegistrationAttribute> 表示 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 应在搜索资源时忽略非托管的附属 Dll，例如，通过使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsShell.LoadPackageString%2A>。 如果 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 遇到两个或更多具有相同资源 ID 的资源，它将使用它找到的第一个资源。

## <a name="example"></a>示例
 下面的示例是工具窗口图标的托管表示形式。

```
<data name="1001"
type="System.Resources.ResXFileRef,System.Windows.Forms">
     <value>
     MyToolWinIcon.bmp;
     System.Drawing.Bitmap,
     System.Drawing,
     Version=1.0.0.0,
     Culture=neutral,
     PublicKeyToken=b03f5f7f11d50a3a
     </value>
</data>
```

 下面的示例演示如何嵌入 CTO 字节数组，该数组必须命名为 CTMENU。

```
<data name="CTMENU"
type="System.Resources.ResXFileRef,System.Windows.Forms">
     <value>
     MyPackage.cto;
     System.Byte[],
     mscorlib,
     Version=1.0.0.0,
     Culture=neutral,
     PublicKeyToken=b03f5f7f11d50a3a
     </value>
</data>
```

## <a name="implementation-notes"></a>实现注释
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 尽可能延迟加载 Vspackage。 在 VSPackage 中嵌入 CTO 文件的结果是，在安装过程中，[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 必须在内存中加载所有此类 Vspackage，这是在生成合并的命令表时。 可以通过检查元数据（无需在 VSPackage 中运行代码），从 VSPackage 中提取资源。 此时 VSPackage 未初始化，因此性能损失很小。

 如果 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 在设置后从 VSPackage 请求资源，则可能已加载并初始化该程序包，因此性能损失会降至最低。

## <a name="see-also"></a>请参阅
- [管理 VSPackages](../../extensibility/managing-vspackages.md)
- [MFC 应用程序中已本地化的资源：附属 DLL](/cpp/build/localized-resources-in-mfc-applications-satellite-dlls)
