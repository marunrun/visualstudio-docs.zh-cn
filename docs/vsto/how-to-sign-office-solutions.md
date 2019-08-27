---
title: 如何：对 Office 解决方案进行签名
ms.date: 02/02/2017
ms.topic: conceptual
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
ms.openlocfilehash: 1fff7555c17f4fdac43de2690f8e133cc32881db
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62971116"
---
# <a name="how-to-sign-office-solutions"></a>如何：对 Office 解决方案进行签名
  如果登录解决方案，可以授予对使用证书作为证据的解决方案的信任。 可将同一个证书用于多个解决方案，并且所有解决方案都将没有进行任何额外的安全策略更新受信任。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

 如果你手动编辑应用程序和部署清单通过使用清单生成和编辑工具 (*mage.exe*并*mageui.exe*)，然后才能使用它们，必须重新对清单签名。 有关详细信息，请参阅[如何：对应用程序清单和部署清单重新签名](../deployment/how-to-re-sign-application-and-deployment-manifests.md)。

## <a name="sign-by-using-a-certificate"></a>使用证书进行签名
 证书是包含一个唯一键和解决方案发布商的标识的文件。 可以从证书颁发机构购买证书或创建你自己的证书，并具有对其进行签名的证书颁发机构。

 Visual Studio 对临时证书，以便能够启用调试 Office 解决方案进行签名。 作为证据，不应在已部署的解决方案中使用的临时证书。

### <a name="to-sign-an-office-solution-by-using-a-certificate"></a>若要使用证书签名的 Office 解决方案

1. 上**项目**菜单上，单击_SolutionName_**属性**。

2. 单击“签名”选项卡。

3. 选择**ClickOnce 清单签名**。

4. 通过单击来查找**从存储中选择**或**从文件中选择**并导航到该证书。

5. 若要验证是否正在使用正确的证书，请单击**更多详细信息**来查看证书信息。

## <a name="see-also"></a>请参阅

- [保护 Office 解决方案](../vsto/securing-office-solutions.md)
- [向 Office 解决方案授予信任](../vsto/granting-trust-to-office-solutions.md)
- [“项目设计器”->“签名”页](../ide/reference/signing-page-project-designer.md)
