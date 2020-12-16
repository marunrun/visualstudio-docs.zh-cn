---
title: 如何：对 Office 解决方案进行签名
description: 了解如何通过使用证书作为证据向 Microsoft Office 解决方案授予信任。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- certificates [Office development in Visual Studio], Office solutions
- security [Office development in Visual Studio], signing Office solutions
- signing manifests [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 7451630570e6d557dc5d2b635d149ebc07cfb388
ms.sourcegitcommit: 4bd2b770e60965fc0843fc25318a7e1b46137875
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/15/2020
ms.locfileid: "97528117"
---
# <a name="how-to-sign-office-solutions"></a>如何：对 Office 解决方案进行签名
  如果对解决方案进行签名，则可以使用证书作为证据向解决方案授予信任。 你可以为多个解决方案使用相同的证书，并且所有解决方案都将受信任，且无其他安全策略更新。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

 如果通过使用清单生成和编辑工具 (*mage.exe* 和 *mageui.exe*) 手动编辑应用程序和部署清单，则必须先对清单重新签名，然后才能使用它们。 有关详细信息，请参阅[如何：对应用程序和部署清单重新签名](../deployment/how-to-re-sign-application-and-deployment-manifests.md)。

## <a name="sign-by-using-a-certificate"></a>使用证书进行签名
 证书是一个文件，其中包含解决方案发行者的唯一密钥和标识。 你可以从证书颁发机构购买证书，或创建你自己的证书，并让证书颁发机构对其进行签名。

 Visual Studio 使用临时证书对 Office 解决方案进行签名，以启用调试。 不应在已部署的解决方案中使用临时证书作为证据。

### <a name="to-sign-an-office-solution-by-using-a-certificate"></a>使用证书对 Office 解决方案进行签名

1. 在 " **项目** " 菜单上，单击 " _解决方案名称_**属性**"。

2. 单击“签名”  选项卡。

3. 选择 **"为 ClickOnce 清单签名"**。

4. 通过单击 " **从存储中选择** "，或 **选择 "从文件** " 并导航到证书定位证书。

5. 若要验证是否正在使用正确的证书，请单击 " **更多详细信息** " 以查看证书信息。

## <a name="see-also"></a>另请参阅

- [保护 Office 解决方案](../vsto/securing-office-solutions.md)
- [向 Office 解决方案授予信任](../vsto/granting-trust-to-office-solutions.md)
- [“项目设计器”-&gt;“签名”页](../ide/reference/signing-page-project-designer.md)
