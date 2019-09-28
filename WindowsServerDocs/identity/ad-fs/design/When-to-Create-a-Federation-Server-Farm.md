---
ms.assetid: 02580b2f-a339-4470-947c-d700b2d55f3f
title: 페더레이션 서버 팜을 만들어야 하는 경우
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: fcfc7d640d3688bf0e23557af9bd56082418ef37
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71358938"
---
# <a name="when-to-create-a-federation-server-farm"></a>페더레이션 서버 팜을 만들어야 하는 경우

Active Directory Federation Services \(AD FS @ no__t-1에서 페더레이션 서버 팜을 만드는 것이 좋습니다. AD FS 배포가 크고 내결함성을 제공 하려는 경우, 부하 @ no__t-2balancing 또는 조직의 페더레이션에 확장성을 제공 하려는 경우 출력소. 동일한 네트워크에 둘 이상의 페더레이션 서버를 만들고 각각 동일한 페더레이션 서비스 사용 하도록 구성한 다음 각 서버의 토큰 @ no__t-0signing 인증서의 공개 키를 AD FS 관리 no__t에 추가 하는 작업은 1in를 만듭니다. 페더레이션 서버 팜.  
  
AD FS 페더레이션 서버 구성 마법사를 사용 하 여 페더레이션 서버 팜을 만들거나 기존 팜에 추가 페더레이션 서버를 설치할 수 있습니다. 자세한 내용은 [When to Create a Federation Server](When-to-Create-a-Federation-Server.md)를 참조하세요.  
  
> [!NOTE]  
> AD FS 페더레이션 서버 구성 마법사를 사용 하 여 **새 페더레이션 서버 팜을** 만드는 옵션을 선택 하면 마법사가 Active Directory에서 @no__t 1for certificate @ no__t-2를 사용 하 여 컨테이너 개체를 만들려고 합니다. 따라서 Active Directory에 이 컨테이너 개체를 만들 수 있는 권한이 있는 계정으로 페더레이션 서버 역할을 설정할 컴퓨터에 먼저 로그온하는 것이 중요합니다.  
  
페더레이션 서버를 팜으로 그룹화 하려면 먼저 해당 서버를 클러스터링 하 여 단일 정규화 된 도메인 이름 \(FQDN @ no__t-1에 도달 하는 요청이 서버 팜의 다양 한 페더레이션 서버로 라우팅되도록 합니다. 회사 네트워크 내에서 네트워크 부하 분산 \(NLB @ no__t-1을 배포 하 여 서버 클러스터를 만들 수 있습니다. 이 가이드에서는 팜의 각 페더레이션 서버를 클러스터링 하도록 NLB를 적절 하 게 구성 했다고 가정 합니다.  
  
Microsoft NLB 기술을 사용 하 여 클러스터 FQDN을 구성 하는 방법에 대 한 자세한 내용은 [클러스터 매개 변수 지정](https://go.microsoft.com/fwlink/?LinkID=74651)을 참조 하세요.  
  
## <a name="best-practices-for-deploying-a-federation-server-farm"></a>페더레이션 서버 팜 배포를 위한 모범 사례  
프로덕션 환경에 페더레이션 서버를 배포 하기 위한 다음 모범 사례를 따르는 것이 좋습니다.  
  
-   동시에 여러 페더레이션 서버를 배포 하거나 시간에 따라 팜에 서버를 더 추가 하는 경우 팜에 기존 페더레이션 서버의 서버 이미지를 만든 다음, cr을 필요할 때 해당 이미지에서 설치 하는 것이 좋습니다. 추가 페더레이션 서버를 신속 하 게 추가 합니다.  
  
    > [!NOTE]  
    > 추가 페더레이션 서버를 배포 하는 데 서버 이미지 방법을 사용 하기로 결정 하는 경우 [Checklist 목록에서 작업을 완료할 필요가 없습니다. 팜에 새 서버를 추가할 때마다 페더레이션 서버 @ no__t를 설정 합니다.  
  
-   NLB 또는 다른 형태의 클러스터링을 사용 하 여 많은 페더레이션 서버 컴퓨터에 단일 IP 주소를 할당 합니다.  
  
-   팜의 각 페더레이션 서버에 대 한 고정 IP 주소를 예약 하 고 도메인 이름 시스템 \(DNS @ no__t 구성에 따라 동적 호스트 구성 프로토콜 \(DHCP @ no__t-3에 각 IP 주소에 대 한 제외를 삽입 합니다. Microsoft NLB 기술에서는 NLB 클러스터에 참여하는 각 서버에 고정 IP 주소가 할당되어야 합니다.  
  
-   AD FS 구성 데이터베이스가 SQL 데이터베이스에 저장 되는 경우 여러 페더레이션 서버에서 동시에 SQL 데이터베이스를 편집 하지 마세요.  
  
## <a name="configuring-federation-servers-for-a-farm"></a>팜에 대한 페더레이션 서버 구성  
다음 표에서는 각 페더레이션 서버가 팜 환경에 참여할 수 있도록 하기 위해 완료 해야 하는 작업에 대해 설명 합니다.  
  
|태스크|설명|  
|--------|---------------|  
|SQL Server를 사용하여 AD FS 구성 데이터베이스를 저장하는 경우|페더레이션 서버 팜은 동일한 AD FS 구성 데이터베이스와 토큰 @ no__t-0 서명 인증서를 공유 하는 둘 이상의 페더레이션 서버로 구성 됩니다. Windows 내부 데이터베이스 또는 SQL Server 데이터베이스에 구성 데이터베이스를 저장할 수 있습니다. SQL 데이터베이스에 구성 데이터베이스를 저장 하려는 경우 팜에 참여 하는 모든 새 페더레이션 서버에서 액세스할 수 있도록 구성 데이터베이스에 액세스할 수 있는지 확인 합니다. **참고:** 팜 시나리오의 경우 해당 팜에 페더레이션 서버로도 참여 하지 않는 컴퓨터에 구성 데이터베이스를 배치 하는 것이 중요 합니다. Microsoft NLB는 팜에 참여하는 컴퓨터가 서로 통신하는 것을 허용하지 않습니다. **참고:** 팜에 참여 하는 모든 페더레이션 서버에서 인터넷 정보 서비스 \(IIS @ no__t-1 @ no__t-2에 있는 AD FS AppPool의 id에 구성 데이터베이스에 대 한 읽기 권한이 있는지 확인 합니다.|  
|인증서 가져오기 및 공유|공용 인증 기관에서 단일 서버 인증 인증서를 가져올 수 있습니다 \(CA @ no__t-1 (예: VeriSign). 그러면 모든 페더레이션 서버가 인증서의 동일한 개인 키 부분을 공유 하도록 인증서를 구성할 수 있습니다. 동일한 인증서를 공유 하는 방법에 대 한 자세한 내용은 [ 검사 목록을 참조 하세요. 페더레이션 서버 설정 @ no__t-0. **참고:** AD FS Management snap @ no__t-0in은 페더레이션 서버에 대 한 서버 인증 인증서를 서비스 통신 인증서로 참조 합니다.<br /><br />자세한 내용은 [Certificate Requirements for Federation Servers](Certificate-Requirements-for-Federation-Servers.md)를 참조하세요.|  
|동일한 SQL Server 인스턴스 가리키기|AD FS 구성 데이터베이스가 SQL 데이터베이스에 저장 되는 경우 새 페더레이션 서버는 팜에 있는 다른 페더레이션 서버에서 사용 하는 것과 동일한 SQL Server 인스턴스를 가리켜야 새 서버가 팜에 참여할 수 있습니다.|  
  
## <a name="see-also"></a>관련 항목
[Windows Server 2012의 AD FS 디자인 가이드](AD-FS-Design-Guide-in-Windows-Server-2012.md)
