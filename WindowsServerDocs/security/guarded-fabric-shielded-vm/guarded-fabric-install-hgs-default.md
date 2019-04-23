---
title: HGS 새 포리스트 설치
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 7f04d9964f1a19e79335e50a1882f0326f15ddc1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59860034"
---
# <a name="install-hgs-in-a-new-forest"></a>HGS 새 포리스트 설치 

>적용 대상: Windows Server, Windows Server 2016, Windows Server (반기 채널) 2019

## <a name="add-the-hgs-server-role"></a>HGS 서버 역할 추가

HGS 서버 역할을 추가 하 고 HGS를 설치 하려면 관리자 권한 PowerShell 세션에서 다음 명령을 실행 합니다.

[!INCLUDE [Install the HGS server role](../../../includes/guarded-fabric-install-hgs-server-role.md)] 

## <a name="install-hgs"></a>HGS 설치 

[!INCLUDE [Install HGS by default](../../../includes/install-hgs-default.md)] 

## <a name="next-steps"></a>다음 단계

- TPM 기반 증명을 설정 하려면 다음 단계를 참조 하세요 [TPM 모드를 사용 하 여 새 전용된 포리스트로, (기본값)에서 HGS 클러스터 초기화](guarded-fabric-initialize-hgs-tpm-mode-default.md)합니다.
- 호스트 키 증명을 설정 하려면 다음 단계를 참조 하세요 [키 모드를 사용 하 여 새 전용된 포리스트로, (기본값)에서 HGS 클러스터 초기화](guarded-fabric-initialize-hgs-key-mode-default.md)합니다.
- 다음에 대 한 관리자 기반 증명 (Windows Server 2019에 사용 되지 않음)를 설정 하는 단계는 다음과 같이 표시 됩니다. [(기본값) 새 전용 포리스트에 AD 모드를 사용 하 여 HGS 클러스터 초기화](guarded-fabric-initialize-hgs-ad-mode-default.md)합니다.

## <a name="next-step"></a>다음 단계

>[!div class="nextstepaction"]
[HGS를 초기화 합니다.](guarded-fabric-initialize-hgs.md)


