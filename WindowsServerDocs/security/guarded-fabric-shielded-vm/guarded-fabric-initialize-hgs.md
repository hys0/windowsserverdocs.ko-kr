---
title: HGS 초기화
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: c689a1d5f69731db0cb85a884f5af2ee0230e7be
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59865454"
---
# <a name="initialize-the-host-guardian-service-hgs"></a>호스트 보호 서비스 (HGS)를 초기화 합니다.

>적용 대상: Windows Server, Windows Server 2016, Windows Server (반기 채널) 2019

HGS를 초기화할 때는 HGS가 보호 된 호스트의 상태를 측정 하는 데 사용할 모드를 지정 합니다. 상호 배타적인 두 가지 옵션이 있습니다. 모드 선택에 대 한 배경 정보를 참조 하세요 [보호 된 패브릭 및 차폐 VM 계획 가이드 호스터](guarded-fabric-planning-for-hosters.md)합니다.

다음 항목에서는 각 모드에 대 한 배포 단계를 설명 합니다.

- [TPM 신뢰할 수 있는 증명 (TPM 모드)](guarded-fabric-initialize-hgs-tpm-mode.md)
- [호스트 키 증명 (키 모드)](guarded-fabric-initialize-hgs-key-mode.md)
- [관리자-신뢰할 수 있는 증명 (AD 모드)](guarded-fabric-initialize-hgs-ad-mode.md)

물리적 서버에서 다음이 단계를 수행 해야 합니다.