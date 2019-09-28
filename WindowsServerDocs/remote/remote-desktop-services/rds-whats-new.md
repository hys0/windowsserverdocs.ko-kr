---
title: 원격 데스크톱 서비스의 새로운 기능
description: 새로운 기능 Windows Server 2016에서 RDS 설명을 제공합니다.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: chrimo
ms.date: 10/11/2016
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 04d52dff-e61b-4633-9908-be8600abc2ba
author: ChristianMontoya
manager: scottman
ms.openlocfilehash: e976f4d4ffa33efb98a744909f8c46ba498ea43b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403840"
---
# <a name="whats-new-in-remote-desktop-services"></a>원격 데스크톱 서비스의 새로운 기능

원격 데스크톱 서비스 (RDS) 기반으로 Windows Server 2016은 다양 한 고객 시나리오를 사용 하도록 설정 하는 가상화 플랫폼입니다. 전반적인 RDS 솔루션에서 향상 된 원격 데스크톱 팀과 다른 기술 파트너가 Microsoft에 의해 수행 된 작업을 통합 합니다. 다음과 같은 시나리오 및 기술에는 새로운 또는 Windows Server 2016에서 개선 된입니다.

또한 Ignite 2016에서 세션을 확인하세요. [Windows Server 2016에서 RDS 향상 기능을 활용](https://channel9.msdn.com/Events/Ignite/2016/BRK3098)합니다. 이 비디오에서는 제품 팀의 모든 새로운 기능과 향상 된 기능 vGPU 지원을 비롯 하 여 원격 데스크톱 서비스에 검토 합니다. 

## <a name="app-compatibility---windows-server-2016-and-windows-10"></a>응용 프로그램 호환성-Windows Server 2016 및 Windows 10
Windows 10의 동일한 기반 기술을 기반으로 한 Windows Server 2016 뿐만 아니라는 동일한 모양과 느낌이 필요 하다는 데스크톱 수 있지만 대부분의 동일한 애플리케이션을 실행할 수도 있습니다. (아래 참조) 그래픽 기능을 통해 Windows Server 2016 쌍 생산성을 높일 수 있는 모든 사용자에 대 한 환경을 제공 합니다. 

## <a name="azure-sql-database---the-new-database-for-your-highly-available-environment"></a>Azure SQL 데이터베이스-항상 사용 가능한 환경에 대 한 새 데이터베이스
RD 연결 브로커는 배포 정보 (예: 연결 상태 및 사용자/호스트 매핑) 모두 Azure SQL 데이터베이스와 같은 공유 SQL 데이터베이스에 저장할 수 있습니다. SQL Server Alwayson 가용성 그룹 배포 설명서를 버릴 Azure SQL 데이터베이스에 연결 문자열 잡은 항상 사용 가능한 환경을 사용 하 여 시작 합니다.

추가 정보: [원격 데스크톱 연결 브로커 고가용성 환경에 Azure SQL DB 사용](https://blogs.technet.microsoft.com/enterprisemobility/2016/05/03/new-windows-server-2016-capability-use-azure-sql-db-for-your-remote-desktop-connection-broker-high-availability-environment/)

## <a name="graphics---solving-graphics-needs-across-various-scenarios"></a>그래픽-다양 한 시나리오에서 그래픽 요구를 해결 합니다.
Hyper-v의 불연속 디바이스 할당, 덕분에 Gpu는 GPU 필요한 애플리케이션에서 사용할 수 있도록 VM에 직접 호스트 컴퓨터에 이제 매핑할 수 있습니다. 또한 향상 되었습니다 OpenGL 4.4, OpenCL 1.1, 4, 000 해상도 및 Windows Server 가상 컴퓨터에 대 한 지원을 포함 하는 RemoteFX vGPU에 있습니다.

추가 정보: [개별 디바이스 할당](https://blogs.technet.microsoft.com/virtualization/2015/11/)

## <a name="rd-connection-broker---improved-connection-handling-during-logon-storms"></a>RD 연결 브로커-로그온 폭주가 발생 하는 동안 처리 되는 향상 된 연결
향상 된 연결 처리와 RD 연결 브로커 "로그온 폭주"가 발생 하는 동안 종종 볼만 개 이상의 동시 로그온 요청을 처리할 수 되었습니다. 향상 된 RD 연결 브로커는 또한 추가 하 여 간단한 배포를 사용 하는 유지 관리 신속 하 게 서버 환경에 다시 추가할 수 있습니다.

추가 정보: [향상된 원격 데스크톱 연결 브로커 성능](https://blogs.technet.microsoft.com/enterprisemobility/2015/12/15/improved-remote-desktop-connection-broker-performance-with-windows-server-2016-and-windows-server-2012-r2-hotfix-kb3091411/)

## <a name="rdp-10---new-capabilities-built-into-the-protocol"></a>RDP 10-프로토콜에 기본 제공 되는 새로운 기능
이제 RDP 10 비디오 및 텍스트 모두에 걸쳐 적절 하 게 최적화 H.264/AVC 444 코덱을 사용 합니다. 이 릴리스와 함께 펜 remoting도 지원 됩니다. 이러한 기능을 사용 하면 원격 세션 가깝게도 로컬 세션을 시작 합니다.  

추가 정보: [Windows 10 및 Windows Server 2016의 RDP 10 AVC/H.264 향상](https://blogs.technet.microsoft.com/enterprisemobility/2016/01/11/remote-desktop-protocol-rdp-10-avch-264-improvements-in-windows-10-and-windows-server-2016-technical-preview/)

## <a name="personal-session-desktops---providing-individual-desktops-to-any-end-user"></a>개인 세션 데스크톱-모든 최종 사용자에 게 개별 데스크톱 제공
개인 세션 데스크톱은 고유한 개인 데스크톱을 클라우드에서 호스트 하는 새로운 방법입니다. 관리 권한 및 전용된 세션 호스트 제거 호스팅 환경 사용자 하려는 것 처럼 데스크톱 관리의 복잡성은 자체입니다.

추가 정보: [개인 세션 데스크톱](rds-personal-session-desktops.md)
