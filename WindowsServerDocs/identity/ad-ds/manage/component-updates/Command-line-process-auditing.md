---
ms.assetid: c8597cc8-bdcb-4e59-a09e-128ef5ebeaf8
title: 명령줄 프로세스 감사
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 66ae6992775319cf614b0cb4c21f864150746687
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59859554"
---
# <a name="command-line-process-auditing"></a>명령줄 프로세스 감사

>적용 대상: Windows Server 2016, Windows Server 2012 R2

**작성자**: Windows 그룹과 Justin Turner, 수석 지원 에스컬레이션 엔지니어  
  
> [!NOTE]  
> 이 콘텐츠는 Microsoft 고객 지원 엔지니어에 의해 작성되었으며 Windows Server 2012 R2의 기능 및 솔루션에 대해 TechNet에서 일반적으로 제공하는 항목보다 더 자세한 기술적 설명을 찾고 있는 숙련된 관리자 및 시스템 설계자를 대상으로 합니다. 그러나 동일한 편집 과정을 수행하지 않았으므로 일부 언어는 일반적으로 TechNet에서 찾을 수 있는 것보다 완벽하지 않을 수 있습니다.  
  
## <a name="overview"></a>개요  
  
-   기존 프로세스 만들기 감사 이벤트 ID 4688 명령줄 프로세스 감사 정보를 포함 합니다.  
  
-   실행 파일의 SHA1/2 해시 Applocker 이벤트 로그에 기록 됩니다 것  
  
    -   응용 프로그램 및 서비스 Logs\Microsoft\Windows\AppLocker  
  
-   GPO를 통해 사용 하도록 설정 되지만 기본적으로 비활성화 됩니다.  
  
    -   "프로세스 생성 이벤트에 명령 줄을 포함 합니다."  
  
![명령줄 감사](media/Command-line-process-auditing/GTR_ADDS_Event4688.gif)  
  
**그림 SEQ 그림 \\ \* 아랍어 16 이벤트 4688**  
  
REF _Ref366427278 \h 그림 16에에서 업데이트 된 이벤트 ID 4688을 검토 합니다.  이전 버전에 대 한 정보를 업데이트할 **프로세스 명령줄** 로그를 가져옵니다.  이 추가 로깅 인해 뿐 아니라 wscript.exe 프로세스가 시작 되었지만 VB 스크립트를 실행 하는 데 이것은 또한 이제 볼 수 있습니다.  
  
## <a name="configuration"></a>Configuration  
이 업데이트의 영향을 확인 하려면 두 가지 정책 설정을 사용 하도록 설정 해야 합니다.  
  
### <a name="you-must-have-audit-process-creation-auditing-enabled-to-see-event-id-4688"></a>프로세스 만들기 감사 감사 이벤트 ID 4688 참조를 사용 하도록 설정 해야 합니다.  
프로세스 만들기 감사 정책을 사용 하려면 다음 그룹 정책을 편집 합니다.  
  
**정책 위치:** 컴퓨터 구성 > 정책 > Windows 설정 > 보안 설정 > 고급 감사 구성 > 자세한 추적  
  
**정책 이름:** 프로세스 만들기 감사  
  
**지원 됩니다.** Windows 7 이상  
  
**설명/도움말:**  
  
이 보안 정책 설정은 운영 체제 프로세스 (시작)를 만들 때 감사 이벤트 및 프로그램 또는 만든 사용자의 이름을 생성 하는지 여부를 결정 합니다.  
  
이러한 이벤트를 감사 하는 컴퓨터는 사용 되는 방식을 이해할 수 및 사용자 활동을 추적 합니다.  
  
이벤트 볼륨: 시스템 사용량에 따라 보통, 낮음  
  
**기본값:** 구성되지 않음  
  
### <a name="in-order-to-see-the-additions-to-event-id-4688-you-must-enable-the-new-policy-setting-include-command-line-in-process-creation-events"></a>이벤트 ID 4688의 추가 표시 하려면 새 정책 설정을 사용 해야 합니다. 명령줄 프로세스 생성 이벤트에 포함  
**테이블 SEQ 테이블 \\ \* 아랍어 19 명령 줄 프로세스 정책 설정**  
  
