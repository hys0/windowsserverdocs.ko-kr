---
title: 네트워크 정책 서버 모범 사례
description: 이 항목에서는 Windows Server 2016에서 네트워크 정책 서버를 배포 하 고 관리 하기 위한 모범 사례를 제공 합니다.
manager: brianlic
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 90e544bd-e826-4093-8c3b-6a6fc2dfd1d6
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 4e6e6d2612af80bdaaa3900414bb08c3f0c18ea3
ms.sourcegitcommit: 3c3dfee8ada0083f97a58997d22d218a5d73b9c4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/03/2020
ms.locfileid: "80639906"
---
# <a name="network-policy-server-best-practices"></a>네트워크 정책 서버 모범 사례

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목을 사용 하 여 NPS\)\(네트워크 정책 서버를 배포 하 고 관리 하는 모범 사례에 대해 알아볼 수 있습니다.

다음 섹션에서는 NPS 배포의 다양 한 측면에 대 한 모범 사례를 제공 합니다.

## <a name="accounting"></a>계정

다음은 NPS 로깅에 대 한 모범 사례입니다.

NPS에는 다음과 같은 두 가지 유형의 계정이 나 로깅이 있습니다.

- NPS에 대 한 이벤트 로깅 이벤트 로깅을 사용 하 여 시스템 및 보안 이벤트 로그에 NPS 이벤트를 기록할 수 있습니다. 주로 연결 시도를 감사 하 고 문제를 해결 하는 데 사용 됩니다.

- 사용자 인증 및 계정 요청을 기록 합니다. 로그 파일에 대 한 사용자 인증 및 계정 요청을 텍스트 형식 또는 데이터베이스 형식으로 기록 하거나 SQL Server 2000 데이터베이스의 저장 프로시저에 기록할 수 있습니다. 요청 로깅은 주로 연결 분석과 요금 청구를 위해 사용 되며, 공격자의 활동을 추적 하는 방법을 제공 하는 보안 조사 도구로도 유용 합니다.

NPS 로깅을 가장 효과적으로 사용 하려면 다음을 수행 합니다.

- 처음에는 인증 및 계정 레코드에 대해\) \(로깅을 설정 합니다. 사용자 환경에 적합 한 항목을 결정 한 후 이러한 선택을 수정 합니다.

- 이벤트 로깅이 로그를 유지 하는 데 충분 한 용량으로 구성 되어 있는지 확인 합니다.

- 모든 로그 파일은 손상 되거나 삭제 될 때 다시 만들 수 없으므로 정기적으로 백업 합니다.

- RADIUS 클래스 특성을 사용 하 여 사용량을 추적 하 고 사용량에 대 한 요금을 청구할 부서나 사용자의 id를 간소화 합니다. 자동으로 생성 된 클래스 특성은 각 요청 마다 고유 하지만, 액세스 서버에 대 한 회신이 손실 되 고 요청을 다시 보내는 경우 중복 레코드가 있을 수 있습니다. 사용 현황을 정확 하 게 추적 하기 위해 로그에서 중복 요청을 삭제 해야 할 수도 있습니다.

- 네트워크 액세스 서버 및 RADIUS 프록시 서버가 NPS에 가상의 연결 요청 메시지를 정기적으로 전송 하 여 NPS가 온라인 상태 인지 확인 하려면 **ping 사용자 이름** 레지스트리 설정을 사용 합니다. 이 설정은 이러한 false 연결 요청을 처리 하지 않고 자동으로 거부 하도록 NPS를 구성 합니다. 또한 NPS는 로그 파일의 가상 사용자 이름과 관련 된 트랜잭션을 기록 하지 않으며,이로 인해 이벤트 로그를 쉽게 해석할 수 있습니다.

- NAS 알림 전달을 사용 하지 않도록 설정 합니다. Nas (네트워크 액세스 서버)에서 NPS에 구성 된 원격 RADIUS 서버 그룹의 구성원으로 시작 및 중지 메시지 전달을 사용 하지 않도록 설정할 수 있습니다. 자세한 내용은 [NAS 알림 전달 사용 안 함](nps-disable-nas-notifications.md)을 참조 하세요.

자세한 내용은 [네트워크 정책 서버 계정 구성](nps-accounting-configure.md)을 참조 하세요.

- SQL Server 로깅으로 장애 조치 (failover) 및 중복성을 제공 하려면 SQL Server를 실행 하는 두 대의 컴퓨터를 다른 서브넷에 두십시오. SQL Server **게시 만들기 마법사** 를 사용 하 여 두 서버 간에 데이터베이스 복제를 설정할 수 있습니다. 자세한 내용은 [SQL Server 기술 설명서](https://msdn.microsoft.com/library/ms130214.aspx) 및 [SQL Server 복제](https://msdn.microsoft.com/library/ms151198.aspx)를 참조 하세요.

## <a name="authentication"></a>인증

다음은 인증에 대 한 모범 사례입니다.

- PEAP\) \(PEAP (Extensible authentication Protocol)와 같은 인증서 기반 인증 방법과 강력한 인증을 위한 EAP\) \(EAP를 사용 합니다. 암호 전용 인증 방법은 다양 한 공격에 취약 하 고 안전 하지 않으므로 사용 하지 마십시오. 보안 무선 인증을 사용 하는 경우 NPS가 서버 인증서를 사용 하 여 무선 클라이언트에 대 한 id를 증명 하는 반면, 사용자는 사용자 이름 및 암호를 사용 하 여 id를 증명 하기 때문에 PEAP\-MS\-  무선 배포에서 NPS를 사용 하는 방법에 대 한 자세한 내용은 [암호 기반 802.1 x 인증 된 무선 액세스 배포](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/cncg/wireless/a-deploy-8021x-wireless-access)를 참조 하세요.
- NPSs에서 서버 인증서를 사용 해야 하는 강력한 인증서 기반 인증 방법 (예: PEAP 및 EAP)을 사용 하는 경우 Active Directory&reg; 인증서 서비스를 사용 하 여 사용자 고유의 인증 기관 \(CA\)를 배포 \(.\) 또한 CA를 사용 하 여 컴퓨터 인증서와 사용자 인증서를 등록할 수 있습니다. NPS 및 원격 액세스 서버에 서버 인증서를 배포 하는 방법에 대 한 자세한 내용은 [802.1 x 유선 및 무선 배포에 대 한 서버 인증서 배포](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/cncg/server-certs/deploy-server-certificates-for-802.1x-wired-and-wireless-deployments)를 참조 하세요.

> [!IMPORTANT]
> NPS (네트워크 정책 서버)는 암호 내에서 확장 ASCII 문자를 사용 하는 것을 지원 하지 않습니다.

## <a name="client-computer-configuration"></a>클라이언트 컴퓨터 구성

클라이언트 컴퓨터 구성에 대 한 모범 사례는 다음과 같습니다.

- 그룹 정책를 사용 하 여 모든 도메인 구성원 802.1 X 클라이언트 컴퓨터를 자동으로 구성 합니다. 자세한 내용은 [무선 액세스 배포](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/cncg/wireless/e-wireless-access-deployment#bkmk_policies)항목의 "무선 네트워크 구성 (IEEE 802.11) 정책" 섹션을 참조 하세요.

## <a name="installation-suggestions"></a>설치 제안

다음은 NPS를 설치 하기 위한 모범 사례입니다.

- NPS를 설치 하기 전에 NPS에서 RADIUS 클라이언트로 구성 하기 전에 로컬 인증 방법을 사용 하 여 각 네트워크 액세스 서버를 설치 하 고 테스트 합니다.

- NPS를 설치 하 고 구성한 후 Windows PowerShell 명령 [내보내기-NpsConfiguration](https://technet.microsoft.com/library/jj872749.aspx)을 사용 하 여 구성을 저장 합니다. Nps를 다시 구성할 때마다이 명령을 사용 하 여 NPS 구성을 저장 합니다.

>[!CAUTION]
>- 내보낸 NPS 구성 파일에는 RADIUS 클라이언트에 대 한 암호화 되지 않은 공유 암호와 원격 RADIUS 서버 그룹의 구성원이 포함 됩니다. 따라서 파일을 안전한 위치에 저장 해야 합니다.
>- 내보내기 프로세스에는 내보낸 파일의 Microsoft SQL Server에 대 한 로깅 설정이 포함 되지 않습니다. 내보낸 파일을 다른 NPS로 가져오는 경우 새 서버에서 SQL Server 로깅을 수동으로 구성 해야 합니다.

## <a name="performance-tuning-nps"></a>NPS 성능 조정

다음은 NPS 성능 조정에 대 한 모범 사례입니다.

- NPS 인증 및 권한 부여 응답 시간을 최적화 하 고 네트워크 트래픽을 최소화 하려면 도메인 컨트롤러에 NPS를 설치 합니다.

- Upn\) 또는 Windows Server 2008 및 Windows Server 2003 도메인 \(universal principal name이 사용 되 면 NPS는 글로벌 카탈로그를 사용 하 여 사용자를 인증 합니다. 이 작업을 수행 하는 데 걸리는 시간을 최소화 하려면 글로벌 카탈로그 서버 또는 글로벌 카탈로그 서버와 동일한 서브넷에 있는 서버에 NPS를 설치 합니다.

- 원격 RADIUS 서버 그룹을 구성 하 고 NPS 연결 요청 정책에서 **다음 원격 radius 서버 그룹의 서버에 대 한 계정 정보 기록** 확인란의 선택을 취소 한 경우 이러한 그룹은 계속 해 서 네트워크 액세스 서버를 전송 합니다 .이는 NAS\) 시작 및 중지 알림 메시지를 \(합니다. 이렇게 하면 불필요 한 네트워크 트래픽이 생성 됩니다. 이 트래픽을 제거 하려면 **이 서버에 대 한 네트워크 전달 시작 및 중지 알림** 확인란의 선택을 취소 하 여 각 원격 RADIUS 서버 그룹의 개별 서버에 대 한 NAS 알림 전달을 사용 하지 않도록 설정 합니다.

## <a name="using-nps-in-large-organizations"></a>대기업에서 NPS 사용

다음은 대기업에서 NPS를 사용 하는 모범 사례입니다.

- 네트워크 정책을 사용 하 여 특정 그룹을 제외한 모든 그룹에 대 한 액세스를 제한 하는 경우 액세스를 허용할 모든 사용자에 대 한 유니버설 그룹을 만든 다음이 유니버설 그룹에 대 한 액세스 권한을 부여 하는 네트워크 정책을 만듭니다. 특히 네트워크에 많은 사용자를 포함 하는 경우 유니버설 그룹에 사용자를 직접 배치 하지 마십시오. 대신 유니버설 그룹의 구성원 인 별도의 그룹을 만들고 해당 그룹에 사용자를 추가 합니다.

- 가능한 경우 사용자를 참조 하려면 사용자 계정 이름을 사용 합니다. 사용자는 도메인 멤버 자격에 관계 없이 동일한 사용자 계정 이름을 가질 수 있습니다. 이 방법은 도메인 수가 많은 조직에 필요할 수 있는 확장성을 제공 합니다.

- 도메인 컨트롤러가 아닌 컴퓨터에 nps\) \(네트워크 정책 서버를 설치 했지만 NPS에서 초당 많은 수의 인증 요청을 수신 하는 경우 nps와 도메인 컨트롤러 간에 허용 되는 동시 인증 수를 늘려서 NPS 성능을 향상 시킬 수 있습니다. 자세한 내용은 [NPS에서 처리 하는 동시 인증 늘리기](https://docs.microsoft.com/windows-server/networking/technologies/nps/nps-concurrent-auth)를 참조 하세요.

## <a name="security-issues"></a>보안 문제

보안 문제를 줄이기 위한 모범 사례는 다음과 같습니다.

NPS를 원격으로 관리 하는 경우 네트워크를 통해 중요 한 데이터 또는 기밀 데이터 (예: 공유 암호 또는 암호)를 일반 텍스트로 보내지 않습니다. NPSs를 원격으로 관리 하는 방법에는 두 가지가 있습니다.

- 원격 데스크톱 서비스를 사용 하 여 NPS에 액세스 합니다. 원격 데스크톱 서비스 사용 하는 경우 클라이언트와 서버 간에 데이터가 전송 되지 않습니다. 서버 (예: 운영 체제 데스크톱 및 NPS 콘솔 이미지)의 사용자 인터페이스만 Windows&reg; 10의 원격 데스크톱 연결 이라는 원격 데스크톱 서비스 클라이언트로 전송 됩니다. 클라이언트는 키보드 및 마우스 입력을 전송 합니다 .이는 원격 데스크톱 서비스 사용 하도록 설정 된 서버에서 로컬로 처리 됩니다. 원격 데스크톱 서비스 사용자가 로그온 하면 서버에서 관리 하 고 서로 독립적인 개별 클라이언트 세션만 볼 수 있습니다. 또한 원격 데스크톱 연결은 클라이언트와 서버 간에 128 비트 암호화를 제공 합니다.

- IPsec (인터넷 프로토콜 보안)을 사용 하 여 기밀 데이터를 암호화 합니다. IPsec을 사용 하 여 nps와 nps를 관리 하는 데 사용 하는 원격 클라이언트 컴퓨터 간의 통신을 암호화할 수 있습니다. 서버를 원격으로 관리 하려면 클라이언트 컴퓨터에 [Windows 10 용 원격 서버 관리 도구](https://www.microsoft.com/download/details.aspx?id=45520) 를 설치 하면 됩니다. 설치 후 MMC (Microsoft Management Console)를 사용 하 여 콘솔에 NPS 스냅인을 추가 합니다.

>[!IMPORTANT]
>Windows 10 Professional 또는 Windows 10 Enterprise의 전체 릴리스에서만 Windows 10 용 원격 서버 관리 도구를 설치할 수 있습니다.

NPS에 대 한 자세한 내용은 [nps (네트워크 정책 서버)](nps-top.md)를 참조 하세요.

