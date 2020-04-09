---
ms.assetid: 38c9bcd3-c6f8-4153-8e42-5fd31568c65a
title: 검사 목록-페더레이션 서버 프록시 설정
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: a9784a7c599f6b1f13d9773a376e40b678106123
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80854596"
---
# <a name="checklist-setting-up-a-federation-server-proxy"></a>검사 목록: 페더레이션 서버 프록시 설정

이 검사 목록에는 Active Directory Federation Services \(AD FS\)에서 페더레이션 서버 프록시 역할에 대해 Windows Server&reg; 2012를 실행 하는 서버를 준비 하기 위한 배포 작업이 포함 되어 있습니다.  
  
> [!NOTE]  
> 이 검사 목록의 작업을 순서대로 완료하세요. 참조 링크가 절차를 안내하는 경우 이 검사 목록의 나머지 작업을 계속 진행하려면 해당 절차의 단계를 완료한 후 이 항목으로 돌아와야 합니다.  
  
페더레이션된 프록시 서버 설정 ![](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**검사 목록: 페더레이션 서버 프록시 설정**  
  
||작업|참조|  
|-|--------|-------------|  
|![페더레이션된 프록시 서버 설정](media/icon_checkboxo.gif)|AD FS 페더레이션 서버 프록시 배포를 시작 하기 전에 AD FS 배포 토폴로지 유형 및 연결 된 서버 배치 및 네트워크 레이아웃 권장 사항을 검토 합니다.|페더레이션된 프록시 서버를 설정 ![](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS 배포 토폴로지 결정](https://technet.microsoft.com/library/gg982491.aspx)<p>페더레이션 프록시 서버를 설정 하는 ![](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[페더레이션 서버 프록시 배치 계획](https://technet.microsoft.com/library/dd807130.aspx)<p>](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[페더레이션 서버 프록시를 넣을](https://technet.microsoft.com/library/dd807048.aspx) 페더레이션 프록시 서버를 설정 하는 ![|  
|![페더레이션된 프록시 서버 설정](media/icon_checkboxo.gif)|프로덕션 환경에서 사용 해야 하는 페더레이션 서버 프록시 중 적절 한 수를 확인 하려면 AD FS 용량 계획 지침을 검토 합니다.|페더레이션 프록시 서버를 설정 하 ![](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[페더레이션 서버 프록시 용량 계획](https://technet.microsoft.com/library/gg749898.aspx)|  
|![페더레이션된 프록시 서버 설정](media/icon_checkboxo.gif)|단일 페더레이션 서버 프록시 또는 페더레이션 서버 프록시 팜 배포를 위한 더 나은 되는지 확인 합니다. **참고:** 페더레이션 서버가 페더레이션 서버 프록시 역할을 수행할 수도 있습니다.|페더레이션 프록시 서버를 설정 하 ![](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[페더레이션 서버 프록시를 만들어야 하는 경우](https://technet.microsoft.com/library/dd807032.aspx)<p>페더레이션 프록시 서버를 설정 하 ![](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[페더레이션 서버 프록시 팜을 만들어야 하는 경우](https://technet.microsoft.com/library/dd807082.aspx)|  
|![페더레이션된 프록시 서버 설정](media/icon_checkboxo.gif)|이 새 페더레이션 서버 프록시 계정 파트너 조직 또는 리소스 파트너 조직의 경계 네트워크에 만들어졌는지 확인 합니다.|페더레이션된 프록시 서버 설정 ![](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[계정 파트너에서 페더레이션 서버 프록시의 역할 검토](https://technet.microsoft.com/library/dd807109.aspx)<p>페더레이션된 프록시 서버 설정 ![](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[리소스 파트너에서 페더레이션 서버 프록시의 역할 검토](https://technet.microsoft.com/library/dd807052.aspx)|  
|![페더레이션된 프록시 서버 설정](media/icon_checkboxo.gif)|서버 인증 인증서를 얻는의 중요성에 대 한 역할을 할 페더레이션 서버 프록시 컴퓨터에 AD FS를 설치 하기 전에 검토-페더레이션 서버 프록시 팜용-추가 또는 팜에 모든 서버 인증서를 공유 합니다.|](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[페더레이션 서버 프록시에 대 한 페더레이션 프록시 서버 인증서 요구 사항을](https://technet.microsoft.com/library/dd807054.aspx) 설정 하는 ![|  
|![페더레이션된 프록시 서버 설정](media/icon_checkboxo.gif)|AD FS 디자인 가이드에서 도메인 이름 시스템을 업데이트 하는 방법에 대 한 정보를 검토 \(DNS\) 주변 네트워크의 페더레이션 서버 및 페더레이션 서버 프록시에 대 한 해당 성공적인 이름 확인 될 수 있도록 합니다.|](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[페더레이션 서버 프록시에 대 한 페더레이션된 프록시 서버 이름 확인 요구 사항을](https://technet.microsoft.com/library/dd807055.aspx) 설정 하는 ![|  
|![페더레이션된 프록시 서버 설정](media/icon_checkboxo.gif)|페더레이션 서버 프록시를 도메인에 가입 되어 있어야 하는지 여부를 결정 합니다. 페더레이션 서버 프록시는 도메인에 가입할 필요가 없지만, 원격 관리를 사용 하 여 관리 하 고 도메인에 가입 된 기능을 그룹 정책 하는 것이 더 쉽습니다.|페더레이션된 프록시 서버 설정 ![컴퓨터를](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[도메인에 가입](Join-a-Computer-to-a-Domain.md)|  
|![페더레이션된 프록시 서버 설정](media/icon_checkboxo.gif)|경계 네트워크에 DNS 인프라 구성 된 방식에 따라 오른쪽에 표시 된 항목의 절차 중 하나 전에 완료 조직의 페더레이션 서버 프록시를 배포 합니다. **참고:** 두 절차를 수행 하지 않습니다. 읽기 [페더레이션 서버 프록시에 대 한 이름 확인 요구 사항](https://technet.microsoft.com/library/dd807055.aspx) 가장 적합 한 절차에는 조직의 요구 사항에 적합 한 결정을 합니다.|페더레이션된 프록시 서버 설정 ![](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[경계 네트워크만 제공 하는 DNS 영역에서 페더레이션 서버 프록시에 대 한 이름 확인을 구성](Configure-Name-Resolution-for-a-Federation-Server-Proxy-in-a-DNS-Zone-That-Serves-Only-the-Perimeter-Network.md) 합니다.<p>페더레이션된 프록시 서버 설정 ![](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[경계 네트워크와 인터넷 클라이언트를 모두 제공 하는 DNS 영역에서 페더레이션 서버 프록시에 대 한 이름 확인을 구성 합니다](Configure-Name-Resolution-for-a-Federation-Server-Proxy-in-a-DNS-Zone-That-Serves-Both-the-Perimeter-Network-and-Internet-Clients.md) .|  
|![페더레이션된 프록시 서버 설정](media/icon_checkboxo.gif)|인터넷 정보 서비스에서 설치 해야 하는 서버 인증 인증서를 얻은 후 \(IIS\) 페더레이션 서버 프록시의 기본 웹 사이트에 있습니다.|페더레이션된 프록시 서버 설정 ![](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[서버 인증 인증서를 기본 웹 사이트로 가져오기](Import-a-Server-Authentication-Certificate-to-the-Default-Web-Site.md)|  
|![페더레이션된 프록시 서버 설정](media/icon_checkboxo.gif)|선택적\)를 \(인증 기관 \(CA\)에서 서버 인증 인증서를 가져오는 대신 IIS를 사용 하 여 페더레이션 서버 프록시에 대 한 샘플 인증서를 가져올 수 있습니다.<p>IIS는 신뢰할 수 있는 원본에서 시작 되지 않은 자체\-서명 된 인증서를 생성 하므로 다음 시나리오 에서만 자체\-서명 된 인증서를 만드는 데 사용 합니다.<p>Secure Sockets Layer를 만들 필요가- \(SSL\) 제한, 알려진 사용자 그룹의와 서버 간의 채널<br />세 번째 문제를 해결 해야 하는-\-파티 인증서 문제 **주의:** 에서 자체를 사용 하 여 프로덕션 환경에서 페더레이션 서버 프록시를 배포 하는 보안 모범 사례 없는\-서명 됨된, 서버 인증 인증서.|페더레이션된 프록시 서버 설정 ![](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[IIS: 자체\-서명 된 서버 인증서 만들기](https://go.microsoft.com/fwlink/?LinkID=108271)|  
|![페더레이션된 프록시 서버 설정](media/icon_checkboxo.gif)|역할을 할 페더레이션 서버 프록시 컴퓨터에서 페더레이션 서비스 프록시 역할 서비스를 설치 합니다.|페더레이션된 프록시 서버를 설정 ![](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[페더레이션 서비스 프록시 역할 서비스를 설치 합니다](Install-the-Federation-Service-Proxy-Role-Service.md) .|  
|![페더레이션된 프록시 서버 설정](media/icon_checkboxo.gif)|AD FSFederation 서버 프록시 구성 마법사를 사용 하 여 페더레이션 서버 프록시 역할을 하도록 컴퓨터에 AD FS 소프트웨어를 구성 합니다.|페더레이션된 프록시 서버 설정 ![](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[페더레이션 서버 프록시 역할에 대 한 컴퓨터 구성](Configure-a-Computer-for-the-Federation-Server-Proxy-Role.md)|  
|![페더레이션된 프록시 서버 설정](media/icon_checkboxo.gif)|이벤트 뷰어를 사용하여 페더레이션 서버 프록시 서비스가 시작되었는지 확인합니다.|페더레이션된 프록시 서버 설정 ![](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[페더레이션 서버 프록시가 작동 하는지 확인](Verify-That-a-Federation-Server-Proxy-Is-Operational.md)|  
