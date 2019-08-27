---
title: 安装和管理本地内容 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- hv_manage
helpviewer_keywords:
- changing content installation source [Help Viewer 2.0]
- updating local content [Help Viewer 2.0]
- Help Viewer 2.0, content installation source
- Help Viewer 2.0, updating local content
- Help Viewer 2.0, changing content installation source
- installing local content [Help Viewer 2.0]
- content installation source [Help Viewer 2.0]
- downloading content [Help Viewer 2.0]
- removing local content [Help Viewer 2.0]
- Help Viewer 2.0, removing local content
- Help Viewer 2.0, installing local content
- Help Viewer 2.0, downloading content
ms.assetid: efd9df4c-2e69-4c50-992c-9678a8d8cf19
caps.latest.revision: 27
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: a5ad9c363a590ef692bdcd1d8c00727d55113b97
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63412360"
---
# <a name="install-and-manage-local-content"></a>安装和管理本地内容
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

通过使用 Microsoft Help Viewer，可以添加、删除、更新和移动安装在计算机上的“帮助”内容，以满足你的软件开发需求。  
  
 若要管理本地计算机上的内容，必须使用具有管理权限的帐户登录。 此外，如果在企业环境中工作，则无法管理本地内容，因为系统管理员可能为你的组织执行这些操作。 有关详细信息，请参阅[帮助查看器管理员指南](../ide/help-viewer-administrator-guide.md)。  
  
## <a name="changing-the-content-installation-source"></a>更改内容安装源  
 默认情况下，帮助查看器通过将 Microsoft 联机服务用作源来安装内容。 通常不应更改内容，除非你所在的企业环境的系统管理员已为其安装其他位置的内容。  
  
#### <a name="to-change-the-content-installation-source"></a>要更改内容安装源  
  
1. 在“管理内容”选项卡上，选择“磁盘”选项按钮。  
  
    > [!NOTE]
    > 如果管理员已阻止你修改内容安装源，“磁盘”选项将不可用。 有关详细信息，请参阅[帮助查看器管理员指南](../ide/help-viewer-administrator-guide.md)。  
  
2. 执行以下步骤之一：  
  
    - 输入 .msha 文件的路径或服务终结点的 URL。  
  
    - 选择“浏览 (**...**)”按钮以导航到 .msha 文件。  
  
    - 在此列表中，选择最近使用的条目。  
  
## <a name="download-and-install-content-locally"></a>下载内容并本地安装  
 如果你下载了内容并安装在本地计算机上，则无需 Internet 连接即可查看主题。  
  
> [!IMPORTANT]
> 若要安装内容，必须使用具有管理权限的帐户登录。  
  
 如果 Visual Studio IDE 设置为英语以外的语言，则可以安装英语内容和/或本地化内容。 但是，如果只安装英语版本，且清除了“查看器选项”对话框中的“所有导航选项卡和 F1 请求中均包含英语内容”复选框，则将不会显示内容。  
  
#### <a name="to-download-and-install-content"></a>要下载和安装内容  
  
1. 选择“管理内容”选项卡。  
  
2. 在内容列表中，选择想下载并安装的丛书旁边的“添加”链接。  
  
     丛书将添加到“挂起的更改”列表中，并且所指定的丛书的预估大小将显示在列表下方。 由于部分丛书可以共享主题，因此多本丛书的总下载大小可能小于制定的每本丛书大小的总和。  
  
3. 选择“更新”按钮。  
  
     所指定的丛书将随计算机上已有的丛书的任何更新一同安装。 安装时间各不相同，但可以在状态栏中查看进度。  
  
## <a name="removing-local-content"></a>删除本地内容  
 可以删除计算机中不需要的内容来节省磁盘空间。  
  
> [!IMPORTANT]
> 必须具有管理权限才能删除内容。  
  
 如果将 Visual Studio IDE 设置为英语以外的语言、删除本地化内容并且清除了“查看器选项”对话框中的“所有导航选项卡和 F1 请求中包括英语内容”复选框，则将不会显示内容。  
  
#### <a name="to-remove-content"></a>要删除内容  
  
1. 选择“管理内容”选项卡。  
  
2. 在内容列表中，选择要删除的丛书旁边的“删除”链接。  
  
     丛书将被添加到“挂起的更改”列表中。  
  
3. 选择“更新”按钮。  
  
     将从计算机中删除所指定的丛书。  
  
## <a name="updating-local-content"></a>更新本地内容  
 状态栏指示已安装内容的更新何时可用。  
  
> [!IMPORTANT]
> 如果希望帮助查看器自动检查联机更新，必须打开“查看器选项”对话框，然后选择“联机检查内容更新”复选框。  
  
#### <a name="to-update-local-content"></a>要更新本地内容  
  
- 在状态栏的右下角，选择“单击此处立即下载”链接。  
  
  安装时间可能不同，但可以在状态栏中查看进度。  
  
## <a name="moving-local-content"></a>删除本地内容  
 可以通过将本地计算机上安装的内容移到网络共享或本地计算机上的其他分区来节省磁盘空间。  
  
> [!IMPORTANT]
> 若要移动内容，必须使用具有管理权限的帐户登录。  
  
#### <a name="to-move-local-content"></a>要移动本地内容  
  
1. 在“管理内容”选项卡上，选择“本地存储路径”下的“移动”按钮。  
  
     将打开“移动内容”对话框。  
  
2. 在“到”文本框中，输入内容的其他位置，然后选择“确定”按钮。  
  
3. 移动内容后，选择“关闭”按钮。  
  
## <a name="see-also"></a>请参阅  
 [Microsoft Help Viewer](../ide/microsoft-help-viewer.md)
