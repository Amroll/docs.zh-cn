---
title: "IHostSecurityManager::ImpersonateLoggedOnUser 方法"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: IHostSecurityManager.ImpersonateLoggedOnUser
api_location: mscoree.dll
api_type: COM
f1_keywords: IHostSecurityManager::ImpersonateLoggedOnUser
helpviewer_keywords:
- ImpersonateLoggedOnUser method [.NET Framework hosting]
- IHostSecurityManager::ImpersonateLoggedOnUser method [.NET Framework hosting]
ms.assetid: acc49ba0-f1d9-45ad-871f-9d053a89dcbe
topic_type: apiref
caps.latest.revision: "9"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 8c5956dcad6908f0117de7f5ff0c6632ad3bb925
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="ihostsecuritymanagerimpersonateloggedonuser-method"></a><span data-ttu-id="93bd3-102">IHostSecurityManager::ImpersonateLoggedOnUser 方法</span><span class="sxs-lookup"><span data-stu-id="93bd3-102">IHostSecurityManager::ImpersonateLoggedOnUser Method</span></span>
<span data-ttu-id="93bd3-103">请求的可执行代码，使用当前用户标识的凭据。</span><span class="sxs-lookup"><span data-stu-id="93bd3-103">Requests that code be executed using the credentials of the current user identity.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="93bd3-104">语法</span><span class="sxs-lookup"><span data-stu-id="93bd3-104">Syntax</span></span>  
  
