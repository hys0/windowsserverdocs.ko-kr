---
title: 보호 된 호스트 (AD)에 대 한 패브릭 DNS 구성
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 074b6d09-f16e-49bf-b88a-377139d35067
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 8a2ddc0f2ab495b2500d4bfe48f3ee83c333c769
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59842754"
---
# <a name="configure-the-fabric-dns-for-guarded-hosts"></a>보호 된 호스트에 대 한 패브릭 DNS 구성

>적용 대상: Windows Server 2016


>[!IMPORTANT]
>AD 모드는 Windows Server 2019로 시작 하는 사용 되지 않습니다. TPM 증명 수 없는 환경에 대 한 구성 [호스트 키 증명](guarded-fabric-initialize-hgs-key-mode.md)합니다. 호스트 키 증명 AD 모드에 유사한 보증을 제공 하며 간단 하 게 설정 합니다. 

패브릭 관리자는 보호 된 호스트는 HGS 클러스터를 확인할 수 있도록 DNS는 패브릭을 구성 해야 합니다. HGS 클러스터 있어야 [HGS 관리자가 설정한](/WindowsServerDocs/virtualization/guarded-fabric-shielded-vm/guarded-fabric-setting-up-the-host-guardian-service-hgs.md)합니다.



[!INCLUDE [Configure fabric DNS](../../../includes/guarded-fabric-configure-fabric-dns.md)] 


## <a name="next-step"></a>다음 단계

>[!div class="nextstepaction"]
[HGS DNS와 단방향 트러스트 구성](guarded-fabric-configure-dns-forwarding-and-trust.md)
