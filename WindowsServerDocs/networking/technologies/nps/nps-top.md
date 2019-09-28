---
title: NPS(네트워크 정책 서버)
description: 이 항목에서는 Windows Server 2016 및 Windows Server 2019의 네트워크 정책 서버에 대 한 개요를 제공 하 고 NPS에 대 한 추가 지침에 대 한 링크를 제공 합니다.
manager: dougkim
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 9c7a67e0-0953-479c-8736-ccb356230bde
ms.author: pashort
author: shortpatti
ms.date: 06/20/2018
ms.openlocfilehash: 5685d4dae742245c131ff2fee3114e905e94e9bc
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71396009"
---
# <a name="network-policy-server-nps"></a>NPS(네트워크 정책 서버)

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2019

이 항목에서는 Windows Server 2016 및 Windows Server 2019의 네트워크 정책 서버에 대 한 개요를 확인할 수 있습니다. NPS는 Windows Server 2016 및 Server 2019에 NPAS (네트워크 정책 및 액세스 서비스) 기능을 설치할 때 설치 됩니다.

> [!NOTE]
> 이 항목 외에도 다음과 같은 NPS 설명서를 사용할 수 있습니다.
> - [네트워크 정책 서버 모범 사례](nps-best-practices.md)
> - [네트워크 정책 서버 시작](nps-getstart-top.md)
> - [네트워크 정책 서버 계획](nps-plan-top.md)
> - [네트워크 정책 서버 배포](nps-deploy.md)
> - [네트워크 정책 서버 관리](nps-manage-top.md)
> - Windows Server 2016 및 Windows 10 용 [Windows PowerShell의 NPS (네트워크 정책 서버) cmdlet](https://technet.microsoft.com/library/jj872739.aspx)
> - Windows Server 2012 R2 및 Windows 8.1에 대 한 [Windows PowerShell의 NPS (네트워크 정책 서버) cmdlet](https://technet.microsoft.com/library/jj872739.aspx)
> - Windows Server 2012 및 Windows 8 용 [Windows PowerShell의 NPS cmdlet](https://technet.microsoft.com/library/jj872739.aspx)

네트워크 정책 서버(NPS)를 사용하면 연결 요청 인증 및 권한 부여를 위해 조직 전체의 네트워크 액세스 정책을 생성하여 적용할 수 있습니다.

연결 요청을 부하 분산 하 고 인증을 위해 올바른 도메인에 전달할 수 있도록 NPS를 RADIUS (RADIUS(Remote Authentication Dial-In User Service)) 프록시로 구성 하 여 연결 요청을 원격 NPS 또는 다른 RADIUS 서버로 전달할 수도 있습니다. 및 권한 부여.

NPS를 사용 하면 다음과 같은 기능을 통해 네트워크 액세스 인증, 권한 부여 및 계정을 중앙에서 구성 하 고 관리할 수 있습니다.

- **RADIUS 서버**. NPS는 무선, 인증 스위치, 원격 액세스 전화 접속 및 VPN (가상 사설망) 연결에 대 한 중앙 집중식 인증, 권한 부여 및 계정을 수행 합니다. NPS를 RADIUS 서버로 사용할 경우 무선 액세스 지점 및 VPN 서버와 같은 네트워크 액세스 서버를 NPS에서 RADIUS 클라이언트로 구성할 수 있습니다. 또한 NPS가 연결 요청에 권한을 부여하는 데 사용하는 네트워크 정책을 구성하고, NPS가 로컬 하드 디스크의 로그 파일이나 Microsoft SQL Server 데이터베이스에 계정 정보를 기록하도록 RADIUS 계정을 구성할 수 있습니다. 자세한 내용은 [RADIUS 서버](#radius-server)를 참조 하세요.
- **RADIUS 프록시**. NPS를 RADIUS 프록시로 사용 하는 경우 다른 RADIUS 서버에 전달 하는 연결 요청 및 연결 요청을 전달 하려는 RADIUS 서버를 NPS에 알리는 연결 요청 정책을 구성 합니다. 또한 원격 RADIUS 서버 그룹에 있는 하나 이상의 컴퓨터에서 기록할 계정 데이터를 전달하도록 NPS를 구성할 수도 있습니다. RADIUS 프록시 서버로 NPS를 구성 하려면 다음 항목을 참조 하십시오. 자세한 내용은 [RADIUS 프록시](#radius-proxy)를 참조 하세요.
    - [연결 요청 정책 구성](nps-crp-configure.md)
- **RADIUS 계정**. 로컬 로그 파일이 나 Microsoft SQL Server의 로컬 또는 원격 인스턴스에 이벤트를 기록 하도록 NPS를 구성할 수 있습니다. 자세한 내용은 [NPS 로깅](#nps-logging)을 참조 하세요.

> [!IMPORTANT]
> 네트워크 액세스 보호 \(NAP @ no__t-1, Health Registration Authority \(HRA @ no__t-3 및 호스트 자격 권한 부여 프로토콜 \(HCAP @ no__t-5는 Windows Server 2012 r 2에서 사용 되지 않으며 Windows Server 2016에서 사용할 수 없습니다. Windows Server 2016 이전 운영 체제를 사용 하는 NAP 배포를 사용 하는 경우 NAP 배포를 Windows Server 2016로 마이그레이션할 수 없습니다.

이러한 기능을 조합 하 여 NPS를 구성할 수 있습니다. 예를 들어 한 NPS를 VPN 연결에 대 한 RADIUS 서버로 구성 하 고, 다른 도메인의 인증 및 권한 부여를 위해 원격 RADIUS 서버 그룹의 구성원에 게 일부 연결 요청을 전달 하는 RADIUS 프록시로 구성할 수 있습니다.

## <a name="windows-server-editions-and-nps"></a>Windows Server 버전 및 NPS

NPS는 설치 하는 Windows Server 버전에 따라 다양 한 기능을 제공 합니다.

### <a name="windows-server-2016-or-windows-server-2019-standarddatacenter-edition"></a>Windows Server 2016 또는 Windows Server 2019 Standard/Datacenter Edition

Windows Server 2016 Standard 또는 Datacenter의 NPS를 사용 하 여 RADIUS 클라이언트와 원격 RADIUS 서버 그룹을 무제한 구성할 수 있습니다. IP 주소 범위를 지정하여 RADIUS 클라이언트를 구성할 수도 있습니다.

> [!NOTE]
> WIndows 네트워크 정책 및 액세스 서비스 기능은 Server Core 설치 옵션과 함께 설치 된 시스템에서 사용할 수 없습니다.

다음 섹션에서는 RADIUS 서버 및 프록시로 NPS에 대 한 자세한 정보를 제공 합니다.

## <a name="radius-server-and-proxy"></a>RADIUS 서버 및 프록시

RADIUS 서버, RADIUS 프록시 또는 둘 다로 NPS를 사용할 수 있습니다.

### <a name="radius-server"></a>RADIUS 서버

NPS는 Rfc 2865 및 2866의 Internet 공학적 작업 Force \(IETF @ no__t-1로 지정 된 RADIUS 표준의 Microsoft 구현입니다. RADIUS 서버인 NPS는 무선, 인증 스위치, 전화 접속 및 VPN (가상 사설망) \(VPN @ no__t 원격 액세스를 포함 하 여 다양 한 유형의 네트워크 액세스에 대 한 중앙 집중식 연결 인증, 권한 부여 및 계정을 수행 합니다. 라우터 간 연결

> [!NOTE]
> RADIUS 서버로 NPS를 배포 하는 방법에 대 한 자세한 내용은 [네트워크 정책 서버 배포](nps-deploy.md)를 참조 하세요.

NPS를 사용 하면 유형이 다른 무선, 스위치, 원격 액세스 또는 VPN 장비 집합을 사용할 수 있습니다. Windows Server 2016에서 사용할 수 있는 원격 액세스 서비스와 함께 NPS를 사용할 수 있습니다.

NPS는 Active Directory Domain Services \(AD DS @ no__t-1 도메인 또는 로컬 SAM (보안 계정 관리자) 사용자 계정 데이터베이스를 사용 하 여 연결 시도에 대 한 사용자 자격 증명을 인증 합니다. NPS를 실행 하는 서버가 AD DS 도메인의 구성원이 면 NPS는 디렉터리 서비스를 사용자 계정 데이터베이스로 사용 하 고 Single Sign-On 솔루션의 일부입니다. 네트워크 액세스 제어 @no__t 네트워크 액세스 제어에 사용 되는 자격 증명 집합은 네트워크 @ no__t-1에 대 한 액세스를 인증 하 고 권한을 부여 하 고 AD DS 도메인에 로그온 하는 데 사용 됩니다.

> [!NOTE]
> NPS는 사용자 계정 및 네트워크 정책의 전화 접속 속성을 사용 하 여 연결에 권한을 부여 합니다.

인터넷 서비스 공급자 \(ISPs @ no__t-1 및 네트워크 액세스를 유지 관리 하는 조직에서는 사용 되는 네트워크 액세스 장비의 유형에 관계 없이 단일 관리 지점에서 모든 유형의 네트워크 액세스를 관리할 수 있는 문제를 증가 시켰습니다. RADIUS 표준은 동일한 환경 및 다른 유형의 환경에서이 기능을 지원 합니다. RADIUS는 radius 서버에 인증 및 계정 요청을 제출 하기 위해 네트워크 액세스 장비 (RADIUS 클라이언트로 사용 됨)를 사용 하도록 설정 하는 클라이언트-서버 프로토콜입니다.

RADIUS 서버는 사용자 계정 정보에 액세스할 수 있으며 네트워크 액세스 인증 자격 증명을 확인할 수 있습니다. 사용자 자격 증명을 인증 하 고 연결 시도에 권한이 부여 된 경우 RADIUS 서버는 지정 된 조건에 따라 사용자 액세스 권한을 부여 하 고 계정 로그에 네트워크 액세스 연결을 기록 합니다. RADIUS를 사용 하면 네트워크 액세스 사용자 인증, 권한 부여 및 계정 데이터를 각 액세스 서버가 아닌 중앙 위치에서 수집 하 고 유지 관리할 수 있습니다.

#### <a name="using-nps-as-a-radius-server"></a>RADIUS 서버로 NPS 사용

다음과 같은 경우 NPS를 RADIUS 서버로 사용할 수 있습니다.

- 액세스 클라이언트의 사용자 계정 데이터베이스로 AD DS 도메인 또는 로컬 SAM 사용자 계정 데이터베이스를 사용 하 고 있습니다. 
- 여러 전화 접속 서버, VPN 서버 또는 필요 시 전화 접속 라우터에 원격 액세스를 사용 하 고 있으며 네트워크 정책 및 연결 로깅 및 계정 구성을 모두 중앙 집중화 하려고 합니다. 
- 전화 접속, VPN 또는 무선 액세스를 서비스 공급자에 게 아웃소싱 합니다. 액세스 서버는 RADIUS를 사용 하 여 조직의 구성원이 만든 연결을 인증 하 고 권한을 부여 합니다.
- 다른 유형의 액세스 서버 집합에 대 한 인증, 권한 부여 및 계정을 중앙 집중화 하려고 합니다.

다음 그림은 NPS를 다양 한 액세스 클라이언트의 RADIUS 서버로 보여 줍니다. 

![RADIUS 서버로 서의 NPS](../../media/Nps-Server/Nps-Server.jpg)

### <a name="radius-proxy"></a>RADIUS 프록시

RADIUS 프록시로 NPS는 NPS 및 기타 RADIUS 서버에 인증 및 계정 메시지를 전달 합니다. NPS를 RADIUS 프록시로 사용 하 여 radius @no__t 클라이언트 (네트워크 액세스 서버 @ no__t-1)와 사용자 인증, 권한 부여 및 연결 시도에 대 한 계정을 수행 하는 RADIUS 서버 라고도 하는 radius 서버 간에 RADIUS 메시지 라우팅을 제공할 수 있습니다. 

RADIUS 프록시로 사용 되는 경우 NPS는 RADIUS 액세스 및 계정 메시지가 전달 되는 중앙 전환 또는 라우팅 지점입니다. NPS는 전달 되는 메시지에 대 한 정보를 계정 로그에 기록 합니다.

#### <a name="using-nps-as-a-radius-proxy"></a>RADIUS 프록시로 NPS 사용

다음과 같은 경우 NPS를 RADIUS 프록시로 사용할 수 있습니다.

- 여러 고객에 게 아웃소싱 전화 접속, VPN 또는 무선 네트워크 액세스 서비스를 제공 하는 서비스 공급자입니다. Nas NPS RADIUS 프록시로 연결 요청을 보냅니다. 연결 요청에 있는 사용자 이름의 영역 부분에 따라 NPS RADIUS 프록시는 고객이 관리 하는 RADIUS 서버에 연결 요청을 전달 하 고 연결 시도를 인증 하 고 권한을 부여할 수 있습니다.
- NPS가 구성원 이거나 NPS가 구성원 인 도메인과 양방향 트러스트 관계가 있는 다른 도메인의 구성원이 아닌 사용자 계정에 대 한 인증 및 권한 부여를 제공 하려고 합니다. 여기에는 트러스트 되지 않은 도메인의 계정, 단방향 트러스트 된 도메인 및 기타 포리스트가 포함 됩니다. NPS RADIUS 서버에 연결 요청을 보내도록 액세스 서버를 구성 하는 대신 NPS radius 프록시로 연결 요청을 보내도록 구성할 수 있습니다. NPS RADIUS 프록시는 사용자 이름의 영역 이름 부분을 사용 하 고 올바른 도메인 또는 포리스트의 NPS에 요청을 전달 합니다. 한 도메인 또는 포리스트의 사용자 계정에 대 한 연결 시도는 다른 도메인 또는 포리스트의 Nas에 대해 인증 될 수 있습니다.
- Windows 계정 데이터베이스가 아닌 데이터베이스를 사용 하 여 인증 및 권한 부여를 수행 하려고 합니다. 이 경우 지정 된 영역 이름과 일치 하는 연결 요청은 RADIUS 서버에 전달 되며,이 서버는 다른 사용자 계정 및 권한 부여 데이터에 액세스할 수 있습니다. 다른 사용자 데이터베이스의 예로는 NDS (Novell Directory Services) 및 구조적 쿼리 언어 (SQL) 데이터베이스가 있습니다.
- 많은 수의 연결 요청을 처리 하려고 합니다. 이 경우 RADIUS 클라이언트를 구성 하 여 여러 RADIUS 서버에서 연결 및 계정 요청의 균형을 조정 하는 대신 NPS RADIUS 프록시에 연결 및 계정 요청을 전송 하도록 구성할 수 있습니다. NPS RADIUS 프록시는 여러 RADIUS 서버에서 연결 및 계정 요청의 부하를 동적으로 분산 하 고 초당 많은 수의 RADIUS 클라이언트 및 인증의 처리를 늘립니다.
- 아웃소싱 서비스 공급자에 대 한 RADIUS 인증 및 권한 부여를 제공 하 고 인트라넷 방화벽 구성을 최소화 하려고 합니다. 인트라넷 방화벽은 경계 네트워크 (인트라넷과 인터넷 간의 네트워크)와 인트라넷 사이에 있습니다. 경계 네트워크에 NPS를 배치 하면 경계 네트워크와 인트라넷 간의 방화벽이 NPS와 여러 도메인 컨트롤러 간에 트래픽을 전송 하도록 허용 해야 합니다. Nps를 NPS 프록시로 바꾸면 방화벽에서 RADIUS 트래픽만 인트라넷 내에서 NPS 프록시와 하나 또는 여러 개의 NPSs 사이에서 이동 하도록 허용 해야 합니다.

다음 그림은 NPS를 radius 클라이언트와 radius 서버 간의 RADIUS 프록시로 보여 줍니다.

![RADIUS 프록시로 서의 NPS](../../media/Nps-Proxy/Nps-Proxy.jpg)

NPS를 사용 하면 조직에서 사용자 인증, 권한 부여 및 계정에 대 한 제어를 유지 하면서 원격 액세스 인프라를 서비스 공급자에 게 아웃소싱 할 수도 있습니다.

NPS 구성은 다음과 같은 시나리오에 대해 만들 수 있습니다.

- 무선 액세스
- 조직 전화 접속 또는 VPN (가상 사설망) 원격 액세스
- 아웃소싱 전화 접속 또는 무선 액세스
- 인터넷 액세스
- 비즈니스 파트너를 위한 엑스트라넷 리소스에 대 한 인증 된 액세스

## <a name="radius-server-and-radius-proxy-configuration-examples"></a>RADIUS 서버 및 RADIUS 프록시 구성 예제

다음 구성 예제에서는 RADIUS 서버와 RADIUS 프록시로 NPS를 구성 하는 방법을 보여 줍니다.

**RADIUS 서버로 서의 NPS**. 이 예에서 NPS는 RADIUS 서버로 구성 되 고, 기본 연결 요청 정책은 유일 하 게 구성 된 정책이 며, 모든 연결 요청은 로컬 NPS에 의해 처리 됩니다. NPS는 계정이 NPS 및 트러스트 된 도메인에 속해 있는 사용자를 인증 하 고 권한을 부여할 수 있습니다.

**RADIUS 프록시로 서의 NPS**. 이 예에서 NPS는 두 개의 트러스트 되지 않은 도메인의 원격 RADIUS 서버 그룹에 연결 요청을 전달 하는 RADIUS 프록시로 구성 됩니다. 기본 연결 요청 정책이 삭제 되 고 두 개의 트러스트 되지 않은 도메인에 요청을 전달 하기 위해 두 개의 새로운 연결 요청 정책이 생성 됩니다. 이 예에서 NPS는 로컬 서버에서 연결 요청을 처리 하지 않습니다. 

**Radius 서버와 radius 프록시로 모두 NPS** 연결 요청을 로컬로 처리 하도록 지정 하는 기본 연결 요청 정책 외에도 연결 요청을 신뢰할 수 없는 도메인의 NPS 또는 다른 RADIUS 서버에 전달 하는 새 연결 요청 정책이 만들어집니다. 이 두 번째 정책의 이름은 프록시 정책입니다. 이 예제에서는 정책에 대 한 순서가 지정 된 목록에 프록시 정책이 먼저 표시 됩니다. 연결 요청이 프록시 정책과 일치 하는 경우 연결 요청은 원격 RADIUS 서버 그룹의 RADIUS 서버로 전달 됩니다. 연결 요청이 프록시 정책과 일치 하지 않지만 기본 연결 요청 정책과 일치 하는 경우 NPS는 로컬 서버에서 연결 요청을 처리 합니다. 연결 요청이 두 정책과 일치 하지 않으면 삭제 됩니다.

**NPS는 원격 계정 서버를 사용 하는 RADIUS 서버**입니다. 이 예에서 로컬 NPS는 계정을 수행 하도록 구성 되지 않으며, RADIUS 계정 메시지가 원격 RADIUS 서버 그룹의 NPS 또는 다른 RADIUS 서버에 전달 되도록 기본 연결 요청 정책이 수정 됩니다. 계정 메시지가 전달 되는 경우에도 인증 및 권한 부여 메시지가 전달 되지 않고 로컬 NPS는 로컬 도메인 및 모든 트러스트 된 도메인에 대해 이러한 기능을 수행 합니다.

**원격 RADIUS에서 Windows 사용자 매핑으로 NPS** 이 예제에서 NPS는 인증 요청을 원격 RADIUS 서버에 전달 하는 동시에 권한 부여에 대 한 로컬 Windows 사용자 계정을 사용 하 여 각 개별 연결 요청에 대 한 radius 프록시로 RADIUS 서버 역할을 합니다. 이 구성은 연결 요청 정책의 조건으로 원격 RADIUS에서 Windows 사용자 매핑 특성을 구성 하 여 구현 합니다. @no__t 사용자 계정은 원격 RADIUS 서버에서 인증을 수행 하는 원격 사용자 계정과 동일한 이름을 가진 RADIUS 서버에서 로컬로 만들어야 합니다. \)

## <a name="configuration"></a>Configuration

NPS를 RADIUS 서버로 구성 하려면 NPS 콘솔 또는 서버 관리자에서 표준 구성 또는 고급 구성을 사용할 수 있습니다. RADIUS 프록시로 NPS를 구성 하려면 고급 구성을 사용 해야 합니다.

### <a name="standard-configuration"></a>표준 구성

표준 구성을 사용 하는 경우 다음과 같은 시나리오에서 NPS를 구성 하는 데 도움이 되는 마법사가 제공 됩니다.

- 전화 접속 또는 VPN 연결용 RADIUS 서버
- 802.1X 무선 또는 유선 연결용 RADIUS 서버

마법사를 사용 하 여 NPS를 구성 하려면 NPS 콘솔을 열고 앞의 시나리오 중 하나를 선택한 다음 마법사가 열리는 링크를 클릭 합니다.

### <a name="advanced-configuration"></a>고급 구성

고급 구성을 사용 하는 경우 NPS를 RADIUS 서버 또는 RADIUS 프록시로 수동으로 구성 합니다. 

고급 구성을 사용 하 여 NPS를 구성 하려면 NPS 콘솔을 열고 **고급 구성** 옆의 화살표를 클릭 하 여이 섹션을 확장 합니다.

다음 고급 구성 항목이 제공 됩니다.

#### <a name="configure-radius-server"></a>RADIUS 서버 구성

RADIUS 서버로 NPS를 구성 하려면 radius 클라이언트, 네트워크 정책 및 RADIUS 계정을 구성 해야 합니다.

이러한 구성을 만드는 방법에 대 한 지침은 다음 항목을 참조 하세요.

- [RADIUS 클라이언트 구성](nps-radius-clients-configure.md)
- [네트워크 정책 구성](nps-np-configure.md)
- [네트워크 정책 서버 계정 구성](nps-accounting-configure.md)

#### <a name="configure-radius-proxy"></a>RADIUS 프록시 구성

RADIUS 프록시로 NPS를 구성 하려면 RADIUS 클라이언트, 원격 RADIUS 서버 그룹 및 연결 요청 정책을 구성 해야 합니다.

이러한 구성을 만드는 방법에 대 한 지침은 다음 항목을 참조 하세요.

- [RADIUS 클라이언트 구성](nps-radius-clients-configure.md)
- [원격 RADIUS 서버 그룹 구성](nps-crp-rrsg-configure.md)
- [연결 요청 정책 구성](nps-crp-configure.md)

## <a name="nps-logging"></a>NPS 로깅

NPS 로깅은 RADIUS 계정이 라고도 합니다. NPS를 RADIUS 서버, 프록시 또는 이러한 구성의 조합으로 사용 하는지 여부에 대 한 요구 사항에 대 한 NPS 로깅을 구성 합니다.

NPS 로깅을 구성 하려면 이벤트 뷰어을 사용 하 여 기록 및 볼 이벤트를 구성 하 고 기록할 다른 정보를 결정 해야 합니다. 또한 로컬 컴퓨터 또는 원격 컴퓨터의 SQL Server 데이터베이스 또는 로컬 컴퓨터에 저장 된 텍스트 로그 파일에 사용자 인증 및 계정 정보를 기록할지 여부를 결정 해야 합니다.

자세한 내용은 [네트워크 정책 서버 계정 구성](nps-accounting-configure.md)을 참조 하세요.
