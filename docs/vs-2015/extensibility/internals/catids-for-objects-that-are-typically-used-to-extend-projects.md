---
title: 对象通常用于扩展项目的 Catid |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, CATIDs
- GUIDs, VSPackages
- CATIDs for VSPackages
ms.assetid: 0c7fdb66-ed96-4b36-89f6-021bca573572
caps.latest.revision: 17
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 1cf5bd504bb5f7090dc07bea32e73333c0f182d0
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68162088"
---
# <a name="catids-for-objects-that-are-typically-used-to-extend-projects"></a>通常用于扩展项目的对象的 CATID
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

下表列出了用于扩展的 Catid`Project`并`ProjectItem`自动化对象[!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]， [!INCLUDE[csprcs](../../includes/csprcs-md.md)]，和[!INCLUDE[vcprvc](../../includes/vcprvc-md.md)]项目。 这些 Catid VSLangProj.olb 中定义。  
  
## <a name="listing-of-catids"></a>列出的 Catid  
  
|名称|GUID|  
|----------|----------|  
|<xref:VSLangProj.PrjCATID.prjCATIDProject>|{610D4614-D0D5-11D2-8599-006097C68E81}|  
|<xref:VSLangProj.PrjCATID.prjCATIDProjectItem>|{610D4615-D0D5-11D2-8599-006097C68E81}|  
  
## <a name="visual-basic-catids"></a>Visual Basic Catid  
 下表列出了用于扩展的 Catid[!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]浏览对象。 所有 VSLangProj.olb 中定义它们。  
  
|名称|GUID|  
|----------|----------|  
|<xref:VSLangProj.PrjBrowseObjectCATID.prjCATIDVBProjectBrowseObject>|{E0FDC879-C32A-4751-A3D3-0B3824BD575F}|  
|<xref:VSLangProj.PrjBrowseObjectCATID.prjCATIDVBProjectConfigBrowseObject>|{67F8DD11-14EB-489b-87F0-F01C52AF3870}|  
|<xref:VSLangProj.PrjBrowseObjectCATID.prjCATIDVBFileBrowseObject>|{EA5BD05D-3C72-40A5-95A0-28A2773311CA}|  
|<xref:VSLangProj.PrjBrowseObjectCATID.prjCATIDVBFolderBrowseObject>|{932DC619-2EAA-4192-B7E6-3D15AD31DF49}|  
|<xref:VSLangProj.PrjBrowseObjectCATID.prjCATIDVBReferenceBrowseObject>|{2289B812-8191-4e81-B7B3-174045AB0CB5}|  
  
## <a name="visual-c-catids"></a>Visual C# Catid  
 以下 Catid 可以用于扩展[!INCLUDE[csprcs](../../includes/csprcs-md.md)]浏览对象。 所有 VSLangProj.olb 中定义它们。  
  
|名称|GUID|  
|----------|----------|  
|<xref:VSLangProj.PrjBrowseObjectCATID.prjCATIDCSharpProjectBrowseObject>|{4EF9F003-DE95-4d60-96B0-212979F2A857}|  
|<xref:VSLangProj.PrjBrowseObjectCATID.prjCATIDCSharpProjectConfigBrowseObject>|{A12CE10A-227F-4963-ADB6-3A43388513CA}|  
|<xref:VSLangProj.PrjBrowseObjectCATID.prjCATIDCSharpFileBrowseObject>|{8D58E6AF-ED4E-48B0-8C7B-C74EF0735451}|  
|<xref:VSLangProj.PrjBrowseObjectCATID.prjCATIDCSharpFolderBrowseObject>|{914FE278-054A-45DB-BF9E-5F22484CC84C}|  
|<xref:VSLangProj.PrjBrowseObjectCATID.prjCATIDCSharpReferenceBrowseObject>|{2F0FA3B8-C855-4a4e-95A5-CB45C67D6C27}|  
  
## <a name="c-catids"></a>C++Catid  
 以下[!INCLUDE[vcprvc](../../includes/vcprvc-md.md)]项目的系统中的类型库中未公开 Catid [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] .NET 2003年和一定要包括在代码中，只要您想要扩展这些项目对象。 在更高版本的中的类型库中将包含这些 Catid [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]。  
  
|name|GUID|  
|----------|----------|  
|`CVCProjectNode`|{EE8299CB-19B6-4f20-ABEA-E1FD9A33B683}|  
|`CVCFolderNode`|{EE8299CA-19B6-4f20-ABEA-E1FD9A33B683}|  
|`CVCFileNode`|{EE8299C9-19B6-4f20-ABEA-E1FD9A33B683}|  
  
 下面的代码示例演示如何编写程序代码中的这些 Catid。  
  
```  
const LPOLESTR CVCProjectNode::s_wszCATID = L"{EE8299CB-19B6-4f20-ABEA-E1FD9A33B683}";  
const LPOLESTR CVCFolderNode::s_wszCATID = L"{EE8299CA-19B6-4f20-ABEA-E1FD9A33B683}";  
const LPOLESTR CVCFileNode::s_wszCATID = L"{EE8299C9-19B6-4f20-ABEA-E1FD9A33B683}";  
```  
  
 以下[!INCLUDE[vcprvc](../../includes/vcprvc-md.md)]项目的系统中的类型库中还未公开 Catid [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] .NET 2003年和一定要包括在代码中，只要您想要扩展这些项目对象。 是仅适用于这些 Catid [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] .NET 2003年和将不能在更高版本的[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]。  
  
|name|GUID|  
|----------|----------|  
|`CVCAssemblyReferenceNode` **:**|{FE8299C9-19B6-4f20-ABEA-E1FD9A33B683}|  
|`CVCProjectReferenceNode`|{593DCFCE-20A7-48e4-ACA1-49ADE9049887}|  
|`CVCActiveXReferenceNode`|{9E8182D3-C60A-44f4-A74B-14C90EF9CACE}|  
|`CVCReferences`|{FE8299CA-19B6-4f20-ABEA-E1FD9A33B683}|  
  
 下面的代码示例演示如何编写程序代码中的这些 Catid:  
  
```  
const LPOLESTR CVCAssemblyReferenceNode::s_wszCATID = L"{FE8299C9-19B6-4f20-ABEA-E1FD9A33B683}";  
const LPOLESTR CVCProjectReferenceNode::s_wszCATID = L"{593DCFCE-20A7-48e4-ACA1-49ADE9049887}";  
const LPOLESTR CVCActiveXReferenceNode::s_wszCATID = L"{9E8182D3-C60A-44f4-A74B-14C90EF9CACE}";  
const LPOLESTR CVCReferences::s_wszCATID = L"{FE8299CA-19B6-4f20-ABEA-E1FD9A33B683}";  
```  
  
 有关 Guid[!INCLUDE[csprcs](../../includes/csprcs-md.md)]和[!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]项目类型显示在下表中。  
  
|项目类型|GUID|  
|------------------|----------|  
|[!INCLUDE[csprcs](../../includes/csprcs-md.md)]|{FAE04EC0-301F-11D3-BF4B-00C04F79EFBC}|  
|[!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]|{F184B08F-C81C-45F6-A57F-5ABD9991F28F}|  
  
## <a name="see-also"></a>请参阅  
 [添加项目和项目项模板](../../extensibility/internals/adding-project-and-project-item-templates.md)   
 [注册项目和项模板](../../extensibility/internals/registering-project-and-item-templates.md)
