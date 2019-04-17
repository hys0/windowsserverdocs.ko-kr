---
ms.assetid: 02580b2f-a339-4470-947c-d700b2d55f3f
title: "Federation 서버 팜 만들어야 하는 경우"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 2e7c991cf87bc0e6914e158f0878bcadbede3c22
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="when-to-create-a-federation-server-farm"></a>Federation 서버 팜 만들어야 하는 경우

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

큰 ADFS 배포 결함 허용, load\ 분산 또는 확장성 조직의 Federation 서비스를 제공 해야 할 때의 Active Directory Federation Services \(AD FS\) federation 서버 농장을 만드는 것이 좋습니다. 동일한 네트워크에 있는 두 개 이상의 federation 서버 만드는 작업을 동일한 Federation 서비스를 사용 하 고 각 구성 하 고 각 서버 token\ 서명 인증서의 공개 키 snap\에서 AD FS 관리를 추가 federation 서버 팜을 만듭니다.  
  
Federation 서버 팜 만들거나 AD FS Federation 서버 구성 마법사를 사용 하 여 추가 federation 서버 기존 농장을 설치할 수 있습니다. 자세한 내용은 참조 [Federation 서버를 만들 때](When-to-Create-a-Federation-Server.md)합니다.  
  
> [!NOTE]  
> 만드는 옵션을 선택할 때는 **새 federation 서버 팜** AD FS Federation 서버 구성 마법사를 사용 하는 마법사가 컨테이너 개체를 만들려면 \(for sharing certificates\) Active Directory에 있습니다. 따라서이 처음에 로그온 할를 설정 하는 federation 서버 역할 Active directory이 컨테이너 개체를 만들 수 있는 권한이 있는 계정으로 컴퓨터를 중요 합니다.  
  
Federation 서버 농장으로 그룹화 할 수, 하기 전에 자녀가 해야 먼저 클러스터 되므로 요청을 처리 단일에 도착 하는 완전히 된 \(FQDN\) 서버 발전소의 다양 한 federation 서버에 전달은 도메인 이름입니다. 서버 클러스터 배포 회사의 네트워크 안에 네트워크 부하 분산 \(NLB\) 하 여 만들 수 있습니다. 이 가이드 클러스터 각 그룹에 federation 서버를 NLB 적절 하 게 구성 된 것으로 간주 합니다.  
  
클러스터 FQDN 구성 하는 방법에 대 한 자세한 내용은 참조 Microsoft NLB 기술을 사용 하 여 [클러스터 매개 지정](https://go.microsoft.com/fwlink/?LinkID=74651)합니다.  
  
## <a name="best-practices-for-deploying-a-federation-server-farm"></a>Federation 서버 농장 배포 하기 위한 모범 사례  
Federation 서버 생산 환경에서 배포 하기 위한 다음과 같은 유용한을 사용 하는 것이 좋습니다.  
  
-   여러 federation 서버 동시에 배포 될 하거나를 추가할 것 서버를 더 그룹에 시간이 지남에 따라 알고, 그룹에 기존 federation 서버의 서버 이미지를 만들고 추가 federation 서버를 신속 하 게 만드는 필요할 때 해당 이미지의 다음 설치 것이 좋습니다.  
  
    > [!NOTE]  
    > 작업을 완료 하는 서버 이미지 방법을 추가 federation 서버를 배포 하는 데 사용 하려는 경우 하지 [검사: Federation 서버 설정을](../../ad-fs/deployment/Checklist--Setting-Up-a-Federation-Server.md) 서버 새 그룹에 추가할 때마다 합니다.  
  
-   NLB 또는 다른 형태의 클러스터링를 사용 하 여 많은 federation 서버 컴퓨터에 단일 IP 주소를 할당 합니다.  
  
-   그룹의 각 federation 서버에 대 한 고정 IP 주소를 예약 하 고 Domain Name System \(DNS\) 구성에 따라 Dynamic Host Configuration Protocol \(DHCP\)에 제외 각 IP 주소에 대 한 삽입 합니다. Microsoft NLB 기술 nlb에 참여 하는 각 서버에서 고정 IP 주소를 할당 될 필요 합니다.  
  
-   ADFS 구성 데이터베이스 SQL 데이터베이스에 저장 됩니다, 동시에 여러 federation 서버에서 SQL 데이터베이스 편집 하 않도록 합니다.  
  
## <a name="configuring-federation-servers-for-a-farm"></a>Federation 서버 농장에 대 한 구성  
다음 표에서 각 federation 서버 farmed 환경에 참여할 수 있도록 완료 해야 하는 작업에 설명 합니다.  
  
|작업|설명|  
|--------|---------------|  
|ADFS 구성 데이터베이스를 저장할 SQL Server를 사용 하는 경우|동일한 ADFS 구성 공유 하는 두 개 이상의 federation 서버 이루어져 federation 서버 팜 데이터베이스와 token\ 서명 인증서 합니다. 구성 데이터베이스 SQL Server 데이터베이스에 또는 Windows 내부 데이터베이스 중 하나에 저장할 수 있습니다. 구성 데이터베이스 SQL 데이터베이스에 저장 하려는 경우 팜에 참여 하는 모든 새로운 federation 서버에서 액세스할 수 있도록 구성 데이터베이스가 액세스할 수 있는지 확인 합니다. **참고:** 팜 시나리오에 대 한 것이 중요 구성 데이터베이스에서 농장 해당 federation 서버로 참여 하지 않는 하는 컴퓨터에서 찾을 수 있습니다. Microsoft NLB 서로 통신할 수 팜에 참여 하는 컴퓨터 허용 하지 않습니다. **참고:** 팜에 참여 하는 모든 federation 서버의 \(IIS\)\) 인터넷 정보 서비스에서에서 광고 FS AppPool id 구성 데이터베이스에 읽기 액세스에 있는지 확인 합니다.|  
|얻고 인증서를 공유|공용 인증 기관에서 단일 서버 인증 인증서를 받을 수 있습니다 \ (CA\) 등 VeriSign 예입니다. 그런 다음 모든 federation 서버 같은 개인 인증서의 주요 부분을 공유 하는 인증서를 구성할 수 있습니다. 동일한 인증서를 공유 하는 방법에 대 한 자세한 내용은 참조 [검사: Federation 서버 설정을](../../ad-fs/deployment/Checklist--Setting-Up-a-Federation-Server.md)합니다. **참고:** 서비스 통신 인증서도 federation 서버에 대 한 서버 인증 인증서의 snap\ AD FS 관리 가리킵니다.<br /><br />자세한 내용은 참조 [Federation 서버의 인증서 요구](Certificate-Requirements-for-Federation-Servers.md)합니다.|  
|동일한 SQL Server 인스턴스를 가리킨|ADFS 구성 데이터베이스 SQL 데이터베이스에 저장 됩니다, 지점 새 서버 팜에 참여할 수 있도록 그룹의 다른 federation 서버에서 사용 되는 동일한 SQL Server 인스턴스를 새 federation 서버 해야 합니다.|  
  
## <a name="see-also"></a>참조 하십시오
[Windows Server 2012의에서 지침에 따라 AD FS 디자인](AD-FS-Design-Guide-in-Windows-Server-2012.md)
