---
title: 새 포리스트에 HGS 설치
ms.custom: na
ms.prod: windows-server
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 6dfbe24fb4d9011b48f366d7e5df92fdb80685d5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71386594"
---
# <a name="install-hgs-in-a-new-forest"></a>새 포리스트에 HGS 설치 

>적용 대상: Windows server 2019, Windows Server (반기 채널), Windows Server 2016

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


