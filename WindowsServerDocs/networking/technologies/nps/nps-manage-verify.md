---
title: 구성 NPS 서버 변경 된 후 확인
description: 서버에 IP 주소 또는 이름을 변경 후 Windows Server 2016 네트워크 정책 서버 구성 확인 하려면이 항목을 사용할 수 있습니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: fc77450e-2af1-47ba-bb23-1fd36d9efdbf
ms.author: pashort
author: shortpatti
ms.openlocfilehash: f4d7e003fb037d18c5e5f2036a419383885eaf9e
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="verify-configuration-after-nps-server-changes"></a>구성 NPS 서버 변경 된 후 확인

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

서버에 IP 주소 또는 이름을 변경 후 NPS 원인일 수를 확인 하려면이 항목을 사용할 수 있습니다.

## <a name="verify-configuration-after-an-nps-server-ip-address-change"></a>구성 NPS 서버 IP 주소 변경 후 확인

경우도 NPS 서버 또는 프록시 서버를 다른 IP 서브넷 이동할 때 등의 IP 주소를 변경 해야 합니다. 

NPS 서버 또는 프록시 IP 주소를 변경 하면 NPS 배포의 일부를 다시 구성 하는 데 필요한입니다. 

네트워크 액세스 인증, 인증, 또는 계정 NPS RADIUS 서버와 RADIUS 프록시 서버에 대 한 네트워크에는 IP 주소 변경 중단 되지 않고 확인 하는 데 도움이 되도록 일반 다음 지침을 사용 합니다.

소속 있어야 **관리자**, 또는 해당이 절차를 수행 합니다.

### <a name="to-verify-configuration-after-an-nps-server-ip-address-change"></a>구성을 NPS 후 확인 하려면 다음 서버 IP 주소 변경

1. 무선 액세스 포인트 및 VPN 서버의 NPS 서버 새 IP 주소와 같이 모든 RADIUS 클라이언트를 다시 합니다.

2. NPS 서버를 원격 RADIUS 서버 그룹의 회원 NPS 프록시 NPS 서버 새 IP 주소를 다시 구성 합니다.

3. SQL Server 로깅 사용 하 여 NPS 서버 구성한 경우 SQL Server 및 NPS 서버를 실행 하는 컴퓨터 사이의 연결이 제대로 작동 하는지 확인 합니다.

4. RADIUS 트래픽 NPS 서버와 NPS 프록시 또는 기타 서버 또는 디바이스 간에 보안 IPsec 배포한 IPsec 정책이 나 방침 NPS 서버 새 IP 주소를 사용 하 여 고급 보안이 포함된 Windows 방화벽 연결 보안 규칙 다시 구성 합니다.

5. NPS 서버는 다중 홈 경우 특정 네트워크 어댑터에 연결 하는 서버 구성한 경우 새 IP 주소를 사용 하 여 NPS 포트 설정을 다시 구성 합니다.

### <a name="to-verify-configuration-after-an-nps-proxy-ip-address-change"></a>프록시 IP 주소 변경 NPS 후 구성 되었는지 확인 하려면

1. 무선 액세스 포인트 및 VPN 서버의 NPS 프록시의 새 IP 주소와 같이 모든 RADIUS 클라이언트를 다시 합니다.

2. NPS 프록시 다중 홈은 특정 네트워크 어댑터에 연결 하는 프록시 구성한 경우 새 IP 주소를 사용 하 여 NPS 포트 설정을 다시 구성 합니다.

3. 프록시 서버 IP 주소를 가진 모든 원격 RADIUS 서버 그룹의 모든 구성원이 다시 구성 합니다. NPS 프록시 RADIUS 클라이언트도 구성 된 각 NPS 서버에이 작업을 수행 합니다.

    한 합니다. 두 번 클릭 **NPS (로컬)**를 두 번 클릭 **RADIUS 클라이언트 및 서버**, 클릭 **RADIUS 클라이언트**, 다음 세부 정보 창에 변경 하려는 RADIUS 클라이언트를 두 번 클릭 합니다.

    B 합니다. RADIUS 클라이언트에서 **속성**에 **주소 \(IP or DNS\)**, NPS 프록시의 새 IP 주소를 입력 합니다.

4. SQL Server 로깅 사용 하 여 NPS 프록시 구성한 경우 SQL Server 및 NPS 프록시 실행 중인 컴퓨터 간의 연결이 제대로 작동 하는지 확인 합니다.

## <a name="verify-configuration-after-renaming-an-nps-server"></a>구성 NPS 서버 이름을 바꾼 후 확인

NPS 서버 또는 프록시 서버에 대해 명명 규칙 재설계 때 등의 이름을 변경 하려는 경우 상황 수 있습니다.

NPS 서버 또는 프록시 이름 변경 하면 NPS 배포의 일부를 다시 구성 하는 데 필요한입니다. 

서버 이름 변경 네트워크 액세스 인증, 인증, 또는 계정 중단 되지 않고 확인 하는 데 도움이 되도록 일반 다음 지침을 사용 합니다.

소속 있어야 **관리자**, 또는 해당이 절차를 수행 합니다.

### <a name="to-verify-configuration-after-an-nps-server-or-proxy-name-change"></a>NPS 서버 또는 프록시 이름 변경 후 구성 되었는지 확인 하려면

1. NPS 서버 원격 RADIUS 서버 그룹의 회원 이며 그룹 구성 된 IP 주소를 사용 하지 않고 컴퓨터 이름, 새 NPS 서버 이름의 원격 RADIUS 서버 그룹 다시 구성 합니다.

2. 가지 옵션이 인증 방법을 NPS 서버에 배포 되 면 이름 변경 서버 인증서를 무효화 됩니다. 인증 기관 관리자에서 새 인증서를 요청 또는 컴퓨터가 도메인 회원 컴퓨터와 하면 도메인 회원 자동 등록 인증서를 통해 자동 등록 새 인증서를 얻는 그룹 정책 복구할 수 있습니다. 그룹 정책을 복구 하려면:

    한 합니다. Windows PowerShell 또는 명령 프롬프트를 엽니다.

    B 합니다. 입력 **gpupdate**, ENTER 키를 누릅니다.


3. 새 서버 인증서를 사용 하는 후 캐나다 관리자 취소할 오래 된 인증서를 요청 합니다. 

     이전 인증서가 해지 한 후 이전 인증서가 만료 될 때까지 사용할 NPS 계속 합니다. 기본적으로 이전 인증서 유효 최대 시간을 한 주 10 시간에 대 한 합니다. 이 시간 동안 기본값으로에서 해지 CRL 인증서 목록 () 만료 및 Transport Layer Security TLS () 캐시 시간이 만료 있는 수정 여부에 따라 달라질 수 있습니다. 기본 CRL 만료는 1 주일 후 부터는; 기본 TLS 시간이 만료는 10 시간을 캐시 합니다. 

     그러나 바로 새 인증서를 사용 하 여 NPS 구성 하려면 새 인증서를 사용 하 여 네트워크 정책을 수동으로 재구성 수 합니다.

4. 이전 인증서가 만료 되 면 NPS을 자동으로 새 인증서를 사용 하 여 시작 합니다. 

5. SQL Server 로깅 사용 하 여 NPS 서버 구성한 경우 SQL Server 및 NPS 서버를 실행 하는 컴퓨터 사이의 연결이 제대로 작동 하는지 확인 합니다.

