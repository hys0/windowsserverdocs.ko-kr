---
ms.assetid: 80d50a9f-428e-40fe-b6b3-9837fd9a3efc
title: 구성 리소스 파트너 조직 목록
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 4c73d84a6a32a90f5a5a60f0a0f6e6405ea3b729
ms.sourcegitcommit: f26d2668f57624a3865ca4ffd36a698eea7b503e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/12/2018
---
# <a name="checklist-configuring-the-resource-partner-organization"></a>구성 리소스 파트너 조직 검사:

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

파트너 조직 리소스 호스팅 계정 파트너에는 사용자가 액세스할 수 있는 Web\ 기반 응용 프로그램의 웹 서버 포함 되어 있습니다. 이 기관에 관리자 계정 파트너 조직의 보안 관계를 대표 하 클레임 제공자 신뢰를 만들 수 snap\에 AD FS 관리를 사용 해야 합니다. 그러면 계정 파트너 관리자 신뢰 하려는 각 계정 파트너 조직에 대 한 신뢰 파티 신뢰 만들어야 합니다.  
  
이 검사는 Active Directory Federation Services \(AD FS\) 리소스 파트너 조직에서 배포 하는 데 필요한는 작업이 포함 됩니다. 또한 federation 간 산학 협동의 one\ 절반 설정 하는 데 필요한 구성 요소를 구성 하기 위한 작업이 포함 됩니다.  
  