|정책 구성|설명|  
|------------------------|-----------|  
|**경로**|관리 Templates\System\Audit 프로세스 만들기|  
|**설정**|**명령줄 프로세스 생성 이벤트에 포함**|  
|**기본 설정**|(사용 되지 않음) 구성 되지 않음|  
|**지원 됩니다.**|?|  
|**설명**|이 정책 설정은 정보와 새 프로세스가 만들어지면 보안 감사 이벤트에 기록 됩니다 결정 합니다.<br /><br />이 설정은 프로세스 만들기 감사 정책을 사용 하는 경우에 적용 됩니다. 텍스트로 감사 프로세스 만들기 이벤트 4688의 일환으로 보안 이벤트 로그에 기록 됩니다. 모든 프로세스에 대 한 명령줄 정보를 설정 합니다.이 정책을 사용 하도록 설정 하면 "새 프로세스가 has been created," 워크스테이션 및이 서버에 정책 설정이 적용 됩니다.<br /><br />사용 하지 않도록 설정 하거나이 정책 설정을 구성 하지 않은 경우 프로세스의 명령줄 정보 프로세스 만들기 감사 이벤트에 포함 되지 않습니다.<br /><br />Default: 구성되지 않음<br /><br />참고: 이 정책 설정을 사용 하는 경우 보안 이벤트에 대 한 명령줄 인수를 성공적으로 읽을 수 읽기 액세스 권한이 있는 모든 사용자 프로세스를 만들었습니다. 명령줄 인수는 암호 또는 사용자 데이터와 같은 중요 한 개인 정보를 포함할 수 있습니다.|  
  
![명령줄 감사](media/Command-line-process-auditing/GTR_ADDS_IncludeCLISetting.gif)  
  
고급 감사 정책 구성 설정을 사용하는 경우 기본 감사 정책 설정으로 이 설정을 덮어쓰지 않았는지 확인해야 합니다.  이벤트 4719 설정을 덮어쓰여지는 경우 기록 됩니다.  
  
![명령줄 감사](media/Command-line-process-auditing/GTR_ADDS_Event4719.gif)  
  
다음 절차에서는 기본 감사 정책 설정을 적용하지 못하도록 차단하여 충돌을 방지하는 방법을 보여 줍니다.  
  
### <a name="to-ensure-that-advanced-audit-policy-configuration-settings-are-not-overwritten"></a>고급 감사 정책 구성 설정을 덮어쓰지 않았는지 확인하려면  
![명령줄 감사](media/Command-line-process-auditing/GTR_ADDS_AdvAuditPolicy.gif)  
  
1.  그룹 정책 관리 콘솔을 열으십시오  
  
2.  기본 도메인 정책에서를 마우스 오른쪽 단추로 클릭 하 고 편집을 클릭 합니다.  
  
3.  컴퓨터 구성, 정책을 두 번 클릭 하 고 Windows 설정을 두 번 클릭 합니다.  
  
4.  보안 설정을 두 번 클릭 하 고, 로컬 정책을 두 번 클릭 및 보안 옵션을 차례로 클릭 합니다.  
  
5.  감사를 두 번 클릭 합니다. Force 감사 정책 하위 범주 설정 (Windows Vista 이상) 감사 정책 범주 설정 재정의 한 다음이 정책 설정 정의 클릭 합니다.  
  
6.  사용을 클릭 하 고 확인을 클릭 합니다.  
  
## <a name="additional-resources"></a>추가 리소스  
[프로세스 만들기 감사](https://technet.microsoft.com/library/dd941613(v=WS.10).aspx)  
  
[고급 보안 감사 정책 단계별 가이드](https://technet.microsoft.com/library/dd408940(v=WS.10).aspx)  
  
[AppLocker: 질문과 대답](https://technet.microsoft.com/library/ee619725(v=ws.10).aspx)  
  
## <a name="try-this-explore-command-line-process-auditing"></a>다음과 같이 해보십시오. 명령줄 프로세스 감사 탐색  
  
1.  사용 하도록 설정 **프로세스 만들기 감사** 이벤트 고급 감사 정책 구성을 덮어쓰지 않습니다을 보장 하 고  
  
2.  관심 있는 일부 이벤트를 생성 되며 스크립트를 실행 하는 스크립트를 만듭니다.  이벤트를 확인 합니다.  단원에서 이벤트를 생성 하는 데 스크립트는 다음과 같았습니다.  
  
    ```  
    mkdir c:\systemfiles\temp\commandandcontrol\zone\fifthward  
    copy \\192.168.1.254\c$\hidden c:\systemfiles\temp\hidden\commandandcontrol\zone\fifthward  
    start C:\systemfiles\temp\hidden\commandandcontrol\zone\fifthward\ntuserrights.vbs  
    del c:\systemfiles\temp\*.* /Q  
    ```  
  
3.  명령줄 프로세스 감사를 사용 하도록 설정  
  
4.  앞으로 동일한 스크립트를 실행 하 고 이벤트를 확인  
  


