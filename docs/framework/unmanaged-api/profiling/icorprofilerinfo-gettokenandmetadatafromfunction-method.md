---
title: "ICorProfilerInfo::GetTokenAndMetadataFromFunction 方法"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorProfilerInfo.GetTokenAndMetadataFromFunction
api_location: mscorwks.dll
api_type: COM
f1_keywords: ICorProfilerInfo::GetTokenAndMetadataFromFunction
helpviewer_keywords:
- ICorProfilerInfo::GetTokenAndMetadataFromFunction method [.NET Framework profiling]
- GetTokenAndMetadataFromFunction method [.NET Framework profiling]
ms.assetid: e525aa16-c923-4b16-833b-36f1f0dd70fc
topic_type: apiref
caps.latest.revision: "14"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.openlocfilehash: 585b28161814045777cf2294f78bafc3229bfae9
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2017
---
# <a name="icorprofilerinfogettokenandmetadatafromfunction-method"></a><span data-ttu-id="7161b-102">ICorProfilerInfo::GetTokenAndMetadataFromFunction 方法</span><span class="sxs-lookup"><span data-stu-id="7161b-102">ICorProfilerInfo::GetTokenAndMetadataFromFunction Method</span></span>
<span data-ttu-id="7161b-103">获取元数据标记和可用于指定的函数对标记的元数据接口实例。</span><span class="sxs-lookup"><span data-stu-id="7161b-103">Gets the metadata token and a metadata interface instance that can be used against the token for the specified function.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="7161b-104">语法</span><span class="sxs-lookup"><span data-stu-id="7161b-104">Syntax</span></span>  
  
```  
HRESULT GetTokenAndMetaDataFromFunction(  
    [in]  FunctionID functionId,  
    [in]  REFIID     riid,  
    [out] IUnknown   **ppImport,  
    [out] mdToken    *pToken);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="7161b-105">参数</span><span class="sxs-lookup"><span data-stu-id="7161b-105">Parameters</span></span>  
 `functionId`  
 <span data-ttu-id="7161b-106">[in]要为其获取元数据标记和元数据接口的函数 ID。</span><span class="sxs-lookup"><span data-stu-id="7161b-106">[in] The ID of the function for which to get the metadata token and metadata interface.</span></span>  
  
 `riid`  
 <span data-ttu-id="7161b-107">[in]要获取的实例元数据接口的引用 ID。</span><span class="sxs-lookup"><span data-stu-id="7161b-107">[in] The reference ID of the metadata interface to get the instance of.</span></span>  
  
 `ppImport`  
 <span data-ttu-id="7161b-108">[out]指向可用于指定的函数对标记的元数据接口实例的地址的指针。</span><span class="sxs-lookup"><span data-stu-id="7161b-108">[out] A pointer to the address of the metadata interface instance that can be used against the token for the specified function.</span></span>  
  
 `pToken`  
 <span data-ttu-id="7161b-109">[out]指向指定的函数的元数据标记的指针。</span><span class="sxs-lookup"><span data-stu-id="7161b-109">[out] A pointer to the metadata token for the specified function.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="7161b-110">要求</span><span class="sxs-lookup"><span data-stu-id="7161b-110">Requirements</span></span>  
 <span data-ttu-id="7161b-111">**平台：**请参阅[系统要求](../../../../docs/framework/get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="7161b-111">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="7161b-112">**头文件：** CorProf.idl、CorProf.h</span><span class="sxs-lookup"><span data-stu-id="7161b-112">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="7161b-113">**库：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="7161b-113">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="7161b-114">**.NET framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="7161b-114">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="7161b-115">另请参阅</span><span class="sxs-lookup"><span data-stu-id="7161b-115">See Also</span></span>  
 [<span data-ttu-id="7161b-116">ICorProfilerInfo 接口</span><span class="sxs-lookup"><span data-stu-id="7161b-116">ICorProfilerInfo Interface</span></span>](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-interface.md)