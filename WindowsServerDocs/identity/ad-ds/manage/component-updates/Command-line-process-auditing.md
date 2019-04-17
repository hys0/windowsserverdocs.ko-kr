---
ms.assetid: c8597cc8-bdcb-4e59-a09e-128ef5ebeaf8
title: "명령줄 프로세스 감사"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 61e7a5ca2b9c00c9976e6032bb10adb1974020b0
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="command-line-process-auditing"></a>명령줄 프로세스 감사

>적용 대상: Windows Server 2016, Windows Server 2012 r 2

**작성자**: Windows 그룹과 조자룡 Turner, 선임 지원 엔지니어로  
  
> [!NOTE]  
> 이 콘텐츠는 Microsoft 고객 지원 담당자가 작성 하며 경험이 관리자와 technet 항목 일반적으로 제공 하는 것 보다에 대 한 보다 긴밀 기술 설명은 기능 및 Windows Server 2012 r 2에 대 한 해결 방법을 찾는 누가 시스템 개발자를 위한 것입니다. 그러나 받지 않았습니다 동일한 편집 가공 일부 언어 일반적으로 technet 찾을 수 보다 세련 된 적게 보일 수 있도록 합니다.  
  
## <a name="overview"></a>개요  
  
-   기존 프로세스 생성 감사 이벤트 ID 4688 명령줄 프로세스에 대 한 감사 정보 이제 포함 됩니다.  
  
-   실행 파일 콘텐츠의 해시 SHA1/2 Applocker 이벤트 로그에 기록도  
  
    -   응용 프로그램 및 서비스 Logs\Microsoft\Windows\AppLocker  
  
-   GPO을 통해 했지만 기본적으로 사용 안 함  
  
    -   "명령줄 프로세스를 만드는 이벤트에 포함할"  
  
![명령줄 감사](media/Command-line-process-auditing/GTR_ADDS_Event4688.gif)  
  
**SEQ 골격을 그린 그림 \\\ * 아랍어 16 이벤트 4688**  
  
참조 _Ref366427278 \h 그림 16에서에서 업데이트 된 이벤트 ID 4688 검토 합니다.  이 이전에 대 한 정보를 업데이트 **프로세스 명령줄** 기록 합니다.  이제이 추가 로깅 때문 뿐만 아니라 wscript.exe 프로세스 시작 되었지만 VB 스크립트를 실행 하는 데 사용도 된 볼 수 있습니다.  
  
## <a name="configuration"></a>구성  
이 업데이트의 효과 보려면 두 정책 설정을 사용 해야 합니다.  
  
### <a name="you-must-have-audit-process-creation-auditing-enabled-to-see-event-id-4688"></a>이벤트 ID 4688 볼 수 있도록 권장 설정 감사 프로세스 만들기 감사 있어야 합니다.  
감사 프로세스 만들기 정책을 사용 하려면 다음 그룹 정책을 편집 합니다.  
  
**정책 위치:** 컴퓨터 구성 > 정책을 > Windows 설정 > 보안 설정 > 고급 감사 구성 > 자세히 추적  
  
**정책 이름:** 감사 프로세스 만들기  
  
**지원 되는:** Windows 7 이상  
  
**도움말/설명 합니다.**  
  
이 보안 정책 설정 프로세스를 (시작)를 만들 때 감사 이벤트 및 프로그램이 나을 만든 사용자의 이름 운영 체제에서 생성 있는지 여부를 결정 합니다.  
  
이러한 이벤트 감사 컴퓨터를 어떻게 사용 되 고 있는지를 파악 하는 데 도움이 사용자의 활동을 추적 하 고 있습니다.  
  
이벤트 볼륨: 낮거나 중간 시스템 사용에 따라  
  
**기본값:** 구성 되지 않음  
  
### <a name="in-order-to-see-the-additions-to-event-id-4688-you-must-enable-the-new-policy-setting-include-command-line-in-process-creation-events"></a>이벤트 ID 4688에 대 한 추가 확인을 위해 새로운 정책 설정을 사용 해야 합니다: 프로세스 생성 이벤트에 명령줄 포함  
**테이블 SEQ 테이블 \\\ * 아랍어 19 명령 선 프로세스 정책 설정**  
  
