---
ms.assetid: 38c9bcd3-c6f8-4153-8e42-5fd31568c65a
title: 검사 목록-페더레이션 서버 프록시 설정
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 57951787b1ac7694cacca170b376087a60e34543
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59844054"
---
# <a name="checklist-setting-up-a-federation-server-proxy"></a>검사 목록: 페더레이션 서버 프록시 설정

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Active Directory Federation Services에서 페더레이션 서버 프록시 역할 용 Windows Server® 2012를 실행 하는 서버를 준비 하기 위한 배포 태스크를 포함 하는이 검사 목록 \(AD FS\)합니다.  
  
> [!NOTE]  
> 이 검사 목록의 작업을 순서대로 완료하세요. 참조 링크가 절차를 안내하는 경우 이 검사 목록의 나머지 작업을 계속 진행하려면 해당 절차의 단계를 완료한 후 이 항목으로 돌아와야 합니다.  
  
![페더레이션된 프록시 서버 설정](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**검사 목록: 페더레이션 서버 프록시 설정**  
  
||태스크|참조|  
|-|--------|-------------|  
|![페더레이션된 프록시 서버 설정](media/icon_checkboxo.gif)|AD FS 페더레이션 서버 프록시 배포를 시작 하기 전에 AD FS 배포 토폴로지 유형 및 연결 된 서버 배치 및 네트워크 레이아웃 권장 사항을 검토 합니다.|![페더레이션된 프록시 서버 설정](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS 배포 토폴로지 결정](https://technet.microsoft.com/library/gg982491.aspx)<br /><br />![페더레이션된 프록시 서버 설정](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[페더레이션 서버 프록시 배치 계획](https://technet.microsoft.com/library/dd807130.aspx)<br /><br />![페더레이션된 프록시 서버 설정](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[페더레이션 서버 프록시 배치 위치](https://technet.microsoft.com/library/dd807048.aspx)|  
|![페더레이션된 프록시 서버 설정](media/icon_checkboxo.gif)|프로덕션 환경에서 사용 해야 하는 페더레이션 서버 프록시 중 적절 한 수를 확인 하려면 AD FS 용량 계획 지침을 검토 합니다.|![페더레이션된 프록시 서버 설정](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[페더레이션 서버 프록시 용량 계획](https://technet.microsoft.com/library/gg749898.aspx)|  
|![페더레이션된 프록시 서버 설정](media/icon_checkboxo.gif)|단일 페더레이션 서버 프록시 또는 페더레이션 서버 프록시 팜 배포를 위한 더 나은 되는지 확인 합니다. **참고:** 페더레이션 서버는 또한 페더레이션 서버 프록시 역할을 수행합니다.|![페더레이션된 프록시 서버 설정](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[페더레이션 서버 프록시를 만들어야 하는 경우](https://technet.microsoft.com/library/dd807032.aspx)<br /><br />![페더레이션된 프록시 서버 설정](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[페더레이션 서버 프록시 팜을 만들어야 하는 경우](https://technet.microsoft.com/library/dd807082.aspx)|  
|![페더레이션된 프록시 서버 설정](media/icon_checkboxo.gif)|이 새 페더레이션 서버 프록시 계정 파트너 조직 또는 리소스 파트너 조직의 경계 네트워크에 만들어졌는지 확인 합니다.|![페더레이션된 프록시 서버 설정](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[계정 파트너에서 페더레이션 서버 프록시의 역할 검토](https://technet.microsoft.com/library/dd807109.aspx)<br /><br />![페더레이션된 프록시 서버 설정](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[리소스 파트너에서 페더레이션 서버 프록시의 역할 검토](https://technet.microsoft.com/library/dd807052.aspx)|  
|![페더레이션된 프록시 서버 설정](media/icon_checkboxo.gif)|서버 인증 인증서를 얻는의 중요성에 대 한 역할을 할 페더레이션 서버 프록시 컴퓨터에 AD FS를 설치 하기 전에 검토-페더레이션 서버 프록시 팜용-추가 또는 팜에 모든 서버 인증서를 공유 합니다.|![페더레이션된 프록시 서버 설정](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[페더레이션 서버 프록시에 대 한 인증서 요구 사항](https://technet.microsoft.com/library/dd807054.aspx)|  
|![페더레이션된 프록시 서버 설정](media/icon_checkboxo.gif)|AD FS 디자인 가이드에서 도메인 이름 시스템을 업데이트 하는 방법에 대 한 정보를 검토 \(DNS\) 주변 네트워크의 페더레이션 서버 및 페더레이션 서버 프록시에 대 한 해당 성공적인 이름 확인 될 수 있도록 합니다.|![페더레이션된 프록시 서버 설정](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[페더레이션 서버 프록시에 대 한 이름 확인 요구 사항](https://technet.microsoft.com/library/dd807055.aspx)|  
|![페더레이션된 프록시 서버 설정](media/icon_checkboxo.gif)|페더레이션 서버 프록시를 도메인에 가입 되어 있어야 하는지 여부를 결정 합니다. 페더레이션 서버 프록시는 도메인에 조인할 필요가 없습니다, 있지만 도메인에 참가할 때 원격 관리 및 그룹 정책 기능을 사용 하 여 관리 하기가있지 않습니다.|![페더레이션된 프록시 서버 설정](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[컴퓨터를 도메인에 가입](Join-a-Computer-to-a-Domain.md)|  
|![페더레이션된 프록시 서버 설정](media/icon_checkboxo.gif)|경계 네트워크에 DNS 인프라 구성 된 방식에 따라 오른쪽에 표시 된 항목의 절차 중 하나 전에 완료 조직의 페더레이션 서버 프록시를 배포 합니다. **참고:** 두 절차를 수행 하지 않습니다. 읽기 [페더레이션 서버 프록시에 대 한 이름 확인 요구 사항](https://technet.microsoft.com/library/dd807055.aspx) 가장 적합 한 절차에는 조직의 요구 사항에 적합 한 결정을 합니다.|![페더레이션된 프록시 서버 설정](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[경계 네트워크 에서만 작동 하는 DNS 영역에 페더레이션 서버 프록시에 대 한 이름 확인 구성](Configure-Name-Resolution-for-a-Federation-Server-Proxy-in-a-DNS-Zone-That-Serves-Only-the-Perimeter-Network.md)<br /><br />![페더레이션된 프록시 서버 설정](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[DNS 영역을 역할 모두 경계 네트워크 및 인터넷 클라이언트에서 페더레이션 서버 프록시에 대 한 이름 확인 구성](Configure-Name-Resolution-for-a-Federation-Server-Proxy-in-a-DNS-Zone-That-Serves-Both-the-Perimeter-Network-and-Internet-Clients.md)|  
|![페더레이션된 프록시 서버 설정](media/icon_checkboxo.gif)|인터넷 정보 서비스에서 설치 해야 하는 서버 인증 인증서를 얻은 후 \(IIS\) 페더레이션 서버 프록시의 기본 웹 사이트에 있습니다.|![페더레이션된 프록시 서버 설정](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[기본 웹 사이트로 서버 인증 인증서 가져오기](Import-a-Server-Authentication-Certificate-to-the-Default-Web-Site.md)|  
|![페더레이션된 프록시 서버 설정](media/icon_checkboxo.gif)|\(선택적\) 인증 기관에서 서버 인증 인증서를 얻는 대 안으로 \(CA\), IIS를 사용 하면 페더레이션 서버 프록시에 대 한 샘플 인증서를 얻을 수 있습니다.<br /><br />IIS에서 자체를 생성 하므로\-하지 않는 신뢰할 수 있는 소스에서 시작를 자체를 만드는 데 사용할 서명 된 인증서\-서명 된 인증서는 다음과 같은 시나리오에만:<br /><br />Secure Sockets Layer를 만들 필요가- \(SSL\) 제한, 알려진 사용자 그룹의와 서버 간의 채널<br />-세 번째 문제를 해결 해야 할 때는\-파티 인증서 문제 **주의 해야 합니다.** 자체를 사용 하 여 프로덕션 환경에서 페더레이션 서버 프록시를 배포 하는 보안 모범 사례 아닙니다\-서버 인증 인증서를 서명된 합니다.|![페더레이션된 프록시 서버 설정](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[IIS: 자동 만들기\-서명 된 서버 인증서](https://go.microsoft.com/fwlink/?LinkID=108271)|  
|![페더레이션된 프록시 서버 설정](media/icon_checkboxo.gif)|역할을 할 페더레이션 서버 프록시 컴퓨터에서 페더레이션 서비스 프록시 역할 서비스를 설치 합니다.|![페더레이션된 프록시 서버 설정](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[페더레이션 서비스 프록시 역할 서비스 설치](Install-the-Federation-Service-Proxy-Role-Service.md)|  
|![페더레이션된 프록시 서버 설정](media/icon_checkboxo.gif)|AD FSFederation 서버 프록시 구성 마법사를 사용 하 여 페더레이션 서버 프록시 역할을 하도록 컴퓨터에 AD FS 소프트웨어를 구성 합니다.|![페더레이션된 프록시 서버 설정](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[페더레이션 서버 프록시 역할에 대 한 컴퓨터를 구성 합니다.](Configure-a-Computer-for-the-Federation-Server-Proxy-Role.md)|  
|![페더레이션된 프록시 서버 설정](media/icon_checkboxo.gif)|이벤트 뷰어를 사용하여 페더레이션 서버 프록시 서비스가 시작되었는지 확인합니다.|![페더레이션된 프록시 서버 설정](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[확인 하는 페더레이션 서버 프록시 작동](Verify-That-a-Federation-Server-Proxy-Is-Operational.md)|  
