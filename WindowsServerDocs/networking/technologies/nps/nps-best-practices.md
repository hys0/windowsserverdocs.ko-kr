---
title: 네트워크 정책 서버에 대 한 유용한 정보
description: 이 항목에서는 배포 및 Windows Server 2016에 네트워크 정책 서버 관리에 대 한 유용한 정보를 제공 합니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 90e544bd-e826-4093-8c3b-6a6fc2dfd1d6
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 5a9a68965d0d19504352ad67f7ab268b3d344fb2
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="network-policy-server-best-practices"></a>네트워크 정책 서버에 대 한 유용한 정보

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

배포 하 고 네트워크 정책 서버 \(NPS\) 관리에 대 한 유용한에 대 한 자세한 내용은이 항목을 사용할 수 있습니다.

다음 섹션 NPS 배포의 다양 한 기능에 대 한 유용한 정보를 제공합니다.

## <a name="accounting"></a>계정 관리

다음은 NPS 로그인에 대 한 유용한입니다.

두 가지 방법으로 계정, 로그인, NPS 또는 수 있습니다.

- 이벤트 로깅에서 nps 합니다. 시스템 및 보안 이벤트 로그에 기록 NPS 이벤트 이벤트 로깅에서 사용할 수 있습니다. 이 주로 감사 및 문제 해결 시도 연결에 사용 됩니다.

- 사용자 인증과 계정 요청 로그온 합니다. 사용자 인증과 계정에 대 한 요청 텍스트 형식이 나 데이터베이스 형식 파일 로그인 로그인 할 수 있습니다 또는 SQL Server 2000 데이터베이스에 저장 된 절차에 로그인 할 수 있습니다. 요청 로깅이 주로 연결 분석 및 청구 목적을 위해 사용 되 고 공격자 동작을 추적 하는 방법을 제공 하는 보안 조사 도구도 큰 도움이 됩니다.

가장 효과적인 NPS 로깅 사용 하려면:

- 인증과 계정 기록의 로깅 \(initially\) 켭니다. 귀하의 환경에 대 한 적절 한 란 결정 하 고 나면 이러한 선택 수정 합니다.

- 이벤트 로깅에서 충분 한 로그를 유지할는 용량을으로 구성 되어 있는지 확인 합니다.

- 손상 되거나 삭제 될 때 만들어야 수 없는 때문에 모든 로그 파일을 정기적으로 백업 합니다.

- 사용량을 추적 하 식별 어떤 부서 또는 사용자 사용량에 따라 요금이 결제를 간단 하 게 RADIUS Class 특성을 사용 합니다. 자동으로 생성 된 Class 특성 지 각 요청에 대 한 고유 중복 레코드가 액세스 서버에 회신 손실 되는 요청을 다시 보냅니다 하는 경우에서 있을 수 있습니다. 사용량을 추적 정확 하 게 하려면 로그에서 중복 요청을 삭제 해야 할 수 있습니다.

- 네트워크 액세스 서버 및 RADIUS 프록시 서버 주기적으로 가상 연결 요청 메시지를 보내는 NPS NPS 서버 온라인 상태 인지 확인을 위해 사용 하는 경우는 **사용자 이름 ping** 레지스트리 설정 합니다. 이 설정을 구성 NPS를 자동으로 처리 하지 않고 이러한 false 연결 요청을 거부 합니다. 또한, NPS 거래 이벤트 로그를 보다 쉽게 해석 하는 모든 로그 파일에서 가상 사용자 이름을 포함 된 기록 하지 않습니다.

- NAS 알림 전달 사용 하지 않도록 설정 합니다. 시작 전달 사용 하지 않도록 설정 및 원격 RADIUS 서버의 회원 네트워크 Nas 액세스 서버 ()에서 중지 메시지 그룹 NPS 구성 해당 IS 합니다. 자세한 내용은 참조 [NAS 알림 전달 비활성화](nps-disable-nas-notifications.md)합니다.

자세한 내용은 참조 [네트워크 정책 서버 계정과 구성](nps-accounting-configure.md)합니다.

