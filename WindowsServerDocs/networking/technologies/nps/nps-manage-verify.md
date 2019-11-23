---
title: NPS 변경 후 구성 확인
description: 이 항목을 사용 하 여 IP 주소 또는 서버 이름을 변경한 후 Windows Server 2016 네트워크 정책 서버 구성을 확인할 수 있습니다.
manager: brianlic
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: fc77450e-2af1-47ba-bb23-1fd36d9efdbf
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 9ba1f5f494228f6bdba22b300a2336fa6eb37690
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405357"
---
# <a name="verify-configuration-after-nps-changes"></a>NPS 변경 후 구성 확인

>적용 대상: Windows Server(반기 채널), Windows Server 2016

IP 주소 또는 서버 이름 변경 후 NPS 구성을 확인 하려면이 항목을 사용할 수 있습니다.

## <a name="verify-configuration-after-an-nps-ip-address-change"></a>NPS IP 주소 변경 후 구성 확인

서버를 다른 IP 서브넷으로 이동 하는 경우와 같이 NPS 또는 프록시의 IP 주소를 변경 해야 하는 경우가 있을 수 있습니다. 

NPS 또는 프록시 IP 주소를 변경 하는 경우 NPS 배포의 일부를 다시 구성 해야 합니다. 

다음 일반 지침을 사용 하 여 IP 주소 변경이 네트워크에서 NPS RADIUS 서버 및 RADIUS 프록시 서버에 대 한 네트워크 액세스 인증, 권한 부여 또는 계정을 방해 하지 않는지 확인 하는 데 도움을 줍니다.

이러한 절차를 수행 하려면 **관리자**또는 이와 동등한 그룹의 구성원 이어야 합니다.

### <a name="to-verify-configuration-after-an-nps-ip-address-change"></a>NPS IP 주소 변경 후 구성을 확인 하려면

1. 무선 액세스 지점이 나 VPN 서버와 같은 모든 RADIUS 클라이언트를 NPS의 새 IP 주소와 다시 구성 합니다.

2. NPS가 원격 RADIUS 서버 그룹의 구성원 인 경우 nps의 새 IP 주소를 사용 하 여 NPS 프록시를 다시 구성 합니다.

3. SQL Server 로깅을 사용 하도록 NPS를 구성한 경우 SQL Server를 실행 하는 컴퓨터와 NPS 간의 연결이 여전히 제대로 작동 하는지 확인 합니다.

4. NPS와 NPS 프록시 또는 다른 서버나 장치 간의 RADIUS 트래픽을 보호 하기 위해 IPsec을 배포한 경우 NPS의 새 IP 주소를 사용 하려면 고급 보안이 설정 된 Windows 방화벽에서 IPsec 정책 또는 연결 보안 규칙을 다시 구성 합니다.

5. NPS가 멀티홈 이며 특정 네트워크 어댑터에 바인딩되도록 서버를 구성한 경우에는 새 IP 주소를 사용 하 여 NPS 포트 설정을 다시 구성 하십시오.

### <a name="to-verify-configuration-after-an-nps-proxy-ip-address-change"></a>NPS 프록시 IP 주소 변경 후 구성을 확인 하려면

1. 무선 액세스 지점이 나 VPN 서버와 같은 모든 RADIUS 클라이언트를 NPS 프록시의 새 IP 주소로 다시 구성 합니다.

2. NPS 프록시가 멀티홈 이며 특정 네트워크 어댑터에 바인딩하기 위해 프록시를 구성한 경우에는 새 IP 주소를 사용 하 여 NPS 포트 설정을 다시 구성 하십시오.

