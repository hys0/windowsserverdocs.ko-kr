---
ms.assetid: 7b22adfa-298d-413c-88d0-1231825b7d4d
title: "동적 액세스 제어 시나리오 개요"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: f70bd138a16b23f1fbf7bfabc98ee184e3b9ab37
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="dynamic-access-control-scenario-overview"></a>동적 액세스 제어: 시나리오 개요

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Windows Server 2012에서 데이터 관리 정보에 액세스 하 여 파일 서버 정보에 액세스할 수 있는 사용자를 제어 하 고 감사 적용할 수 있습니다. 동적 액세스 제어 수 있습니다.  
  
-   자동 및 수동 분류 파일을 사용 하 여 데이터를 식별 합니다. 예를 들어, 파일 서버에 데이터 조직에서 태그 될 수 있습니다.  
  
-   중앙 액세스 정책을 사용 하는 net 보호 정책이 적용 하 여 파일에 대 한 액세스를 제어 합니다. 예를 들어, 조직 내 의료 정보에 액세스할 수 있는 사용자 정의 수 있습니다.  
  
-   중앙 감사 정책을 준수 보고 한 법적 분석을 위해 사용 하 여 파일에 액세스를 감사 합니다. 예를 들어, 누가 매우 중요 한 정보에 액세스 확인할 수 있습니다.  
  
-   중요 한 Microsoft Office 문서에 대 한 자동 RMS 암호화를 사용 하 여 서비스 RMS (권한 관리) 보호를 적용 됩니다. 예를 들어, 건강 한 책임 Act (HIPAA) 정보가 포함 된 모든 문서를 암호화 RMS 구성할 수 있습니다.  
  
동적 액세스 제어 기능 집합 파트너 하 여 더 이상 사용 및 온라인 비즈니스 응용 프로그램, 될 수 있는 infrastructure 투자를 식별할 기반으로 하며 기능에 대 한 Active Directory를 사용 하는 조직의 멋진 가치를 제공할 수 있습니다. 이 인프라는 다음과 같습니다.  
  
-   식 조건 및 정책 중앙 처리할 수 있는 Windows에 대 한 새로운 감사 하 고 승인 엔진 합니다.  
  
-   사용자 클레임 및 장치 클레임 Kerberos 인증 지원 합니다.  
  
-   파일 분류 Infrastructure (FCI) 개선 되었습니다.  
  
-   RMS 확장성 파트너는 Microsoft가 아닌 타사 파일을 암호화 솔루션을 제공할 수 있도록 지원 합니다.  
  
## <a name="in-this-scenario"></a>이 경우  
다음 시나리오 및 지침이 콘텐츠 세트의 일부로 포함 됩니다.  
  
## <a name="BKMK_APP"></a>동적 액세스 제어 콘텐츠 로드맵  
  
