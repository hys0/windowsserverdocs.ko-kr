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
ms.openlocfilehash: a89337457cc71ffee78e3f73fecc2262f1fb38e9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59855204"
---
# <a name="configure-additional-hgs-nodes"></a>추가 HGS 노드 구성

>적용 대상: Windows Server, Windows Server 2016, Windows Server (반기 채널) 2019

프로덕션 환경에서 HGS는 설정 해야 고가용성 클러스터에는 보호 된 Vm 수에 전원을 켤 수는 HGS 노드가 다운 되 면 경우에 확인 합니다. 테스트 환경에 대 한 보조 HGS 노드 필요 하지 않습니다.

사용자 환경에 대 한 모범 사례로 적합 한, HGS 노드를 추가 하려면 다음이 방법 중 하나를 사용 합니다.

|                |                         |                              | 
|----------------|-------------------------|------------------------------|
|새 HGS 포리스트  | [PFX 파일을 사용 하 여](#dedicated-hgs-forest-with-pfx-certificates) | [인증서 지문을 사용 하 여](#dedicated-hgs-forest-with-certificate-thumbprints) |
|기존 배스 천 포리스트 |  [PFX 파일을 사용 하 여](#existing-bastion-forest-with-pfx-certificates) | [인증서 지문을 사용 하 여](#existing-bastion-forest-with-certificate-thumbprints) |

## <a name="prerequisites"></a>사전 요구 사항

있는지 각 추가 노드에: 
- 에 주 노드와 같은 하드웨어 및 소프트웨어 구성 
- 다른 HGS 서버와 동일한 네트워크에 연결 된
- 다른 HGS 서버 DNS 이름으로 해결할 수 있습니다.

## <a name="dedicated-hgs-forest-with-pfx-certificates"></a>PFX 인증서를 사용 하 여 전용된 HGS 포리스트

1. HGS 노드를 도메인 컨트롤러로 승격
2. HGS 서버를 초기화 합니다.

### <a name="promote-the-hgs-node-to-a-domain-controller"></a>HGS 노드를 도메인 컨트롤러로 승격

[!INCLUDE [Promote to a domain controller](../../../includes/guarded-fabric-promote-domain-controller.md)] 

### <a name="initialize-the-hgs-server"></a>HGS 서버를 초기화 합니다.

[!INCLUDE [Initialize the HGS server](../../../includes/guarded-fabric-initialize-hgs-on-the-node.md)] 

## <a name="dedicated-hgs-forest-with-certificate-thumbprints"></a>인증서 지문 사용 하 여 전용된 HGS 포리스트
 
1. HGS 노드를 도메인 컨트롤러로 승격
2. HGS 서버를 초기화 합니다.
3. 인증서 개인 키를 설치 합니다.

### <a name="promote-the-hgs-node-to-a-domain-controller"></a>HGS 노드를 도메인 컨트롤러로 승격

[!INCLUDE [Promote to a domain controller](../../../includes/guarded-fabric-promote-domain-controller.md)] 

### <a name="initialize-the-hgs-server"></a>HGS 서버를 초기화 합니다.

[!INCLUDE [Initialize the HGS server](../../../includes/guarded-fabric-initialize-hgs-on-the-node.md)] 

### <a name="install-the-private-keys-for-the-certificates"></a>인증서 개인 키를 설치 합니다.

[!INCLUDE [Install private keys](../../../includes/guarded-fabric-install-private-keys.md)]

## <a name="existing-bastion-forest-with-pfx-certificates"></a>PFX 인증서를 사용 하 여 기존 배스 천 포리스트

1. 노드를 기존 도메인에 가입
2. GMSA 암호 검색 Install-adserviceaccount를 실행 하는 컴퓨터 권한 부여
3. HGS 서버를 초기화 합니다.

### <a name="join-the-node-to-the-existing-domain"></a>노드를 기존 도메인에 가입

1. 노드에서 하나 이상의 NIC가 첫 번째 HGS 서버에 DNS 서버를 사용 하도록 구성 되어 있는지 확인 합니다.
2. 새 HGS 노드를 첫 번째 HGS 노드로 동일한 도메인에 가입 합니다. 

### <a name="grant-the-machine-rights-to-retrieve-gmsa-password-and-run-install-adserviceaccount"></a>GMSA 암호 검색 Install-adserviceaccount를 실행 하는 컴퓨터 권한 부여

[!INCLUDE [Grant the machine rights to retrieve the group MSA](../../../includes/guarded-fabric-grant-machine-rights-to-retrieve-gmsa.md)] 

### <a name="initialize-the-hgs-server"></a>HGS 서버를 초기화 합니다.

[!INCLUDE [Initialize the HGS server](../../../includes/guarded-fabric-initialize-hgs-on-the-node.md)] 

## <a name="existing-bastion-forest-with-certificate-thumbprints"></a>인증서 지문 사용 하 여 기존 배스 천 포리스트

1. 노드를 기존 도메인에 가입
2. GMSA 암호 검색 Install-adserviceaccount를 실행 하는 컴퓨터 권한 부여
3. HGS 서버를 초기화 합니다.
4. 인증서 개인 키를 설치 합니다.

### <a name="join-the-node-to-the-existing-domain"></a>노드를 기존 도메인에 가입

1. 노드에서 하나 이상의 NIC가 첫 번째 HGS 서버에 DNS 서버를 사용 하도록 구성 되어 있는지 확인 합니다.
2. 새 HGS 노드를 첫 번째 HGS 노드로 동일한 도메인에 가입 합니다. 

### <a name="grant-the-machine-rights-to-retrieve-gmsa-password-and-run-install-adserviceaccount"></a>GMSA 암호 검색 Install-adserviceaccount를 실행 하는 컴퓨터 권한 부여

[!INCLUDE [Grant the machine rights to retrieve the group MSA](../../../includes/guarded-fabric-grant-machine-rights-to-retrieve-gmsa.md)] 

### <a name="initialize-the-hgs-server"></a>HGS 서버를 초기화 합니다.

[!INCLUDE [Initialize the HGS server](../../../includes/guarded-fabric-initialize-hgs-on-the-node.md)] 

이 노드로 복제할 첫 번째 HGS 서버에서 암호화 및 서명 인증서에 대 일 분 정도 걸립니다.

### <a name="install-the-private-keys-for-the-certificates"></a>인증서 개인 키를 설치 합니다.

[!INCLUDE [Install private keys](../../../includes/guarded-fabric-install-private-keys.md)]

## <a name="configure-hgs-for-https-communications"></a>HTTPS 통신을 위해 HGS 구성

SSL 인증서를 사용 하 여 HGS 끝점을 보호 하려는 경우에 HGS 클러스터의 다른 모든 노드에 뿐만 아니라이 노드를 SSL 인증서를 구성 해야 합니다.
SSL 인증서 *되지* HGS에서 복제 되 고 동일한 키를 사용 하 여 모든 노드 (즉, 할 수 있습니다 각 노드에 대해 다른 SSL 인증서)에 대 한 필요가 없습니다.

SSL 인증서를 요청 하는 경우 클러스터 정규화 된 도메인 이름 확인 (출력에 표시 된 것 처럼 `Get-HgsServer`)은 주체 일반 이름은 인증서 또는 주체 대체 DNS 이름으로 포함 합니다.
인증 기관에서 인증서를 구입한 했습니다 하는 경우와 함께 사용 하는 HGS를 구성할 수 있습니다 [집합 HgsServer](https://technet.microsoft.com/itpro/powershell/windows/hgsserver/set-hgsserver)합니다.

```powershell
$sslPassword = Read-Host -AsSecureString -Prompt "SSL Certificate Password"
Set-HgsServer -Http -Https -HttpsCertificatePath 'C:\temp\HgsSSLCertificate.pfx' -HttpsCertificatePassword $sslPassword
```

이미 로컬 인증서 저장소에 인증서를 설치 하 고 지 문으로 참조 하려면, 하는 경우 대신 다음 명령을 실행 합니다.

```powershell
Set-HgsServer -Http -Https -HttpsCertificateThumbprint 'A1B2C3D4E5F6...'
```

HGS는 항상 통신에 대 한 HTTP 및 HTTPS 포트를 노출 합니다.
포트 80 통한 통신을 차단 하도록 Windows 방화벽 또는 다른 네트워크 방화벽 기술을 사용할 수 있지만 IIS에서 HTTP 바인딩을 제거 하려면 지원 되지 않습니다.

## <a name="decommission-an-hgs-node"></a>HGS 노드를 서비스 해제

HGS 노드를 역할 해제 합니다.

1. [HGS 구성 지우기](guarded-fabric-manage-hgs.md#clearing-the-hgs-configuration)합니다.

   이 클러스터에서 노드를 제거 하 고 증명 및 키 보호 서비스를 제거 합니다. 
   하는 경우 클러스터의 마지막 노드인지를-Force로 마지막 노드를 제거 하 고 Active Directory에서 클러스터를 삭제 하려면 필요한 합니다. 
   
   HGS는 배스 천 포리스트 (기본값)에 배포 하는 경우 이것이 유일한 단계입니다. 
   필요에 따라 도메인에서 컴퓨터를 가입 하 고 Active Directory에서 gMSA 계정을 제거할 수 있습니다.

1. HGS 자체 도메인을 만든 경우 수행 해야 [HGS 제거](guarded-fabric-manage-hgs.md#clearing-the-hgs-configuration) 도메인 했다가 도메인 컨트롤러 수준 내리기.



## <a name="next-step"></a>다음 단계

>[!div class="nextstepaction"]
[HGS 구성 유효성 검사](guarded-fabric-verify-hgs-configuration.md)