```  
HRESULT ImpersonateLoggedOnUser (  
    [in] HANDLE hToken  
);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="93bd3-105">参数</span><span class="sxs-lookup"><span data-stu-id="93bd3-105">Parameters</span></span>  
 `hToken`  
 <span data-ttu-id="93bd3-106">[in]表示要模拟的用户的凭据的标记。</span><span class="sxs-lookup"><span data-stu-id="93bd3-106">[in] A token representing the credentials of the user to be impersonated.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="93bd3-107">返回值</span><span class="sxs-lookup"><span data-stu-id="93bd3-107">Return Value</span></span>  
  
|<span data-ttu-id="93bd3-108">HRESULT</span><span class="sxs-lookup"><span data-stu-id="93bd3-108">HRESULT</span></span>|<span data-ttu-id="93bd3-109">描述</span><span class="sxs-lookup"><span data-stu-id="93bd3-109">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="93bd3-110">S_OK</span><span class="sxs-lookup"><span data-stu-id="93bd3-110">S_OK</span></span>|<span data-ttu-id="93bd3-111">`ImpersonateLoggedOnUser`已成功返回。</span><span class="sxs-lookup"><span data-stu-id="93bd3-111">`ImpersonateLoggedOnUser` returned successfully.</span></span>|  
|<span data-ttu-id="93bd3-112">HOST_E_CLRNOTAVAILABLE</span><span class="sxs-lookup"><span data-stu-id="93bd3-112">HOST_E_CLRNOTAVAILABLE</span></span>|<span data-ttu-id="93bd3-113">公共语言运行时 (CLR) 尚未加载到进程中，或 CLR 处于不能运行托管的代码或成功处理调用的状态。</span><span class="sxs-lookup"><span data-stu-id="93bd3-113">The common language runtime (CLR) has not been loaded into a process, or the CLR is in a state in which it cannot run managed code or process the call successfully.</span></span>|  
|<span data-ttu-id="93bd3-114">HOST_E_TIMEOUT</span><span class="sxs-lookup"><span data-stu-id="93bd3-114">HOST_E_TIMEOUT</span></span>|<span data-ttu-id="93bd3-115">调用操作已超时。</span><span class="sxs-lookup"><span data-stu-id="93bd3-115">The call timed out.</span></span>|  
|<span data-ttu-id="93bd3-116">HOST_E_NOT_OWNER</span><span class="sxs-lookup"><span data-stu-id="93bd3-116">HOST_E_NOT_OWNER</span></span>|<span data-ttu-id="93bd3-117">调用方不拥有该锁。</span><span class="sxs-lookup"><span data-stu-id="93bd3-117">The caller does not own the lock.</span></span>|  
|<span data-ttu-id="93bd3-118">HOST_E_ABANDONED</span><span class="sxs-lookup"><span data-stu-id="93bd3-118">HOST_E_ABANDONED</span></span>|<span data-ttu-id="93bd3-119">事件已被取消时被阻塞的线程，或者纤程正在等待它。</span><span class="sxs-lookup"><span data-stu-id="93bd3-119">An event was canceled while a blocked thread or fiber was waiting on it.</span></span>|  
|<span data-ttu-id="93bd3-120">E_FAIL</span><span class="sxs-lookup"><span data-stu-id="93bd3-120">E_FAIL</span></span>|<span data-ttu-id="93bd3-121">出现未知的灾难性故障。</span><span class="sxs-lookup"><span data-stu-id="93bd3-121">An unknown catastrophic failure occurred.</span></span> <span data-ttu-id="93bd3-122">如果某方法返回 E_FAIL，CLR 不再可用进程内。</span><span class="sxs-lookup"><span data-stu-id="93bd3-122">When a method returns E_FAIL, the CLR is no longer usable within the process.</span></span> <span data-ttu-id="93bd3-123">到托管方法的后续调用会返回 HOST_E_CLRNOTAVAILABLE。</span><span class="sxs-lookup"><span data-stu-id="93bd3-123">Subsequent calls to hosting methods return HOST_E_CLRNOTAVAILABLE.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="93bd3-124">备注</span><span class="sxs-lookup"><span data-stu-id="93bd3-124">Remarks</span></span>  
 <span data-ttu-id="93bd3-125">调用`LogonUser`或相关的 Win32 函数来获取当前用户标识的凭据的句柄。</span><span class="sxs-lookup"><span data-stu-id="93bd3-125">Call `LogonUser` or a related Win32 function to get a handle to the credentials of the current user identity.</span></span>  
  
 <span data-ttu-id="93bd3-126">`HANDLE`类型不是 COM 兼容，也就是说，其大小是特定于操作系统，以及它要求自定义封送处理。</span><span class="sxs-lookup"><span data-stu-id="93bd3-126">The `HANDLE` type is not COM-compliant, that is, its size is specific to an operating system, and it requires custom marshaling.</span></span> <span data-ttu-id="93bd3-127">因此，此令牌是仅在 CLR 与主机之间的流程内使用。</span><span class="sxs-lookup"><span data-stu-id="93bd3-127">Thus, this token is for use only within the process, between the CLR and the host.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="93bd3-128">要求</span><span class="sxs-lookup"><span data-stu-id="93bd3-128">Requirements</span></span>  
 <span data-ttu-id="93bd3-129">**平台：**请参阅[系统要求](../../../../docs/framework/get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="93bd3-129">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="93bd3-130">**标头：** MSCorEE.h</span><span class="sxs-lookup"><span data-stu-id="93bd3-130">**Header:** MSCorEE.h</span></span>  
  
 <span data-ttu-id="93bd3-131">**库：**作为 MSCorEE.dll 中的资源</span><span class="sxs-lookup"><span data-stu-id="93bd3-131">**Library:** Included as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="93bd3-132">**.NET framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="93bd3-132">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="93bd3-133">另请参阅</span><span class="sxs-lookup"><span data-stu-id="93bd3-133">See Also</span></span>  
 [<span data-ttu-id="93bd3-134">IHostSecurityContext 接口</span><span class="sxs-lookup"><span data-stu-id="93bd3-134">IHostSecurityContext Interface</span></span>](../../../../docs/framework/unmanaged-api/hosting/ihostsecuritycontext-interface.md)  
 [<span data-ttu-id="93bd3-135">IHostSecurityManager 接口</span><span class="sxs-lookup"><span data-stu-id="93bd3-135">IHostSecurityManager Interface</span></span>](../../../../docs/framework/unmanaged-api/hosting/ihostsecuritymanager-interface.md)  
 [<span data-ttu-id="93bd3-136">RevertToSelf 方法</span><span class="sxs-lookup"><span data-stu-id="93bd3-136">RevertToSelf Method</span></span>](../../../../docs/framework/unmanaged-api/hosting/ihostsecuritymanager-reverttoself-method.md)