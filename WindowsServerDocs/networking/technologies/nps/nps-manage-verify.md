---
title: NPS 변경 된 후 구성 확인
description: 서버에 IP 주소 또는 이름 변경 후 Windows Server 2016 네트워크 정책 서버 구성을 확인 하려면이 항목에서는 사용할 수 있습니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: fc77450e-2af1-47ba-bb23-1fd36d9efdbf
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 144e414e32d413e4863b90ada671753155bc96d7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59880674"
---
# <a name="verify-configuration-after-nps-changes"></a>NPS 변경 된 후 구성 확인

>적용 대상: Windows Server (반기 채널), Windows Server 2016

이 항목에서는 구성 되었는지 확인 하려면 NPS 서버에 IP 주소 또는 이름 변경 후에 사용할 수 있습니다.

## <a name="verify-configuration-after-an-nps-ip-address-change"></a>NPS IP 주소 변경 후 구성을 확인 합니다.

경우도 NPS 또는 서버의 다른 IP 서브넷을 이동할 때 같은 프록시 IP 주소를 변경 해야 합니다. 

NPS 또는 프록시 IP 주소를 변경 하는 경우 NPS 배포의 일부를 다시 구성 하는 데 필요한 것입니다. 

네트워크 액세스 인증, 권한 부여 또는 계정 NPS RADIUS 서버 및 RADIUS 프록시 서버에 대 한 네트워크에 IP 주소 변경을 방해 하지 않습니다 확인 하는 데 도움이 되도록 다음 일반 지침을 따르세요.

멤버 여야 합니다 **관리자**, 또는 이와 동등한이 절차를 수행 하 합니다.

### <a name="to-verify-configuration-after-an-nps-ip-address-change"></a>NPS IP 주소 변경 후 구성을 확인 하려면

1. 무선 액세스 지점 및 NPS의 새 IP 주소를 사용 하 여 VPN 서버와 같은 모든 RADIUS 클라이언트를 다시 구성 합니다.

2. NPS는 원격 RADIUS 서버 그룹의 구성원 인 경우 NPS의 새 IP 주소를 사용 하 여 NPS 프록시를 다시 구성 합니다.

3. SQL Server 로깅을 사용 하도록 NPS를 구성한 경우에 SQL 서버와 NPS를 실행 하는 컴퓨터 간의 연결 올바르게 작동 하는지 확인 합니다.

4. 에 NPS 및는 NPS 프록시 또는 다른 서버 또는 장치 간에 RADIUS 트래픽을 보호 하는 IPsec을 배포한 경우에 IPsec 정책 또는 NPS의 새 IP 주소를 사용 하도록 고급 보안이 포함 된 Windows 방화벽에서 연결 보안 규칙 다시 구성 합니다.

5. NPS 멀티홈을 특정 네트워크 어댑터에 바인딩하도록 서버를 구성한 경우에 새 IP 주소를 사용 하 여 NPS 포트 설정을 다시 구성 합니다.

### <a name="to-verify-configuration-after-an-nps-proxy-ip-address-change"></a>NPS 후 구성을 확인 하려면 프록시 IP 주소 변경

1. 무선 액세스 지점 및 NPS 프록시의 새 IP 주소를 사용 하 여 VPN 서버와 같은 모든 RADIUS 클라이언트를 다시 구성 합니다.

2. NPS 프록시 멀티홈을 특정 네트워크 어댑터에 바인딩하는 프록시를 구성한 경우에 새 IP 주소를 사용 하 여 NPS 포트 설정을 다시 구성 합니다.

3. 프록시 서버 IP 주소를 사용 하 여 모든 원격 RADIUS 서버 그룹의 모든 멤버를 다시 구성 합니다. 각 NPS RADIUS 클라이언트로 구성 된 NPS 프록시 있는에서이 작업을 위해:

    a. 두 번 클릭 **NPS (로컬)** 를 두 번 클릭 **RADIUS 클라이언트 및 서버**, 클릭 **RADIUS 클라이언트**, 다음 세부 정보 창에서 RADIUS 클라이언트를 두 번 클릭 하 고는 변경 하려고 합니다.

    b. RADIUS 클라이언트에서 **속성**의 **주소 \(IP 또는 DNS\)**, NPS 프록시의 새 IP 주소를 입력 합니다.

4. SQL Server 로깅을 사용 하도록 NPS 프록시를 구성한 경우에 SQL Server와 NPS 프록시를 실행 하는 컴퓨터 간의 연결 올바르게 작동 하는지 확인 합니다.

## <a name="verify-configuration-after-renaming-an-nps"></a>NPS의 이름을 바꾼 후 구성 확인

NPS 또는 프록시 서버에 대 한 명명 규칙을 다시 디자인할 때 등의 이름을 변경 해야 하는 경우 상황 수 있습니다.

NPS 또는 프록시 이름, 변경 하는 경우 NPS 배포의 일부를 다시 구성 하는 데 필요한 것입니다. 

네트워크 액세스 인증, 권한 부여 또는 회계 서버 이름 변경을 방해 하지 않습니다 확인 하는 데 도움이 되도록 다음 일반 지침을 따르세요.

멤버 여야 합니다 **관리자**, 또는 이와 동등한이 절차를 수행 하려면.

### <a name="to-verify-configuration-after-an-nps-or-proxy-name-change"></a>NPS 또는 프록시 이름 변경 이후 구성을 확인 하려면

1. NPS는 원격 RADIUS 서버 그룹의 멤버인 경우 IP 주소 대신 컴퓨터 이름을 사용 하 여 그룹 구성 되어 있으면 새 NPS 이름의 원격 RADIUS 서버 그룹을 다시 구성 합니다.

2. 인증서 기반 인증 방법을 NPS로 배포 된 경우 이름이 변경 된 서버 인증서를 무효화 합니다. 인증 기관 (CA) 관리자에서 새 인증서를 요청할 수 있습니다 또는 자동 등록을 통해 새 인증서를 얻는 그룹 정책을 새로 고칠 수 컴퓨터는 도메인 구성원 컴퓨터를 도메인 구성원에 자동 등록 인증서 인 경우 . 그룹 정책을 새로 고치려면:

    a. 명령 프롬프트 또는 Windows PowerShell을 엽니다.

    b. **gpupdate**를 입력한 다음 ENTER 키를 누릅니다.


3. 새 서버 인증서를 만든 후에 CA 관리자가 이전 인증서를 해지 하는 요청 합니다. 

     이전 인증서가 해지 후 NPS 계속 이전 인증서가 만료 될 때까지 사용 합니다. 기본적으로 이전 인증서 유효한 상태로 유지 한 주 10 시간 최대 시간입니다. 이 기간 동안 해당 기본값에서 인증서 해지 목록 (CRL) 만료 및 전송 계층 보안 (TLS) 캐시 시간 만료가 수정 여부에 따라 달라질 수 있습니다. 기본 CRL 만료는 1 주일; TLS 기본값 10 시간 만료 시간을 캐시 합니다. 

     그러나 즉시 새 인증서를 사용 하는 NPS를 구성 하려는 경우 수동으로 다시 구성할 수 있습니다 새 인증서를 사용 하 여 네트워크 정책입니다.

4. 이전 인증서가 만료 되 면 NPS를 자동으로 새 인증서를 사용 하 여 시작 합니다. 

5. SQL Server 로깅을 사용 하도록 NPS를 구성한 경우에 SQL 서버와 NPS를 실행 하는 컴퓨터 간의 연결 올바르게 작동 하는지 확인 합니다.

