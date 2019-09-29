---
ms.assetid: c8597cc8-bdcb-4e59-a09e-128ef5ebeaf8
title: 명령줄 프로세스 감사
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 5d5ab971327ab7ec16bf2748571882458cc38f72
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71368991"
---
# <a name="command-line-process-auditing"></a>명령줄 프로세스 감사

>적용 대상: Windows Server 2016, Windows Server 2012 R2

**작성자**: Justin Turner, Windows 그룹이 포함 된 선임 지원 에스컬레이션 엔지니어  
  
> [!NOTE]  
> 이 콘텐츠는 Microsoft 고객 지원 엔지니어에 의해 작성되었으며 Windows Server 2012 R2의 기능 및 솔루션에 대해 TechNet에서 일반적으로 제공하는 항목보다 더 자세한 기술적 설명을 찾고 있는 숙련된 관리자 및 시스템 설계자를 대상으로 합니다. 그러나 동일한 편집 과정을 수행하지 않았으므로 일부 언어는 일반적으로 TechNet에서 찾을 수 있는 것보다 완벽하지 않을 수 있습니다.  
  
## <a name="overview"></a>개요  
  
-   기존 프로세스 만들기 감사 이벤트 ID 4688는 이제 명령줄 프로세스에 대 한 감사 정보를 포함 합니다.  
  
-   또한 Applocker 이벤트 로그에서 실행 파일의 SHA1/2 해시를 로깅합니다.  
  
    -   응용 프로그램 및 서비스 Logs\Microsoft\Windows\AppLocker  
  
-   GPO를 통해 사용 하도록 설정 하지만 기본적으로 사용 하지 않도록 설정 되어 있습니다.  
  
    -   "프로세스 생성 이벤트에 명령줄 포함"  
  
![명령줄 감사](media/Command-line-process-auditing/GTR_ADDS_Event4688.gif)  
  
**그림 SEQ 그림 \\ @ no__t-2 아랍어 16 이벤트 4688**  
  
REF _Ref366427278 \h 그림 16에서 업데이트 된 이벤트 ID 4688을 검토 합니다.  이 업데이트 이전에는 **프로세스 명령줄** 에 대 한 정보가 기록 되지 않습니다.  이 추가 로깅으로 인해 이제 wscript.exe 프로세스가 시작 되었지만 VB 스크립트를 실행 하는 데에도 사용 되었다는 것을 알 수 있습니다.  
  
## <a name="configuration"></a>Configuration  
이 업데이트의 결과를 확인 하려면 두 가지 정책 설정을 사용 하도록 설정 해야 합니다.  
  
### <a name="you-must-have-audit-process-creation-auditing-enabled-to-see-event-id-4688"></a>이벤트 ID 4688을 보려면 감사 프로세스 만들기 감사를 사용 하도록 설정 해야 합니다.  
프로세스 만들기 감사 정책을 사용 하도록 설정 하려면 다음 그룹 정책을 편집 합니다.  
  
**정책 위치:** 컴퓨터 구성 > 정책 > Windows 설정 > 보안 설정 > 고급 감사 구성 > 자세한 추적  
  
**정책 이름:** 프로세스 만들기 감사  
  
**지원 되는 위치:** Windows 7 이상  
  
**설명/도움말:**  
  
이 보안 정책 설정에 따라 프로세스를 만들 때 운영 체제에서 감사 이벤트를 생성할지 여부를 결정 합니다. (시작) 프로세스를 만든 프로그램 또는 사용자의 이름입니다.  
  
이러한 감사 이벤트는 컴퓨터가 사용 되는 방식을 이해 하 고 사용자 작업을 추적 하는 데 도움이 될 수 있습니다.  
  
이벤트 볼륨: 시스템 사용량에 따라 낮음-보통  
  
**기본값:** 구성되지 않음  
  
### <a name="in-order-to-see-the-additions-to-event-id-4688-you-must-enable-the-new-policy-setting-include-command-line-in-process-creation-events"></a>이벤트 ID 4688에 대 한 추가 사항을 보려면 새 정책 설정을 사용 하도록 설정 해야 합니다. 프로세스 생성 이벤트에 명령줄 포함  
**테이블 SEQ 테이블 \\ @ no__t-2 아랍어 19 명령줄 프로세스 정책 설정**  
  
