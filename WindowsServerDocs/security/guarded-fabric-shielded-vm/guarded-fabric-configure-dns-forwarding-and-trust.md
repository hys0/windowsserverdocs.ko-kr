---
title: DNS 전달 및 도메인 트러스트 구성
ms.custom: na
ms.prod: windows-server
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 5d8ffe82065caeee27c5d13f5243f13addc6c325
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71386743"
---
# <a name="configure-dns-forwarding-in-the-hgs-domain-and-a-one-way-trust-with-the-fabric-domain"></a>HGS 도메인의 DNS 전달과 패브릭 도메인을 사용 하 여 단방향 트러스트 구성

>적용 대상: Windows Server(반기 채널), Windows Server 2016

>[!IMPORTANT]
>AD 모드는 Windows Server 2019부터 사용 되지 않습니다. TPM 증명을 사용할 수 없는 환경의 경우 [호스트 키 증명](guarded-fabric-initialize-hgs-key-mode.md)을 구성 합니다. 호스트 키 증명은 AD 모드와 비슷한 보증을 제공 하 고 설정 하는 것이 더 간단 합니다. 

다음 단계를 사용 하 여 DNS 전달을 설정 하 고 패브릭 도메인과 단방향 트러스트를 설정 합니다. 이러한 단계를 통해 HGS는 패브릭 도메인 컨트롤러를 찾고 Hyper-v 호스트의 그룹 멤버 자격에 대 한 유효성을 검사할 수 있습니다.

1.  관리자 권한 PowerShell 세션에서 다음 명령을 실행 하 여 DNS 전달을 구성 합니다. Fabrikam.com을 패브릭 도메인의 이름으로 바꾸고 패브릭 도메인에 있는 DNS 서버의 IP 주소를 입력 합니다. 더 높은 가용성을 위해 둘 이상의 DNS 서버를 가리킵니다.

    ```powershell
    Add-DnsServerConditionalForwarderZone -Name "fabrikam.com" -ReplicationScope "Forest" -MasterServers <DNSserverAddress1>, <DNSserverAddress2>
    ```

2.  단방향 포리스트 트러스트를 만들려면 관리자 권한 명령 프롬프트에서 다음 명령을 실행 합니다.

    `bastion.local`를 HGS 도메인의 이름으로 바꾸고 `fabrikam.com`를 패브릭 도메인의 이름으로 바꿉니다. 패브릭 도메인의 관리자에 대 한 암호를 제공 합니다.

        netdom trust bastion.local /domain:fabrikam.com /userD:fabrikam.com\Administrator /passwordD:<password> /add

## <a name="next-step"></a>다음 단계 

> [!div class="nextstepaction"]
> [HTTPS 구성](guarded-fabric-configure-hgs-https.md)
