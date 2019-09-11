---
title: 추가 HGS 노드 구성
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 227f723b-acb2-42a7-bbe3-44e82f930e35
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 10/22/2018
ms.openlocfilehash: fe9cd63f08da849c2cb002ab853501370d736f0f
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70870592"
---
# <a name="configure-additional-hgs-nodes"></a>추가 HGS 노드 구성

>적용 대상: Windows server 2019, Windows Server (반기 채널), Windows Server 2016

프로덕션 환경에서는 hgs 노드가 중단 된 경우에도 보호 된 Vm의 전원이 켜 졌는 지 확인 하기 위해 고가용성 클러스터에서 HGS를 설정 해야 합니다. 테스트 환경의 경우 보조 HGS 노드가 필요 하지 않습니다.

이러한 방법 중 하나를 사용 하 여 사용자 환경에 가장 적합 한 HGS 노드를 추가 합니다.

|                |                         |                              | 
|----------------|-------------------------|------------------------------|
|새 HGS 포리스트  | [PFX 파일 사용](#dedicated-hgs-forest-with-pfx-certificates) | [인증서 지문 사용](#dedicated-hgs-forest-with-certificate-thumbprints) |
|기존 요새 포리스트 |  [PFX 파일 사용](#existing-bastion-forest-with-pfx-certificates) | [인증서 지문 사용](#existing-bastion-forest-with-certificate-thumbprints) |

## <a name="prerequisites"></a>사전 요구 사항

각 추가 노드가 다음과 같은지 확인 합니다. 
- 에는 주 노드와 동일한 하드웨어 및 소프트웨어 구성이 있습니다. 
- 다른 HGS 서버와 동일한 네트워크에 연결 되어 있습니다.
- DNS 이름으로 다른 HGS 서버를 확인할 수 있습니다.

## <a name="dedicated-hgs-forest-with-pfx-certificates"></a>PFX 인증서를 사용 하는 전용 HGS 포리스트

1. 도메인 컨트롤러에 대 한 HGS 노드 수준 올리기
2. HGS 서버 초기화

### <a name="promote-the-hgs-node-to-a-domain-controller"></a>도메인 컨트롤러에 대 한 HGS 노드 수준 올리기

[!INCLUDE [Promote to a domain controller](../../../includes/guarded-fabric-promote-domain-controller.md)] 

### <a name="initialize-the-hgs-server"></a>HGS 서버 초기화

[!INCLUDE [Initialize the HGS server](../../../includes/guarded-fabric-initialize-hgs-on-the-node.md)] 

## <a name="dedicated-hgs-forest-with-certificate-thumbprints"></a>인증서 지문을 사용 하는 전용 HGS 포리스트
 
1. 도메인 컨트롤러에 대 한 HGS 노드 수준 올리기
2. HGS 서버 초기화
3. 인증서에 대 한 개인 키 설치

### <a name="promote-the-hgs-node-to-a-domain-controller"></a>도메인 컨트롤러에 대 한 HGS 노드 수준 올리기

[!INCLUDE [Promote to a domain controller](../../../includes/guarded-fabric-promote-domain-controller.md)] 

### <a name="initialize-the-hgs-server"></a>HGS 서버 초기화

[!INCLUDE [Initialize the HGS server](../../../includes/guarded-fabric-initialize-hgs-on-the-node.md)] 

### <a name="install-the-private-keys-for-the-certificates"></a>인증서에 대 한 개인 키 설치

[!INCLUDE [Install private keys](../../../includes/guarded-fabric-install-private-keys.md)]

## <a name="existing-bastion-forest-with-pfx-certificates"></a>PFX 인증서를 사용 하는 기존 요새 포리스트

1. 기존 도메인에 노드 조인
2. GMSA 암호를 검색 하 고 Uninstall-adserviceaccount를 실행 하는 컴퓨터 권한을 부여 합니다.
3. HGS 서버 초기화

### <a name="join-the-node-to-the-existing-domain"></a>기존 도메인에 노드 조인

1. 노드에서 하나 이상의 NIC가 첫 번째 HGS 서버에서 DNS 서버를 사용 하도록 구성 되어 있는지 확인 합니다.
2. 첫 번째 HGS 노드와 동일한 도메인에 새 HGS 노드를 조인 합니다. 

### <a name="grant-the-machine-rights-to-retrieve-gmsa-password-and-run-install-adserviceaccount"></a>GMSA 암호를 검색 하 고 Uninstall-adserviceaccount를 실행 하는 컴퓨터 권한을 부여 합니다.

[!INCLUDE [Grant the machine rights to retrieve the group MSA](../../../includes/guarded-fabric-grant-machine-rights-to-retrieve-gmsa.md)] 

### <a name="initialize-the-hgs-server"></a>HGS 서버 초기화

[!INCLUDE [Initialize the HGS server](../../../includes/guarded-fabric-initialize-hgs-on-the-node.md)] 

## <a name="existing-bastion-forest-with-certificate-thumbprints"></a>인증서 지문이 있는 기존 요새 포리스트

1. 기존 도메인에 노드 조인
2. GMSA 암호를 검색 하 고 Uninstall-adserviceaccount를 실행 하는 컴퓨터 권한을 부여 합니다.
3. HGS 서버 초기화
4. 인증서에 대 한 개인 키 설치

### <a name="join-the-node-to-the-existing-domain"></a>기존 도메인에 노드 조인

1. 노드에서 하나 이상의 NIC가 첫 번째 HGS 서버에서 DNS 서버를 사용 하도록 구성 되어 있는지 확인 합니다.
2. 첫 번째 HGS 노드와 동일한 도메인에 새 HGS 노드를 조인 합니다. 

### <a name="grant-the-machine-rights-to-retrieve-gmsa-password-and-run-install-adserviceaccount"></a>GMSA 암호를 검색 하 고 Uninstall-adserviceaccount를 실행 하는 컴퓨터 권한을 부여 합니다.

[!INCLUDE [Grant the machine rights to retrieve the group MSA](../../../includes/guarded-fabric-grant-machine-rights-to-retrieve-gmsa.md)] 

### <a name="initialize-the-hgs-server"></a>HGS 서버 초기화

[!INCLUDE [Initialize the HGS server](../../../includes/guarded-fabric-initialize-hgs-on-the-node.md)] 

첫 번째 HGS 서버의 암호화 및 서명 인증서가이 노드에 복제 되는 데 최대 10 분이 소요 됩니다.

### <a name="install-the-private-keys-for-the-certificates"></a>인증서에 대 한 개인 키 설치

[!INCLUDE [Install private keys](../../../includes/guarded-fabric-install-private-keys.md)]

## <a name="configure-hgs-for-https-communications"></a>HTTPS 통신에 대 한 HGS 구성

SSL 인증서를 사용 하 여 HGS 끝점의 보안을 유지 하려면이 노드의 SSL 인증서 뿐만 아니라 HGS 클러스터의 다른 모든 노드를 구성 해야 합니다.
SSL 인증서 *는* HGS에 의해 복제 되지 않으며, 모든 노드에 대해 동일한 키를 사용할 필요가 없습니다 (즉, 각 노드에 대해 서로 다른 SSL 인증서를 사용할 수 있음).

SSL 인증서를 요청할 때 클러스터의 정규화 된 도메인 이름 (출력 `Get-HgsServer`에 표시)이 인증서의 주체 일반 이름 이거나 주체 대체 DNS 이름으로 포함 되어 있는지 확인 합니다.
인증 기관에서 인증서를 받은 경우 [HgsServer](https://technet.microsoft.com/itpro/powershell/windows/hgsserver/set-hgsserver)에서 사용 하도록 HGS를 구성할 수 있습니다.

```powershell
$sslPassword = Read-Host -AsSecureString -Prompt "SSL Certificate Password"
Set-HgsServer -Http -Https -HttpsCertificatePath 'C:\temp\HgsSSLCertificate.pfx' -HttpsCertificatePassword $sslPassword
```

인증서를 로컬 인증서 저장소에 이미 설치 했 고 지문을 통해 인증서를 참조 하려는 경우에는 다음 명령을 대신 실행 합니다.

```powershell
Set-HgsServer -Http -Https -HttpsCertificateThumbprint 'A1B2C3D4E5F6...'
```

HGS는 통신을 위해 항상 HTTP 및 HTTPS 포트를 노출 합니다.
IIS에서 HTTP 바인딩을 제거 하는 것은 지원 되지 않지만 Windows 방화벽 또는 다른 네트워크 방화벽 기술을 사용 하 여 80 포트를 통한 통신을 차단할 수 있습니다.

## <a name="decommission-an-hgs-node"></a>HGS 노드 서비스 해제

HGS 노드를 서비스 해제 하려면:

1. [HGS 구성의 선택을 취소](guarded-fabric-manage-hgs.md#clearing-the-hgs-configuration)합니다.

   그러면 클러스터에서 노드가 제거 되 고 증명 및 키 보호 서비스가 제거 됩니다. 
   클러스터의 마지막 노드인 경우-Force는 마지막 노드를 제거 하 고 Active Directory에서 클러스터를 삭제 하는 작업을 수행 하는 데 필요 합니다. 
   
   HGS가 요새 포리스트에 배포 된 경우 (기본값) 유일한 단계입니다. 
   필요에 따라 도메인에서 컴퓨터의 가입을 취소 하 고 Active Directory에서 gMSA 계정을 제거할 수 있습니다.

1. HGS가 자체 도메인을 만든 경우 도메인 가입을 취소 하 고 도메인 컨트롤러의 수준을 내리려면 [hgs도 제거](guarded-fabric-manage-hgs.md#clearing-the-hgs-configuration) 해야 합니다.



## <a name="next-step"></a>다음 단계

> [!div class="nextstepaction"]
> [HGS 구성 유효성 검사](guarded-fabric-verify-hgs-configuration.md)

