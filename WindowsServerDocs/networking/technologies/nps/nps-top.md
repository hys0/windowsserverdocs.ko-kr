---
title: 네트워크 정책 서버 NPS)
description: 이 항목 네트워크 정책 서버 Windows Server 2016 대 한 개요를 제공 하 고 NPS에 대 한 추가 지침은에 대 한 링크를 포함 합니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 9c7a67e0-0953-479c-8736-ccb356230bde
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 8f48cbdaec82e9e60f734a4a8949082187b13166
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="network-policy-server-nps"></a>네트워크 정책 서버 NPS)

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

Windows Server 2016에 네트워크 정책 서버에 대 한 개요가이 항목을 사용할 수 있습니다.

>[!NOTE]
>이 항목 외에 다음과 같은 NPS 문서를 사용할 수 있습니다.
> - [네트워크 정책 서버에 대 한 유용한 정보](nps-best-practices.md)
> - [네트워크 정책 서버 시작](nps-getstart-top.md)
> - [네트워크 정책 서버 계획](nps-plan-top.md)
> - [네트워크 정책 서버를 배포 합니다.](nps-deploy.md)
> - [네트워크 정책 서버 관리](nps-manage-top.md)
> - [정책 (NPS) 서버 Cmdlet 네트워크](https://technet.microsoft.com/library/jj872739.aspx) Windows 10 및 Windows Server 2016 용
> - [네트워크에서 Windows PowerShell 정책 (NPS) 서버 Cmdlet](https://technet.microsoft.com/library/jj872739.aspx) .1 Windows 8 및 Windows Server 2012 r 2에 대 한
> - [Windows PowerShell Cmdlet NPS](https://technet.microsoft.com/library/jj872739.aspx) Windows 8 및 Windows Server 2012에 대 한

네트워크 NPS 정책 서버 () 조직 전체 네트워크 연결 요청 인증과 대 한 액세스 정책을 적용을 만들고 수 있습니다.

또한 연결 요청 잔액을 로드할 하 고 인증과 대 한 올바른 도메인에 게 전달할 수 있도록 원격 NPS 또는 기타 RADIUS 서버에 연결 요청을 전송 하도록 RADIUS(Remote Authentication Dial-In User Service) (RADIUS) 프록시 NPS 구성할 수 있습니다.

NPS 중앙 구성 하 고 네트워크 액세스 인증, 권한 및 다음과 같은 기능과 함께 계정 관리할 수 있습니다.

- **RADIUS 서버**합니다. NPS 중앙 집중식된 인증, 권한 및 계정에 대 한 수행 무선 인증 스위치를 원격 액세스 전화 접속 및 가상 개인 네트워크 (VPN) 연결 합니다. NPS RADIUS 서버를 사용 하면에 NPS RADIUS 클라이언트로 무선 액세스 포인트 등 네트워크 액세스 서버 및 VPN 서버의 구성 합니다. NPS 사용 하 여 연결 요청을 승인 하는 네트워크 정책을 구성할 수도 있으며 NPS 기록 계정 정보 또는 Microsoft SQL Server 데이터베이스 로컬 하드 디스크에 파일을 기록 하 않도록 RADIUS 계정을 구성할 수 있습니다. 자세한 내용은 참조 [RADIUS 서버](#bkmk_server)합니다.
- **RADIUS 프록시**합니다. NPS RADIUS 프록시도를 사용 하면 연결 하 고 연결 요청을 전송 하 고 싶은 RADIUS 서버를 다른 RADIUS 서버에 전달 하도록 요청 NPS 서버 알려주는 연결 요청 정책 구성 합니다. 또한 NPS 계정 데이터를 원격 RADIUS 서버 그룹에서 하나 또는 여러 개의 컴퓨터에서 기록 전달를 구성할 수 있습니다. 다음 항목을 참조 NPS RADIUS 프록시 서버를 구성 합니다. 자세한 내용은 참조 [RADIUS 프록시](#bkmk_proxy)합니다.
    - [구성 연결 요청 정책](nps-crp-configure.md)
- **RADIUS 계정을**합니다. NPS 로컬 로그 파일 또는 Microsoft SQL Server의 시내 / 원격 인스턴스 이벤트 기록를 구성할 수 있습니다. 자세한 내용은 참조 [NPS 로깅](#bkmk_logging)합니다.

>[!IMPORTANT]
>네트워크 액세스 보호 \(NAP\), 건강 등록 기관 \(HRA\) 및 호스트 자격 증명 인증 프로토콜 \(HCAP\) Windows Server 2012 r 2에는 사용 되지 않으며은 Windows Server 2016에 사용할 수 없습니다. Windows Server 2016 이전 운영 체제를 사용 하 여 NAP 배포를 사용 하는 경우 Windows Server 2016에 NAP 배포를 마이그레이션할 수 없습니다.

이러한 기능 중 조합으로 NPS 구성할 수 있습니다. 예를 들어 VPN 연결에 대 한 RADIUS 서버 및 인증과 다른 도메인에 대 한 원격 RADIUS 서버 그룹의 회원 일부 연결 요청을 전송 하도록 RADIUS 프록시도도 NPS 서버를 구성할 수 있습니다.

## <a name="windows-server-editions-and-nps"></a>Windows Server 제품 및 NPS

NPS 설치 하는 Windows Server의 버전에 따라 다양 한 기능을 제공 합니다.

### <a name="windows-server-2016-datacenter-edition"></a>Windows Server 2016 Datacenter Edition

Windows Server 2016 데이터 센터에 nps RADIUS 클라이언트 및 원격 RADIUS 서버 그룹 무제한을 구성할 수 있습니다. 또한, IP 주소 범위를 지정 하 여 RADIUS 클라이언트 구성할 수 있습니다.

### <a name="windows-server-2016-standard-edition"></a>Windows Server 2016 Standard Edition

Windows Server 2016 표준에서 NPS 최대 50 RADIUS 클라이언트 및 최대 원격 RADIUS 서버 그룹 2를 구성할 수 있습니다. 정식된 도메인 이름 또는 주소를 사용 하 여 RADIUS 클라이언트를 정의할 수 있지만 IP 주소 범위를 지정 하 여 그룹 RADIUS 클라이언트의 정의 수 없습니다. 정식된 도메인 이름 RADIUS 클라이언트의 여러 IP 주소를 확인, NPS 서버 시스템 DNS (도메인 이름) 쿼리에서 반환 첫 번째 IP 주소를 사용 합니다.

다음 섹션 RADIUS 서버 및 프록시 NPS에 대 한 자세한 정보를 제공합니다.

## <a name="radius-server-and-proxy"></a>RADIUS 서버 및 프록시

NPS RADIUS 서버, RADIUS 프록시 또는 둘 다로 사용할 수 있습니다.

### <a name="bkmk_server"></a>RADIUS 서버

NPS은 표준 RADIUS 2865 Rfc 및 2866 인터넷 엔지니어링 작업 힘 \(IETF\)로 지정 된 Microsoft 구현 합니다. RADIUS 서버, NPS 네트워크 액세스를 스위치를 전화 접속 인증 무선 및 가상 개인 네트워크 \(VPN\) 원격 액세스 라우터에 연결 등의 다양 한 종류에 대 한 중앙 집중식된 연결, 인증, 인증과 계정 수행 합니다.

>[!NOTE]
>에 대 한 내용은 배포 NPS RADIUS 서버, [네트워크 정책 서버 배포](nps-deploy.md)합니다.

NPS 무선 다른 유형의 설정, 전환, 원격 액세스 또는 VPN 장치를 사용할을 수 있습니다. NPS와 Windows Server 2016에서 사용할 수 있는 원격 액세스 서비스를 사용할 수 있습니다.

NPS 된 Active Directory Domain Services를 사용 하 여 \ (AD DS \) 도메인 또는 로컬 보안 계정을 관리자 (삼로) 사용자 계정 인증 연결 시도 대 한 사용자 자격 증명을 데이터베이스 합니다. NPS 실행 하는 서버 AD DS 도메인의 회원 있으면 NPS는 디렉터리 서비스를 사용 하 여 사용자 계정 데이터베이스도 하며 단일 솔루션 로그온의 일부입니다. 네트워크 액세스를 제어 자격 증명에 동일한 설정 사용 됩니다 \ (인증 및는 network\에 대 한 액세스 권한을 부여) 및 AD DS 도메인 로그온 합니다.

>[!NOTE]
>NPS는 사용자 계정 및 네트워크 정책 전화 접속 속성 승인할 연결을 사용 합니다.

인터넷 서비스 공급자 \(ISPs\)와 조직의 네트워크 액세스를 유지 하는 모든 종류의 액세스 네트워크 관리를 사용 하는 네트워크 access 장치의 종류에 관계 없이 한 지점에서 관리 하는 향상 된 문제를 있습니다. RADIUS 표준은 같은 및 다른 유형의 환경에서이 기능을 지원 합니다. RADIUS 인증과 계정 요청 RADIUS 서버에 전송 하 네트워크 액세스 장치 (RADIUS 클라이언트로 사용) 사용 하는 클라이언트 서버가 프로토콜입니다.

RADIUS 서버 사용자 계정 정보에 액세스할 수 있고 네트워크 액세스 인증 자격 증명을 확인할 수 있습니다. 사용자 자격 증명이 인증 연결 시도 권한이 부여 된 경우 RADIUS 서버 지정된 조건에 따라 사용자에 게 액세스 권한을 부여 하 고 네트워크 액세스 연결 계정 로그에 기록 됩니다. 네트워크 액세스 사용자 인증 인증과 계정 데이터를 수집 하 고 각 액세스 서버의 아니라를 중앙 위치에 유지 RADIUS 사용할 수 있게 합니다.

#### <a name="using-nps-as-a-radius-server"></a>NPS RADIUS 서버도 사용 하 여

NPS RADIUS 서버를 사용 하면 다음과 같습니다.

- 사용자 계정 데이터베이스와 AD DS 도메인 또는 삼로 로컬 사용자 계정 데이터베이스를 사용 하 여 액세스 클라이언트는 합니다. 
- 여러 전화 접속 서버에 VPN 서버의에 대 한 원격 액세스를 사용 하는 또는 접속 라우터 하 고 네트워크 정책 및 로깅 및 계정 연결 구성을 집중 하려고 합니다. 
- 위탁 하는 경우 전화 접속, VPN 또는 서비스 공급자에 게 무선 액세스 합니다. 액세스 서버 인증 하 고 연결 조직의 회원 수행한 승인할 RADIUS을 사용 합니다.
- 인증, 인증과 계정 액세스 서버 다른 유형의 집합에 대 한 중앙에 집중 하려고 합니다.

다음 그림으로 표시 되 NPS RADIUS 서버 액세스 클라이언트 다양 합니다. 

![NPS RADIUS 서버](../../media/Nps-Server/Nps-Server.jpg)

### <a name="bkmk_proxy"></a>프록시 RADIUS

RADIUS 프록시 NPS NPS RADIUS 서버 다른를 인증과 계정 메시지 전달합니다. 클라이언트 RADIUS 간에 RADIUS 프록시 RADIUS 경로 제공 하기 위해 메시지 NPS 사용할 수 있습니다 \ (네트워크 액세스 servers\ 라고도 함)와 사용자 인증, 권한 및 계정 연결 시도 대 한 수행 RADIUS 서버 합니다. 

RADIUS 프록시도 사용 하는 경우 중앙 전환 또는 RADIUS 액세스 및 계정 메시지 흘러 통해 라우팅 지점 NPS입니다. NPS 정보 계정 전달 되는 메시지에 대 한 로그에 기록 됩니다.

#### <a name="using-nps-as-a-radius-proxy"></a>NPS RADIUS 프록시도 사용 하 여

NPS RADIUS 프록시도 사용할 수 있습니다 경우:

- 서비스 공급자를 여러 고객에 게 외부 위탁된 전화 접속, VPN 또는 무선 네트워크 액세스 서비스를 제공 하 게 됩니다. 사용자 Nas NPS RADIUS 프록시 연결 요청을 보냅니다. 연결 요청에 사용자 이름의 영역 부분에 따라, NPS RADIUS 프록시 고객이 유지 관리 되는 RADIUS 서버에 연결 요청 전달 하 고 수 있는 인증 고 권한을 부여 연결 시도.
- 인증과 NPS 서버 인 회원 도메인 또는 다른에 NPS 서버 인 회원 도메인 양방향 신뢰 하는 도메인의 회원 하지 않은 사용자 계정에 대 한 권한을 제공 하려고 합니다. 신뢰할 수 없는 도메인, 단방향 신뢰할 수 있는 도메인 및 기타 숲에서 계정 포함 됩니다. 요청을 보낼 자신의 연결 NPS RADIUS 서버에 대 한 액세스 서버를 구성 하는 대신 NPS RADIUS 프록시 자신의 연결 요청을 보낼 수 있도록 구성할 수 있습니다. NPS RADIUS 프록시 사용자 이름의 이름을 영역 부분을 사용 하 여 올바른 도메인 또는 숲 NPS 서버에 요청을 전달 합니다. 사용자 계정에 한 도메인 또는 숲 Nas 다른 도메인 또는 숲에 대해 인증할 수 있습니다.에 대 한 연결 시도 합니다.
- 데이터베이스 Windows 계정 데이터베이스를 사용 하 여 인증과 수행 하려고 합니다. 이 경우 연결 요청 지정한 영역 이름과 일치 하는 다른 사용자 계정 및 인증 데이터 데이터베이스에 액세스할 수 있는 RADIUS 서버, 전달 됩니다. 다른 사용자 데이터베이스의 예로 Novell 디렉터리 서비스 (NDS) 및 구조적 쿼리 SQL (언어) 데이터베이스 있습니다.
- 많은 수의 연결 요청을 처리할 하려고 합니다. 이 경우 대신 구성 RADIUS 클라이언트를 시도 하는 연결 및 계정 요청 여러 RADIUS 서버, NPS RADIUS 프록시 연결 및 계정 요청을 보낼 수 있도록 구성할 수 있습니다. NPS RADIUS 프록시 연결 로드 동적으로 조정 하 고 계정 여러 RADIUS 서버에 요청 많은 RADIUS 클라이언트 처리와 초당 인증을 높여 줍니다.
- 방화벽 인트라넷 최소화 및 RADIUS 인증과 외부 위탁된 서비스 공급자에 대 한 권한을 제공 하려고 합니다. 주변 네트워크 (있는 간을 인트라넷과 인터넷) 및 인트라넷 간에 인트라넷 방화벽이입니다. 주변 네트워크 NPS 서버를 배치 하 여 주변 네트워크 사이의 인트라넷 방화벽 간에 NPS 서버와 여러 도메인 컨트롤러에 대 한 교통량을 허용 해야 합니다. NPS 서버, NPS 프록시 바꿔서 방화벽 간에 NPS 프록시와 인트라넷 하나 또는 여러 개의 NPS 서버에만 RADIUS 교통량을 허용 해야 합니다.

다음 그림 NPS RADIUS 클라이언트 및 서버 RADIUS 간의 RADIUS 프록시 표시 됩니다.

![NPS RADIUS 프록시도](../../media/Nps-Proxy/Nps-Proxy.jpg)


Nps, 조직 제어 사용자 인증, 권한 및 계정을 유지 하면서 또한 서비스 공급자에 대 한 원격 액세스 infrastructure를 외부 수 있습니다.

다음과 같은 경우에 대 한 NPS 구성 만들 수 있습니다.

- 무선 액세스
- 조직 전화 접속 또는 가상 VPN (사설망)에 대 한 원격 액세스
- 외부 위탁된 전화 접속 또는 무선 액세스
- 인터넷 액세스
- 인증 된 리소스에 액세스할 수 엑스트라넷 비즈니스 파트너를 위해

## <a name="radius-server-and-radius-proxy-configuration-examples"></a>RADIUS 서버 및 RADIUS 프록시 구성 예제

다음과 같은 구성 예 NPS RADIUS 서버와 RADIUS 프록시 구성 하는 방법을 설명 합니다.

**NPS RADIUS 서버**합니다. 여기에서 NPS RADIUS 서버도 구성 되어 기본 연결 요청 정책을 유일한 구성 된 정책 및 로컬 NPS 서버에서 모든 연결 요청을 처리 됩니다. NPS 서버 인증 되 고 신뢰할 수 있는 도메인와 NPS 서버 도메인에 있는 계정이 있는 사용자에 게 권한을 부여 수 있습니다.

**NPS RADIUS 프록시**합니다. 여기에서 서버 NPS RADIUS 프록시 신뢰할 수 없는 도메인 두 가지 원격 RADIUS 서버 그룹에 연결 요청 전달 하으로 구성 됩니다. 기본 연결 요청 정책을 삭제 하 고 각 두 신뢰할 수 없는 도메인 앞으로 요청에 두 가지 새로운 연결 요청 정책을 만들어집니다. 여기에서 NPS 로컬 서버에 연결 요청을 처리 하지 않습니다. 

**NPS RADIUS 서버와 RADIUS 프록시**합니다. 연결 요청 로컬로 처리 됩니다으로 지정 하는 기본 연결 요청 정책을 뿐 아니라 NPS 나 다른 RADIUS 서버 신뢰할 수 없는 도메인에 연결 요청을 전달 하는 새 연결 요청 정책을 만들어집니다. 이 두 번째 정책은 프록시 정책을 라고 합니다. 여기에서 프록시 정책 정책 정렬된 목록에서 첫 번째 표시 됩니다. 연결 요청 일치 하는 프록시 정책을 연결 요청 원격 RADIUS 서버 그룹에 RADIUS 서버에 게 전달 됩니다. 연결 요청 프록시 정책 일치 하지 않는 기본 연결 요청 정책을 일치 하는 경우, NPS 로컬 서버에 연결 요청을 처리 합니다. 연결 요청 중 하나 정책 일치 하지 않을 경우 삭제 됩니다.

**NPS RADIUS 서버 계정 서버를 원격으로**합니다. 여기에서 로컬 NPS 서버 계정 작업을 수행 하도록 구성 되지 않은 및 기본 연결 요청 정책을 하도록 수정 RADIUS 계정 메시지 NPS 서버 또는 다른 RADIUS 서버 원격 RADIUS 서버 그룹에 전달 됩니다. 계정 메시지를 전달 있지만 인증과 메시지를 전달 되지 않습니다 및 로컬 NPS 서버 로컬 도메인에 대 한 이러한 기능을 수행 하 고 신뢰할 수 있는 모든 도메인.

**NPS RADIUS Windows 사용자 지도를 원격으로**합니다. 여기에서 NPS RADIUS 서버를 원격으로 인증 요청 인증을 위해 Windows 로컬 사용자 계정을 사용 하는 동안 전달 하 여 RADIUS 서버 및 각 개별 연결 요청에 대 한 프록시 RADIUS로 작동 합니다. 이 구성은 RADIUS Windows 사용자 매핑 특성을 원격 연결 요청 정책 조건으로 구성 구현 합니다. \ (또한, 사용자 계정 로컬로 만들어야 원격 RADIUS 서버 인증을 수행 하는 원격 사용자 계정 이름이 같은 RADIUS 서버에서. \)

## <a name="configuration"></a>구성

구성 NPS RADIUS 서버, NPS 콘솔 또는 서버 관리자에서 표준 구성 또는 고급 구성 사용할 수 있습니다. 고급 구성 NPS RADIUS 프록시를 구성 하려면 사용 해야 합니다.

### <a name="standard-configuration"></a>표준 구성

표준 구성 된 NPS 다음과 같은 경우에 대 한 구성 하는 데 도움이 되는 마법사 제공 됩니다.

- 전화 접속 또는 VPN 연결에 대 한 RADIUS 서버
- 802.1 X 유선 또는 무선 연결을 위한 RADIUS 서버

마법사를 사용 하 여 NPS로 구성 하려면 NPS console을 엽니다 앞에서 설명한 시나리오 중 하나를 선택 하 고 마법사 열리는 링크를 클릭 한 다음 합니다.

### <a name="advanced-configuration"></a>고급 구성

고급 구성을 사용 하면 수동으로 RADIUS 서버 또는 RADIUS 프록시 NPS를 구성 합니다. 

고급 구성을 사용 하 여 NPS 구성, NPS 콘솔을 열고 옆에 있는 화살표를 클릭 **고급 구성** 이 섹션을 확장 합니다.

다음과 같은 고급 구성 항목이 제공 됩니다.

#### <a name="configure-radius-server"></a>구성 RADIUS 서버

NPS RADIUS 서버를 구성 하려면 RADIUS 고객과 네트워크 정책 RADIUS 계정을 구성 해야 합니다.

이 구성에 지침은 다음과 같은 항목을 참조 합니다.

- [구성 RADIUS 클라이언트](nps-radius-clients-configure.md)
- [네트워크 정책을 구성합니다](nps-np-configure.md)
- [네트워크 정책 서버 계정 구성](nps-accounting-configure.md)

#### <a name="configure-radius-proxy"></a>프록시 RADIUS 구성

NPS RADIUS 프록시를 구성 하려면 RADIUS 클라이언트 원격 RADIUS 서버 그룹와 연결 요청 정책 구성 해야 합니다.

이 구성에 지침은 다음과 같은 항목을 참조 합니다.

- [구성 RADIUS 클라이언트](nps-radius-clients-configure.md)
- [원격 RADIUS 서버 그룹 구성](nps-crp-rrsg-configure.md)
- [구성 연결 요청 정책](nps-crp-configure.md)

## <a name="bkmk_logging"></a>NPS 로그인

로그인 NPS RADIUS 계정을 라고도 합니다. 구성 NPS NPS RADIUS 서버, 프록시 또는이 구성 조합으로 사용 되 든 요구 사항에 로그인 합니다.

NPS 로깅 구성를 기록 하 고 본 이벤트 뷰어를 사용 하 고 다음 다른 정보를 결정 이벤트 로그인 하려면 구성 해야 합니다. 또한, 로컬 컴퓨터에 저장 된 텍스트 로그 파일에 또는 SQL Server 데이터베이스 로컬 컴퓨터 또는 원격 컴퓨터에 사용자 인증과 계정 정보를 기록 것인지 여부를 결정 해야 합니다.

자세한 내용은 참조 [네트워크 정책 서버 계정과 구성](nps-accounting-configure.md)합니다.
