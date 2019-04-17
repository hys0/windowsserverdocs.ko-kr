---
ms.assetid: 826974ea-3635-40df-aa37-77dd12a363c8
title: "계정 파트너 조직 구성 목록"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: df8057bf8afb51cbd9ca2ec704144b5863bdf064
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="checklist-configuring-the-account-partner-organization"></a>구성 계정 파트너 조직 검사:

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

계정 파트너 조직 리소스 파트너에 Web\ 기반 응용 프로그램에 액세스 하는 사용자가 포함 되어 있습니다. 이 기관에 관리자 리소스 파트너 조직의 보안 관계를 대표 하 파티 신뢰 신뢰를 만들 수 snap\에서 광고 FS 관리를 사용 해야 합니다. 그러면 리소스 파트너 관리자가 신뢰 하려는 각 계정 파트너 조직에 대 한 청구 제공자 신뢰 만들어야 합니다.  
  
이 검사 Active Directory Federation Services \(AD FS\) 계정 파트너 조직에서 배포 하기 위한 작업이 포함 됩니다. 또한 federation 간 산학 협동의 one\ 절반 설정 하는 데 필요한 구성 요소를 구성 하기 위한 작업이 포함 됩니다.  
  
배포 하는 경우는 [웹 SSO 디자인](https://technet.microsoft.com/library/dd807033.aspx)를 따라이 검사 필요가 없습니다. 하지만이 검사에 성공적으로 배포할의 작업을 완료 해야, 한 [웹 SSO 디자인 연방](https://technet.microsoft.com/library/dd807050.aspx)합니다.  
  
> [!IMPORTANT]  
> 리소스 파트너 조직에는 관리자에 대 한 지침을 따릅니다 있는지 확인 [검사: 리소스 파트너 조직 구성](Checklist--Configuring-the-Resource-Partner-Organization.md) 를 만들기 위해 두 번째 federation 간 산학 협동의 절반 모든 배포 필요한 작업을 완료할 수는 있습니다.  
  
> [!NOTE]  
> 주문에서이 검사의 작업을 완료 합니다. 이 검사에서 나머지 작업 진행할 수 있도록이 절차의 단계를 완료 한 후이 항목을 참조 링크는 절차로 이동 때 돌아갑니다.  
  
![계정 파트너 조직 구성](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**검사: 계정 파트너 조직 구성**  
  
||작업|참조|  
|-|--------|-------------|  
|![계정 파트너 조직 구성](media/icon_checkboxo.gif)|실제 환경에서 오늘 기존 ADFS 1.0 또는 1.1 배포 있는 경우 현재 Federation 서비스에서 설정을 한 새 ADFS Federation 서비스로 마이그레이션할 하는 방법에 대 한 내용은 오른쪽에 있는 링크를 참조 하십시오. 배포 하는 경우 ADFS 처음으로 조직에서 Adfs을 사용 하 여 사용자 수이 단계를 건너뛰고 새 계정 파트너 조직을 설정 하는 방법에 대 한 정보에 대 한이 검사에 다음 작업을 계속 합니다.|![계정 파트너 조직 구성](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[ADFS 2.0으로 마이그레이션을 계획](https://technet.microsoft.com/library/ff678044.aspx)|  
|![계정 파트너 조직 구성](media/icon_checkboxo.gif)|연결 된 응용 프로그램에 대 한 액세스를 사용자에 게 제공 하는 데 필요한 구성 요소에 대 한 정보를 검토 배포 목표에 based 합니다.|![계정 파트너 조직 구성](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[제공 나만의 Active Directory 사용자에 대 한 액세스 클레임 인식 나만의 응용 프로그램 및 서비스](https://technet.microsoft.com/library/dd807071.aspx)<br /><br />![계정 파트너 조직 구성](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[제공 나만의 Active Directory 사용자에 대 한 액세스 응용 프로그램 및 기타 조직 서비스](https://technet.microsoft.com/library/dd807123.aspx)<br /><br />![계정 파트너 조직 구성](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[클레임 인식 나만의 응용 프로그램 및 서비스에 대 한 또 다른 조직 액세스에 사용자가 제공](https://technet.microsoft.com/library/dd807099.aspx)|  
|![계정 파트너 조직 구성](media/icon_checkboxo.gif)|결정는 ADFS 디자인이 계정 파트너 조직 연결 됩니다.|![계정 파트너 조직 구성](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[웹 SSO 디자인](https://technet.microsoft.com/library/dd807033.aspx)<br /><br />![계정 파트너 조직 구성](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[웹 연방 SSO 디자인](https://technet.microsoft.com/library/dd807050.aspx)|  
|![계정 파트너 조직 구성](media/icon_checkboxo.gif)|ADFS 서버를 배포 하기 시작 하기 전에 검토; 1. \) Windows 내부 데이터베이스 \(WID\) 또는 SQL Server ADFS 구성 저장 하도록 선택 하면의 장단점 데이터베이스 2. \) ADFS 배포 토폴로지 유형과 관련된 서버 네트워크 위치와 위치 레이아웃 추천 합니다.|![계정 파트너 조직 구성](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[해당 AD FS 배포가 확인](https://technet.microsoft.com/library/gg982491.aspx)<br /><br />![계정 파트너 조직 구성](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[광고 FS 배포 토폴로지 고려](https://technet.microsoft.com/library/gg982489.aspx)|  
|![계정 파트너 조직 구성](media/icon_checkboxo.gif)|해당 federation 서버와 federation 서버 프록시 서버 생산 환경에서 사용 해야 수를 확인 하 지침 계획 ADFS 용량을 검토 합니다.|![계정 파트너 조직 구성](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[광고 FS 서버 용량에 대 한 계획](https://technet.microsoft.com/library/gg749899.aspx)|  
|![계정 파트너 조직 구성](media/icon_checkboxo.gif)|효과적인 계획 및 계정 파트너 배포용 실제 토폴로지 구현, federation 서버 또는 federation 서버 프록시 ADFS 디자인 필요한 지 여부를 결정 합니다.|![계정 파트너 조직 구성](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[검사: Federation 서버 설정](Checklist--Setting-Up-a-Federation-Server.md)<br /><br />![계정 파트너 조직 구성](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[검사: Federation 서버 프록시를를 크게 설정](Checklist--Setting-Up-a-Federation-Server-Proxy.md)|  
|![계정 파트너 조직 구성](media/icon_checkboxo.gif)|Adfs에 추가할 특성 스토어의 종류를 결정 합니다. snap\ AD FS 관리를 사용 하 여 특성 저장소를 추가 합니다.|![계정 파트너 조직 구성](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[The 특성 스토어 역할](../../ad-fs/technical-reference/The-Role-of-Attribute-Stores.md)<br /><br />![계정 파트너 조직 구성](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[특성 저장소 추가](../../ad-fs/operations/Add-an-Attribute-Store.md)|  
|![계정 파트너 조직 구성](media/icon_checkboxo.gif)|전송 해야 하는 경우에 주장 하 리소스 파트너 중 하나를 사용 하는 ADFS 1.0 또는 1.1 Federation 서비스를 사용 하거나 이전 버전의 Adfs와 상호 작용 ADFS 구성 하는 방법에 대 한 내용은 오른쪽에 대 한 링크를 참조 하세요. 리소스 파트너 조직도을 사용 하는 Adfs을 보내거나 클레임 조직에 사용 하는 경우이 단계를 건너뛰고이 검사에 다음 작업을 계속 수 있습니다.|![계정 파트너 조직 구성](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[ADFS 상호 운용성 계획 1.x](https://technet.microsoft.com/library/ff678040.aspx)|  
|![계정 파트너 조직 구성](media/icon_checkboxo.gif)|계정 파트너 조직에서 첫 번째 federation 서버를 배포한 후 snap\에서 AD FS 관리를 사용 하 여 신뢰 파티 신뢰 관계를 만듭니다. 신뢰 파티 신뢰 또는 리소스 파트너 회사의 관리자가 사용자에 게 제공 하는 federation URL 메타 데이터를 사용 하 여 수동으로 파트너 리소스에 대 한 데이터를 입력 하 여 만들 수 있습니다. 리소스 파트너에 대 한 데이터를 자동으로 검색 하는 federation 메타 데이터를 사용할 수 있습니다. **참고:** 리소스 파트너 게시 해당 federation 메타 데이터를 사용 하 여 사용자의 파일 복사본을 제공할 수,는 데이터를 검색 하 여 자동으로 시간을 절약할 수 있으므로 것이 좋습니다.|![계정 파트너 조직 구성](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[필요로 하 파티 신뢰 수동으로 만들](../../ad-fs/operations/Create-a-Relying-Party-Trust.md)<br /><br />![계정 파트너 조직 구성](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[의존 파티 신뢰를 사용 하 여 Federation 메타 데이터를 만들려면](../../ad-fs/operations/Create-a-Relying-Party-Trust.md)|  
|![계정 파트너 조직 구성](media/icon_checkboxo.gif)|조직의 필요에 따라 클레임 적절 하 게 발급 한가의 snap\ AD FS 관리에 지정 된 각 신뢰 파티 보안에 대 한 하나 또는 여러 개의 클레임 규칙 집합을 만듭니다.|![계정 파트너 조직 구성](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[검사: 필요로 하는 타사 신뢰할에 대 한 청구 규칙 만들기](Checklist--Creating-Claim-Rules-for-a-Relying-Party-Trust.md)|  
|![계정 파트너 조직 구성](media/icon_checkboxo.gif)|클레임 설명 아직 없는 경우 만들 수 있어야 하는 조직의의 요구를 충족 됩니다. Adfs는 snap\에서 광고 FS 관리에 표시 된 청구 설명의 기본 설정으로 제공 됩니다.|![계정 파트너 조직 구성](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[클레임 설명을 추가](../../ad-fs/operations/Add-a-Claim-Description.md)|  
|![계정 파트너 조직 구성](media/icon_checkboxo.gif)|사용 하 여 신원을 위임 승인할 또는 "역할 을" 하거나 다른 사용자에 게 가장 지정된 된 계정 제한 조직은 해야 하는지 여부를 결정 합니다. 이것은 종종 요구 사항 front\ 종료 웹 응용 프로그램 back\ 웹 서비스 상호 작용 해야 합니다.|![계정 파트너 조직 구성](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[사용 하 여 신원을 위임 하는 경우](https://technet.microsoft.com/library/dd807122.aspx)|  
|![계정 파트너 조직 구성](media/icon_checkboxo.gif)|하 여 federation 클라이언트 컴퓨터를 준비 합니다.<br /><br />-계정 파트너 federation 서버에 대 한 URL 클라이언트 브라우저에 대 한 신뢰할 수 있는 사이트 목록에 추가 합니다.<br />3를 사용 하 여 그룹 정책에 적절 한 주소 \(SSL\) 인증서 클라이언트 컴퓨터를 합니다.|![계정 파트너 조직 구성](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[클라이언트 컴퓨터에 계정 파트너 준비](https://technet.microsoft.com/library/dd807114(v=ws.11).aspx)<br /><br />![계정 파트너 조직 구성](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[계정 Federation 서버 신뢰 하는 클라이언트 컴퓨터 구성](Configure-Client-Computers-to-Trust-the-Account-Federation-Server.md)<br /><br />![계정 파트너 조직 구성](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[인증서 그룹 정책을 사용 하 여 컴퓨터에 배포](Distribute-Certificates-to-Client-Computers-by-Using-Group-Policy.md)| 