배포 하는 경우는 [웹 SSO 디자인](https://technet.microsoft.com/library/dd807033.aspx)를 따라이 검사 필요가 없습니다. 하지만이 검사에 성공적으로 배포할의 작업을 완료 해야, 한 [웹 SSO 디자인 연방](https://technet.microsoft.com/library/dd807050.aspx)합니다.  
  
> [!IMPORTANT]  
> 관리자 계정 파트너 회사의에 대 한 지침을 따릅니다 있는지 확인 [검사: 계정 파트너 조직 구성](Checklist--Configuring-the-Account-Partner-Organization.md) federation 간 산학 협동의 절반 두 번째를 성공적으로 만들기 위해 모든 배포 필요한 작업을 완료할 수는 확인 하기  
  
> [!NOTE]  
> 주문에서이 검사의 작업을 완료 합니다. 이 검사에서 나머지 작업 진행할 수 있도록이 절차의 단계를 완료 한 후이 항목을 참조 링크는 절차로 이동 때 돌아갑니다.  
  
![구성 리소스 파트너 조직](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**검사: 리소스 파트너 조직의 구성**  
  
||작업|참조|  
|-|--------|-------------|  
|![구성 파트너 조직 리소스](media/icon_checkboxo.gif)|실제 환경에서 오늘 기존 ADFS 1.0 또는 1.1 배포 있는 경우 현재 Federation 서비스에서 설정을 한 새 ADFS Federation 서비스로 마이그레이션할 하는 방법에 대 한 내용은 오른쪽에 있는 링크를 참조 하십시오. 배포 하는 경우 ADFS 처음으로 조직에서 Adfs을 사용 하 여 사용자 수이 단계를 건너뛰고 새로운 리소스 파트너 조직을 설정 하는 방법에 대 한 정보에 대 한이 검사에 다음 작업을 계속 합니다.|![구성 리소스 파트너 조직](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Adfs로 마이그레이션을 계획](https://technet.microsoft.com/library/ff678044.aspx)|  
|![구성 파트너 조직 리소스](media/icon_checkboxo.gif)|연결 된 응용 프로그램에 대 한 액세스를 사용자에 게 제공 하는 데 필요한 구성 요소에 대 한 정보를 검토 배포 목표에 based 합니다.|![구성 리소스 파트너 조직](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[제공 나만의 Active Directory 사용자에 대 한 액세스 클레임 인식 나만의 응용 프로그램 및 서비스](https://technet.microsoft.com/library/dd807071.aspx)<br /><br />![구성 리소스 파트너 조직](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[제공 나만의 Active Directory 사용자에 대 한 액세스 응용 프로그램 및 기타 조직 서비스](https://technet.microsoft.com/library/dd807123.aspx)<br /><br />![구성 리소스 파트너 조직](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[클레임 인식 나만의 응용 프로그램 및 서비스에 대 한 또 다른 조직 액세스에 사용자가 제공](https://technet.microsoft.com/library/dd807099.aspx)|  
|![구성 파트너 조직 리소스](media/icon_checkboxo.gif)|결정는 ADFS 디자인이 리소스 파트너 조직 연결 됩니다.|![구성 리소스 파트너 조직](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[웹 SSO 디자인](https://technet.microsoft.com/library/dd807033.aspx)<br /><br />![구성 리소스 파트너 조직](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[웹 연방 SSO 디자인](https://technet.microsoft.com/library/dd807050.aspx)|  
|![구성 파트너 조직 리소스](media/icon_checkboxo.gif)|다른 응용 프로그램 유형, 검토 및 응용 프로그램 배포을 결정 합니다.|![구성 리소스 파트너 조직](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[결정 나만의 연방 응용 프로그램에서에서 전략 리소스 파트너](https://technet.microsoft.com/library/dd807077.aspx)|  
|![구성 파트너 조직 리소스](media/icon_checkboxo.gif)|ADFS 서버를 배포 하기 시작 하기 전에 검토; 1. \) Windows 내부 데이터베이스 \(WID\) 또는 SQL Server ADFS 구성 저장 하도록 선택 하면의 장단점 데이터베이스 2. \) ADFS 배포 토폴로지 유형과 관련된 서버 네트워크 위치와 위치 레이아웃 추천 합니다.|![구성 리소스 파트너 조직](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[해당 AD FS 배포가 확인](https://technet.microsoft.com/library/gg982491.aspx)<br /><br />![구성 리소스 파트너 조직](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[광고 FS 배포 토폴로지 고려](https://technet.microsoft.com/library/gg982489.aspx)|  
|![구성 파트너 조직 리소스](media/icon_checkboxo.gif)|해당 federation 서버와 federation 서버 프록시 서버 생산 환경에서 사용 해야 수를 확인 하 지침 계획 ADFS 용량을 검토 합니다.|![구성 리소스 파트너 조직](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[광고 FS 서버 용량에 대 한 계획](https://technet.microsoft.com/library/gg749899.aspx)|  
|![구성 파트너 조직 리소스](media/icon_checkboxo.gif)|효과적인 계획 및 계정 파트너 배포용 실제 토폴로지 구현, federation 서버 또는 federation 서버 프록시 ADFS 디자인 필요한 지 여부를 결정 합니다.|![구성 리소스 파트너 조직](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[검사: Federation 서버 설정](Checklist--Setting-Up-a-Federation-Server.md)<br /><br />![구성 리소스 파트너 조직](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[검사: Federation 서버 프록시를를 크게 설정](Checklist--Setting-Up-a-Federation-Server-Proxy.md)|  
|![구성 파트너 조직 리소스](media/icon_checkboxo.gif)|Adfs에 추가할 특성 스토어의 종류를 결정 합니다. snap\ AD FS 관리를 사용 하 여 특성 저장소를 추가 합니다.|![구성 리소스 파트너 조직](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[The 특성 스토어 역할](../../ad-fs/technical-reference/The-Role-of-Attribute-Stores.md)<br /><br />![구성 리소스 파트너 조직](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[특성 저장소 추가](../../ad-fs/operations/Add-an-Attribute-Store.md)|  
|![구성 파트너 조직 리소스](media/icon_checkboxo.gif)|전송 해야 하는 경우 주장 또는 클레임 중 하나를 사용 하는 계정 파트너 로부터 ADFS 1.0 또는 1.1 Federation 서비스는 소모, 연결 ADFS 구성 하는 방법에 대 한 내용은 권리를 이전 버전의 Adfs와 상호 작용을 볼 수 있습니다. 계정 파트너 조직도을 사용 하는 Adfs을 보내거나 클레임 조직에 사용 하는 경우이 단계를 건너뛰고이 검사에 다음 작업을 계속 수 있습니다.|![구성 리소스 파트너 조직](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[ADFS 상호 운용성 계획 1.x](https://technet.microsoft.com/library/ff678040.aspx)|  
|![구성 파트너 조직 리소스](media/icon_checkboxo.gif)|첫 번째 federation 서버 리소스 파트너 조직에를 배포한 후 snap\에서 AD FS 관리를 사용 하 여 클레임 공급자 신뢰 관계를 만듭니다. 청구 공급자 신뢰 계정 파트너 수동으로 대 한 데이터를 입력 하 여 또는 계정 파트너 회사의 관리자가 사용자에 게 제공 하는 federation URL 메타 데이터를 사용 하 여 만들 수 있습니다. 리소스 파트너에 대 한 데이터를 자동으로 검색 하는 federation 메타 데이터를 사용할 수 있습니다. **참고:** 계정 파트너 게시 해당 federation 메타 데이터를 사용 하 여 사용자의 파일 복사본을 제공할 수,는 데이터를 검색 하 여 자동으로 시간을 절약할 수 있으므로 것이 좋습니다.|![구성 리소스 파트너 조직](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[필요로 하 파티 신뢰 수동으로 만들](../operations/create-a-relying-party-trust.md#to-create-a-claims-aware-relying-party-trust-manually)<br /><br />![구성 리소스 파트너 조직](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[의존 파티 신뢰를 사용 하 여 Federation 메타 데이터를 만들려면](../operations/create-a-relying-party-trust.md#to-create-a-claims-aware-relying-party-trust-using-federation-metadata)|  
|![구성 파트너 조직 리소스](media/icon_checkboxo.gif)|조직의 필요에 따라 들어오는 클레임을 통해 전달 됩니다 snap\에서 광고 FS 관리에 지정 된 각 청구 공급자 신뢰를 하나 또는 여러 개의 클레임 규칙 집합 변형, 이거나 리소스 파트너에 해당 청구 발생 시에도 연결 되어 적절 하 게 만듭니다.|![구성 리소스 파트너 조직](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[검사: 신뢰 클레임 공급자에 대 한 청구 규칙 만들기](Checklist--Creating-Claim-Rules-for-a-Claims-Provider-Trust.md)|  
|![구성 파트너 조직 리소스](media/icon_checkboxo.gif)|\(Optional\) 클레임 설명 하나 아직 없는 하는 경우 자동으로 생성 해야 할 수 조직의 요구를 충족 됩니다. Adfs의 snap\ AD FS 관리에 노출 클레임 설명의 기본 설정 포함 되어 있습니다.|![구성 리소스 파트너 조직](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[클레임 설명을 추가](../../ad-fs/operations/Add-a-Claim-Description.md)|  
