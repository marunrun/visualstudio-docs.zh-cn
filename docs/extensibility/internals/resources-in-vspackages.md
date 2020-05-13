---
title: VS 包中的资源 |微软文档
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
ms.openlocfilehash: 493e9834e3d7cf6d82cebb8dd93d5369678c7be0
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80705606"
---
# <a name="resources-in-vspackages"></a>VSPackage 中的资源
您可以将本地化资源嵌入到本机卫星 UI DLL、托管卫星 DLL 或托管 VSPackage 本身中。

 某些资源不能嵌入到 VSPackages 中。 可以嵌入以下托管类型：

- 字符串

- 包加载键（也是字符串）

- 工具窗口图标

- 编译的命令表输出 （CTO） 文件

- CTO 位图

- 命令行帮助

- 关于对话框数据

  托管包中的资源由资源 ID 选择。 CTO 文件是一个例外，该文件必须命名为 CTMENU。 CTO 文件必须在资源表中显示为`byte[]`。 所有其他资源项均按类型标识。

  可以使用 该<xref:Microsoft.VisualStudio.Shell.PackageRegistrationAttribute>属性指示[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]该托管资源可用。

  [!code-csharp[VSSDKResources#1](../../extensibility/internals/codesnippet/CSharp/resources-in-vspackages_1.cs)]
  [!code-vb[VSSDKResources#1](../../extensibility/internals/codesnippet/VisualBasic/resources-in-vspackages_1.vb)]

  以这种方式<xref:Microsoft.VisualStudio.Shell.PackageRegistrationAttribute>设置指示在[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]搜索资源时应忽略非托管的卫星 DLL，例如，通过使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsShell.LoadPackageString%2A>。 如果[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]遇到两个或多个具有相同资源 ID 的资源，则使用它找到的第一个资源。

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

 下面的示例演示如何嵌入必须命名为 CTMENU 的 CTO 字节数组。

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
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]尽可能延迟 VSPackages 的加载。 在 VSPackage 中嵌入 CTO 文件的结果是在安装程序[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]期间（即生成合并的命令表）期间，必须在内存中加载所有此类 VS 包。 无需在 VSPackage 中运行代码即可从 VSPackage 中提取资源。 VSPackage 此时未初始化，因此性能损失最小。

 在[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]安装程序后从 VSPackage 请求资源时，该包可能已加载和初始化，因此性能损失最小。

## <a name="see-also"></a>请参阅
- [管理 VSPackages](../../extensibility/managing-vspackages.md)
- [MFC 应用程序中的本地化资源：附属 DLL](/cpp/build/localized-resources-in-mfc-applications-satellite-dlls)
