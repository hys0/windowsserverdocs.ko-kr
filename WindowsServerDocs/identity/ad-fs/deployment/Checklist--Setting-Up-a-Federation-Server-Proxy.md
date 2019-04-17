---
ms.assetid: 38c9bcd3-c6f8-4153-8e42-5fd31568c65a
title: "검사-Federation 서버 프록시 설정"
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 997ee901172eb2d873ad02fa8ce39da09c5171c7
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="checklist-setting-up-a-federation-server-proxy"></a>검사 목록: Federation 서버 프록시 설정

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 검사 준비 federation 서버 프록시 역할 \(AD FS\) Active Directory Federation Services에에서 대 한® Windows Server 2012를 실행 하는 서버에 대 한 배포 작업이 포함 됩니다.  
  
> [!NOTE]  
> 주문에서이 검사의 작업을 완료 합니다. 이 검사에서 나머지 작업 진행할 수 있도록이 절차의 단계를 완료 한 후이 항목을 참조 링크는 절차로 이동 때 돌아갑니다.  
  
![연결 된 프록시 서버 설정](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**검사: federation 서버 프록시 설정**  
  
||작업|참조|  
|-|--------|-------------|  
|![연결 된 프록시 서버 설정](media/icon_checkboxo.gif)|ADFS federation 서버 프록시 여 배포를 시작 하기 전에 검토 관련된 서버 배치 ADFS 배포 토폴로지 유형 및 네트워크 레이아웃으로 추천 합니다.|![연결 된 프록시 서버 설정](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[해당 AD FS 배포가 확인](https://technet.microsoft.com/library/gg982491.aspx)<br /><br />![연결 된 프록시 서버 설정](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Federation 서버 프록시 배치](https://technet.microsoft.com/library/dd807130.aspx)<br /><br />![연결 된 프록시 서버 설정](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Federation 서버 프록시 위치](https://technet.microsoft.com/library/dd807048.aspx)|  
|![연결 된 프록시 서버 설정](media/icon_checkboxo.gif)|해당 federation 서버 프록시 생산 환경에서 사용 해야 수를 확인 하려면 지침 계획 ADFS 용량을 검토 합니다.|![연결 된 프록시 서버 설정](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Federation 서버 프록시 용량에 대 한 계획](https://technet.microsoft.com/library/gg749898.aspx)|  
|![연결 된 프록시 서버 설정](media/icon_checkboxo.gif)|단일 federation 프록시 서버 또는 federation 서버 프록시 농장 배포에 대 한 개선 되는지 확인 합니다. **참고:** Federation 서버 federation 서버 프록시 책임을 수행할 수도 있습니다.|![연결 된 프록시 서버 설정](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Federation 프록시 서버를 만들 때](https://technet.microsoft.com/library/dd807032.aspx)<br /><br />![연결 된 프록시 서버 설정](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Federation 서버 프록시 농장 만들어야 하는 경우](https://technet.microsoft.com/library/dd807082.aspx)|  
|![연결 된 프록시 서버 설정](media/icon_checkboxo.gif)|이 새로운 federation 서버 프록시 주변 계정 파트너 회사나 리소스 파트너 조직의 네트워크에 만들가 있는지 확인 합니다.|![연결 된 프록시 서버 설정](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[계정 파트너의 Federation 서버 프록시 역할을 검토](https://technet.microsoft.com/library/dd807109.aspx)<br /><br />![연결 된 프록시 서버 설정](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[리소스 파트너에 Federation 서버 프록시 역할을 검토](https://technet.microsoft.com/en-us/library/dd807052.aspx)|  
|![연결 된 프록시 서버 설정](media/icon_checkboxo.gif)|ADFS federation 서버 프록시가 컴퓨터에 설치 하기 전에 서버 인증 인증서를 얻는의 중요성 내용 등 federation 서버 프록시 농장에 대 한-추가 또는 농장 모든 서버 인증서를 공유 합니다.|![연결 된 프록시 서버 설정](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Federation 서버 프록시 인증서 요구 사항](https://technet.microsoft.com/library/dd807054.aspx)|  
|![연결 된 프록시 서버 설정](media/icon_checkboxo.gif)|주변 네트워크에서 Domain Name System \(DNS\) federation 서버 및 federation 서버 프록시 성공 이름 확인 발생할 수 있도록 업데이트 하는 방법에 대 한 AD FS 디자인 가이드의 정보를 검토 합니다.|![연결 된 프록시 서버 설정](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Federation 서버 프록시 이름 해상도 요구 사항](https://technet.microsoft.com/library/dd807055.aspx)|  
|![연결 된 프록시 서버 설정](media/icon_checkboxo.gif)|Federation 서버 프록시 도메인에 가입 해야 있는지 여부를 결정 합니다. 하지만 federation 서버 프록시가 도메인에 가입 하는 도메인에 가입한 경우 원격 관리 기능과 그룹 정책으로 관리 하기 쉽게는 합니다.|![연결 된 프록시 서버 설정](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[컴퓨터 도메인에 가입](Join-a-Computer-to-a-Domain.md)|  
|![연결 된 프록시 서버 설정](media/icon_checkboxo.gif)|주변 네트워크에서 DNS infrastructure 구성 된 방식에 따라 중 하나를 수행 항목에서 절차에는 조직에서 federation 프록시 서버에 배포 하기는 전에 직접 합니다. **참고:** 두 절차를 수행 하지 않습니다. 읽기 [이름 해상도 요구 사항을 Federation 서버 프록시](https://technet.microsoft.com/library/dd807055.aspx) 최상의 절차 맞는 조직의 요구 사항을 확인 하려면.|![연결 된 프록시 서버 설정](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[Federation 서버 프록시 주변 네트워크만 사용 하는 DNS 영역에 대해 구성 이름 확인](Configure-Name-Resolution-for-a-Federation-Server-Proxy-in-a-DNS-Zone-That-Serves-Only-the-Perimeter-Network.md)<br /><br />![연결 된 프록시 서버 설정](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[Federation 서버 프록시 DNS 영역은 대용 모두 주변 네트워크 및 인터넷 클라이언트에 대해 구성 이름 확인](Configure-Name-Resolution-for-a-Federation-Server-Proxy-in-a-DNS-Zone-That-Serves-Both-the-Perimeter-Network-and-Internet-Clients.md)|  
|![연결 된 프록시 서버 설정](media/icon_checkboxo.gif)|서버 인증 인증서를 얻는 후 인터넷 정보 서비스 \(IIS\) federation 서버 프록시의 기본 웹 사이트의 설치 해야 합니다.|![연결 된 프록시 서버 설정](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[서버 인증 인증서를 기본 웹 사이트를 가져오기](Import-a-Server-Authentication-Certificate-to-the-Default-Web-Site.md)|  
|![연결 된 프록시 서버 설정](media/icon_checkboxo.gif)|인증 기관에서 서버 인증 인증서를 얻는 하는 대신 \(Optional\) \(CA\), IIS federation 프록시 서버에 대 한 샘플 인증서를 얻는를 사용할 수 있습니다.<br /><br />IIS 출처를 신뢰할 수 있는 하지 않고도 self\ 서명 인증서를 생성을 하기 때문에 사용 하 여 다음과 같은 경우에만 self\ 서명 인증서를 만들려면 다음과 같습니다.<br /><br />-서버와 제한적으로 알려진의 사용자 그룹 사이 주소 \(SSL\) 채널을 만들 수 있는 때<br />-Third\ 자 인증서 문제를 해결 하는 경우 **주의:** federation 서버 프록시 서버 인증 인증서를 self\ 서명를 사용 하 여 생산 환경에서 배포 하는 가장 좋은 보안 않습니다.|![연결 된 프록시 서버 설정](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[IIS: Self\-Signed 서버 인증서를 만듭니다.](https://go.microsoft.com/fwlink/?LinkID=108271)|  
|![연결 된 프록시 서버 설정](media/icon_checkboxo.gif)|Federation 서비스 프록시 역할 서비스 federation 서버 프록시가 컴퓨터에 설치 합니다.|![연결 된 프록시 서버 설정](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[Federation 서비스 프록시 역할 서비스 설치](Install-the-Federation-Service-Proxy-Role-Service.md)|  
|![연결 된 프록시 서버 설정](media/icon_checkboxo.gif)|컴퓨터에서 광고 FSFederation 프록시 서버 구성 마법사를 사용 하 여 federation 서버 프록시 역할에서 행동을 ADFS 소프트웨어를 구성 합니다.|![연결 된 프록시 서버 설정](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[Federation 서버 프록시 역할 컴퓨터를 구성 합니다.](Configure-a-Computer-for-the-Federation-Server-Proxy-Role.md)|  
|![연결 된 프록시 서버 설정](media/icon_checkboxo.gif)|이벤트 뷰어를 사용 하는 federation 서버 프록시 서비스 시작 되었는지 확인 합니다.|![연결 된 프록시 서버 설정](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[되어 있는지 확인 한 Federation 서버 프록시가 작동](Verify-That-a-Federation-Server-Proxy-Is-Operational.md)|  
