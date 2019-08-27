---
title: 如何：将数据文件包括在 ClickOnce 应用程序 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, data
- deploying applications [ClickOnce], data files
- data access, ClickOnce applications
ms.assetid: 89ee46ef-bc8c-4ab0-a2ac-1220f9da06fc
caps.latest.revision: 17
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 9120a5b3cb60f6c607ed97ab2df24bb157c72371
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68153767"
---
# <a name="how-to-include-a-data-file-in-a-clickonce-application"></a>如何：将数据文件包括到 ClickOnce 应用程序中
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

每个[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]安装的应用程序分配一个应用程序可以在其中管理其自己的数据的目标计算机的本地磁盘上的数据目录。 数据文件可以包含任何类型的文件： 文本文件、 XML 文件或甚至 Microsoft Access 数据库 (.mdb) 文件。 以下过程显示如何将添加到任何类型的数据文件在[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]应用程序。  
  
### <a name="to-include-a-data-file-by-using-mageexe"></a>若要将数据文件包括通过使用 Mage.exe  
  
1. 将数据文件添加到你的应用程序目录与应用程序的文件的其余部分。  
  
    通常情况下，在应用程序目录将标记为部署的当前版本的目录 — 例如，v1.0.0.0。  
  
2. 到列表数据文件中更新应用程序清单。  
  
    **mage -u v1.0.0.0\Application.manifest -FromDirectory v1.0.0.0**  
  
    执行此任务将重新创建应用程序清单中的文件列表，并且还会自动生成的哈希签名。  
  
3. 在您首选的文本或 XML 编辑器中打开应用程序清单，并找到`file`最近添加的文件的元素。  
  
    如果添加一个名为 XML 文件`Data.xml`，该文件将类似于下面的代码示例。  
  
   `<file name="Data.xml" hash="23454C18A2DC1D23E5B391FEE299B1F235067C59" hashalg="SHA1" asmv2:size="39500" />`  
  
4. 将属性添加`type`到此元素，并将其提供的值为`data`。  
  
   `<file name="Data.xml" writeableType="applicationData" hash="23454C18A2DC1D23E5B391FEE299B1F235067C59" hashalg="SHA1" asmv2:size="39500" />`  
  
5. 使用密钥对或证书，请重新签名应用程序清单，然后重新签名部署清单。  
  
    因为它的应用程序清单的哈希已更改，必须重新签名部署清单。  
  
    **mage-s 应用程序清单-cf cert_file-pwd 密码**  
  
    **mage-u 部署清单 appm 应用程序清单**  
  
    **mage-s 部署清单-cf certfile-pwd 密码**  
  
6. 
  
### <a name="to-include-a-data-file-by-using-mageuiexe"></a>若要通过使用 MageUI.exe 中包含的数据文件  
  
1. 将数据文件添加到你的应用程序目录与应用程序的文件的其余部分。  
  
2. 通常情况下，在应用程序目录将标记为部署的当前版本的目录 — 例如，v1.0.0.0。  
  
3. 上**文件**菜单上，单击**打开**以打开应用程序清单。  
  
4. 选择**文件**选项卡。  
  
5. 在选项卡顶部的文本框中，输入包含应用程序的文件的目录，然后单击**Populate**。  
  
     你的数据文件会在网格中显示。  
  
6. 设置**文件类型**的数据文件的值**数据**。  
  
7. 保存应用程序清单，然后重新登录该文件。  
  
     MageUI.exe 将提示您重新对文件进行签名。  
  
8. 部署清单重新签名  
  
     因为它的应用程序清单的哈希已更改，必须重新签名部署清单。  
  
## <a name="see-also"></a>请参阅  
 [在 ClickOnce 应用程序中访问本地数据和远程数据](../deployment/accessing-local-and-remote-data-in-clickonce-applications.md)
