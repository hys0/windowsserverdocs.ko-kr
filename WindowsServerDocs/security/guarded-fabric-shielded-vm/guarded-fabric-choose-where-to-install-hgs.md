---
title: 기존 배스 천 포리스트 또는 새 포리스트에 자체에서 HGS를 설치할지 여부를 선택합니다
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 4e02cd37391e629c9b947095fe32626bd15726ff
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59827504"
---
# <a name="choose-whether-to-install-hgs-in-its-own-dedicated-forest-or-in-an-existing-bastion-forest"></a>자체 전용된 포리스트 또는 기존 배스 천 포리스트의 HGS를 설치할지 여부를 선택합니다

>적용 대상: Windows Server, Windows Server 2016, Windows Server (반기 채널) 2019


HGS에 대 한 Active Directory 포리스트는 해당 관리자 제어 보호 된 Vm의 키에 액세스할 수 있으므로 중요 합니다. 기본 설치 하도록 설정 된 새 포리스트 전용 HGS를 다른 종속성을 구성 합니다. 이 옵션은 자체 포함 된 환경 이므로 권장 이며 만들어질 때 안전한 것으로 알려진. 

기술만 기존 포리스트에 있는 HGS를 설치 하기 위한 요구 사항인 루트 도메인;에 추가할 것 루트가 아닌 도메인 지원 되지 않습니다. 하지만 밖에도 운영 요구 사항 및 기존 포리스트를 사용 하 여에 대 한 보안 관련 모범 사례입니다. 적합 한 포리스트에서 사용 하는 포리스트 같은 중요 한 함수 하나에 맞도록 의도적으로 빌드됩니다 [AD DS에 대 한 Privileged Access Management](https://docs.microsoft.com/microsoft-identity-manager/pam/privileged-identity-management-for-active-directory-domain-services) 요소나 [향상 된 보안 관리 환경 (ESAE) 포리스트에](https://technet.microsoft.com/windows-server-docs/security/securing-privileged-access/securing-privileged-access-reference-material#ESAE_BM). 이러한 포리스트는 일반적으로 다음과 같은 특징을 나타냅니다.

- 몇 가지 관리자 (패브릭 관리자가 별도)를가지고
- 이러한 많은 낮은 로그온
- 이들은 특성에서 범용 

프로덕션 포리스트 같은 범용 포리스트 HGS 사용에 적합 하지 않습니다. HGS 패브릭 관리자 로부터 격리 해야 하므로 fabric 포리스트 적합도 하지 않습니다.

## <a name="next-step"></a>다음 단계

사용자 환경에 가장 적합 한 설치 옵션을 선택 합니다.

- [HGS는 자체 전용된 포리스트에 설치](guarded-fabric-install-hgs-default.md)
- [기존 배스 천 포리스트의 HGS를 설치 합니다.](guarded-fabric-install-hgs-in-a-bastion-forest.md)


