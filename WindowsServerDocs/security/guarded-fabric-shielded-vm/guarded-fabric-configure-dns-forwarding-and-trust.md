---
title: DNS 전달 및 도메인 트러스트 구성
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: ebc9c2a3cac85ab998075d784111808b3d590d46
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59854144"
---
# <a name="configure-dns-forwarding-in-the-hgs-domain-and-a-one-way-trust-with-the-fabric-domain"></a>HGS 도메인과 단방향 트러스트가 fabric 도메인에서 DNS 전달 구성

>적용 대상: Windows Server (반기 채널), Windows Server 2016

>[!IMPORTANT]
>AD 모드는 Windows Server 2019로 시작 하는 사용 되지 않습니다. TPM 증명 수 없는 환경에 대 한 구성 [호스트 키 증명](guarded-fabric-initialize-hgs-key-mode.md)합니다. 호스트 키 증명 AD 모드에 유사한 보증을 제공 하며 간단 하 게 설정 합니다. 

다음 단계를 사용 하 여 DNS 전달을 설정 하 여 패브릭 도메인과 단방향 트러스트를 설정 합니다. 이러한 단계는 도메인 컨트롤러 패브릭에 찾으려고 HGS를 허용 하 고 Hyper-v 호스트의 그룹 멤버 자격의 유효성을 검사.

1.  DNS 전달을 구성 하려면 관리자 권한 PowerShell 세션에서 다음 명령을 실행 합니다. Fabrikam.com fabric 도메인의 이름으로 바꾸고 fabric 도메인에 DNS 서버의 IP 주소를 입력 합니다. 더 높은 가용성을 둘 이상의 DNS 서버를 가리키도록 합니다.

    ```powershell
    Add-DnsServerConditionalForwarderZone -Name "fabrikam.com" -ReplicationScope "Forest" -MasterServers <DNSserverAddress1>, <DNSserverAddress2>
    ```

2.  단방향 포리스트 트러스트를 만들려면 관리자 권한 명령 프롬프트에서 다음 명령을 실행 합니다.

    바꿉니다 `bastion.local` HGS 도메인의 이름 및 `fabrikam.com` fabric 도메인의 이름입니다. Fabric 도메인의 관리자에 대 한 암호를 제공 합니다.

        netdom trust bastion.local /domain:fabrikam.com /userD:fabrikam.com\Administrator /passwordD:<password> /add

## <a name="next-step"></a>다음 단계 

>[!div class="nextstepaction"]
[HTTPS 구성](guarded-fabric-configure-hgs-https.md)