- 장애 조치과 중복 SQL Server 로깅을 제공 하려면 서로 다른 서브넷 SQL Server 실행 두 대의 컴퓨터를 배치 합니다. SQL Server 사용 하 여 **게시 만들기 마법사** 두 서버 복제가 데이터베이스를 설정 합니다. 자세한 내용은 참조 [SQL Server 기술 문서](https://msdn.microsoft.com/library/ms130214.aspx) 및 [SQL Server 복제](https://msdn.microsoft.com/library/ms151198.aspx)합니다.

## <a name="authentication"></a>인증

인증에 대 한 유용한은 다음과가 같습니다.

- 강력한 인증에 대 한 확장 인증 프로토콜 보호 \(PEAP\) 확장 인증 프로토콜 \(EAP\) 등 가지 옵션이 인증 방법을 사용 합니다. 다양 한 공격에 안전 하지 않은 있기 때문에 암호만 인증 방법을 사용 하지 마십시오. 무선 인증 보안에 대 한 PEAP\ 기능 MS\ 기능을 제공 v 2를 사용 하는 것이 좋습니다 NPS 서버가 해당 id 무선 클라이언트를 사용자의 신원을 사용자 이름 및 암호와 입증 하는 동안 서버 인증서를 사용 하 여 증명 합니다.  무선 배포에서 NPS 사용에 대 한 자세한 내용은 참조 [암호 배포 기반 802.1 X 인증 무선 액세스](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/cncg/wireless/a-deploy-8021x-wireless-access)합니다.
- 인증 기관 배포 \(CA\) Active directory&reg; 인증서 서비스 \ (AD CS \) 서버 NPS 서버의 인증서 사용 해야 하는 등 PEAP EAP 강력한 인증서 기반 인증 방법을 사용 하면 됩니다. 등록 인증서 컴퓨터와 사용자 인증서를 인증도 사용할 수 있습니다. 에 대 한 자세한 내용은 서버 인증서 NPS 및 원격 액세스 서버에 배포, [802.1 X 유선 및 무선 배포에 대 한 서버 인증서 배포](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/cncg/server-certs/deploy-server-certificates-for-802.1x-wired-and-wireless-deployments)합니다.

## <a name="client-computer-configuration"></a>클라이언트 컴퓨터 구성

클라이언트 컴퓨터 구성에 대 한 유용한은 다음과가 같습니다.

- 사용자 도메인 구성원 802.1 X 클라이언트 컴퓨터의 모든 그룹 정책을 사용 하 여 자동으로 구성 됩니다. 자세한 내용은 "항목에서" 구성 무선 네트워크 (IEEE 802.11) 정책을 섹션 참조 [무선 액세스 배포](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/cncg/wireless/e-wireless-access-deployment#bkmk_policies)합니다.

## <a name="installation-suggestions"></a>설치 제안

다음은 NPS 설치 하기 위한 모범 사례.

- 설치 하기 전에 NPS, 설치 하 고 각에서 NPS RADIUS 클라이언트로 구성 하기 전에 로컬 인증 방법을 사용 하 여 네트워크 액세스 서버 테스트 합니다.

- 을 설치 및 구성 NPS 나면 Windows PowerShell 명령을 사용 하 여 구성을 저장 [내보내기 NpsConfiguration](https://technet.microsoft.com/en-us/library/jj872749.aspx)합니다. 이 명령을 NPS 서버 재구성 때마다도 NPS 구성을 저장 합니다.

>[!CAUTION]
>- 내보낸된 NPS 구성 파일 RADIUS 클라이언트 및 원격 RADIUS 서버 그룹의 회원에 대 한 암호화 되지 않은 공유 암호 포함 되어 있습니다. 이 인해 안전한 장소에 파일을 저장 하면 있는지 확인 합니다.
>- 내보내기 프로세스는 Microsoft SQL Server에 대 한 설정을 로깅 내보낸된 파일에 포함 되지 않습니다. 내보낸된 파일을 다른 NPS 서버 가져오면 SQL Server 새 서버에 기록 수동으로 구성 해야 합니다.

## <a name="performance-tuning-nps"></a>성능 NPS 조정

성능 NPS 조정에 대 한 유용한은 다음과가 같습니다.

- NPS 인증과 응답 시간을 최적화 하 고 네트워크 교통 최소화, NPS 도메인 컨트롤러에 설치 합니다.

- 사용자 이름 유니버설 \(UPNs\) 또는 Windows Server 2008 및 Windows Server 2003 도메인을 사용 하면 NPS 드를 사용 하 여 사용자를 인증 합니다. 이 작업을 수행 하는 데 걸리는 시간을 최소화 하려면 NPS 드 서버 또는 드 서버와 같은 서브넷 켜져 있는 서버에 설치 합니다.

- 때 원격 RADIUS 서버 그룹 구성 되어 있으며, NPS 연결 요청 정책에서 선택을 취소는 **다음 원격 RADIUS 서버 그룹에서 계정 정보는 서버에 기록** 확인란을 이러한 그룹 여전히 보낸 네트워크 액세스 서버 \(NAS\) 시작 알림 메시지를 중지 하 고 있습니다. 불필요 한 네트워크 교통을 만듭니다. 이 교통을 제거 하려면 NAS 알림 전달 원격 RADIUS 서버 그룹 각각의 개별 서버에 대 한 선택을 취소 하 여 사용 안 함은 **앞으로 네트워크 시작 및 중지이 서버에 알림에** 확인란을 선택 합니다.

## <a name="using-nps-in-large-organizations"></a>NPS 대기업에서 사용 하 여

다음은 NPS 대기업에서 사용 하기 위한 모범 사례.

- 네트워크 정책에 대 한 액세스를 제한 하기 위해 사용 하는 경우 모든 있지만 특정 그룹의 모든 사용자에 대 한 액세스를 허용 하려면 사용자에 대 한 유니버설 그룹을 만들고 유니버설이 그룹에 대 한 액세스 권한을 부여 하는 네트워크 정책 만듭니다. 많은 수의 네트워크에 있는 경우에 특히 유니버설 그룹에 직접 모든 사용자에 게 부여 하지 마십시오. 대신 유니버설 그룹의 회원 및 사용자가 해당 그룹에 추가 하는 별도 그룹 만듭니다.

- 사용자 계정 이름을 사용 하 여 엔지니어가 가능한 한 사용자에 게 참조할 수 있습니다. 사용자는 도메인 구성원에 관계 없이 동일 사용자 계정 이름을 가질 수 있습니다. 이 이렇게 하는 도메인의 많은 조직에서 필요할 수 있는 확장성을 제공 합니다.

- 네트워크 정책 서버 \(NPS\) 도메인 컨트롤러 아닌 다른 컴퓨터에 설치한 경우 NPS 서버 인증 요청 초당 많은 수신 허용 NPS 서버와 도메인 컨트롤러 동시 인증 수가 증가 하 여 NPS 성능을 개선할 수 있습니다. 자세한 내용은 참조 하세요. 

## <a name="security-issues"></a>보안 문제

다음은 보안 문제를 줄이기 위한 모범 사례.

NPS 서버를 원격으로 관리 하는 경우 일반 네트워크를 통해 중요 한 기밀 데이터 (예: 공유 암호 또는 암호)를 보내지 않습니다. 원격 NPS 서버 관리 하기 위한 권장된 방법 두 가지

- 원격 데스크톱 서비스를 사용 하 여 NPS 서버에 액세스할 수 있습니다. 원격 데스크톱 서비스를 사용 하면 데이터가 클라이언트 및 서버 간에 전송 되지 않습니다. Windows에서 원격 데스크톱 연결 라고 하는 클라이언트 원격 데스크톱 서비스에는 사용자 인터페이스 (예: 데스크톱 운영 체제 및 NPS 콘솔 이미지) 서버 전송&reg; 10 합니다. 클라이언트가 보냅니다 키보드와 마우스를 입력 하 고, 원격 데스크톱 서비스가 설정 된 서버 로컬로 처리 합니다. 원격 데스크톱 서비스가 사용자가 로그인을의 개별 클라이언트 세션을에서 서버 관리 독립적으로 했던 볼 수 있습니다. 또한, 원격 데스크톱 연결 128-bit 클라이언트 및 서버의 암호화를 제공합니다.

- 중요 한 기밀 데이터를 암호화 하 인터넷 프로토콜 보안을 사용 합니다. IPsec NPS 서버 NPS 관리를 사용 하는 클라이언트 원격 컴퓨터와 통신 암호화를 사용할 수 있습니다. 원격 서버 관리를 설치할 수 있는 [Windows 10에 대 한 원격 서버 관리 도구](https://www.microsoft.com/download/details.aspx?id=45520) 클라이언트 컴퓨터에서 합니다. 설치 후 Microsoft Management Console (MMC) 사용 하 여 본체에 NPS 서버 스냅인 추가 합니다.

>[!IMPORTANT]
>Windows 10에 대 한 Windows 10 Professional 또는 Windows 10 Enterprise 전체 출시에만 원격 서버 관리 도구를 설치할 수 있습니다.

NPS에 대 한 자세한 내용은 참조 [네트워크 NPS 정책 서버 ()](nps-top.md)합니다.

