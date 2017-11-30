---
title: "CustomDumpItem 结构"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: CustomDumpItem
api_location: mscoree.dll
api_type: COM
f1_keywords: CustomDumpItem
helpviewer_keywords: CustomDumpItem structure [.NET Framework hosting]
ms.assetid: fd9085ff-7beb-4c38-97f0-037cd8ba4f65
topic_type: apiref
caps.latest.revision: "7"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 547204385b20d5b7e64bda9ea0a9e790f2ba3471
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2017
---
# <a name="customdumpitem-structure"></a><span data-ttu-id="ae443-102">CustomDumpItem 结构</span><span class="sxs-lookup"><span data-stu-id="ae443-102">CustomDumpItem Structure</span></span>
<span data-ttu-id="ae443-103">描述要添加到自定义转储错误报告中的项。</span><span class="sxs-lookup"><span data-stu-id="ae443-103">Describes an item to be added to a custom dump in error reporting.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="ae443-104">语法</span><span class="sxs-lookup"><span data-stu-id="ae443-104">Syntax</span></span>  
  
```  
struct {  
    ECustomDumpItemKind itemKind;   
    union {  
        UINT_PTR pReserved;  
    }  
} CustomDumpItem;  
```  
  
## <a name="members"></a><span data-ttu-id="ae443-105">成员</span><span class="sxs-lookup"><span data-stu-id="ae443-105">Members</span></span>  
  
|<span data-ttu-id="ae443-106">成员</span><span class="sxs-lookup"><span data-stu-id="ae443-106">Member</span></span>|<span data-ttu-id="ae443-107">描述</span><span class="sxs-lookup"><span data-stu-id="ae443-107">Description</span></span>|  
|------------|-----------------|  
|`itemKind`|<span data-ttu-id="ae443-108">[ECustomDumpItemKind](../../../../docs/framework/unmanaged-api/hosting/ecustomdumpitemkind-enumeration.md)值，该值指示要添加项的种类。</span><span class="sxs-lookup"><span data-stu-id="ae443-108">An [ECustomDumpItemKind](../../../../docs/framework/unmanaged-api/hosting/ecustomdumpitemkind-enumeration.md) value that indicates the kind of item to be added.</span></span>|  
|`pReserved`|<span data-ttu-id="ae443-109">当前未使用。</span><span class="sxs-lookup"><span data-stu-id="ae443-109">Not currently used.</span></span> <span data-ttu-id="ae443-110">任何项添加到联合必须不大于指针大小。</span><span class="sxs-lookup"><span data-stu-id="ae443-110">Any items added to the union must be no larger than pointer size.</span></span> <span data-ttu-id="ae443-111">如果`struct`是必需的必须单独分配，并指向它。</span><span class="sxs-lookup"><span data-stu-id="ae443-111">If a `struct` is required, you must allocate it separately and point to it.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="ae443-112">备注</span><span class="sxs-lookup"><span data-stu-id="ae443-112">Remarks</span></span>  
 <span data-ttu-id="ae443-113">[Iclrerrorreportingmanager:: Begincustomdump](../../../../docs/framework/unmanaged-api/hosting/iclrerrorreportingmanager-begincustomdump-method.md)采用类型的参数`CustomDumpItem`。</span><span class="sxs-lookup"><span data-stu-id="ae443-113">[ICLRErrorReportingManager::BeginCustomDump](../../../../docs/framework/unmanaged-api/hosting/iclrerrorreportingmanager-begincustomdump-method.md) takes a parameter of type `CustomDumpItem`.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="ae443-114">要求</span><span class="sxs-lookup"><span data-stu-id="ae443-114">Requirements</span></span>  
 <span data-ttu-id="ae443-115">**平台：**请参阅[系统要求](../../../../docs/framework/get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="ae443-115">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="ae443-116">**标头：** MSCorEE.idl</span><span class="sxs-lookup"><span data-stu-id="ae443-116">**Header:** MSCorEE.idl</span></span>  
  
 <span data-ttu-id="ae443-117">**库：**作为 MSCorEE.dll 中的资源</span><span class="sxs-lookup"><span data-stu-id="ae443-117">**Library:** Included as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="ae443-118">**.NET framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="ae443-118">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="ae443-119">另请参阅</span><span class="sxs-lookup"><span data-stu-id="ae443-119">See Also</span></span>  
 [<span data-ttu-id="ae443-120">承载结构</span><span class="sxs-lookup"><span data-stu-id="ae443-120">Hosting Structures</span></span>](../../../../docs/framework/unmanaged-api/hosting/hosting-structures.md)