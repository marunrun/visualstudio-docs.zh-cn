---
title: 将数据保存在项目文件 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- data [Visual Studio], saving in project files
- project files
- project files, saving data
ms.assetid: a3d4b15b-a91e-41ba-b235-e62632d11bc5
caps.latest.revision: 29
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: fc671963854e4fa0c2af763de5000fac82a839b8
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63432516"
---
# <a name="saving-data-in-project-files"></a>将数据保存在项目文件中
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

项目子类型可以保存和检索子类型特定的项目文件中的数据。 托管包框架 (MPF) 提供了两个接口来完成此任务：  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage>接口允许对访问属性值从**MSBuild**项目文件的部分。 提供的方法<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage>用户需要加载或保存生成相关的数据时可调用的任何用户。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment>用于保存非生成自由格式的 XML 中的相关的数据。 提供的方法<xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment>由调用[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]每当[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]永久保存在项目文件中的非生成相关的数据。  
  
  有关如何保留生成和非生成相关的数据的详细信息，请参阅[MSBuild 项目文件中保存数据](../extensibility/internals/persisting-data-in-the-msbuild-project-file.md)。  
  
## <a name="saving-and-retrieving-build-related-data"></a>保存和检索生成的相关数据  
  
#### <a name="to-save-a-build-related-data-in-the-project-file"></a>若要保存对生成相关的项目文件中的数据  
  
- 调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage.SetPropertyValue%2A>方法以保存项目文件的完整路径。  
  
    ```  
    private SpecializedProject project;  
    IVsBuildPropertyStorage projectStorage = (IVsBuildPropertyStorage)project;  
    string newFullPath = GetNewFullPath();  
    // Set a full path of the project file.  
    ErrorHandler.ThrowOnFailure(projectStorage.SetPropertyValue(  
        "MSBuildProjectDirectory",  
        String.Empty,  
        (uint)_PersistStorageType.PST_PROJECT_FILE, newFullPath));  
    ```  
  
#### <a name="to-retrieve-build-related-data-from-the-project-file"></a>从项目文件检索生成相关的数据  
  
- 调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage.GetPropertyValue%2A>方法来检索其中的项目文件的完整路径。  
  
    ```  
    private SpecializedProject project;  
    IVsBuildPropertyStorage projectStorage = (IVsBuildPropertyStorage)project;  
    string fullPath;  
    // Get a full path of the project file.  
    ErrorHandler.ThrowOnFailure(projectStorage.GetPropertyValue(  
        "MSBuildProjectDirectory",  
        String.Empty,  
        (uint)_PersistStorageType.PST_PROJECT_FILE, out fullPath));  
    ```  
  
## <a name="saving-and-retrieving-non-build-related-data"></a>保存和检索与非生成相关的数据  
  
#### <a name="to-save-non-build-related-data-in-the-project-file"></a>若要保存非生成相关的项目文件中的数据  
  
1. 实现<xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment.IsFragmentDirty%2A>方法，以确定是否已更改的 XML 片段，表明自上次保存到其当前文件。  
  
    ```  
    public int IsFragmentDirty(uint storage, out int pfDirty)  
    {  
        pfDirty = 0;  
        switch (storage)  
        {  
            case (uint)_PersistStorageType.PST_PROJECT_FILE:  
            {  
                if (isDirty)  
                    pfDirty |= 1;  
                break;  
            }  
            case (uint)_PersistStorageType.PST_USER_FILE:  
            {  
                // We do not store anything in the user file.  
                break;  
            }  
        }  
  
        // Forward the call to inner flavor(s)   
        if (pfDirty == 0 && innerCfg != null && this.innerCfg is IPersistXMLFragment)  
            return ((IPersistXMLFragment)this.innerCfg).IsFragmentDirty(storage, out pfDirty);  
  
        return VSConstants.S_OK;  
  
    }  
    ```  
  
