---
title: 새 포리스트 또는 기존 요새 포리스트에 HGS를 설치할지 여부를 선택 합니다.
ms.prod: windows-server
ms.topic: article
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 52376a4e193b8021dc58214003e9b7579b096a79
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80856886"
---
# <a name="choose-whether-to-install-hgs-in-its-own-dedicated-forest-or-in-an-existing-bastion-forest"></a>자체 전용 포리스트 또는 기존 요새 포리스트에 HGS를 설치할지 여부를 선택 합니다.

>적용 대상: Windows Server 2019, Windows Server (반기 채널), Windows Server 2016


해당 관리자는 보호 된 Vm을 제어 하는 키에 액세스할 수 있으므로 HGS의 Active Directory 포리스트는 중요 합니다. 기본 설치에서는 HGS 전용의 새 포리스트를 설정 하 고 다른 종속성을 구성 합니다. 환경이 자체 포함 되 고 생성 시 보안이 유지 되는 것으로 알려져 있으므로이 옵션을 선택 하는 것이 좋습니다. 

기존 포리스트에 HGS를 설치 하기 위한 유일한 기술적 요구 사항은 루트 도메인에 추가 된다는 것입니다. 루트가 아닌 도메인은 지원 되지 않습니다. 그러나 기존 포리스트 사용에 대 한 운영 요구 사항 및 보안 관련 모범 사례도 있습니다. 적절 한 포리스트는 AD DS 또는 [ESAE (강화 된 보안 관리 환경) 포리스트에](https://technet.microsoft.com/windows-server-docs/security/securing-privileged-access/securing-privileged-access-reference-material#ESAE_BM) [대해 Privileged Access Management](https://docs.microsoft.com/microsoft-identity-manager/pam/privileged-identity-management-for-active-directory-domain-services) 에서 사용 하는 포리스트와 같은 하나의 중요 한 기능을 제공 하도록 의도적으로 빌드됩니다. 이러한 포리스트에는 일반적으로 다음과 같은 특징이 있습니다.

- 소수의 관리자 (패브릭 관리자와 구분)가 있습니다.
- 적은 수의 로그온을 포함 합니다.
- 기본적으로 일반적인 용도가 아닙니다. 

프로덕션 포리스트와 같은 범용 포리스트는 HGS에서 사용 하기에 적합 하지 않습니다. 또한 패브릭 포리스트는 패브릭 관리자와 격리 해야 하기 때문에 적합 하지 않습니다.

## <a name="next-step"></a>다음 단계

환경에 가장 적합 한 설치 옵션을 선택 합니다.

- [자체 전용 포리스트에 HGS 설치](guarded-fabric-install-hgs-default.md)
- [기존 요새 포리스트에 HGS 설치](guarded-fabric-install-hgs-in-a-bastion-forest.md)


