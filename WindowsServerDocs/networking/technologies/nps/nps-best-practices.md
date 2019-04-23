---
title: 네트워크 정책 서버 모범 사례
description: 이 항목에서는 배포 및 Windows Server 2016에서 네트워크 정책 서버 관리에 대 한 모범 사례를 제공 합니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 90e544bd-e826-4093-8c3b-6a6fc2dfd1d6
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 6cbd606edec06a80767ee997ef6a1397b66b7843
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59834234"
---
# <a name="network-policy-server-best-practices"></a>네트워크 정책 서버 모범 사례

>적용 대상: Windows Server (반기 채널), Windows Server 2016

이 항목에서는 사용 하 여 배포 및 네트워크 정책 서버 관리에 대 한 모범 사례에 대해 자세히 알아보려면 \(NPS\)합니다.

다음 섹션에서는 NPS 배포의 다양 한 측면에 대 한 모범 사례를 제공합니다.

## <a name="accounting"></a>계정

다음은 NPS 로깅에 대 한 모범 사례입니다.

회계, NPS에서 로깅의 다음과 같은 두 종류가 있습니다.

- NPS에 대 한 이벤트 로깅 시스템 및 보안 이벤트 로그에서 이벤트를 기록 하려면 NPS 이벤트 로깅을 사용할 수 있습니다. 감사 및 문제해결 연결 시도에 주로 사용 됩니다.

- 사용자 인증 및 계정 요청을 기록 합니다. 텍스트 형식으로 또는 데이터베이스 형식 로그 파일에 사용자 인증 및 계정 관리 요청을 기록할 수 있습니다 또는 저장 프로시저는 SQL Server 2000 데이터베이스에 로그인 할 수 있습니다. 로깅 연결 분석 및 청구 목적으로 주로 사용 되 고 공격자 작업을 추적 하는 방법을 제공 하는 보안 조사 도구로 서 유용도 요청 합니다.

NPS 로깅 가장 효과적인 사용할 수 있도록 합니다.

- 로깅 켜기 \(처음에\) 인증 및 계정 레코드에 대 한 합니다. 환경에 적합 한 새로운 기능을 확인 한 후 이러한 선택 항목을 수정 합니다.

- 이벤트 로깅 로그를 유지 하기 위해 충분 한 용량을 사용 하 여 구성 되어 있는지 확인 합니다.

- 손상 되거나 삭제 된 경우 다시 사용할 수 없습니다 때문에 정기적으로 모든 로그 파일을 백업 합니다.

- 사용량을 추적 및 사용량에 대 한 요금을 청구 하는 부서 또는 사용자의 식별을 간소화 하려면 RADIUS 클래스 특성을 사용 합니다. 자동으로 생성 된 클래스 특성은 각 요청에 대해 고유 하지만 액세스 서버에 대 한 회신이 손실 요청을 다시 하는 경우 중복 레코드가 있을 수 있습니다. 정확 하 게 사용량을 추적 하 여 로그에서 중복 된 요청을 삭제 해야 합니다.

- 네트워크 액세스 서버 및 RADIUS 프록시 서버에 주기적으로 가상의 연결 요청 메시지를 전송 NPS 온라인 상태 인지 확인 하 고 사용 하 여 NPS 경우 합니다 **사용자 이름을 ping** 레지스트리 설정 합니다. 이 설정은 자동으로 이러한 false 연결 요청을 처리 하지 않고 거부 하도록 NPS를 구성 합니다. 또한 NPS 이벤트 로그를 더 쉽게 해석 하는 모든 로그 파일을 가상의 사용자 이름이 포함 된 트랜잭션을 기록 하지 않습니다.

- NAS 알림을 전달 하는 사용 하지 않도록 설정 합니다. 시작의 전달을 사용 하지 않도록 설정 하 고 (Nas) 네트워크 액세스 서버에서 중지 메시지는 원격 RADIUS 서버의 멤버를 NPS에 구성 하는 IS를 그룹화 합니다. 자세한 내용은 [NAS 알림 전달 사용 하지 않도록 설정](nps-disable-nas-notifications.md)합니다.

자세한 내용은 [네트워크 정책 서버 계정 구성](nps-accounting-configure.md)합니다.

