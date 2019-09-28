---
title: 보호 된 호스트 (AD)에 대 한 패브릭 DNS 구성
ms.custom: na
ms.prod: windows-server
ms.topic: article
ms.assetid: 074b6d09-f16e-49bf-b88a-377139d35067
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 411b845d57c36916dcbc73d51675f5d9f92bfa0e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71386760"
---
# <a name="configure-the-fabric-dns-for-guarded-hosts"></a>보호 된 호스트에 대 한 패브릭 DNS 구성

>적용 대상: Windows Server 2016


>[!IMPORTANT]
>AD 모드는 Windows Server 2019부터 사용 되지 않습니다. TPM 증명을 사용할 수 없는 환경의 경우 [호스트 키 증명](guarded-fabric-initialize-hgs-key-mode.md)을 구성 합니다. 호스트 키 증명은 AD 모드와 비슷한 보증을 제공 하 고 설정 하는 것이 더 간단 합니다. 

패브릭 관리자는 보호 된 호스트가 HGS 클러스터를 확인할 수 있도록 패브릭 DNS를 구성 해야 합니다. Hgs 클러스터가 이미 hgs 관리자에 [의해 설정](/WindowsServerDocs/virtualization/guarded-fabric-shielded-vm/guarded-fabric-setting-up-the-host-guardian-service-hgs.md)되어 있어야 합니다.



[!INCLUDE [Configure fabric DNS](../../../includes/guarded-fabric-configure-fabric-dns.md)] 


## <a name="next-step"></a>다음 단계

> [!div class="nextstepaction"]
> [HGS DNS 및 단방향 트러스트 구성](guarded-fabric-configure-dns-forwarding-and-trust.md)