|시나리오|평가|요금제|배포|운영 하|  
|------------|------------|--------|----------|-----------|  
|**중앙 액세스 시나리오가: 정책**<br /><br />파일 허용 중앙 배포 하 고 사용 하 여 사용자 청구, 장치 클레임 및 리소스 속성 조건부 식을 포함 승인 정책을 관리 조직에 대 한 중앙 액세스 정책 만드는 중입니다. 이러한 정책을 준수 및 비즈니스 규정을 기반으로 합니다. 이 정책 만들고 따라서 쉽게 관리 하 고 배포 Active Directory에 호스팅된 합니다.<br /><br />**클레임 숲을 통한 배포**<br /><br />Windows Server 2012에서 AD DS 각 숲 속의 '클레임 사전'을 유지 하 고 모든 주장 숲 내 사용에서 형식은 Active Directory 숲 수준 정의 됩니다. 주체 신뢰 경계 통과 해야 할 수 있는 경우도 있습니다. 이 경우 클레임 신뢰 범위를 통과 하는 방법을 설명 합니다.|[동적 액세스 제어: 시나리오 개요](Dynamic-Access-Control--Scenario-Overview.md)<br /><br />[숲 클레임 배포](Deploy-Claims-Across-Forests.md)|[요금제: 중앙 액세스 정책 배포](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f)<br /><br />-   [프로세스를 비즈니스 요청 하는 중앙 액세스 정책](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f#BKMK_1)<br />-   [위임 동적 액세스 제어를 위한 관리](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f#BKMK_3.1)<br />-   [중앙 액세스 정책 계획에 대 한 예외 메커니즘](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f#BKMK_3.2)<br /><br />사용자 클레임 사용에 대 한 유용한<br /><br />-   [사용자 도메인 클레임 수 있도록 오른쪽 구성을 선택](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f#BKMK_DC_OP3)<br />-   [사용자 클레임 수 있도록 작업](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f#BKMK_3.4.2)<br />-   [고려 파일 서버에 사용자 클레임 사용에 대 한 중앙 액세스 정책 사용 하지 않고 임의 Acl](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f#BKMK_5)<br /><br />[장치 클레임 및 장치 보안 그룹을 사용 하 여](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f#BKMK_DeviceClaims)<br /><br />-   [클레임 고정 디바이스를 사용 하 여 사항](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f#BKMK_4.1)<br />-   [작업 클레임 디바이스를 사용 하도록 설정 하려면](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f#BKMK_4.3)<br /><br />배포에 대 한 도구<br /><br />-   [데이터 분류 도구 키트](https://go.microsoft.com/fwlink/?LinkId=%20244300)|[중앙 액세스 정책 & #40; 데모 단계 & #41; 배포](Deploy-a-Central-Access-Policy--Demonstration-Steps-.md)<br /><br />[숲 & #40; 데모 단계 & #41; 클레임 배포](Deploy-Claims-Across-Forests--Demonstration-Steps-.md)|-모델링 중앙 액세스 정책|  
|**시나리오가: 감사 액세스 파일**<br /><br />보안 감사 하는 엔터프라이즈의 보안을 유지 하는 데 도움이 가장 강력한 도구 중 하나입니다. 보안 감사의 핵심 목표 중 하나는 규정을 준수 합니다. 예를 들어, 산업 표준을 명시 Oxley, HIPAA, 및 결제 카드 산업 (PCI)과 같은 기업 무과실 규칙 데이터 보안 및 개인 정보 보호 관련 된 집합을 수행 하도록 필요 합니다. 보안 감사 도움말 이러한 정책; 여부가 설정 따라서 이러한 표준 준수 여부 증명 합니다. 또한 보안 감사 비정상적인 문제를 검색 하 고, 파악의 보안 정책 간격을 완화 하는 데 도움이 및 만들어 법적 분석을 위해 사용할 수 있는 사용자 활동에 대 한 기록을 무책임 문제를 방지 합니다.|[시나리오가: 감사 액세스 파일](Scenario--File-Access-Auditing.md)|[파일에 대 한 계획 액세스 감사](Plan-for-File-Access-Auditing.md)|[보안 중앙 감사 정책 및 #40, 데모 단계 & #41; 감사 배포](Deploy-Security-Auditing-with-Central-Audit-Policies--Demonstration-Steps-.md)|-   [모니터 파일 서버에 적용 되는 중앙 액세스 정책](https://technet.microsoft.com/library/jj574188.aspx)<br />-   [모니터에 연결 된 파일 및 폴더 중앙 액세스 정책](https://technet.microsoft.com/library/jj574198.aspx)<br />-   [파일 및 폴더에 리소스 특성 모니터](https://technet.microsoft.com/library/jj574208.aspx)<br />-   [모니터 클레임 유형](https://technet.microsoft.com/library/jj574086.aspx)<br />-   [로그인 하는 동안 사용자와 디바이스 클레임 모니터](https://technet.microsoft.com/library/jj574082.aspx)<br />-   [모니터 중앙 액세스 정책과 규칙 정의](https://technet.microsoft.com/library/jj574115.aspx)<br />-   [모니터 리소스 특성 정의](https://technet.microsoft.com/library/jj574155.aspx)<br />-   [이동식 저장소 장치 사용 모니터링](https://technet.microsoft.com/library/jj574128.aspx)합니다.|  
|**액세스 거부 Assistance 시나리오:**<br /><br />오늘, 사용자가 원격 파일 서버에서 파일에 액세스 하려고 하면 표시 되는 액세스 거부 되었습니다 됩니다. IT 관리자는 문제를 파악 해야 하는 자주 관리자에 게 사용자에 게 적절 한 상황에 맞는 하기 어렵게 문제를 해결 하는 또는 이렇게 고객 지원 센터에 대 한 요청을 생성 합니다. <br />Windows Server 2012에서 작업자 정보 및 비즈니스 소유자 데이터 액세스 거부 IT 가져옵니다 하기 전에 문제를 처리 하는 데 도움이 하는 관련 된 시기와 IT가 관여, 빨리 해결에 대 한 모든 정보를 제공 합니다. 이 목표를 달성 하는 데 문제 중 하나는 액세스 거부 다루는 데 중앙 방법은 하 고 모든 응용 프로그램 사용 하 여 다르게 deals 따라서 Windows Server 2012에서 목표 중 하나는 Windows 탐색기에 대 한 액세스 거부 환경을 개선 하기 위해입니다.|[액세스 거부 Assistance 시나리오:](Scenario--Access-Denied-Assistance.md)|[요금제에 대 한 액세스 거부 지원](assetId:///b169f0a4-8b97-4da8-ae4a-c8f1986d19e1)<br /><br />-   [지원 액세스 거부 모델 확인](assetId:///b169f0a4-8b97-4da8-ae4a-c8f1986d19e1#BKMK_1.1)<br />-   [액세스 요청을 처리 하 게 확인](assetId:///b169f0a4-8b97-4da8-ae4a-c8f1986d19e1#BKMK_12)<br />-   [액세스 거부 지원 메시지를 사용자 지정](assetId:///b169f0a4-8b97-4da8-ae4a-c8f1986d19e1#BKMK_13)<br />-   [요금제에 대 한 예외](assetId:///b169f0a4-8b97-4da8-ae4a-c8f1986d19e1#BKMK_1.4)<br />-   [어떻게 액세스 거부 지원 결정을 배포](assetId:///b169f0a4-8b97-4da8-ae4a-c8f1986d19e1#BKMK_1.5)|[액세스 거부 지원 #40, 데모 단계 & #41; 배포](Deploy-Access-Denied-Assistance--Demonstration-Steps-.md)||  
|**Office 문서에 대 한 분류 기반 암호화 시나리오:**<br /><br />중요 한 정보를 보호 주로 조직에 대 한 위험을 완화입니다. HIPAA 또는 결제 카드 Industry 데이터 보안 표준 (PCI-DSS) 등의 다양 한 준수 규정 받아쓰게 한 정보를 암호화 되며 비즈니스 중요 한 정보를 암호화 하는 여러 비즈니스 가지 이유가 있습니다. 그러나 듭니다 정보를 암호화 하 고 업무 생산성 손상 될 수 있습니다. 따라서 조직에는 다른 방법 및 우선 순위를 해당 정보를 암호화 하는 경우가 많습니다. <br />이 시나리오를 지원 하기 위해 Windows Server 2012 자신의 분류에 따라 중요 한 Windows Office 파일을 자동으로 암호화 하는 기능을 제공 합니다. 이 Active Directory Rights Management (AD RMS) 서버에 대 한 보호 문서 중요 한 파일 파일 서버에 중요 한 파일 것으로 확인 된 후 몇 초 호출 하는 파일 관리 작업을 통해 수행 됩니다.|[Office 문서에 대 한 분류 기반 암호화 시나리오:](Scenario--Classification-Based-Encryption-for-Office-Documents.md)|[문서의 암호화 분류 기반 배포할 계획](assetId:///14714ba6-d6a2-45e4-aae5-d3318817e52a)|[Office 파일 & #40 암호화; 데모 단계 & #41; 배포](Deploy-Encryption-of-Office-Files--Demonstration-Steps-.md)||  
|**시나리오: 분류를 사용 하 여 사용자의 데이터에 대 한 정보 가져오기**<br /><br />데이터와 저장소 리소스에 의존 계속 대부분 조직에 대 한 중요의 증가 하 합니다. IT 관리자의 적절 한 수준의 유지 총 소유 비용도 절감 되도록 책임을 동시에 담당 하는 동안 복잡해 저장소 인프라 감독 과제가 성장 합니다. 저장소 리소스 관리 없는 경우 거의 볼륨 나 데이터를 더 이상 하지만 회사 정책과 저장소 효율적인 활용도 및 위험을 완화 하 준수 수 있도록 소모 되는 방식을 파악 집행에 대 한 일 파일 분류 인프라 보다 효율적으로 사용자의 데이터를 관리할 수 있도록 분류 프로세스 자동화 하 여 사용자의 데이터에 대 한 정보를 제공 합니다. 다음 분류 방법 파일 분류 인프라를 사용할 수 있는: 수동, 프로그래밍 방식으로 자동 하 고 있습니다. 이 경우 자동으로 파일을 분류 방법에 집중합니다.|[시나리오: 분류를 사용 하 여 사용자의 데이터에 대 한 정보 가져오기](Scenario--Get-Insight-into-Your-Data-by-Using-Classification.md)|[자동으로 파일 분류 계획](assetId:///e3c3bb4b-3034-42b7-b391-8ef5f5851955)|[자동으로 파일 분류 & #40; 데모 단계 & #41; 배포](Deploy-Automatic-File-Classification--Demonstration-Steps-.md)||  
|**파일 서버에 보유 한 정보를 구현 하는 시나리오:**<br /><br />보유 기간은 문서 되어야 하는 시간을 만료 되기 전에 유지 합니다. 조직에 따라 보존 기간 다를 수 있습니다. 짧은, 중간 또는 장기 보존 기간 것으로 폴더의 파일을을 분류 하 고 각 기간에 대 한 시간 프레임 지정할 수 있습니다. 법률 대기 하 여 파일을 계속 유지 수도 있습니다. <br />파일 분류 인프라와 파일 서버 리소스 관리자 및 사용 하 여 파일 관리 작업 파일 분류 일련의 파일에 대 한 보존 기간을 적용 합니다. 폴더에 고정 기간 지정 하 고 파일 관리 작업을 사용 하 여 마지막에 할당 된 보존 기간은 얼마나 걸리나요 구성할 수 있습니다. 폴더의 파일 만료 되 면 통보 이메일이 해당 파일의 소유자가 가져옵니다. 파일을 하는 파일 관리 작업 파일을 만료 되지 것입니다 법적 보류 중으로 분류 수도 있습니다.|[파일 서버에 보유 한 정보를 구현 하는 시나리오:](Scenario--Implement-Retention-of-Information-on-File-Servers.md)|[보유 한 파일 서버에 대 한 정보에 대 한 계획](assetId:///edf13190-7077-455a-ac01-f534064a9e0c)|[파일 서버 #40, 데모 단계 & #41; 보유 한 정보를 구현 배포](Deploy-Implementing-Retention-of-Information-on-File-Servers--Demonstration-Steps-.md)||  
  
> [!NOTE]  
> 동적 액세스 제어 ReFS (복원 파일 시스템)에서 지원 되지 않습니다.  
  
## <a name="BKMK_LINKS"></a>참조 하십시오  
  
|콘텐츠 종류|참조|  
|----------------|--------------|  
|**제품 평가**|-   [동적 액세스 제어 검토자 가이드](https://go.microsoft.com/fwlink/?LinkId=244309)<br />-   [동적 액세스 제어 개발자 지침](https://go.microsoft.com/fwlink/?LinkId=245870)|  
|**계획**|-   [중앙 액세스 정책 배포를 계획](assetId:///0311a76d-d66c-4ddb-ade6-af586a2ad82f)<br />-   [파일에 대 한 계획 액세스 감사](Plan-for-File-Access-Auditing.md)|  
|**배포**|-   [Active Directory 배포](https://go.microsoft.com/fwlink/p/?LinkID=238318)<br />-   [파일 및 저장소 서비스 배포](https://go.microsoft.com/fwlink/?LinkID=24430)|  
|**작업**|[동적 액세스 제어 PowerShell 참조](https://go.microsoft.com/fwlink/?LinkId=243150)|  
|**도구 및 설정**|[데이터 분류 도구 키트](https://go.microsoft.com/fwlink/?LinkID=244300)|  
|**커뮤니티 리소스**|[디렉터리 서비스 포럼](https://social.technet.microsoft.com/Forums/winserverDS/threads)|  
  