|정책 구성|설명|  
|------------------------|-----------|  
|**경로**|관리 Templates\System\Audit 프로세스 만들기|  
|**설정**|**프로세스 생성 이벤트에 명령줄 포함**|  
|**기본 설정**|구성 되지 않음 (사용할 수 없음)|  
|**지원 되는 위치:**|?|  
|**설명**|이 정책 설정은 새 프로세스를 만들 때 보안 감사 이벤트에 기록 되는 정보를 결정 합니다.<br /><br />이 설정은 감사 프로세스 만들기 정책을 사용 하는 경우에만 적용 됩니다. 이 정책을 사용 하도록 설정 하면 모든 프로세스에 대 한 명령줄 정보가 감사 프로세스 만들기 이벤트 4688, "새 프로세스를 만들었습니다."의 일부로이 정책이 설정 된 워크스테이션과 서버에서 일반 텍스트로 기록 됩니다. 설정이 적용 됩니다.<br /><br />이 정책 설정을 사용 하지 않도록 설정 하거나 구성 하지 않으면 프로세스의 명령줄 정보가 감사 프로세스 생성 이벤트에 포함 되지 않습니다.<br /><br />기본값: 구성되지 않음<br /><br />참고: 이 정책 설정을 사용 하도록 설정 하면 보안 이벤트를 읽을 수 있는 액세스 권한이 있는 모든 사용자가 성공적으로 생성 된 프로세스에 대 한 명령줄 인수를 읽을 수 있습니다. 명령줄 인수는 암호나 사용자 데이터와 같은 중요 한 정보나 개인 정보를 포함할 수 있습니다.|  
  
![명령줄 감사](media/Command-line-process-auditing/GTR_ADDS_IncludeCLISetting.gif)  
  
고급 감사 정책 구성 설정을 사용하는 경우 기본 감사 정책 설정으로 이 설정을 덮어쓰지 않았는지 확인해야 합니다.  설정을 덮어쓸 때 이벤트 4719이 기록 됩니다.  
  
![명령줄 감사](media/Command-line-process-auditing/GTR_ADDS_Event4719.gif)  
  
다음 절차에서는 기본 감사 정책 설정을 적용하지 못하도록 차단하여 충돌을 방지하는 방법을 보여 줍니다.  
  
### <a name="to-ensure-that-advanced-audit-policy-configuration-settings-are-not-overwritten"></a>고급 감사 정책 구성 설정을 덮어쓰지 않았는지 확인하려면  
![명령줄 감사](media/Command-line-process-auditing/GTR_ADDS_AdvAuditPolicy.gif)  
  
1.  그룹 정책 관리 콘솔을 엽니다.  
  
2.  기본 도메인 정책을 마우스 오른쪽 단추로 클릭 한 다음 편집을 클릭 합니다.  
  
3.  컴퓨터 구성을 두 번 클릭 하 고 정책을 두 번 클릭 한 다음 Windows 설정을 두 번 클릭 합니다.  
  
4.  보안 설정을 두 번 클릭 하 고 로컬 정책을 두 번 클릭 한 다음 보안 옵션을 클릭 합니다.  
  
5.  감사를 두 번 클릭 합니다. 감사 정책 하위 범주 설정 (Windows Vista 이상)을 적용 하 여 감사 정책 범주 설정을 재정의 하 고이 정책 설정 정의를 클릭 합니다.  
  
6.  사용을 클릭 한 다음 확인을 클릭 합니다.  
  
## <a name="additional-resources"></a>추가 리소스  
[프로세스 만들기 감사](https://technet.microsoft.com/library/dd941613(v=WS.10).aspx)  
  
[고급 보안 감사 정책 단계별 가이드](https://technet.microsoft.com/library/dd408940(v=WS.10).aspx)  
  
[ Applocker: 질문과 대답](https://technet.microsoft.com/library/ee619725(v=ws.10).aspx)  
  
## <a name="try-this-explore-command-line-process-auditing"></a>다음을 시도 합니다. 명령줄 프로세스 감사 살펴보기  
  
1.  **프로세스 생성 이벤트 감사** 를 사용 하도록 설정 하 고 고급 감사 정책 구성을 덮어쓰지 않았는지 확인 합니다.  
  
2.  관련 된 일부 이벤트를 생성 하 고 스크립트를 실행 하는 스크립트를 만듭니다.  이벤트를 관찰 합니다.  이 단원에서 이벤트를 생성 하는 데 사용 되는 스크립트는 다음과 같습니다.  
  
    ```  
    mkdir c:\systemfiles\temp\commandandcontrol\zone\fifthward  
    copy \\192.168.1.254\c$\hidden c:\systemfiles\temp\hidden\commandandcontrol\zone\fifthward  
    start C:\systemfiles\temp\hidden\commandandcontrol\zone\fifthward\ntuserrights.vbs  
    del c:\systemfiles\temp\*.* /Q  
    ```  
  
3.  명령줄 프로세스 감사를 사용 하도록 설정  
  
4.  이전과 같은 스크립트를 실행 하 고 이벤트를 관찰 합니다.  
  


