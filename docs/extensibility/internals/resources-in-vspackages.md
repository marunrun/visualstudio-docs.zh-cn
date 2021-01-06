---
title: Vspackage 中的资源 |Microsoft Docs
description: 了解可在 Vspackage 中嵌入哪些类型的本地化资源。 你还可以在本机附属 UI Dll 或托管附属 Dll 中嵌入资源。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- managed VSPackages, resources in
- resources, managed VSPackages
- VSPackages, managed resources
ms.assetid: cc8c17a6-b190-4856-b001-0c1104f104b2
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2693d25e0b175a075bcc644077895076b75b7578
ms.sourcegitcommit: 0c9155e9b9408fb7481d79319bf08650b610e719
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/05/2021
ms.locfileid: "97875721"
---
# <a name="resources-in-vspackages"></a>VSPackage 中的资源
可以将本地化的资源嵌入到本机附属 UI Dll、托管的附属 Dll 或托管的 VSPackage 本身中。

 无法在 Vspackage 中嵌入某些资源。 可以嵌入以下托管类型：

- 字符串

- 包加载键 (也是字符串) 

- 工具窗口图标

- 编译的命令表输出 (CTO) 文件

- CTO 位图

- 命令行帮助

- "关于" 对话框数据

  按资源 ID 选择管理包中的资源。 异常是 CTO 文件，必须将其命名为 CTMENU。 CTO 文件必须以形式出现在资源表中 `byte[]` 。 所有其他资源项都按类型进行标识。

  你可以使用 <xref:Microsoft.VisualStudio.Shell.PackageRegistrationAttribute> 属性来指示 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 该托管资源可用。

  [!code-csharp[VSSDKResources#1](../../extensibility/internals/codesnippet/CSharp/resources-in-vspackages_1.cs)]
  [!code-vb[VSSDKResources#1](../../extensibility/internals/codesnippet/VisualBasic/resources-in-vspackages_1.vb)]

  <xref:Microsoft.VisualStudio.Shell.PackageRegistrationAttribute>以这种方式设置时，指示在 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 搜索资源时应忽略非托管的附属 dll，例如通过使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsShell.LoadPackageString%2A> 。 如果 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 遇到两个或多个具有相同资源 ID 的资源，它将使用它找到的第一个资源。

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

## <a name="implementation-notes"></a>实现说明
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 尽可能延迟加载 Vspackage。 在 VSPackage 中嵌入 CTO 文件的结果是，在 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 安装过程中必须在内存中加载所有此类 vspackage，这是在生成合并的命令表时。 可以通过检查元数据（无需在 VSPackage 中运行代码），从 VSPackage 中提取资源。 此时 VSPackage 未初始化，因此性能损失很小。

 如果在 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 安装后从 VSPackage 请求资源，则可能已加载并初始化该程序包，因此性能损失会降至最低。

## <a name="see-also"></a>另请参阅
- [管理 VSPackages](../../extensibility/managing-vspackages.md)
- [MFC 应用程序中已本地化的资源：附属 DLL](/cpp/build/localized-resources-in-mfc-applications-satellite-dlls)
