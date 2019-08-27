---
title: Visual Studio 模板架构参考 |Microsoft Docs
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- VSTEMPLATE files
- Visual Studio templates, schema
- .vstemplate files
ms.assetid: 6f74a2d5-3811-43d6-8b10-eb5823ad8995
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: af0a11e2e75b8a9be44dacb58eeac2505613e86d
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66323041"
---
# <a name="visual-studio-template-schema-reference"></a>Visual Studio 模板架构参考
本部分包含有关中的 XML 元素的信息 *.vstemplate*文件，这些文件用于存储项目模板、 项模板和初学者工具包的元数据文件。

 可以使用*vstemplate.xsd*若要验证自定义 *.vstemplate*文件。 此文件将出现在 *...\\ \<Visual Studio 安装文件夹 > \Xml\Schemas\1033\vstemplate.xsd*。

|元素|子元素|特性|
|-------------|--------------------|----------------|
|[AppliesTo](../extensibility/appliesto-element-visual-studio-templates.md)|None|None|
|[程序集 （模板）](../extensibility/assembly-element-visual-studio-templates.md)|--|--|
|[程序集 （向导扩展）](../extensibility/assembly-element-visual-studio-template-wizard-extension.md)|--|--|
|[BuildProjectOnload](../extensibility/buildprojectonload-element-visual-studio-templates.md)|--|--|
|[CreateInPlace](../extensibility/createinplace-visual-studio-templates.md)|--|--|
|[CreateNewFolder](../extensibility/createnewfolder-element-visual-studio-templates.md)|--|--|
|[CustomDataSignature](../extensibility/customdatasignature-element-visual-studio-templates.md)|--|--|
|[CustomParameter](../extensibility/customparameter-element-visual-studio-templates.md)|--|名称<br /><br /> 值|
|[CustomParameters](../extensibility/customparameters-element-visual-studio-templates.md)|CustomParameter|--|
|[DefaultName](../extensibility/defaultname-element-visual-studio-templates.md)|--|--|
|[说明](../extensibility/description-element-visual-studio-templates.md)|--|package<br /><br /> Id|
|[EnableEditOfLocationField](../extensibility/enableeditoflocationfield-element-visual-studio-templates.md)|--|--|
|[EnableLocationBrowseButton](../extensibility/enablelocationbrowsebutton-element-visual-studio-templates.md)|--|--|
|[文件夹](../extensibility/folder-element-visual-studio-project-templates.md)|ProjectItem<br /><br /> 文件夹|名称|
||[已弃用]|--|
|[FullClassName](../extensibility/fullclassname-element-visual-studio-template-wizard-extension.md)|--|--|
|[Hidden](../extensibility/hidden-element-visual-studio-templates.md)|--|--|
|[图标](../extensibility/icon-element-visual-studio-templates.md)|--|package<br /><br /> Id|
|[LocationField](../extensibility/locationfield-element-visual-studio-project-templates.md)|--|--|
|[LocationFieldMRUPrefix](../extensibility/locationfieldmruprefix-element-visual-studio-templates.md)|--|--|
|[MaxFrameworkVersion](../extensibility/maxframeworkversion-element-visual-studio-templates.md)|--|--|
|[名称](../extensibility/name-element-visual-studio-templates.md)|--|package<br /><br /> Id|
|[NumberOfParentCategoriesToRollUp](../extensibility/numberofparentcategoriestorollup-visual-studio-templates.md)|--|--|
|[PreviewImage](../extensibility/previewimage-element-visual-studio-templates.md)|--|--|
|[Project](../extensibility/project-element-visual-studio-templates.md)|文件夹<br /><br /> ProjectItem|文件<br /><br /> TargetFileName<br /><br /> ReplaceParameters|
|[ProjectCollection](../extensibility/projectcollection-element-visual-studio-templates.md)|ProjectTemplateLink<br /><br /> SolutionFolder|--|
|[ProjectItem （项模板）](../extensibility/projectitem-element-visual-studio-item-templates.md)|--|子类型<br /><br /> CustomTool<br /><br /> ItemType<br /><br /> ReplaceParameters<br /><br /> TargetFileName|
|[ProjectItem （项目模板）](../extensibility/projectitem-element-visual-studio-project-templates.md)|--|TargetFileName<br /><br /> ReplaceParameters<br /><br /> OpenInEditor<br /><br /> OpenOrder<br /><br /> OpenInWebBrowser<br /><br /> OpenInHelpBrowser|
|[ProjectSubType](../extensibility/projectsubtype-element-visual-studio-templates.md)|--|--|
|[ProjectTemplateLink](../extensibility/projecttemplatelink-element-visual-studio-templates.md)|--|ProjectName|
|[ProjectType](../extensibility/projecttype-element-visual-studio-templates.md)|--|--|
|[PromptForSaveOnCreation](../extensibility/promptforsaveoncreation-element-visual-studio-templates.md)|--|--|
|[ProvideDefaultName](../extensibility/providedefaultname-element-visual-studio-templates.md)|--|--|
|[引用](../extensibility/reference-element-visual-studio-templates.md)|Assembly|--|
|[参考资料](../extensibility/references-element-visual-studio-templates.md)|参考|--|
|[RequiredFrameworkVersion](../extensibility/requiredframeworkversion-element-visual-studio-templates.md)|--|--|
|[RequiredPlatformVersion](../extensibility/requiredplatformversion-element-visual-studio-templates.md)|--|Version|
|[SDKReference](../extensibility/sdkreference-element-visual-studio-templates.md)|--|package|
|[ShowByDefault](../extensibility/showbydefault-visual-studio-templates.md)|--|--|
|[SolutionFolder](../extensibility/solutionfolder-element-visual-studio-templates.md)|ProjectTemplateLink<br /><br /> SolutionFolder|名称|
|[SortOrder](../extensibility/sortorder-element-visual-studio-templates.md)|--|--|
|[SupportsCodeSeparation](../extensibility/supportscodeseparation-element-visual-studio-templates.md)|--|--|
|[SupportsLanguageDropDown](../extensibility/supportslanguagedropdown-element-visual-studio-templates.md)|--|--|
|[SupportsMasterPage](../extensibility/supportsmasterpage-element-visual-studio-templates.md)|--|--|
|[TargetPlatformName](../extensibility/targetplatformname-element-visual-studio-templates.md)|RequiredPlatformVersion|--|
|[TemplateContent](../extensibility/templatecontent-element-visual-studio-templates.md)|ProjectCollection<br /><br /> 项目<br /><br /> 参考资料<br /><br /> ProjectItem<br /><br /> CustomParameters|[BuildOnLoad](../extensibility/buildonload-visual-studio-templates.md)|
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|名称<br /><br /> 描述<br /><br /> 图标<br /><br /> PreviewImage<br /><br /> ProjectType<br /><br /> ProjectSubType<br /><br /> TemplateID<br /><br /> TemplateGroupID<br /><br /> SortOrder<br /><br /> CreateNewFolder<br /><br /> DefaultName<br /><br /> ProvideDefaultName<br /><br /> PromptForSaveOnCreation<br /><br /> EnableLocationBrowseButton<br /><br /> EnableEditOfLocationField<br /><br /> Hidden<br /><br /> DisplayInParentCategories<br /><br /> LocationFieldMRUPrefix<br /><br /> NumberOfParentCategoriesToRollUp<br /><br /> CreateInPlace<br /><br /> BuildOnLoad<br /><br /> BuildProjectOnload<br /><br /> ShowByDefault<br /><br /> LocationField<br /><br /> SupportsMasterPage<br /><br /> SupportsCodeSeparation<br /><br /> SupportsLanguageDropDown<br /><br /> RequiredFrameworkVersion<br /><br /> FrameworkVersion<br /><br /> MaxFrameworkVersion<br /><br /> CustomDataSignature<br /><br /> TargetPlatformName|--|
|[TemplateGroupID](../extensibility/templategroupid-element-visual-studio-templates.md)|--|--|
|[TemplateID](../extensibility/templateid-element-visual-studio-templates.md)|--|--|
|[VSTemplate](../extensibility/vstemplate-element-visual-studio-templates.md)|TemplateData<br /><br /> TemplateContent<br /><br /> WizardExtension<br /><br /> WizardData|类型<br /><br /> Version|
|[WizardData](../extensibility/wizarddata-element-visual-studio-templates.md)|--|名称|
|[WizardExtension](../extensibility/wizardextension-element-visual-studio-templates.md)|Assembly<br /><br /> FullClassName|--|

## <a name="see-also"></a>请参阅

- [创建项目和项模板](../ide/creating-project-and-item-templates.md)