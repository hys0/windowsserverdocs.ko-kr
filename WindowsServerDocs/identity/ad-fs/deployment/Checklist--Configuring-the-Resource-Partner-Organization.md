---
ms.assetid: 80d50a9f-428e-40fe-b6b3-9837fd9a3efc
title: 검사 목록-리소스 파트너 조직 구성
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 62c8a00ea71635c8198fba1f34dee157ab9b3888
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80854636"
---
# <a name="checklist-configuring-the-resource-partner-organization"></a>검사 목록: 리소스 파트너 조직 구성

웹 호스팅 웹 서버를 포함 하는 리소스 파트너 조직의\-계정 파트너의 사용자가 액세스할 수 있는 응용 프로그램을 기반으로 합니다. 이 조직에서 관리자는 AD FS 관리 스냅인을 사용 해야\-하려면 계정 파트너 조직과 트러스트 관계를 나타내는 클레임 공급자 트러스트를 만듭니다. 차례로 계정 파트너 관리자 신뢰 하고자 하는 각 계정 파트너 조직에 대 한 신뢰 당사자 트러스트를 만들어야 합니다.  
  
이 검사 목록에는 리소스 파트너 조직의\) AD FS \(Active Directory Federation Services 배포 하는 데 필요한 작업이 포함 되어 있습니다. 또한 하나를 설정 하는 데 필요한 구성 요소를 구성 하기 위한 작업이 포함 되어\-페더레이션 파트너 관계의 절반입니다.  
  
배포 하는 경우는 [웹 SSO 디자인](https://technet.microsoft.com/library/dd807033.aspx), 이 검사 목록을 사용 해야 합니다. 그러나, 필요가 성공적으로 배포 하려면이 검사 목록의 작업을 완료 하는 [페더레이션된 웹 SSO 디자인](https://technet.microsoft.com/library/dd807050.aspx)합니다.  
  
> [!IMPORTANT]  
> 계정 파트너 조직의 관리자의 지침에 따르는지 확인 [검사 목록: 계정 파트너 조직 구성](Checklist--Configuring-the-Account-Partner-Organization.md) 모든 필요한 배포 작업을 만들려면 두 번째 페더레이션 파트너 관계의 절반에 완료 됩니다 하기 위해  
  
> [!NOTE]  
> 이 검사 목록의 작업을 순서대로 완료하세요. 참조 링크가 절차를 안내하는 경우 이 검사 목록의 나머지 작업을 계속 진행하려면 해당 절차의 단계를 완료한 후 이 항목으로 돌아와야 합니다.  
  
리소스 파트너](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**조직 구성 검사 목록: 리소스 파트너 조직 구성** ![  
  
||작업|참조|  
|-|--------|-------------|  
|![리소스 파트너 조직 구성](media/icon_checkboxo.gif)|현재 프로덕션 환경에 기존 AD FS 1.0 또는 1.1 배포가 있는 경우 현재 페더레이션 서비스의 설정을 새 AD FS 페더레이션 서비스로 마이그레이션하는 방법에 대 한 자세한 내용은 오른쪽의 링크를 참조 하세요. 조직에서 AD FS를 사용 하 여 처음으로 AD FS를 배포 하는 경우이 단계를 건너뛰고이 검사 목록에서 다음 작업을 진행 하 여 새 리소스 파트너 조직을 설정 하는 방법에 대 한 정보를 확인할 수 있습니다.|리소스 파트너 조직 구성 ![](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS로 마이그레이션 계획](https://technet.microsoft.com/library/ff678044.aspx)|  
|![리소스 파트너 조직 구성](media/icon_checkboxo.gif)|배포 목표에 based, 페더레이션된 애플리케이션에 액세스할 수 있는 사용자에 게 제공 하는 데 필요한 구성 요소에 대 한 정보를 검토 합니다.|![리소스 파트너 조직 구성](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Active Directory 사용자에 게 클레임 인식 응용 프로그램 및 서비스에 대 한 액세스를 제공](https://technet.microsoft.com/library/dd807071.aspx) 합니다.<p>![리소스 파트너 조직 구성](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Active Directory 사용자에 게 다른 조직의 응용 프로그램 및 서비스에 대 한 액세스 권한을 제공 합니다](https://technet.microsoft.com/library/dd807123.aspx) .<p>리소스 파트너 조직 구성 ![](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[다른 조직의 사용자에 게 클레임 인식 응용 프로그램 및 서비스에 대 한 액세스 권한을 제공 합니다](https://technet.microsoft.com/library/dd807099.aspx) .|  
|![리소스 파트너 조직 구성](media/icon_checkboxo.gif)|AD FS 디자인에는이 리소스 파트너 조직의 연관 될 것을 확인 합니다.|![리소스 파트너 조직](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[웹 SSO 디자인](https://technet.microsoft.com/library/dd807033.aspx) 구성<p>![리소스 파트너 조직](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[페더레이션된 웹 SSO 디자인](https://technet.microsoft.com/library/dd807050.aspx) 구성|  
|![리소스 파트너 조직 구성](media/icon_checkboxo.gif)|다른 애플리케이션 종류를 검토 하 고 배포 하는 애플리케이션을 결정 합니다.|리소스 파트너 조직 구성 ![](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[리소스 파트너에서 페더레이션 응용 프로그램 전략 결정](https://technet.microsoft.com/library/dd807077.aspx)|  
|![리소스 파트너 조직 구성](media/icon_checkboxo.gif)|AD FS 서버 배포를 시작 하기 전에을 검토 하십시오. 1. Windows 내부 데이터베이스 \(WID\)를 선택 하거나 AD FS 구성 데이터베이스 2를 저장 하는 SQL Server의 장점과 단점을\) 합니다.\) 배포 토폴로지 유형 및 연결 된 서버 배치 및 네트워크 레이아웃 권장 사항을 AD FS 합니다.|![리소스 파트너 조직 구성](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS 배포 토폴로지 결정](https://technet.microsoft.com/library/gg982491.aspx)<p>리소스 파트너 조직](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS 배포 토폴로지 고려 사항](https://technet.microsoft.com/library/gg982489.aspx) 구성 ![|  
|![리소스 파트너 조직 구성](media/icon_checkboxo.gif)|페더레이션 서버 및 프로덕션 환경에서 사용 해야 하는 페더레이션 서버 프록시 서버에 적절 한 수를 확인 하려면 AD FS 용량 계획 지침을 검토 합니다.|리소스 파트너 조직](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS 서버 용량 계획](https://technet.microsoft.com/library/gg749899.aspx) ![구성|  
|![리소스 파트너 조직 구성](media/icon_checkboxo.gif)|효과적으로 계획 하 고 계정 파트너 배포에 대 한 물리적 토폴로지를 구현, AD FS 디자인 하나 이상의 페더레이션 서버 또는 페더레이션 서버 프록시에 필요한 지 여부를 결정 합니다.|![리소스 파트너 조직 구성](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[검사 목록: 페더레이션 서버 설정](Checklist--Setting-Up-a-Federation-Server.md)<p>![리소스 파트너 조직 구성](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[검사 목록: 페더레이션 서버 프록시 설정](Checklist--Setting-Up-a-Federation-Server-Proxy.md)|  
|![리소스 파트너 조직 구성](media/icon_checkboxo.gif)|AD FS에 추가할 특성 저장소의 유형을 결정 합니다. 그런 다음 AD FS 관리 스냅인을 사용 하 여 특성 저장소 추가\-에 있습니다.|리소스 파트너 조직 구성 ![](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[특성 저장소의 역할](../../ad-fs/technical-reference/The-Role-of-Attribute-Stores.md)<p>![리소스 파트너 조직 구성](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[특성 저장소 추가](../../ad-fs/operations/Add-an-Attribute-Store.md)|  
|![리소스 파트너 조직 구성](media/icon_checkboxo.gif)|AD FS 1.0 또는 1.1 페더레이션 서비스를 사용 하는 계정 파트너에서 클레임을 전송 하거나 클레임을 사용 해야 하는 경우 이전 버전의 AD FS와 상호 운용 하도록 AD FS를 구성 하는 방법에 대 한 자세한 내용은 오른쪽의 링크를 참조 하세요. 계정 파트너 조직의 AD FS을 사용 하 여 송신 또는 조직에 대 한 클레임을 사용 하는, 하는 경우이 단계를 건너뛰고이 검사 목록에서 다음 작업을 진행할 수 있습니다.|리소스 파트너 조직 구성 ![](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[AD FS 1.x와의 상호 운용성 계획](https://technet.microsoft.com/library/ff678040.aspx)|  
|![리소스 파트너 조직 구성](media/icon_checkboxo.gif)|리소스 파트너 조직에 첫 번째 페더레이션 서버를 배포한 후 AD FS 관리 스냅인을 사용 하 여 클레임 공급자 트러스트 관계를 만들\-에 있습니다. 수동으로 계정 파트너에 대 한 데이터를 입력 하거나 귀하에 게 관리자 계정 파트너 조직에 제공 하는 페더레이션 메타 데이터 URL을 사용 하 여 클레임 공급자 트러스트를 만들 수 있습니다. 또한, 페더레이션 메타데이터를 사용하여 리소스 파트너에 대한 데이터를 자동으로 검색할 수 있습니다. **참고:** 계정 파트너의 페더레이션 메타 데이터를 게시 또는 파일을 사용 하 여의 복사본을 제공할 수, 하는 경우 데이터를 검색할 수는 자동으로 시간을 절약할 수 있으므로 것이 좋습니다.|리소스 파트너 조직 구성 ![](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[수동으로 신뢰 당사자 트러스트 만들기](../operations/create-a-relying-party-trust.md#to-create-a-claims-aware-relying-party-trust-manually)<p>![리소스 파트너 조직 구성](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[페더레이션 메타 데이터를 사용 하 여 신뢰 당사자 트러스트 만들기](../operations/create-a-relying-party-trust.md#to-create-a-claims-aware-relying-party-trust-using-federation-metadata)|  
|![리소스 파트너 조직 구성](media/icon_checkboxo.gif)|만들 사용자 조직의 요구에 따라 각 클레임 공급자 트러스트 지정 된 대 한 더 많은 클레임 규칙 집합 또는 AD FS 관리 스냅인에서\-에서 들어오는 클레임을 통해 전달 되며 되도록 변환 된, 또는 적절 하 게 하려면 매핑된 해당 클레임을 리소스 파트너입니다.|![리소스 파트너 조직 구성](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[검사 목록: 클레임 공급자 트러스트에 대 한 클레임 규칙 만들기](Checklist--Creating-Claim-Rules-for-a-Claims-Provider-Trust.md)|  
|![리소스 파트너 조직 구성](media/icon_checkboxo.gif)|선택적\) \(조직의 요구를 충족 하는 클레임 설명이 아직 없는 경우 만들어야 할 수 있습니다. AD FS에 노출 되는 클레임 설명의 기본 집합에 포함 되어 AD FS 관리 스냅인에서\-에 있습니다.|![리소스 파트너 조직 구성](media/15dd35b6-6cc6-421f-93f8-7109920e7144.gif)[클레임 설명 추가](../../ad-fs/operations/Add-a-Claim-Description.md)|  