- SQL Server 로그인을 사용 하 여 장애 조치 및 중복성을 제공 합니다 하려면 서로 다른 서브넷에 SQL Server를 실행 하는 두 개의 컴퓨터를 배치 합니다. SQL Server를 사용 하 여 **게시 만들기 마법사** 두 서버 간 데이터베이스 복제를 설정 합니다. 자세한 내용은 [SQL Server 기술 설명서](https://msdn.microsoft.com/library/ms130214.aspx) 하 고 [SQL Server 복제](https://msdn.microsoft.com/library/ms151198.aspx)합니다.

## <a name="authentication"></a>인증

다음은 인증에 대 한 모범 사례입니다.

- Protected Extensible Authentication Protocol 같은 인증서 기반 인증 방법을 사용 하 여 \(PEAP\) 및 Extensible Authentication Protocol \(EAP\) 강력한 인증에 대 한 합니다. 다양 한 공격에 취약 하며 안전 하지 않기 때문에 암호 인증 메서드를 사용 하지 마세요. PEAP를 사용 하 여 안전한 무선 인증을 위해\-MS\-CHAP v2는 것이 좋습니다, NPS는 사용자가 자신의 사용자 이름과 암호를 사용 하 여 자신의 id를 증명 하는 동안 서버 인증서를 사용 하 여 무선 클라이언트에 해당 id를 증명 합니다.  NPS를 사용 하 여 무선 배포에 대 한 자세한 내용은 참조 하세요. [배포 암호 기반 802.1x 인증 무선 액세스](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/cncg/wireless/a-deploy-8021x-wireless-access)합니다.
- 배포 전에 고유한 인증 기관을 \(CA\) Active Directory를 사용 하 여&reg; 인증서 서비스 \(AD CS\) PEAP 및 EAP 같은 강력한 인증서 기반 인증 방법을 사용 하는 경우는 NPSs에 서버 인증서를 사용을 해야 합니다. 또한 컴퓨터 인증서 및 사용자 인증서를 등록 하도록 CA를 사용할 수 있습니다. NPS 및 원격 액세스 서버에 서버 인증서를 배포 하는 방법에 대 한 자세한 내용은 참조 하세요. [802.1 X 유선 및 무선 배포에 대 한 서버 인증서 배포](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/cncg/server-certs/deploy-server-certificates-for-802.1x-wired-and-wireless-deployments)합니다.

## <a name="client-computer-configuration"></a>클라이언트 컴퓨터 구성

다음은 클라이언트 컴퓨터 구성에 대 한 모범 사례입니다.

- 에 도메인 구성원 802.1 X 클라이언트 컴퓨터의 모든 그룹 정책을 사용 하 여 자동으로 구성 합니다. 자세한 내용은 "항목의" 무선 네트워크 (IEEE 802.11) 정책 구성 섹션을 참조 하세요 [무선 액세스 배포](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/cncg/wireless/e-wireless-access-deployment#bkmk_policies)합니다.

## <a name="installation-suggestions"></a>설치 제안

다음은 NPS를 설치 하기 위한 모범 사례입니다.

- NPS를 설치 하기 전에 설치 하 고 각 NPS에서 RADIUS 클라이언트로 구성 하기 전에 로컬 인증 메서드를 사용 하 여 네트워크 액세스 서버를 테스트 합니다.

- 설치 하 고 NPS를 구성 하는 후 Windows PowerShell 명령을 사용 하 여 구성을 저장 [내보내기 NpsConfiguration](https://technet.microsoft.com/library/jj872749.aspx)합니다. NPS를 다시 구성 될 때마다가이 명령을 사용 하 여 NPS 구성을 저장 합니다.

>[!CAUTION]
>- 내보낸된 NPS 구성 파일은 RADIUS 클라이언트와 원격 RADIUS 서버 그룹의 멤버에 대 한 암호화 되지 않은 공유 암호를 포함 합니다. 따라서 안전한 위치에 파일을 저장 해야 합니다.
>- 내보내기 프로세스는 Microsoft SQL Server에 대 한 로깅 설정이 내보낸된 파일에 포함 되지 않습니다. 다른 NPS로 내보낸된 파일을 가져와야 하는 경우 수동으로 구성 해야 SQL Server 로깅 새 서버에 있습니다.

## <a name="performance-tuning-nps"></a>NPS를 튜닝 하는 성능

다음은 NPS를 튜닝 하는 성능에 대 한 모범 사례입니다.

- NPS 인증 및 권한 부여 응답 시간을 최적화 하 고 네트워크 트래픽을 최소화 하는 도메인 컨트롤러에 NPS를 설치 합니다.

- 때 유니버설 사용자 이름 \(Upn\) 또는 Windows Server 2008 및 Windows Server 2003 도메인에서 사용 되 고, NPS 글로벌 카탈로그를 사용 하 여 사용자를 인증 합니다. 이 작업을 수행 하는 데 걸리는 시간을 최소화 하려면 글로벌 카탈로그 서버 또는 글로벌 카탈로그 서버와 동일한 서브넷에 있는 서버에 NPS를 설치 합니다.

- 있고 경우에 구성 된 원격 RADIUS 서버 그룹, NPS 연결 요청 정책에서 선택을 취소 합니다 **다음 원격 RADIUS 서버 그룹의 서버에서 계정 정보를 기록** 확인란, 이러한 그룹은 여전히 네트워크 액세스 서버를 보내는 \(NAS\) 시작 하 고 알림 메시지를 중지 합니다. 이렇게 하면 불필요 한 네트워크 트래픽을 만들어집니다. 이 트래픽을 제거 하려면 선택을 취소 하 여 각 원격 RADIUS 서버 그룹의 개별 서버에 대 한 알림을 전달 NAS를 해제 합니다 **전달 네트워크 시작 및 중지이 서버에 알림을** 확인란 합니다.

## <a name="using-nps-in-large-organizations"></a>대규모 조직에서는 NPS를 사용 하 여

다음은 대규모 조직에서는 NPS를 사용 하는 모범 사례입니다.

- 네트워크 정책에 대 한 액세스를 제한 하려면 사용 중인 경우 특정 제외한 모든 그룹의 모든 사용자에 대 한 액세스를 허용 하려는 사용자에 대 한 유니버설 그룹을 만들 한 다음이 유니버설 그룹에 대 한 액세스를 부여 하는 네트워크 정책을 만듭니다. 특히 많은 수의 네트워크에 있는 경우 유니버설 그룹에 직접 모든 사용자가 배치 하지 마세요. 대신, 유니버설 그룹의 멤버인 사용자가 해당 그룹에 추가 하는 별도 그룹을 만듭니다.

- 가능 하면 사용자에 게 참조 하는 사용자 계정 이름을 사용 합니다. 사용자는 도메인 구성원 자격에 관계 없이 동일한 사용자 계정 이름이 있습니다. 이 방법은 도메인 수가 많은 조직에서 필요할 수 있는 확장성을 제공 합니다.

- 네트워크 정책 서버를 설치한 경우 \(NPS\) 도메인 외의 컴퓨터에서 컨트롤러 및 NPS 수신 하는 많은 수의 초당 인증 요청의 수를 늘려 NPS 성능을 향상 시킬 수 있습니다 NPS와 도메인 컨트롤러 간에 허용 되는 동시 인증입니다. 자세한 내용은 다음을 참조하세요. 

## <a name="security-issues"></a>보안 문제

다음은 보안 문제를 줄이기 위한 모범 사례입니다.

NPS를 원격으로 관리할 때 일반 텍스트로 네트워크를 통해 중요 한 정보나 기밀 데이터 (예: 공유 암호 또는 암호)를 보내지 않습니다. NPSs의 원격 관리를 위한 권장된 하는 방법이 두 가지

- 원격 데스크톱 서비스를 사용 하 여 NPS 액세스. 원격 데스크톱 서비스를 사용 하면 클라이언트와 서버 간의 데이터 전송 되지 않습니다. Windows에서 원격 데스크톱 연결 라고 하는 원격 데스크톱 서비스 클라이언트에 전송 됩니다 (예: 운영 체제 데스크톱 및 NPS 콘솔 이미지) 서버의 사용자 인터페이스만&reg; 10입니다. 클라이언트가 보냅니다 키보드 및 마우스 입력을 사용 하도록 설정 하는 원격 데스크톱 서비스 서버에서 로컬로 처리 됩니다. 사용자가 원격 데스크톱 서비스에 로그온 하는 경우에 해당 개별 클라이언트 세션을 서버에서 관리 되는 서로 관련이 있으며를 볼 수 있습니다. 또한 원격 데스크톱 연결 클라이언트와 서버 간에 128 비트 암호화를 제공합니다.

- 인터넷 프로토콜 보안 (IPsec)를 사용 하 여 기밀 데이터를 암호화 합니다. NPS를 관리 하는 데 사용 하는 원격 클라이언트 컴퓨터와 NPS 간의 통신을 암호화 하려면 IPsec을 사용할 수 있습니다. 설치할 수는 서버를 원격으로 관리 하는 [원격 서버 관리 도구에 대 한 Windows 10](https://www.microsoft.com/download/details.aspx?id=45520) 클라이언트 컴퓨터의 합니다. 설치 후 콘솔에 NPS 스냅인을 추가 하려면 Microsoft Management Console (MMC)를 사용 합니다.

>[!IMPORTANT]
>원격 서버 관리 도구에 대 한 Windows 10 정식 버전의 Windows 10 Professional 또는 Windows 10 Enterprise만 설치할 수 있습니다.

NPS에 대 한 자세한 내용은 참조 하세요. [네트워크 정책 (NPS 서버)](nps-top.md)합니다.

