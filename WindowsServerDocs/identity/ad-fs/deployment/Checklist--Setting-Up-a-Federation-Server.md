---
ms.assetid: 8f954004-40d5-4c5e-8e0d-e8700c8ec7b1
title: "검사-Federation 서버 설정"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 44448088184d86874e91855d8a51ef40d8cea049
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="checklist-setting-up-a-federation-server"></a>Federation 서버 설정 검사:

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 검사에 대 한 Active Directory Federation Services \(AD FS\)의 federation 서버 역할® Windows Server 2012를 실행 하는 서버를 준비 하는 데 필요한는 배포 작업이 포함 됩니다.  
  
> [!NOTE]  
> 주문에서이 검사의 작업을 완료 합니다. 이 검사에서 나머지 작업 진행할 수 있도록이 절차의 단계를 완료 한 후이 항목을 참조 링크는 절차로 이동 때 돌아갑니다.  
  
![연결 된 서버 설정](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**검사: federation 서버 설정**  
  
||작업|참조|  
|-|--------|-------------|  
|![연결 된 서버 설정](media/icon_checkboxo.gif)|ADFS federation 서버를 배포 하기 시작 하기 전에 검토; 1. \) Windows 내부 데이터베이스 \(WID\) 또는 SQL Server ADFS 구성 저장 하도록 선택 하면의 장단점 데이터베이스 2. \) ADFS 배포 토폴로지 유형과 관련된 서버 네트워크 위치와 위치 레이아웃 추천 합니다.|![연결 된 서버 설정](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[해당 AD FS 배포가 확인](https://technet.microsoft.com/library/gg982491.aspx)<br /><br />![연결 된 서버 설정](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[광고 FS 배포 토폴로지 고려](https://technet.microsoft.com/library/gg982489.aspx)|  
|![연결 된 서버 설정](media/icon_checkboxo.gif)|해당 federation 서버 생산 환경에서 사용 해야 수를 확인 하려면 지침 계획 ADFS 용량을 검토 합니다.|![연결 된 서버 설정](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Federation 서버 용량에 대 한 계획](https://technet.microsoft.com/library/gg749917.aspx)|  
|![연결 된 서버 설정](media/icon_checkboxo.gif)|조직에서 federation 서버를 어디에 AD FS 디자인 가이드의 정보를 검토|![연결 된 서버 설정](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Federation 서버 배치 계획](https://technet.microsoft.com/library/dd807069.aspx)<br /><br />![연결 된 서버 설정](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Federation 서버 위치](https://technet.microsoft.com/library/dd807127.aspx)|  
|![연결 된 서버 설정](media/icon_checkboxo.gif)|Stand\만 federation 서버 또는 federation 서버 농장 배포에 대 한 개선 되는지 확인 합니다.|![연결 된 서버 설정](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Federation 서버 만들어야 하는 경우](https://technet.microsoft.com/library/dd807101.aspx)<br /><br />![연결 된 서버 설정](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Federation 서버 농장 만들어야 하는 경우](https://technet.microsoft.com/library/dd807062.aspx)|  
|![연결 된 서버 설정](media/icon_checkboxo.gif)|계정 파트너 조직 또는 리소스 파트너 조직에서이 새 federation 서버를 만들 수 있는지 여부를 결정 합니다.|![연결 된 서버 설정](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[계정 파트너에 해당 Federation 서버의 역할을 검토](https://technet.microsoft.com/library/dd807117.aspx)<br /><br />![연결 된 서버 설정](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[리소스 파트너에 해당 Federation 서버의 역할을 검토](https://technet.microsoft.com/library/dd807065.aspx)|  
|![연결 된 서버 설정](media/icon_checkboxo.gif)|Federation 서버를 안전 하 게 클라이언트 및 federation 서버 프록시 요청 인증 서비스 통신 인증서 및 token\ 서명 인증서를 사용 방법에 대 한 정보를 검토 합니다. **주의:** https:\/\/myserver 등 호스트 자격이 없는 이름으로 인증서를 사용 하 여 일반적으로 오랫동안, 이러한 인증서 보안 값이 없는 있고 공격자 가장 엔터프라이즈 클라이언트 ADFS Federation 서비스를 사용 하도록 설정할 수 있습니다. 따라서 것이 좋습니다 정식된 도메인을 사용 하는 등 https:\/\/myserver.contoso.com \(FQDN\) 이름을 지정 하 고만 해당 Federation 서비스 FQDN에 발급 SSL 인증서를 사용 합니다.|![연결 된 서버 설정](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Federation 서버의 인증서 요구 사항](https://technet.microsoft.com/library/dd807040.aspx)|  
|![연결 된 서버 설정](media/icon_checkboxo.gif)|회사 네트워크 Domain Name System \(DNS\) federation 서버에 성공 이름 확인 발생할 수 있도록 업데이트 하는 방법에 대 한 정보를 검토 합니다.|![연결 된 서버 설정](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Federation 서버에 대 한 이름 해상도 요구 사항](https://technet.microsoft.com/library/dd807041.aspx)|  
|![연결 된 서버 설정](media/icon_checkboxo.gif)|도메인 계정 파트너 숲 또는 사용자가 해당 숲 속의 또는 숲 신뢰 하는 인증을 사용할 수는 리소스 파트너 숲에 federation 서버가 컴퓨터에 참여 합니다. **참고:** 의 컴퓨터 또는 숲 신뢰 하는 해당 숲에서 사용자를 인증 해당 federation 서버는 사용할 숲 속의 모든 도메인에 가입 먼저 해야 계정 파트너 조직에서 federation 서버를 설정 해야 합니다.|![연결 된 서버 설정](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[컴퓨터 도메인에 가입](Join-a-Computer-to-a-Domain.md)|  
|![연결 된 서버 설정](media/icon_checkboxo.gif)|DNS federation 서버 DNS 호스트 이름을 federation 서버의 IP 주소를 가리키는 회사 네트워크에서 새로운 리소스 기록을 생성 합니다.|![연결 된 서버 설정](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[호스트 & #40; 추가 & #41; 회사 DNS Federation 서버에 대 한 리소스 기록](Add-a-Host--A--Resource-Record-to-Corporate-DNS-for-a-Federation-Server.md)|  
|![연결 된 서버 설정](media/icon_checkboxo.gif)|먼저 개인 키 기존 token\ 서명 인증서를 내보냅니다 해야 할 수 \(Optional\) federation 서버에 federation 서버 팜에 추가 될 경우, \ (서버의 첫 번째 federation에는 farm\) 준비 인증서의 파일 형식 않아도 때 다른 federation 서버 가져와야 동일한 인증서 합니다.<br /><br />개인 키 내보내기 필요 하지 않습니다 여러 대의 컴퓨터에서 발급된 서버 인증 인증서를 다시 사용할 수 있는 경우 \ (를 않고도 export\) 때 사용자가 가져오지 못할 고유한 서버 인증 인증서의 농장의 각 federation 서버에 대 한 또는 합니다. **참고:** 서비스 통신 인증서도 federation 서버에 대 한 서버 인증 인증서의 snap\ AD FS 관리 가리킵니다.|![연결 된 서버 설정](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[내보내려면 서버 인증 인증서의 개인 키 부분](Export-the-Private-Key-Portion-of-a-Server-Authentication-Certificate.md)|  
|![연결 된 서버 설정](media/icon_checkboxo.gif)|서버 인증 인증서를 얻는 후 \(or private key\) 인증 기관에서 \(CA\), 다음 가져와야 인증서 파일 각 federation 서버에 대 한 기본 웹 사이트를 참조 합니다. **참고:** AD FS Federation 서버 구성 마법사를 사용 하려면 먼저 필요는 기본 웹 사이트의이 인증서를 설치 합니다.|![연결 된 서버 설정](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[서버 인증 인증서를 기본 웹 사이트를 가져오기](Import-a-Server-Authentication-Certificate-to-the-Default-Web-Site.md)|  
|![연결 된 서버 설정](media/icon_checkboxo.gif)|캘리포니아는에서 서버 인증 인증서를 얻는 하는 대신 \(Optional\) 인증서를 만들려면 샘플 해당 federation 서버에 대 한 \(IIS\) 인터넷 정보 서비스를 사용할 수 있습니다. **주의:** 생산 환경에서 federation 서버 self\ 서명 서버 인증 인증서를 사용 하 여 배포 하는 가장 좋은 보안 않습니다.|![연결 된 서버 설정](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[IIS: Self\-Signed 서버 인증서를 만들기](https://go.microsoft.com/fwlink/?LinkID=108271) 다음 다음을 수행 하 고 [서버 인증 인증서를 기본 웹 사이트를 가져오기](Import-a-Server-Authentication-Certificate-to-the-Default-Web-Site.md)|  
|![연결 된 서버 설정](media/icon_checkboxo.gif)|계정 파트너 조직에서 federation 서버 팜 환경 구성는, 경우 만들고 해야 Active Directory Domain Services에서 전용된 서비스 계정을 구성 \ (AD DS \) 팜은 거주 하 고이 계정을 사용 하 여 팜에서 각 federation 서버를 구성 합니다. 이 절차를 수행 하 여 회사 네트워크에서 사용 하 여 Windows 통합 인증 농장 federation 서버 인증을 클라이언트 하면 수 있습니다.|![연결 된 서버 설정](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[수동으로 서비스 계정을 Federation 서버 농장에 대 한 구성](Manually-Configure-a-Service-Account-for-a-Federation-Server-Farm.md)|  
|![연결 된 서버 설정](media/icon_checkboxo.gif)|Federation 서비스 역할 federation 서버가 컴퓨터에 설치 합니다.|![연결 된 서버 설정](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[Federation 서비스 역할 설치](Install-the-Federation-Service-Role-Service.md)|  
|![연결 된 서버 설정](media/icon_checkboxo.gif)|컴퓨터에서 광고 FS Federation 서버 구성 마법사를 사용 하 여 해당 federation 서버 역할에 행동을 ADFS 소프트웨어를 구성 합니다.<br /><br />Stand\만 federation 서버 설정 첫 번째 federation 서버 새 그룹에 만들거나 컴퓨터도 기존 federation 서버 그룹에 연결 하려면 다음이 단계를 수행 합니다. **참고:** 웹 단일 Sign\-On 연방 \(SSO\) 디자인에 대 한 계정 파트너 조직에서 하나 이상의 federation 서버 및 리소스 파트너 조직에서 하나 이상의 federation 서버를 되어 있어야 합니다.|![연결 된 서버 설정](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[독립 실행형 Federation 서버 만들기](Create-a-Stand-Alone-Federation-Server.md)<br /><br />![연결 된 서버 설정](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[Federation 서버 농장의 첫 번째 Federation 서버 만들기](Create-the-First-Federation-Server-in-a-Federation-Server-Farm.md)<br /><br />![연결 된 서버 설정](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[Federation 서버 Federation 서버 농장을 추가](Add-a-Federation-Server-to-a-Federation-Server-Farm.md)|  
|![연결 된 서버 설정](media/icon_checkboxo.gif)|\(Optional\) 사용 광고 FS 관리 snap\에 추가 하 고 필요한 ADFS 인증서 구성 디자인을 배포 하는 데 필요한 합니다. 추가 하거나 snap\ 기능을 사용 하는 인증서를 변경 하는 경우에 대 한 자세한 내용은 참조 [Federation 서버의 인증서 요구](https://technet.microsoft.com/library/dd807040.aspx)합니다.|![연결 된 서버 설정](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[토큰 서명 인증서 추가 합니다.](Add-a-Token-Signing-Certificate.md)<br /><br />![연결 된 서버 설정](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[토큰 암호를 해독 인증서 추가 합니다.](Add-a-Token-Decrypting-Certificate.md)<br /><br />![연결 된 서버 설정](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[서비스 통신 인증서 설정](Set-a-Service-Communications-Certificate.md)|  
|![연결 된 서버 설정](media/icon_checkboxo.gif)|첫 번째 federation 서버 조직에는이 ADFS 디자인에 맞도록 Federation 서비스를 구성 합니다.|![연결 된 서버 설정](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[검사: 계정 파트너 조직 구성](Checklist--Configuring-the-Account-Partner-Organization.md)<br /><br />![연결 된 서버 설정](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[검사: 리소스 파트너 조직의 구성](Checklist--Configuring-the-Resource-Partner-Organization.md)|  
|![연결 된 서버 설정](media/icon_checkboxo.gif)|클라이언트 컴퓨터에서 federation 서버 작동 중인지 확인 합니다.|![연결 된 서버 설정](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[되어 있는지 확인 한 Federation 서버는 운영](Verify-That-a-Federation-Server-Is-Operational.md)| 