3. 프록시 서버 IP 주소를 사용 하 여 모든 원격 RADIUS 서버 그룹의 모든 구성원을 다시 구성 합니다. 이 작업을 수행 하려면 NPS 프록시가 RADIUS 클라이언트로 구성 된 각 NPS에서 다음을 수행 합니다.

    a. **NPS (로컬)** 를 두 번 클릭 하 고 **Radius 클라이언트 및 서버**를 두 번 클릭 한 다음 **radius 클라이언트**를 클릭 하 고 세부 정보 창에서 변경할 radius 클라이언트를 두 번 클릭 합니다.

    b. RADIUS 클라이언트 **속성**의 **주소 \(ip 또는 DNS\)** 에 NPS 프록시의 새 IP 주소를 입력 합니다.

4. SQL Server 로깅을 사용 하도록 NPS 프록시를 구성한 경우 SQL Server를 실행 하는 컴퓨터와 NPS 프록시가 제대로 작동 하는지 확인 합니다.

## <a name="verify-configuration-after-renaming-an-nps"></a>NPS 이름을 바꾼 후 구성 확인

서버에 대 한 명명 규칙을 다시 디자인 하는 경우와 같이 NPS 또는 프록시 이름을 변경 해야 하는 경우가 있을 수 있습니다.

NPS 또는 프록시 이름을 변경 하는 경우 NPS 배포의 일부를 다시 구성 해야 합니다. 

다음 일반 지침을 사용 하 여 서버 이름 변경으로 인해 네트워크 액세스 인증, 권한 부여 또는 계정이 중단 되지 않는지 확인 하는 데 도움을 받을 수 있습니다.

이 절차를 수행 하려면 **관리자**또는 이와 동등한 그룹의 구성원 이어야 합니다.

### <a name="to-verify-configuration-after-an-nps-or-proxy-name-change"></a>NPS 또는 프록시 이름을 변경한 후 구성을 확인 하려면

1. NPS가 원격 RADIUS 서버 그룹의 구성원이 고 그룹이 IP 주소가 아닌 컴퓨터 이름으로 구성 된 경우에는 새 NPS 이름을 사용 하 여 원격 RADIUS 서버 그룹을 다시 구성 하십시오.

2. NPS에서 인증서 기반 인증 방법을 배포 하는 경우 이름 변경으로 서버 인증서가 무효화 됩니다. CA (인증 기관) 관리자 로부터 새 인증서를 요청 하거나, 컴퓨터가 도메인 구성원 컴퓨터이 고 도메인 구성원에 대 한 인증서를 자동으로 등록 하는 경우 자동 등록을 통해 새 인증서를 가져오기 위해 그룹 정책를 새로 고칠 수 있습니다. . 그룹 정책를 새로 고치려면:

    a. 명령 프롬프트 또는 Windows PowerShell을 엽니다.

    b. **gpupdate**를 입력한 다음 ENTER 키를 누릅니다.


3. 새 서버 인증서가 있으면 CA 관리자가 이전 인증서를 해지 하도록 요청 합니다. 

     이전 인증서가 해지 되 면 NPS는 이전 인증서가 만료 될 때까지이 인증서를 계속 사용 합니다. 기본적으로 이전 인증서는 최대 1 주 및 10 시간 동안 유효한 상태로 유지 됩니다. 이 기간은 CRL (인증서 해지 목록) 만료 및 TLS (전송 계층 보안) 캐시 시간 만료가 기본값에서 수정 되었는지 여부에 따라 달라질 수 있습니다. 기본 CRL 만료는 1 주일입니다. 기본 TLS 캐시 시간 만료는 10 시간입니다. 

     그러나 새 인증서를 즉시 사용 하도록 NPS를 구성 하려는 경우 새 인증서를 사용 하 여 네트워크 정책을 수동으로 다시 구성할 수 있습니다.

4. 이전 인증서가 만료 된 후 NPS는 자동으로 새 인증서를 사용 하기 시작 합니다. 

5. SQL Server 로깅을 사용 하도록 NPS를 구성한 경우 SQL Server를 실행 하는 컴퓨터와 NPS 간의 연결이 여전히 제대로 작동 하는지 확인 합니다.

