---
ms.assetid: 02580b2f-a339-4470-947c-d700b2d55f3f
title: 페더레이션 서버 팜을 만들어야 하는 경우
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 91a0122198639bf75e9e43e9da9edf68dd0453d9
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2019
ms.locfileid: "66190682"
---
# <a name="when-to-create-a-federation-server-farm"></a>페더레이션 서버 팜을 만들어야 하는 경우

Active Directory Federation Services에서 페더레이션 서버 팜을 만드는 것이 좋습니다 \(AD FS\) 있고 경우에 AD FS 배포를 더 큰 내결함성을 제공, 로드 하려는\-분산 또는 확장성을 프로그램 조직의 페더레이션 서비스입니다. 동일한 네트워크에 둘 이상의 페더레이션 서버를 만들고, 각각 동일한 페더레이션 서비스를 사용 하도록 구성 하 고 각 서버의 공개 키 토큰의 추가 act\-서명 인증서를 AD FS 관리 스냅인\-에서 페더레이션 서버 팜을 만듭니다.  
  
페더레이션 서버 팜을 만들거나 AD FS 페더레이션 서버 구성 마법사를 사용 하 여 기존 팜에 추가 페더레이션 서버를 설치할 수 있습니다. 자세한 내용은 [When to Create a Federation Server](When-to-Create-a-Federation-Server.md)를 참조하세요.  
  
> [!NOTE]  
> 만드는 옵션을 선택 하는 경우는 **새 페더레이션 서버 팜에서** AD FS 페더레이션 서버 구성 마법사를 사용 하 여 마법사 하려고 컨테이너 개체를 만들 \(인증서 공유를 위한\) Active directory. 따라서 Active Directory에 이 컨테이너 개체를 만들 수 있는 권한이 있는 계정으로 페더레이션 서버 역할을 설정할 컴퓨터에 먼저 로그온하는 것이 중요합니다.  
  
페더레이션 서버 팜으로 그룹화 할 수 있습니다, 전에 먼저 클러스터 되어야는 완전히 단일에 도착 하는 요청에 정규화 된 도메인 이름 \(FQDN\) 서버 팜의 다양 한 페더레이션 서버로 라우팅됩니다. 네트워크 부하 분산 배포 하 여 서버 클러스터를 만들 수 있습니다 \(NLB\) 회사 네트워크 내부에 있습니다. 이 가이드에서는 각 팜의 페더레이션 서버 클러스터를 NLB 적절 하 게 구성 된 가정 합니다.  
  
Microsoft NLB 기술을 사용 하 여 클러스터 FQDN을 구성 하는 방법에 대 한 자세한 내용은 참조 [클러스터 매개 변수 지정](https://go.microsoft.com/fwlink/?LinkID=74651)합니다.  
  
## <a name="best-practices-for-deploying-a-federation-server-farm"></a>페더레이션 서버 팜 배포를 위한 모범 사례  
프로덕션 환경에서 페더레이션 서버를 배포 하기 위한 다음 모범 사례를 사용 하는 것이 좋습니다.  
  
-   동시에 여러 페더레이션 서버를 배포할 경우는 추가할 서버를 팜에 시간이 지남에 따라 알고는 것이 좋습니다 팜의 기존 페더레이션 서버에 대 한 서버 이미지를 만들고 다음 cr 해야 할 때 해당 이미지에서 설치 추가 페더레이션 서버 eate 신속 하 게 합니다.  
  
    > [!NOTE]  
    > 추가 페더레이션 서버를 배포 하기 위한 서버 이미지 방법을 사용 하기로 하는 경우 작업을 완료 필요가 없습니다 [검사 목록: Setting Up a Federation Server](../../ad-fs/deployment/Checklist--Setting-Up-a-Federation-Server.md) 팜에 새 서버를 추가할 때마다 합니다.  
  
-   NLB 또는 다른 형태의 클러스터링을 사용 하 여 여러 페더레이션 서버 컴퓨터에 대 한 단일 IP 주소를 할당 합니다.  
  
-   각 페더레이션 서버 팜의 도메인 이름 시스템에 따라 고정 IP 주소를 예약 \(DNS\) 구성, 동적 호스트 구성 프로토콜에서 각 IP에 대 한 제외 주소 삽입 \(DHCP\). Microsoft NLB 기술에서는 NLB 클러스터에 참여하는 각 서버에 고정 IP 주소가 할당되어야 합니다.  
  
-   AD FS 구성 데이터베이스를 SQL 데이터베이스에 저장할 경우 동시에 여러 페더레이션 서버에서 SQL 데이터베이스를 편집 하지 마세요.  
  
## <a name="configuring-federation-servers-for-a-farm"></a>팜에 대한 페더레이션 서버 구성  
다음 표에서 각 페더레이션 서버 팜된 환경에 참여할 수 있도록 완료 해야 하는 작업을 설명 합니다.  
  
|태스크|설명|  
|--------|---------------|  
|SQL Server를 사용하여 AD FS 구성 데이터베이스를 저장하는 경우|페더레이션 서버 팜에 AD FS 구성 데이터베이스와 토큰을 공유 하는 두 개 이상의 페더레이션 서버 구성\-서명 인증서. Windows 내부 데이터베이스 또는 SQL Server 데이터베이스에 구성 데이터베이스를 저장할 수 있습니다. 구성 데이터베이스를 SQL 데이터베이스에 저장 하려는 경우는 팜에 참여 하는 모든 새 페더레이션 서버에서 액세스할 수 있도록 구성 데이터베이스에 액세스할 수 있는지 확인 해야 합니다. **참고:** 팜 시나리오에 대 한 것이 중요 구성 데이터베이스는 팜에 페더레이션 서버로 참여 하지 않는 컴퓨터에 있는 것입니다. Microsoft NLB는 팜에 참여하는 컴퓨터가 서로 통신하는 것을 허용하지 않습니다. **참고:** 인터넷 정보 서비스에서 AD FS AppPool의 id 했는지 \(IIS\) \) 모든 페더레이션 팜에 참여 하는 서버에 구성 데이터베이스에 대 한 읽기 액세스입니다.|  
|인증서 가져오기 및 공유|공용 인증 기관에서 단일 서버 인증 인증서를 얻을 수 있습니다 \(CA\)-예를 들어, VeriSign 합니다. 그런 다음 모든 페더레이션 서버 인증서의 동일한 개인 키 부분을 공유할 수 있도록 인증서를 구성할 수 있습니다. 동일한 인증서를 공유 하는 방법에 대 한 자세한 내용은 참조 하세요. [검사 목록: 페더레이션 서버를 설정할](../../ad-fs/deployment/Checklist--Setting-Up-a-Federation-Server.md)합니다. **참고:** AD FS 관리 스냅인\-에서 서버 인증 인증서를 서비스 통신 인증서로 페더레이션 서버에 대 한 참조입니다.<br /><br />자세한 내용은 [Certificate Requirements for Federation Servers](Certificate-Requirements-for-Federation-Servers.md)를 참조하세요.|  
|동일한 SQL Server 인스턴스 가리키기|AD FS 구성 데이터베이스를 SQL 데이터베이스에 저장할 경우 새 페더레이션 서버는 새 서버 팜에 참여할 수 있도록는 팜의 다른 페더레이션 서버에서 사용 되는 동일한 SQL Server 인스턴스를 가리키도록 해야 합니다.|  
  
## <a name="see-also"></a>관련 항목
[Windows Server 2012의 AD FS 디자인 가이드](AD-FS-Design-Guide-in-Windows-Server-2012.md)
