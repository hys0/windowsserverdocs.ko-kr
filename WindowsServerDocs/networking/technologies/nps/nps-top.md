---
title: NPS(네트워크 정책 서버)
description: 이 항목에서는 Windows Server 2016 및 Windows Server 2019에 네트워크 정책 서버 개요를 제공 하 고 NPS에 대 한 추가 설명서 링크가 포함 되어 있습니다.
manager: dougkim
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 9c7a67e0-0953-479c-8736-ccb356230bde
ms.author: pashort
author: shortpatti
ms.date: 06/20/2018
ms.openlocfilehash: 515012a21ba6e90abe2c4db2150fd1feaad06677
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66812372"
---
# <a name="network-policy-server-nps"></a>NPS(네트워크 정책 서버)

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2019

이 항목에서는 Windows Server 2016 및 Windows Server 2019에 네트워크 정책 서버에 대 한 개요에 사용할 수 있습니다. NPS는 Windows Server 2016 및 Server 2019에 네트워크 정책 및 액세스 서비스 (NPAS) 기능을 설치할 때 설치 됩니다.

> [!NOTE]
> 이 항목 외에 다음 NPS 설명서는 사용할 수 있습니다.
> - [네트워크 정책 서버에 대 한 유용한 정보](nps-best-practices.md)
> - [네트워크 정책 서버를 사용 하 여 시작](nps-getstart-top.md)
> - [네트워크 정책 서버 계획](nps-plan-top.md)
> - [네트워크 정책 서버를 배포 합니다.](nps-deploy.md)
> - [네트워크 정책 서버 관리](nps-manage-top.md)
> - [네트워크 정책 (NPS) 서버 Cmdlet Windows PowerShell에서](https://technet.microsoft.com/library/jj872739.aspx) Windows Server 2016 및 Windows 10
> - [네트워크 정책 (NPS) 서버 Cmdlet Windows PowerShell에서](https://technet.microsoft.com/library/jj872739.aspx) Windows Server 2012 R2 및 Windows 8.1 대 한
> - [Windows PowerShell의 NPS Cmdlet](https://technet.microsoft.com/library/jj872739.aspx) Windows Server 2012 및 Windows 8

네트워크 정책 서버(NPS)를 사용하면 연결 요청 인증 및 권한 부여를 위해 조직 전체의 네트워크 액세스 정책을 생성하여 적용할 수 있습니다.

요청의 부하를 분산 연결 하 고 인증에 대 한 올바른 도메인에 전달할 수 있도록 다른 RADIUS 서버 또는 원격 NPS 연결 요청을 전달 하는 전화 접속 사용자 서비스 RADIUS (Remote Authentication) 프록시로 NPS를 구성할 수도 있습니다. 및 권한 부여 합니다.

NPS를 사용 하면 중앙에서 구성 하 고 네트워크 액세스 인증, 권한 부여 및 다음 기능을 통해 계정을 관리할 수 있습니다.

- **RADIUS 서버**합니다. NPS 중앙 집중식된 인증, 권한 부여 및 계정에 대해 수행 무선 스위치, 원격 액세스 전화 접속 및 가상 사설망 (VPN) 연결을 인증 합니다. NPS를 RADIUS 서버로 사용할 경우 무선 액세스 지점 및 VPN 서버와 같은 네트워크 액세스 서버를 NPS에서 RADIUS 클라이언트로 구성할 수 있습니다. 또한 NPS가 연결 요청에 권한을 부여하는 데 사용하는 네트워크 정책을 구성하고, NPS가 로컬 하드 디스크의 로그 파일이나 Microsoft SQL Server 데이터베이스에 계정 정보를 기록하도록 RADIUS 계정을 구성할 수 있습니다. 자세한 내용은 [RADIUS 서버](#radius-server)합니다.
- **RADIUS 프록시**합니다. RADIUS 프록시로 NPS를 사용 하는 경우 NPS 연결 요청을 전달 하려는 RADIUS 서버를 다른 RADIUS 서버로 전달 하는 연결 요청을 알리는 연결 요청 정책을 구성 합니다. 또한 원격 RADIUS 서버 그룹에 있는 하나 이상의 컴퓨터에서 기록할 계정 데이터를 전달하도록 NPS를 구성할 수도 있습니다. NPS를 RADIUS 프록시 서버를 구성 하려면 다음 항목을 참조 합니다. 자세한 내용은 [RADIUS 프록시](#radius-proxy)합니다.
    - [연결 요청 정책 구성](nps-crp-configure.md)
- **RADIUS 계정**합니다. 로컬 로그 파일 또는 Microsoft SQL Server의 로컬 또는 원격 인스턴스에 이벤트를 기록 하는 NPS를 구성할 수 있습니다. 자세한 내용은 [NPS 로깅](#nps-logging)합니다.

> [!IMPORTANT]
> 네트워크 액세스 보호 \(NAP\), 상태 등록 기관 \(HRA\), 및 호스트 자격 인증 프로토콜 \(HCAP\) Windows Server 2012 R2에서 사용 되지 않는 및를 Windows Server 2016에서 사용할 수 없습니다. Windows Server 2016 이전의 운영 체제를 사용 하 여 NAP 배포를 사용 하는 경우에 Windows Server 2016으로 NAP 배포를 마이그레이션할 수 없습니다.

이러한 기능의 조합을 사용 하 여 NPS를 구성할 수 있습니다. 예를 들어 VPN 연결용 RADIUS 서버와도 일부 연결 요청 인증 및 다른 도메인에서 권한 부여에 대 한 원격 RADIUS 서버 그룹의 구성원에 게 전달 하는 RADIUS 프록시로 NPS를 구성할 수 있습니다.

## <a name="windows-server-editions-and-nps"></a>NPS 및 Windows Server 버전

NPS는 설치 하는 Windows Server 버전에 따라 다른 기능을 제공 합니다.

### <a name="windows-server-2016-or-windows-server-2019-standarddatacenter-edition"></a>Windows Server 2016 또는 Windows Server 2019 Standard/Datacenter Edition

Windows Server 2016 Standard 또는 Datacenter에 NPS를 사용 하 여 RADIUS 클라이언트와 원격 RADIUS 서버 그룹을 무제한을 구성할 수 있습니다. IP 주소 범위를 지정하여 RADIUS 클라이언트를 구성할 수도 있습니다.

> [!NOTE]
> WIndows 네트워크 정책 및 액세스 서비스 기능에는 Server Core 설치 옵션과 함께 설치 되는 시스템에서 사용할 수 없는 경우

다음 섹션에서는 RADIUS 서버 및 프록시로 NPS에 대 한 자세한 정보를 제공합니다.

## <a name="radius-server-and-proxy"></a>RADIUS 서버 및 프록시

NPS를 RADIUS 서버로, RADIUS 프록시 또는 둘 다로 사용할 수 있습니다.

### <a name="radius-server"></a>RADIUS 서버

NPS는 Microsoft에서 구현한 RADIUS 표준 Internet Engineering Task Force에서 지정한 \(IETF\) Rfc 2865 및 2866에에서 있습니다. RADIUS 서버로 NPS에서 중앙 집중식된 연결 인증, 권한 부여 및 계정에 대 한 다양 한 유형의 네트워크 액세스, 무선, 인증 스위치를 포함 하 여 전화 접속 및 가상 사설망 \(VPN\) 원격 액세스 및 라우터 연결 합니다.

> [!NOTE]
> NPS를 RADIUS 서버로 배포에 대 한 자세한 내용은 [네트워크 정책 서버 배포](nps-deploy.md)합니다.

NPS는 무선 여러 이기종, 스위치, 원격 액세스 또는 VPN 장치를 사용 하도록 설정 합니다. Windows Server 2016에서 사용할 수 있는 원격 액세스 서비스를 사용 하 여 NPS를 사용할 수 있습니다.

NPS는 Active Directory Domain Services를 사용 하 여 \(AD DS\) 도메인 또는 로컬 보안 계정 관리자 (SAM) 사용자 계정을 데이터베이스 연결 시도 대 한 사용자 자격 증명을 인증 합니다. NPS를 실행 하는 서버는 AD DS 도메인의 멤버인 경우 NPS 디렉터리 서비스를 사용 하 여 해당 사용자 계정 데이터베이스 및 single sign-on 솔루션의 일부입니다. 네트워크 액세스 제어에 대 한 동일한 자격 증명 집합이 되 \(인증 및 네트워크에 대 한 액세스 권한 부여\) 및 AD DS 도메인에 로그온 하 합니다.

> [!NOTE]
> NPS 연결 권한을 부여 하려면 사용자 계정 및 네트워크 정책의 전화 접속 속성을 사용 합니다.

인터넷 서비스 공급자 \(Isp\) 네트워크 액세스를 관리 하는 조직 네트워크 액세스 유형에 관계 없이 관리의 단일 지점에서 모든 유형의 네트워크 액세스를 관리 하는 필요성이 증가 했으며 장비를 사용 합니다. RADIUS 표준 같은 유형이 고 다른 유형의 환경에서이 기능을 지원합니다. RADIUS는 클라이언트-서버 프로토콜 (RADIUS 클라이언트로 사용) 하는 네트워크 액세스 장치 인증 및 계정 요청을 RADIUS 서버로 전송할 수 있도록 하는 경우

RADIUS 서버 사용자 계정 정보에 액세스할 수 있고 네트워크 액세스 인증 자격 증명을 확인할 수 있습니다. 사용자 자격 증명을 인증 하 고 연결 시도가 권한이 부여 된 경우 RADIUS 서버는 지정 된 조건 기준으로 사용자 액세스 권한을 부여 하 고 네트워크 액세스 연결 계정 로그에 로그 합니다. RADIUS 사용 하 여 네트워크 액세스 사용자 인증, 권한 부여 및 계정 데이터를 수집 하 고 각 액세스 서버 대신 중앙 위치에서 관리할 수 있습니다.

#### <a name="using-nps-as-a-radius-server"></a>NPS를 RADIUS 서버로 사용 하 여

NPS를 RADIUS 서버로 사용할 수 있습니다 때:

- 사용자 계정 데이터베이스와 AD DS 도메인 또는 로컬 SAM 사용자 계정 데이터베이스를 사용 하 여 액세스 클라이언트에 대 한 됩니다. 
- VPN 서버에서 여러 전화 접속 서버에서 원격 액세스를 사용 하는 또는 필요 시 전화 접속 라우터 하려는 네트워크 정책 및 로그인 및 계정 연결 구성을 중앙 집중화 합니다. 
- 사용자 전화 접속, VPN 또는 서비스 공급자에 대 한 무선 액세스를 아웃소싱하는 경우. 액세스 서버는 RADIUS를 사용 하 여 인증 하 고 조직의 구성원이가 만든 연결에 권한을 부여 합니다.
- 인증, 권한 부여 및 액세스 서버 유형이 다른 집합에 대 한 계정에 중앙 집중화 하려는 합니다.

다음 그림에서는 다양 한 클라이언트 액세스에 대 한 RADIUS 서버로 NPS를 보여 줍니다. 

![NPS를 RADIUS 서버로](../../media/Nps-Server/Nps-Server.jpg)

### <a name="radius-proxy"></a>RADIUS 프록시

RADIUS 프록시로 NPS NPS 및 다른 RADIUS 서버에 인증 및 계정 메시지 전달합니다. RADIUS 클라이언트 간의 메시지 반지름의 라우팅을 제공 하기를 RADIUS 프록시로 NPS 사용할 수 있습니다 \(네트워크 액세스 서버 라고도\) 및 사용자 인증, 권한 부여 및 계정에 대해 수행 하는 RADIUS 서버는 연결 시도 합니다. 

RADIUS 프록시로 사용 하는 경우 NPS 중앙 전환 또는 RADIUS 액세스 및 계정 메시지 흐름을 통해 라우팅 점입니다. NPS는 전달 되는 메시지에 대 한 계정 로그에 정보를 기록 합니다.

#### <a name="using-nps-as-a-radius-proxy"></a>NPS를 RADIUS 프록시로 사용 하 여

NPS를 사용 하 여 RADIUS 프록시로 경우:

- 여러 고객에 게 아웃소싱 된 전화 접속, VPN 또는 무선 네트워크 액세스 서비스를 제공 하는 서비스 공급자 있습니다. Nas에 NPS RADIUS 프록시에 연결 요청을 보냅니다. 연결 요청에 사용자 이름의 영역 부분에 따라 NPS RADIUS 프록시에서는 고객에 의해 유지 관리 되는 RADIUS 서버로 연결 요청 전달 및 수 인증 및 권한 부여 연결 시도 합니다.
- 인증 및 NPS 멤버인 도메인 또는 NPS 멤버인 도메인과 양방향 트러스트 관계가 있는 다른 도메인의 구성원이 아닌 사용자 계정에 대 한 권한 부여를 제공 해야 합니다. 다른 포리스트, 트러스트 되지 않은 도메인 및 단방향 트러스트 된 도메인에 계정이 포함 됩니다. NPS RADIUS 서버로 연결 요청을 전송 하도록 액세스 서버를 구성 하는 대신 해당 연결 요청을 NPS RADIUS 프록시에 보내도록 구성할 수 있습니다. NPS RADIUS 프록시 사용자 이름 영역 이름 부분을 사용 하 고 올바른 도메인 또는 포리스트를 NPS로 요청을 전달 합니다. 연결 시도 사용자 계정 도메인 이나 포리스트에서 다른 도메인 이나 포리스트의 Nas에 대 한 인증 될 수 있습니다.
- Windows 계정 데이터베이스가 아닌 데이터베이스를 사용 하 여 인증 및 권한 부여를 수행 해야 합니다. 이 경우 지정 된 영역 이름과 일치 하는 연결 요청은 사용자 계정 및 권한 부여 데이터의 다른 데이터베이스에 대 한 액세스 권한이 있는 RADIUS 서버로 전달 됩니다. 다른 사용자 데이터베이스의 예로 디렉터리 서비스 NDS (Novell) 및 구조적 쿼리 언어 (SQL) 데이터베이스입니다.
- 많은 수의 연결 요청을 처리 해야 합니다. 이 경우 여러 RADIUS 서버는 연결 및 계정 요청을 분산 하려고 RADIUS 클라이언트를 구성 하는 대신 NPS RADIUS 프록시에는 연결 및 계정 요청을 보내도록 구성할 수 있습니다. 연결의 부하를 동적으로 분산 하는 NPS RADIUS 프록시 및 계정 여러 RADIUS 서버에서 요청 하 고 처리 하는 다 수의 RADIUS 클라이언트 및 초당 인증 증가 합니다.
- RADIUS 인증 및 아웃소싱한 서비스 공급자에 대 한 권한 부여를 제공 하 고 인트라넷 방화벽 구성이 최소화 하려고 합니다. 인트라넷 방화벽은 경계 네트워크 (인트라넷 및 인터넷 간에 네트워크)와 인트라넷 사이입니다. NPS를 경계 네트워크에 배치 하 여 경계 네트워크와 인트라넷 간에 방화벽 NPS 및 여러 도메인 컨트롤러 간에 트래픽을 허용 해야 합니다. NPS 프록시를 사용 하 여 NPS를 바꿔 방화벽 NPS 프록시 및 인트라넷 내에서 하나 이상의 NPSs 간에 전달 RADIUS 트래픽을 허용 해야 합니다.

다음 그림에서는 RADIUS 클라이언트와 RADIUS 서버 사이의 RADIUS 프록시로 NPS를 보여 줍니다.

![RADIUS 프록시로 NPS](../../media/Nps-Proxy/Nps-Proxy.jpg)

NPS를 사용 하 여 조직도 아웃소싱 할 수는 서비스 공급자에 대 한 원격 액세스 인프라 사용자 인증, 권한 부여 및 계정에 대 한 제어를 유지 하면서 합니다.

다음 시나리오에 대 한 NPS 구성은 만들 수 있습니다.

- 무선 액세스
- 조직 전화 접속 또는 가상 사설망 (VPN)에 대 한 원격 액세스
- 아웃소싱 된 전화 접속 또는 무선 액세스
- 인터넷 액세스
- 비즈니스 파트너 엑스트라넷 리소스에 대 한 인증 된 액세스

## <a name="radius-server-and-radius-proxy-configuration-examples"></a>RADIUS 서버 및 RADIUS 프록시 구성 예

다음 구성 예제에서는 RADIUS 서버 및 RADIUS 프록시로 NPS를 구성 하는 방법을 보여 줍니다.

**NPS를 RADIUS 서버로**입니다. 이 예제에서는 NPS를 RADIUS 서버로 구성 된 기본 연결 요청 정책을 구성 된 정책을 이며 로컬 NPS에서 모든 연결 요청을 처리 합니다. NPS는 인증 하 고 신뢰할 수 있는 도메인에서 NPS의 도메인에 계정이 있는 사용자 권한을 부여할 수 있습니다.

**NPS를 RADIUS 프록시로**합니다. 이 예제에서는 두 개의 신뢰할 수 없는 도메인에서 원격 RADIUS 서버 그룹에 연결 요청을 전달 하는 RADIUS 프록시로 NPS 구성 됩니다. 기본 연결 요청 정책을 삭제 되 고, 두 개의 신뢰할 수 없는 도메인의 각 요청에 전달 하기 위해 새 연결 요청 정책 두 개 만들어집니다. 이 예제에서는 NPS는 로컬 서버의 모든 연결 요청을 처리 하지 않습니다. 

**RADIUS 서버와 RADIUS 프록시로 NPS**합니다. 연결 요청이 로컬로 처리 된을 지정 하는 기본 연결 요청 정책의 경우 외에도 NPS 또는 트러스트 되지 않은 도메인에서 다른 RADIUS 서버에 연결 요청을 전달 하는 새 연결 요청 정책을 만들어집니다. 이 두 번째 정책은 프록시 정책을 이라고 합니다. 이 예제에서는 프록시 정책 정책의 정렬된 된 목록에서 가장 먼저 표시 됩니다. 연결 요청에 프록시 정책과 일치 하는 경우 연결 요청이 원격 RADIUS 서버 그룹의 RADIUS 서버로 전달 됩니다. 연결 요청이 프록시 정책과 일치 하지 않습니다 하지만 기본 연결 요청 정책과 일치 하는 경우 NPS는 로컬 서버의 연결 요청을 처리 합니다. 연결 요청 정책 중 하나 일치 하지 않는 경우 삭제 됩니다.

**NPS를 RADIUS 서버로 원격 회계 서버를 사용 하 여**입니다. 이 예제에서는 로컬 NPS 계정 작업을 수행 하도록 구성 되지 않은 하 고 기본 연결 요청 정책을 수정 해야 RADIUS 계정 메시지를 NPS 또는 다른 RADIUS 서버는 원격 RADIUS 서버 그룹에 전달 됩니다. 계정 메시지는 전달 하지만 인증 및 권한 부여 메시지 전달 되지 않습니다 및 로컬 도메인에 대 한 이러한 기능을 수행 하는 로컬 NPS 및 모든 트러스트 된 도메인입니다.

**Windows 사용자 매핑으로 사용자 원격 RADIUS 사용 하 여 NPS**합니다. 이 예제에서는 NPS 권한 부여에 대 한 로컬 Windows 사용자 계정을 사용 하는 동안 원격 RADIUS 서버에 인증 요청을 전달 하 여 RADIUS 서버 및 각 개별 연결 요청에 대 한 RADIUS 프록시로 작동 합니다. 이 구성은 연결 요청 정책 조건으로 Windows 사용자 매핑 특성에 원격 RADIUS를 구성 하 여 구현 됩니다. \(또한 사용자 계정은 원격 RADIUS 서버에서 인증을 수행 하는 원격 사용자 계정으로 동일한 이름을 가진 RADIUS 서버에서 로컬로 생성 해야 합니다.\)

## <a name="configuration"></a>Configuration

NPS를 RADIUS 서버로 구성 하려면 NPS 콘솔 또는 서버 관리자에서 표준 구성 또는 고급 구성을 사용할 수 있습니다. NPS를 RADIUS 프록시로 구성 하려면 고급 구성을 사용 해야 합니다.

### <a name="standard-configuration"></a>표준 구성

표준 구성을 사용 하 여 마법사는 다음 시나리오에 대 한 NPS를 구성할 수 있도록 제공 됩니다.

- 전화 접속 또는 VPN 연결용 RADIUS 서버
- 802.1X 무선 또는 유선 연결용 RADIUS 서버

마법사를 사용 하 여 NPS를 구성, NPS 콘솔을 열고, 앞에서 설명한 시나리오 중 하나를 선택 및 링크를 클릭 하는 마법사를 엽니다.

### <a name="advanced-configuration"></a>고급 구성

고급 구성을 사용 하는 경우 수동으로 RADIUS 서버 또는 RADIUS 프록시로 NPS를 구성 합니다. 

고급 구성을 사용 하 여 NPS를 구성 하려면 NPS 콘솔을 열고 옆에 화살표를 클릭 **고급 구성** 이 섹션을 확장 합니다.

다음과 같은 고급 구성 항목이 제공 됩니다.

#### <a name="configure-radius-server"></a>RADIUS 서버 구성

NPS를 RADIUS 서버로 구성 하려면 RADIUS 클라이언트, 네트워크 정책 및 RADIUS 계정을 구성 해야 합니다.

이 구성을 만드는 방법은 다음 항목을 참조 하십시오.

- [RADIUS 클라이언트 구성](nps-radius-clients-configure.md)
- [네트워크 정책 구성](nps-np-configure.md)
- [네트워크 정책 서버 계정 구성](nps-accounting-configure.md)

#### <a name="configure-radius-proxy"></a>RADIUS 프록시 구성

NPS를 RADIUS 프록시로 구성 하려면 RADIUS 클라이언트, 원격 RADIUS 서버 그룹 및 연결 요청 정책을 구성 해야 합니다.

이 구성을 만드는 방법은 다음 항목을 참조 하십시오.

- [RADIUS 클라이언트 구성](nps-radius-clients-configure.md)
- [원격 RADIUS 서버 그룹 구성](nps-crp-rrsg-configure.md)
- [연결 요청 정책 구성](nps-crp-configure.md)

## <a name="nps-logging"></a>NPS 로깅

NPS 로깅 RADIUS 계정을 라고도 합니다. NPS를 RADIUS 서버로, 프록시 또는 이러한 구성은 조합으로 사용 되는지 여부를 NPS 로깅 요구 사항에 맞게 구성 합니다.

NPS 로깅을 구성 하는 이벤트를 기록 하 고 이벤트 뷰어를 사용 하 여 표시 하 고 다른 정보를 결정 하려면 로그를 구성 해야 합니다. 또한 로컬 컴퓨터 또는 원격 컴퓨터에서 SQL Server 데이터베이스 또는 로컬 컴퓨터에 저장 된 텍스트 로그 파일에 사용자 인증 및 계정 정보를 기록할 것인지 여부를 결정 해야 합니다.

자세한 내용은 [네트워크 정책 서버 계정 구성](nps-accounting-configure.md)합니다.
