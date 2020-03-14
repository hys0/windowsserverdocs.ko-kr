---
ms.assetid: 7b22adfa-298d-413c-88d0-1231825b7d4d
title: 동적 액세스 제어 시나리오 개요
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: e53b267f1319681f4a1914b16aaed149134054a8
ms.sourcegitcommit: 0a0a45bec6583162ba5e4b17979f0b5a0c179ab2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79322975"
---
# <a name="dynamic-access-control-scenario-overview"></a>동적 액세스 제어: 시나리오 개요

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Windows Server 2012에서는 파일 서버 전체에 데이터 관리를 적용 하 여 정보에 액세스할 수 있는 사용자를 제어 하 고 정보에 액세스 한 사용자를 감사할 수 있습니다. 동적 Access Control을 통해 다음을 수행할 수 있습니다.  
  
-   자동 및 수동 파일 분류를 사용하여 데이터 식별. 예를 들어 전사적으로 파일 서버의 데이터에 태그를 지정할 수 있습니다.  
  
-   중앙 액세스 정책을 사용하는 보안 네트워크 정책을 적용하여 파일에 대한 액세스 제어. 예를 들어 조직 내에서 건강 정보에 액세스할 수 있는 사용자를 정의할 수 있습니다.  
  
-   준수 보고 및 법정 분석을 위해 중앙 감사 정책을 사용하여 파일에 대한 액세스 감사 예를 들어 매우 중요한 정보에 액세스한 사용자를 식별할 수 있습니다.  
  
-   중요한 Microsoft Office 문서에 자동 RMS(Rights Management Services) 암호화를 사용하여 RMS 보호 적용. 예를 들어 HIPAA(Health Insurance Portability and Accountability Act) 정보가 포함된 모든 문서를 암호화하도록 RMS를 구성할 수 있습니다.  
  
동적 Access Control 기능 집합은 파트너 및 LOB(기간 업무) 애플리케이션이 유용하게 사용할 수 있는 향상된 인프라에 기반을 두고 있고, Active Directory를 사용하는 조직은 이러한 기능으로 뛰어난 가치를 얻을 수 있습니다. 이러한 인프라에 포함된 요소는 다음과 같습니다.  
  
-   조건식 및 중앙 정책을 처리할 수 있는 새로운 Windows용 권한 부여 및 감사 엔진  
  
-   사용자 클레임 및 디바이스 클레임에 대한 Kerberos 인증 지원  
  
-   FCI(파일 분류 인프라) 기능 향상  
  
-   파트너가 Microsoft가 아닌 타사 파일을 암호화하는 솔루션을 제공할 수 있도록 RMS 확장성 지원  
  
## <a name="in-this-scenario"></a>이 시나리오의 내용  
이 콘텐츠 집합에는 다음과 같은 시나리오 및 지침이 포함되어 있습니다.  
  
## <a name="BKMK_APP"></a>동적 Access Control 콘텐츠 로드맵  
  
