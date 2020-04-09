---
ms.assetid: 02580b2f-a339-4470-947c-d700b2d55f3f
title: 페더레이션 서버 팜을 만들어야 하는 경우
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 61e5c2c31ef4f6771c379c93e61b78640f4a180a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80858506"
---
# <a name="when-to-create-a-federation-server-farm"></a>페더레이션 서버 팜을 만들어야 하는 경우

AD FS 배포가 더 크고 조직의\-에 내결함성, 부하 분산 또는 확장성을 제공 하려는 경우 Active Directory Federation Services \(AD FS\) 페더레이션 서버 팜을 만드는 것이 좋습니다. 동일한 네트워크에 둘 이상의 페더레이션 서버를 만들고 각 서버를 동일한 페더레이션 서비스 사용 하도록 구성 하 고, 각 서버 토큰의 공개 키를 추가 하는 작업은에서 AD FS 관리 스냅인\-에 서명 인증서를\-하 여 페더레이션 서버 팜을 만듭니다.  
  
AD FS 페더레이션 서버 구성 마법사를 사용 하 여 페더레이션 서버 팜을 만들거나 기존 팜에 추가 페더레이션 서버를 설치할 수 있습니다. 자세한 내용은 [When to Create a Federation Server](When-to-Create-a-Federation-Server.md)를 참조하세요.  
  
> [!NOTE]  
> AD FS 페더레이션 서버 구성 마법사를 사용 하 여 **새 페더레이션 서버 팜을** 만드는 옵션을 선택 하는 경우 마법사는 Active Directory에서\) 인증서를 공유 하기 위한 컨테이너 개체 \(만들려고 합니다. 따라서 Active Directory에 이 컨테이너 개체를 만들 수 있는 권한이 있는 계정으로 페더레이션 서버 역할을 설정할 컴퓨터에 먼저 로그온하는 것이 중요합니다.  
  
페더레이션 서버를 팜으로 그룹화 하려면 먼저 해당 서버를 클러스터링 하 여 FQDN\) \(단일 정규화 된 도메인 이름에 도착 하는 요청이 서버 팜의 다양 한 페더레이션 서버로 라우팅되도록 합니다. 회사 네트워크 내부에 NLB\) \(네트워크 부하 분산을 배포 하 여 서버 클러스터를 만들 수 있습니다. 이 가이드에서는 팜의 각 페더레이션 서버를 클러스터링 하도록 NLB를 적절 하 게 구성 했다고 가정 합니다.  
  
Microsoft NLB 기술을 사용 하 여 클러스터 FQDN을 구성 하는 방법에 대 한 자세한 내용은 [클러스터 매개 변수 지정](https://go.microsoft.com/fwlink/?LinkID=74651)을 참조 하세요.  
  
## <a name="best-practices-for-deploying-a-federation-server-farm"></a>페더레이션 서버 팜 배포를 위한 모범 사례  
프로덕션 환경에 페더레이션 서버를 배포 하기 위한 다음 모범 사례를 따르는 것이 좋습니다.  
  
-   동시에 여러 페더레이션 서버를 배포 하거나 시간에 따라 팜에 서버를 더 추가 하는 경우 팜에 기존 페더레이션 서버의 서버 이미지를 만든 다음 추가 페더레이션 서버를 신속 하 게 만들어야 할 때 해당 이미지에서 설치 하는 것이 좋습니다.  
  
    > [!NOTE]  
    > 추가 페더레이션 서버를 배포 하는 데 서버 이미지 방법을 사용 하기로 결정 한 경우 새 서버를 팜에 추가할 때마다 [검사 목록: 페더레이션 서버 설정](../../ad-fs/deployment/Checklist--Setting-Up-a-Federation-Server.md) 에서 작업을 완료할 필요가 없습니다.  
  
-   NLB 또는 다른 형태의 클러스터링을 사용 하 여 많은 페더레이션 서버 컴퓨터에 단일 IP 주소를 할당 합니다.  
  
-   팜의 각 페더레이션 서버에 대 한 고정 IP 주소를 예약 하 고, DNS\) 구성 \(도메인 이름 시스템에 따라 DHCP\)\(동적 호스트 구성 프로토콜에 각 IP 주소에 대 한 제외를 삽입 합니다. Microsoft NLB 기술에서는 NLB 클러스터에 참여하는 각 서버에 고정 IP 주소가 할당되어야 합니다.  
  
-   AD FS 구성 데이터베이스가 SQL 데이터베이스에 저장 되는 경우 여러 페더레이션 서버에서 동시에 SQL 데이터베이스를 편집 하지 마세요.  
  
## <a name="configuring-federation-servers-for-a-farm"></a>팜에 대한 페더레이션 서버 구성  
다음 표에서는 각 페더레이션 서버가 팜 환경에 참여할 수 있도록 하기 위해 완료 해야 하는 작업에 대해 설명 합니다.  
  
|작업|설명|  
|--------|---------------|  
|SQL Server를 사용하여 AD FS 구성 데이터베이스를 저장하는 경우|페더레이션 서버 팜은 서명 인증서\-동일한 AD FS 구성 데이터베이스와 토큰을 공유 하는 둘 이상의 페더레이션 서버로 구성 됩니다. Windows 내부 데이터베이스 또는 SQL Server 데이터베이스에 구성 데이터베이스를 저장할 수 있습니다. SQL 데이터베이스에 구성 데이터베이스를 저장 하려는 경우 팜에 참여 하는 모든 새 페더레이션 서버에서 액세스할 수 있도록 구성 데이터베이스에 액세스할 수 있는지 확인 합니다. **참고:** 팜 시나리오의 경우 해당 팜에 페더레이션 서버로도 참여 하지 않는 컴퓨터에 구성 데이터베이스를 배치 하는 것이 중요 합니다. Microsoft NLB는 팜에 참여하는 컴퓨터가 서로 통신하는 것을 허용하지 않습니다. **참고:** 팜에 참여 하는 모든 페더레이션 서버에서 IIS\)\) \(인터넷 정보 서비스 AD FS AppPool의 id에 구성 데이터베이스에 대 한 읽기 권한이 있는지 확인 합니다.|  
|인증서 가져오기 및 공유|공용 인증 기관 \(CA\)에서 단일 서버 인증 인증서를 가져올 수 있습니다 (예: VeriSign). 그러면 모든 페더레이션 서버가 인증서의 동일한 개인 키 부분을 공유 하도록 인증서를 구성할 수 있습니다. 동일한 인증서를 공유하는 방법에 대한 자세한 내용은 [Checklist: Setting Up a Federation Server](../../ad-fs/deployment/Checklist--Setting-Up-a-Federation-Server.md)을 참조하세요. **참고:** AD FS 관리 스냅인\-서비스 통신 인증서로 페더레이션 서버에 대 한 서버 인증 인증서를 참조 합니다.<p>자세한 내용은 [Certificate Requirements for Federation Servers](Certificate-Requirements-for-Federation-Servers.md)를 참조하세요.|  
|동일한 SQL Server 인스턴스 가리키기|AD FS 구성 데이터베이스가 SQL 데이터베이스에 저장 되는 경우 새 페더레이션 서버는 팜에 있는 다른 페더레이션 서버에서 사용 하는 것과 동일한 SQL Server 인스턴스를 가리켜야 새 서버가 팜에 참여할 수 있습니다.|  
  
## <a name="see-also"></a>참고 항목
[Windows Server 2012의 AD FS 디자인 가이드](AD-FS-Design-Guide-in-Windows-Server-2012.md)