|정책 구성|세부 정보|  
|------------------------|-----------|  
|**경로**|관리 Templates\System\Audit 프로세스 만들기|  
|**설정**|**프로세스를 만드는 이벤트에 명령줄 포함**|  
|**기본 설정**|(사용할 수 없음) 구성 되지 않음|  
|**지원 되는 다음과 같습니다.**|?|  
|**설명**|이 정책 설정을 새 프로세스를 만들 때 보안 감사 이벤트에 기록 됩니다 어떤 정보를 결정 합니다.<br /><br />이 설정은 감사 프로세스 만들기 정책을 사용 하는 경우에 적용 됩니다. 명령줄 정보 모든 프로세스에 대 한 감사 프로세스 만들기 이벤트 4688의 일환으로 일반 텍스트 보안 이벤트 로그에 기록 됩니다이 정책 설정을 사용 하면 "새 프로세스가 만들었습니다," 켜고 워크스테이션 서버가 정책 설정을 적용 됩니다.<br /><br />사용 하지 않거나이 정책 설정을 구성 되어 있지 않으면 명령줄 정보는 프로세스의 감사 프로세스 만들기 이벤트에 포함 되지 않습니다.<br /><br />기본: 구성 되지 않음<br /><br />참고:이 정책 설정을 사용 하면 모든 사용자에 액세스할 수 있는 보안 이벤트에 대 한 명령줄 인수를 읽을 수 있게 됩니다 읽을 수 프로세스를 만들었습니다. 명령줄 인수 암호 또는 사용자 데이터 등 중요 한 개인 정보를 포함할 수 있습니다.|  
  
![명령줄 감사](media/Command-line-process-auditing/GTR_ADDS_IncludeCLISetting.gif)  
  
감사 정책 고급 구성 설정을 사용 하면 이러한 설정을 기본 감사 정책 설정에 의해 덮어쓰지 확인 해야 합니다.  이벤트 4719 설정을 덮어쓰여집니다 때 기록 됩니다.  
  
![명령줄 감사](media/Command-line-process-auditing/GTR_ADDS_Event4719.gif)  
  
다음 절차에서는의 모든 기본적인 감사 정책 설정 응용 프로그램을 차단 하 여 충돌을 방지 하는 방법을 보여 줍니다.  
  
### <a name="to-ensure-that-advanced-audit-policy-configuration-settings-are-not-overwritten"></a>감사 정책 고급 구성 설정을 덮어쓰지 되어 있는지 확인 하려면  
![명령줄 감사](media/Command-line-process-auditing/GTR_ADDS_AdvAuditPolicy.gif)  
  
1.  그룹 정책 관리 콘솔 열기  
  
2.  기본 도메인 정책 마우스 오른쪽 단추로 클릭 한 후 편집을 클릭 합니다.  
  
3.  컴퓨터 구성 두 번 클릭, 정책를 두 번 클릭 한 다음 Windows 설정 두 번 클릭 합니다.  
  
4.  보안 설정 두 번 클릭 하 고 로컬 정책 두 번 클릭 보안 옵션을 클릭 합니다.  
  
5.  감사를 두 번 클릭: 강제 감사 정책 하위 범주 설정 (Windows Vista 이상) 감사 정책 범주 설정을 재정의 누른 다음이 정책 설정 합니다.  
  
6.  사용을 클릭 한 다음 확인을 클릭 합니다.  
  
## <a name="additional-resources"></a>추가 리소스  
[감사 프로세스 만들기](https://technet.microsoft.com/library/dd941613(v=WS.10).aspx)  
  
[고급 보안 감사 정책 Step-by-Step 가이드](https://technet.microsoft.com/library/dd408940(v=WS.10).aspx)  
  
[AppLocker: 질문과 대답](https://technet.microsoft.com/library/ee619725(v=ws.10).aspx)  
  
## <a name="try-this-explore-command-line-process-auditing"></a>명령줄 프로세스 감사 탐색 시도해 보기:  
  
1.  사용 하도록 설정 **감사 프로세스 생성** 이벤트 사전 감사 정책 구성 덮어쓰지 확인 하 고  
  
2.  스크립트 몇 가지 이벤트 관심 생성 하 고 스크립트를 실행할는 만듭니다.  이벤트를 준수 합니다.  이벤트과 생성 하는 데 스크립트가는 다음과 같이 합니다.  
  
    ```  
    mkdir c:\systemfiles\temp\commandandcontrol\zone\fifthward  
    copy \\192.168.1.254\c$\hidden c:\systemfiles\temp\hidden\commandandcontrol\zone\fifthward  
    start C:\systemfiles\temp\hidden\commandandcontrol\zone\fifthward\ntuserrights.vbs  
    del c:\systemfiles\temp\*.* /Q  
    ```  
  
3.  명령줄 감사 프로세스를 사용 하도록 설정  
  
4.  앞으로 동일한 스크립트를 실행할 한 이벤트 되는지 확인  
  