|시나리오|평가|계획|배포|작동|  
|------------|------------|--------|----------|-----------|  
|**시나리오: 중앙 액세스 정책**<br /><br />파일에 대한 중앙 액세스 정책을 만들면 사용자 클레임, 디바이스 클레임 및 리소스 속성을 사용하여 조건식을 포함하는 권한 부여 정책을 중앙에서 배포하고 관리할 수 있습니다. 이러한 정책은 규정 준수 및 비즈니스 규정 요구 사항에 기반을 둡니다. 이러한 정책은 Active Directory에서 생성되고 호스트되므로 관리 및 배포가 더욱 간편합니다.<br /><br />**포리스트에 클레임 배포**<br /><br />Windows Server 2012에서는 AD DS 각 포리스트에 ' 클레임 사전 '을 유지 관리 하 고, 포리스트 내에서 사용 중인 모든 클레임 유형이 Active Directory 포리스트 수준에서 정의 됩니다. 보안 주체가 트러스트 경계를 트래버스해야 하는 시나리오가 많이 있습니다. 이러한 시나리오는 클레임이 트러스트 경계를 트래버스하는 방법을 설명합니다.|[동적 Access Control: 시나리오 개요](Dynamic-Access-Control--Scenario-Overview.md)<br /><br />[포리스트에 클레임 배포](Deploy-Claims-Across-Forests.md)|[요금제: 중앙 액세스 정책 배포](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f)<br /><br />[비즈니스 요청을 중앙 액세스 정책에 매핑하기 위한 -   프로세스](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f#BKMK_1)<br />[동적 Access Control에 대 한 관리 -   위임](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f#BKMK_3.1)<br />[중앙 액세스 정책을 계획 하는 -   예외 메커니즘](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f#BKMK_3.2)<br /><br />사용자 클레임 사용에 대한 모범 사례<br /><br />[사용자 도메인에서 클레임을 사용 하도록 설정 하려면 적절 한 구성을 선택](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f#BKMK_DC_OP3) -   .<br />[사용자 클레임을 사용 하도록 설정 하 -   작업](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f#BKMK_3.4.2)<br />[중앙 액세스 정책을 사용 하지 않고 파일 서버 임의 acl에서 사용자 클레임을 사용 하기 위한 -   고려 사항](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f#BKMK_5)<br /><br />[장치 클레임 및 장치 보안 그룹 사용](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f#BKMK_DeviceClaims)<br /><br />[정적 장치 클레임 사용에 대 한 -   고려 사항](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f#BKMK_4.1)<br />[장치 클레임을 사용 하도록 설정 하 -   작업](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f#BKMK_4.3)<br /><br />배포 도구<br /><br />-   [데이터 분류 도구 키트](https://go.microsoft.com/fwlink/?LinkId=%20244300)|[중앙 액세스 정책 &#40;데모 단계 배포&#41;](Deploy-a-Central-Access-Policy--Demonstration-Steps-.md)<br /><br />[포리스트 &#40;전체에 클레임 배포 데모 단계&#41;](Deploy-Claims-Across-Forests--Demonstration-Steps-.md)|-중앙 액세스 정책 모델링|  
|**시나리오: 파일 액세스 감사**<br /><br />보안 감사는 기업의 보안을 유지 관리할 수 있는 가장 효율적인 도구 중 하나입니다. 보안 감사의 주요 목표 중 하나는 규정 준수입니다. 예를 들어 Sarbanes Oxley, HIPAA, PCI(Payment Card Industry) 등의 업계 표준에서는 기업에서 데이터 보안 및 개인 정보와 관련된 엄격한 규칙 집합을 따르도록 규정하고 있습니다. 보안 감사를 통해 이러한 정책의 유무를 파악하여 해당 표준 준수 여부를 증명할 수 있습니다. 또한 보안 감사를 사용하면 비정상적인 동작을 파악하고, 보안 정책의 결함을 파악 및 완화하며, 법정 분석에 사용할 수 있는 사용자 작업 레코드를 만들어 무책임한 행위를 방지할 수 있습니다.|[시나리오: 파일 액세스 감사](Scenario--File-Access-Auditing.md)|[파일 액세스 감사 계획](Plan-for-File-Access-Auditing.md)|[중앙 감사 정책을 &#40;사용 하 여 보안 감사 배포 데모 단계&#41;](Deploy-Security-Auditing-with-Central-Audit-Policies--Demonstration-Steps-.md)|[파일 서버에 적용 되는 중앙 액세스 정책 -   모니터링](https://technet.microsoft.com/library/jj574188.aspx)<br />[파일 및 폴더와 연결 된 중앙 액세스 정책을 -   모니터링](https://technet.microsoft.com/library/jj574198.aspx)<br />[파일 및 폴더의 리소스 특성을 모니터링](https://technet.microsoft.com/library/jj574208.aspx) -   <br />-   [모니터 클레임 유형](https://technet.microsoft.com/library/jj574086.aspx)<br />[로그인 시 사용자 및 장치 클레임을 모니터링](https://technet.microsoft.com/library/jj574082.aspx) -   <br />[중앙 액세스 정책 및 규칙 정의 -   모니터링](https://technet.microsoft.com/library/jj574115.aspx)<br />[리소스 특성 정의](https://technet.microsoft.com/library/jj574155.aspx) 를 -   모니터링<br />[이동식 저장 장치 사용을 모니터링](https://technet.microsoft.com/library/jj574128.aspx)-   합니다.|  
|**시나리오: 액세스 거부 지원**<br /><br />오늘날 사용자가 파일 서버의 원격 파일에 액세스하려고 하면 액세스가 거부되었다는 메시지만 표시됩니다. 이로 인해 지원 센터 또는 IT 관리자에게 문제 확인 문의가 발생하고, 관리자들은 사용자에게 정확한 정황 정보를 얻기가 곤란해 문제 해결이 더욱 어려워집니다. <br />Windows Server 2012에서 목표는 정보 근로자와 데이터의 비즈니스 소유자가 액세스 거부 문제를 처리 하는 데 도움을 주는 데 도움이 되는 것입니다. 이러한 목표를 달성 하는 문제 중 하나는 액세스 거부를 처리할 수 있는 중앙 방법이 없고 응용 프로그램 마다이를 다르게 처리 하는 것입니다. 따라서 Windows Server 2012에서는 windows 탐색기의 액세스 거부 환경을 개선 하는 것이 목표 중 하나입니다.|[시나리오: 액세스 거부 지원](Scenario--Access-Denied-Assistance.md)|[액세스 거부 지원 계획](assetId:///b169f0a4-8b97-4da8-ae4a-c8f1986d19e1)<br /><br />[액세스 거부 지원 모델을 결정](assetId:///b169f0a4-8b97-4da8-ae4a-c8f1986d19e1#BKMK_1.1) -   <br />[액세스 요청을 처리 해야 하는 사용자를 확인](assetId:///b169f0a4-8b97-4da8-ae4a-c8f1986d19e1#BKMK_12) -   <br />[액세스 거부 지원 메시지 사용자 지정](assetId:///b169f0a4-8b97-4da8-ae4a-c8f1986d19e1#BKMK_13) -   <br />[예외에 대 한 -   계획](assetId:///b169f0a4-8b97-4da8-ae4a-c8f1986d19e1#BKMK_1.4)<br />[액세스 거부 지원이 배포 되는 방법을 결정](assetId:///b169f0a4-8b97-4da8-ae4a-c8f1986d19e1#BKMK_1.5) -   |[액세스 거부 지원 &#40;데모 단계 배포&#41;](Deploy-Access-Denied-Assistance--Demonstration-Steps-.md)||  
|**시나리오: Office 문서에 대 한 분류 기반 암호화**<br /><br />중요한 정보를 보호하는 가장 큰 이유는 조직의 위험을 완화하기 위함입니다. HIPAA 또는 PCI-DSS(Payment Card Industry Data Security Standard)와 같은 다양한 규정에 정보의 암호화가 명시되어 있고, 비즈니스 측면에서 중요한 비즈니스 정보를 암호화해야 하는 이유는 다양합니다. 그러나 정보 암호화는 비용이 많이 들고 비즈니스 생산성을 저하시킬 수 있습니다. 따라서 조직마다 정보 암호화의 접근 방식과 우선 순위가 다양한 편입니다. <br />이 시나리오를 지원 하기 위해 Windows Server 2012에서는 중요 한 Windows Office 파일을 분류에 따라 자동으로 암호화 하는 기능을 제공 합니다. 이 기능은 파일이 파일 서버에서 중요한 파일로 식별되고 몇 초 후 중요한 문서에 대한 AD RMS(Active Directory Rights Management Server) 보호를 호출하는 파일 관리 작업을 통해 수행됩니다.|[시나리오: Office 문서에 대 한 분류 기반 암호화](Scenario--Classification-Based-Encryption-for-Office-Documents.md)|[문서에 대 한 분류 기반 암호화를 위한 배포 계획](assetId:///14714ba6-d6a2-45e4-aae5-d3318817e52a)|[Office 파일 &#40;의 암호화 배포 데모 단계&#41;](Deploy-Encryption-of-Office-Files--Demonstration-Steps-.md)||  
|**시나리오: 분류를 사용 하 여 데이터에 대 한 통찰력 얻기**<br /><br />대부분의 조직에서 데이터 및 스토리지 리소스에 대한 의존도가 점점 높아지고 있습니다. IT 관리자는 점점 커지고 복잡해지는 스토리지 인프라를 관리하는 동시에 총 소유 비용을 합리적인 수준으로 유지해야 하는 과제에 직면했습니다. 스토리지 리소스 관리는 더 이상 데이터의 볼륨이나 가용성에만 국한되지 않습니다. 회사 정책을 적용하고 스토리지가 어떻게 소비되고 있는지 파악하여 효율성을 높이고 규정 준수를 강화함으로써 위험을 완화하는 방법까지 고려해야 합니다. 파일 분류 인프라는 데이터를 보다 효율적으로 관리할 수 있도록 분류 프로세스를 자동화함으로써 데이터에 대한 정보를 제공합니다. 파일 분류 인프라에서는 수동, 프로그래밍 방식, 자동과 같은 분류 방법을 사용할 수 있습니다. 이 시나리오에서는 자동 파일 분류 방법에 중점을 둡니다.|[시나리오: 분류를 사용 하 여 데이터에 대 한 통찰력 얻기](Scenario--Get-Insight-into-Your-Data-by-Using-Classification.md)|[자동 파일 분류 계획](assetId:///e3c3bb4b-3034-42b7-b391-8ef5f5851955)|[자동 파일 분류 &#40;데모 단계 배포&#41;](Deploy-Automatic-File-Classification--Demonstration-Steps-.md)||  
|**시나리오: 파일 서버에 대 한 정보 보존 구현**<br /><br />보존 기간은 문서가 만료되기 전에 보관되어야 하는 기간입니다. 조직에 따라 보존 기간이 다를 수 있습니다. 폴더의 파일을 단기, 중기 또는 장기 보존 기간으로 분류한 다음 각 기간의 시간 범위를 할당할 수 있습니다. 파일에 법적 보존을 설정하여 파일을 무기한으로 보관할 수도 있습니다. <br />파일 분류 인프라 및 파일 서버 리소스 관리자는 파일 관리 작업 및 파일 분류를 사용하여 파일 집합의 보존 기간을 적용합니다. 폴더에 보존 기간을 할당한 다음 파일 관리 작업을 사용하여 할당된 보존 기간을 얼마나 오래 유지할지 구성할 수 있습니다. 폴더의 파일이 곧 만료될 경우 파일 소유자에게 알림 메일이 전송됩니다. 또한 파일 관리 작업으로 인해 파일이 만료되지 않도록 파일을 법적 보존이 설정된 것으로 분류할 수도 있습니다.|[시나리오: 파일 서버에 대 한 정보 보존 구현](Scenario--Implement-Retention-of-Information-on-File-Servers.md)|[파일 서버에 대 한 정보 보존 계획](assetId:///edf13190-7077-455a-ac01-f534064a9e0c)|[파일 서버 &#40;에 정보 보존 구현 데모 단계&#41;](Deploy-Implementing-Retention-of-Information-on-File-Servers--Demonstration-Steps-.md)||  
  
> [!NOTE]  
> ReFS(복원 파일 시스템)에서는 동적 Access Control이 지원되지 않습니다.  
  
## <a name="BKMK_LINKS"></a>참고 항목  
  
|콘텐츠 유형|참조|  
|----------------|--------------|  
|**제품 평가**|-   [동적 Access Control 검토자 가이드](https://go.microsoft.com/fwlink/?LinkId=244309)<br />-   [동적 Access Control 개발자 지침](https://go.microsoft.com/fwlink/?LinkId=245870)|  
|**계획**|[중앙 액세스 정책 배포 -   계획](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f)<br />[파일 액세스 감사에 대 한 -   계획](Plan-for-File-Access-Auditing.md)|  
|**배포**|-   [Active Directory 배포](https://go.microsoft.com/fwlink/p/?LinkID=238318)<br />[파일 및 저장소 서비스 배포](https://go.microsoft.com/fwlink/?LinkID=24430) -   |  
|**작업**|[동적 Access Control PowerShell 참조](https://go.microsoft.com/fwlink/?LinkId=243150)|  
|**도구 및 설정**|[데이터 분류 도구 키트](https://go.microsoft.com/fwlink/?LinkID=244300)|  
|**커뮤니티 리소스**|[디렉터리 서비스 포럼](https://social.technet.microsoft.com/Forums/winserverDS/threads)|  
  


