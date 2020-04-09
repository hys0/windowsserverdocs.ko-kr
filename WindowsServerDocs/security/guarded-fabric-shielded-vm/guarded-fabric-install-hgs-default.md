---
title: 새 포리스트에 HGS 설치
ms.prod: windows-server
ms.topic: article
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 8f896b0cea49f9dd26a828a2580b59a78348763a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80856606"
---
# <a name="install-hgs-in-a-new-forest"></a>새 포리스트에 HGS 설치 

>적용 대상: Windows Server 2019, Windows Server (반기 채널), Windows Server 2016

## <a name="add-the-hgs-server-role"></a>HGS 서버 역할 추가

관리자 권한 PowerShell 세션에서 다음 명령을 실행 하 여 HGS 서버 역할을 추가 하 고 HGS를 설치 합니다.

[!INCLUDE [Install the HGS server role](../../../includes/guarded-fabric-install-hgs-server-role.md)] 

## <a name="install-hgs"></a>HGS 설치 

[!INCLUDE [Install HGS by default](../../../includes/install-hgs-default.md)] 

## <a name="next-steps"></a>다음 단계

- TPM 기반 증명을 설정 하는 다음 단계는 [새 전용 포리스트에서 tpm 모드를 사용 하 여 HGS 클러스터 초기화 (기본값)](guarded-fabric-initialize-hgs-tpm-mode-default.md)를 참조 하세요.
- 호스트 키 증명을 설정 하는 다음 단계는 [새 전용 포리스트에서 키 모드를 사용 하 여 HGS 클러스터 초기화 (기본값)](guarded-fabric-initialize-hgs-key-mode-default.md)를 참조 하세요.
- 관리자 기반 증명을 설정 하는 다음 단계는 (Windows Server 2019에서 사용 되지 않음) [새 전용 포리스트에서 AD 모드를 사용 하 여 HGS 클러스터 초기화 (기본값)](guarded-fabric-initialize-hgs-ad-mode-default.md)를 참조 하세요.

## <a name="next-step"></a>다음 단계

> [!div class="nextstepaction"]
> [HGS 초기화](guarded-fabric-initialize-hgs.md)