2. 实现<xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment.Save%2A>方法以将 XML 数据保存在项目文件中。  
  
    ```  
    public int Save(ref Guid guidFlavor, uint storage, out string pbstrXMLFragment, int fClearDirty)  
    {  
        pbstrXMLFragment = null;  
  
        if (IsMyFlavorGuid(ref guidFlavor))  
        {  
            switch (storage)  
            {  
                case (uint)_PersistStorageType.PST_PROJECT_FILE:  
                {  
                    // Create XML for our data.  
                    XmlDocument doc = new XmlDocument();  
                    XmlNode root = doc.CreateElement(this.GetType().Name);  
  
                    XmlNode node = doc.CreateElement(targetsTag);  
                    node.AppendChild(doc.CreateTextNode(this.TargetsToExecute));  
                    root.AppendChild(node);  
  
                    node = doc.CreateElement(updateTargetsTag);  
                    node.AppendChild(doc.CreateTextNode(this.UpdateTargetList.ToString()));  
                    root.AppendChild(node);  
  
                    doc.AppendChild(root);  
                    // Get XML fragment representing our data  
                    pbstrXMLFragment = doc.InnerXml;  
  
                    if (fClearDirty != 0)  
                        isDirty = false;  
                    break;  
                }  
                case (uint)_PersistStorageType.PST_USER_FILE:  
                {  
                    // We do not store anything in the user file.  
                    break;  
                }  
            }  
        }  
  
        // Forward the call to inner flavor(s)  
        if (this.innerCfg != null && this.innerCfg is IPersistXMLFragment)  
            return ((IPersistXMLFragment)this.innerCfg).Save(ref guidFlavor, storage, out pbstrXMLFragment, fClearDirty);  
  
        return VSConstants.S_OK;  
    }  
    ```  
  
#### <a name="to-retrieve-non-build-related-data-in-the-project-file"></a>若要检索非生成相关的项目文件中的数据  
  
1. 实现<xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment.InitNew%2A>方法以初始化项目扩展属性和其他独立于生成的数据。 如果不存在项目文件中的 XML 配置数据，调用此方法。  
  
    ```  
    public int InitNew(ref Guid guidFlavor, uint storage)  
    {  
        //Return,if it is our guid.  
        if (IsMyFlavorGuid(ref guidFlavor))  
            return VSConstants.S_OK;  
  
        //Forward the call to inner flavor(s).  
        if (this.innerCfg != null && this.innerCfg is IPersistXMLFragment)  
            return ((IPersistXMLFragment)this.innerCfg).InitNew(ref guidFlavor, storage);  
  
        return VSConstants.S_OK;  
    ```  
  
2. 实现<xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment.Load%2A>方法以从项目文件加载 XML 数据。  
  
    ```  
    public int Load(ref Guid guidFlavor, uint storage, string pszXMLFragment)  
    {  
        if (IsMyFlavorGuid(ref guidFlavor))  
        {  
            switch (storage)  
            {  
                case (uint)_PersistStorageType.PST_PROJECT_FILE:  
                {  
                    // Load our data from the XML fragment.  
                    XmlDocument doc = new XmlDocument();  
                    XmlNode node = doc.CreateElement(this.GetType().Name);  
                    node.InnerXml = pszXMLFragment;  
                    if (node == null  
                        || node.FirstChild == null  
                        || node.FirstChild.ChildNodes.Count == 0  
                        || node.FirstChild.ChildNodes[0].Name != targetsTag)  
                        break;  
                    this.TargetsToExecute = node.FirstChild.ChildNodes[0].InnerText;  
  
                    if (node.FirstChild.ChildNodes.Count <= 1  
                        || node.FirstChild.ChildNodes[1].Name != updateTargetsTag)  
                        break;  
                    this.UpdateTargetList = bool.Parse(node.FirstChild.ChildNodes[1].InnerText);  
                    break;  
                }  
                case (uint)_PersistStorageType.PST_USER_FILE:  
                {  
                    // We do not store anything in the user file.  
                    break;  
                }  
            }  
        }  
  
        // Forward the call to inner flavor(s)  
        if (this.innerCfg != null && this.innerCfg is IPersistXMLFragment)  
            return ((IPersistXMLFragment)this.innerCfg).Load(ref guidFlavor, storage, pszXMLFragment);  
  
        return VSConstants.S_OK;  
    }  
    ```  
  
> [!NOTE]
> 本主题中提供的所有代码示例都是一个更大示例的组成部分[VSSDK 示例](../misc/vssdk-samples.md)。  
  
## <a name="see-also"></a>请参阅  
 [保留 MSBuild 项目文件中的数据](../extensibility/internals/persisting-data-in-the-msbuild-project-file.md)
