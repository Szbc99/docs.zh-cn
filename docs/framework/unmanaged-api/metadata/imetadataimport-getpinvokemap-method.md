---
title: "IMetaDataImport::GetPinvokeMap 方法"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: IMetaDataImport.GetPinvokeMap
api_location: mscoree.dll
api_type: COM
f1_keywords: IMetaDataImport::GetPinvokeMap
helpviewer_keywords:
- IMetaDataImport::GetPinvokeMap method [.NET Framework metadata]
- GetPinvokeMap method [.NET Framework metadata]
ms.assetid: b8685c1e-b80c-4198-8eb3-748d6f48a99e
topic_type: apiref
caps.latest.revision: "11"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.openlocfilehash: adb6a9a5f53dcfd8ada5b3aa9d75daac18d50283
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="imetadataimportgetpinvokemap-method"></a><span data-ttu-id="33ac2-102">IMetaDataImport::GetPinvokeMap 方法</span><span class="sxs-lookup"><span data-stu-id="33ac2-102">IMetaDataImport::GetPinvokeMap Method</span></span>
<span data-ttu-id="33ac2-103">获取用于表示 PInvoke 调用的目标程序集的 ModuleRef 标记。</span><span class="sxs-lookup"><span data-stu-id="33ac2-103">Gets a ModuleRef token to represent the target assembly of a PInvoke call.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="33ac2-104">语法</span><span class="sxs-lookup"><span data-stu-id="33ac2-104">Syntax</span></span>  
  
```  
HRESULT GetPinvokeMap (  
   [in]  mdToken       tk,  
   [out] DWORD         *pdwMappingFlags,  
   [out] LPWSTR        szImportName,  
   [in]  ULONG         cchImportName,  
   [out] ULONG         *pchImportName,  
   [out] mdModuleRef   *pmrImportDLL  
);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="33ac2-105">参数</span><span class="sxs-lookup"><span data-stu-id="33ac2-105">Parameters</span></span>  
 `tk`  
 <span data-ttu-id="33ac2-106">[in]要获取的 PInvoke 映射元数据的 FieldDef 或 MethodDef 标记。</span><span class="sxs-lookup"><span data-stu-id="33ac2-106">[in] A FieldDef or MethodDef token to get the PInvoke mapping metadata for.</span></span>  
  
 `pdwMappingFlags`  
 <span data-ttu-id="33ac2-107">[out]指向用于映射的标志的指针。</span><span class="sxs-lookup"><span data-stu-id="33ac2-107">[out] A pointer to flags used for mapping.</span></span> <span data-ttu-id="33ac2-108">此值是从一个位掩码[CorPinvokeMap](../../../../docs/framework/unmanaged-api/metadata/corpinvokemap-enumeration.md)枚举。</span><span class="sxs-lookup"><span data-stu-id="33ac2-108">This value is a bitmask from the [CorPinvokeMap](../../../../docs/framework/unmanaged-api/metadata/corpinvokemap-enumeration.md) enumeration.</span></span>  
  
 `szImportName`  
 <span data-ttu-id="33ac2-109">[out]非托管目标 DLL 的名称。</span><span class="sxs-lookup"><span data-stu-id="33ac2-109">[out] The name of the unmanaged target DLL.</span></span>  
  
 `cchImportName`  
 <span data-ttu-id="33ac2-110">[in]在宽字符为单位的大小`szImportName`。</span><span class="sxs-lookup"><span data-stu-id="33ac2-110">[in] The size in wide characters of `szImportName`.</span></span>  
  
 `pchImportName`  
 <span data-ttu-id="33ac2-111">[out]在中返回的宽字符数`szImportName`。</span><span class="sxs-lookup"><span data-stu-id="33ac2-111">[out] The number of wide characters returned in `szImportName`.</span></span>  
  
 `pmrImportDLL`  
 <span data-ttu-id="33ac2-112">[out]指向表示非托管的目标对象库的 ModuleRef 标记的指针。</span><span class="sxs-lookup"><span data-stu-id="33ac2-112">[out] A pointer to a ModuleRef token that represents the unmanaged target object library.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="33ac2-113">要求</span><span class="sxs-lookup"><span data-stu-id="33ac2-113">Requirements</span></span>  
 <span data-ttu-id="33ac2-114">**平台：**请参阅[系统要求](../../../../docs/framework/get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="33ac2-114">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="33ac2-115">**标头：** Cor.h</span><span class="sxs-lookup"><span data-stu-id="33ac2-115">**Header:** Cor.h</span></span>  
  
 <span data-ttu-id="33ac2-116">**库：**作为 MsCorEE.dll 中的资源</span><span class="sxs-lookup"><span data-stu-id="33ac2-116">**Library:** Included as a resource in MsCorEE.dll</span></span>  
  
 <span data-ttu-id="33ac2-117">**.NET framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="33ac2-117">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="33ac2-118">另请参阅</span><span class="sxs-lookup"><span data-stu-id="33ac2-118">See Also</span></span>  
 [<span data-ttu-id="33ac2-119">IMetaDataImport 接口</span><span class="sxs-lookup"><span data-stu-id="33ac2-119">IMetaDataImport Interface</span></span>](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-interface.md)  
 [<span data-ttu-id="33ac2-120">IMetaDataImport2 接口</span><span class="sxs-lookup"><span data-stu-id="33ac2-120">IMetaDataImport2 Interface</span></span>](../../../../docs/framework/unmanaged-api/metadata/imetadataimport2-interface.md)