---
title: 사용자 프로필 이벤트를 사용 하 여 문제 해결
description: 로드 문제를 해결 하는 방법 및 이벤트 및 추적 로그를 사용 하 여 언로드 사용자 프로필입니다.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 04/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 6099dac7d77e37b761785b4f58b6106472e5ba1e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59827954"
---
# <a name="troubleshoot-user-profiles-with-events"></a>사용자 프로필 이벤트를 사용 하 여 문제 해결

>적용 대상: Windows 10, Windows 8, Windows 8.1, Windows Server 2012, Windows Server 2012 R2 및 Windows Server 2016 합니다.

이 항목에서는 이벤트 및 추적 로그를 사용 하 여 로드 하는 문제를 해결 하는 방법 및 언로드 사용자 프로필을 설명 합니다. 다음 섹션에서는 사용자 프로필 정보를 기록 하는 세 가지 이벤트 로그를 사용 하는 방법에 설명 합니다.

## <a name="step-1-checking-events-in-the-application-log"></a>1단계: 응용 프로그램 로그에 이벤트를 확인 하는 중

로드 및 언로드 이벤트 뷰어를 사용 하 여 모든 경고 및 오류 이벤트는 응용 프로그램에서 사용자 프로필 서비스 레코드 로그를 검사 하려면 사용자 프로필 (로밍 사용자 프로필 포함)를 사용 하 여 문제 해결의 첫 번째 단계입니다.

응용 프로그램 로그에서 사용자 프로필 서비스 이벤트를 보는 방법에는 다음과 같습니다.

1. 이벤트 뷰어를 시작 합니다. 이 위해 엽니다 **Control Panel**를 선택 **시스템 및 보안**를 선택한 후는 **관리 도구** 섹션에서 **이벤트로그를볼**. 이벤트 뷰어 창이 열립니다.
2. 콘솔 트리에서 먼저 이동할 **Windows 로그**, 한 다음 **응용 프로그램**합니다.
3. 작업 창에서 선택 **현재 로그 필터링**합니다. 현재 로그 필터링 대화 상자가 열립니다.
4. 에 **이벤트 원본** 상자에서를 **사용자 프로필 서비스** 확인란을 선택한 후 **확인**합니다.
5. 이벤트, 오류 이벤트에 특히 주의 해 서 목록을 검토 합니다.
6. 주목할 만한 이벤트를 찾으면 추가 정보 및 문제 해결 절차를 표시 하는 이벤트 로그 온라인 도움말 링크를 선택 합니다.
7. 추가 문제 해결을 수행 하려면 주목할 만한 이벤트의 시간과 날짜를 확인 및 살펴본 작업 로그 (설명한 2 단계에서에서) 오류 또는 경고 이벤트의 시간 User Profile Service가 수행 하는 방법에 대 한 세부 정보를 보려면.

>[!NOTE]
>무시 해도 User Profile Service 이벤트가 1530 "Windows 검색 레지스트리 파일을 다른 응용 프로그램 및 서비스에서 사용 하 여 계속 합니다."

## <a name="step-2-view-the-operational-log-for-the-user-profile-service"></a>2단계: 사용자 프로필 서비스에 대 한 작업 로그 보기

단독으로 응용 프로그램 로그를 사용 하 여 문제를 해결할 수 없으면 작업 로그에서 사용자 프로필 서비스 이벤트를 보려면 다음 절차를 따르십시오. 이 로그에는 프로필 로드 위치를 파악 하거나 문제가 발생 하는 프로세스를 언로드할 수 있습니다 및 서비스의 내부 작업 중 일부를 보여 줍니다.

Windows 응용 프로그램 로그 및 사용자 프로필 서비스 작업 로그 모두 모든 Windows 설치에 기본적으로 활성화 됩니다.

사용자 프로필 서비스에 대 한 작업 로그를 보는 방법에는 다음과 같습니다.

1. 이동할 이벤트 뷰어 콘솔 트리에서 **Applications and Services Logs**, 한 다음 **Microsoft**, 한 다음 **Windows**, 다음 **User Profile Service**, 차례로 **Operational**합니다.
2. 응용 프로그램 로그에서 기록한 오류 또는 경고 이벤트의 시간대에 발생 한 이벤트를 검사 합니다.

## <a name="step-3-enable-and-view-analytic-and-debug-logs"></a>3단계: 사용 하도록 설정 하 고 보려면 분석 및 디버그 로그

자세한 운영 로그를 제공 하는 것을 요구할 경우 분석을 사용 하도록 설정 하 고 영향을 받는 컴퓨터의 로그를 디버그할 수 있습니다. 이 로깅 수준을 훨씬 더 자세히 설명 되어 및 제외 하려고 할 때 문제를 해결 하 고 수 없게 됩니다.

분석 보기 및 디버그 로그를 사용 하도록 설정 하는 방법을 다음과 같습니다.

1. 에 **작업** 이벤트 뷰어를 선택 창 **보기**를 선택한 후 **분석 및 디버그 로그 표시**.
2. 이동할 **Applications and Services Logs**, 한 다음 **Microsoft**, 다음 **Windows**, 다음 **User Profile Service**, 차례로  **진단**합니다.
3. 선택 **로그 사용** 선택한 후 **예**합니다. 이렇게 하면 로깅을 시작 하는 진단 로그를 수 있습니다.
4. 더 자세한 정보를 필요로 하는 경우 참조 [4 단계: 만들기 및 추적을 디코딩](#step-4:-creating-and-decoding-a-trace) 추적 로그를 만드는 방법에 대 한 자세한 내용은 합니다.
5. 로 이동 하는 문제 해결 작업을 완료 하는 경우는 **진단** 로그 선택 **로그 사용 안 함**를 선택 **뷰** 의 선택을 취소 합니다는 **표시 분석 및 디버그 로그** 숨기기 분석 및 디버그 로깅을 사용 하려면 확인란을 선택 합니다.

## <a name="step-4-creating-and-decoding-a-trace"></a>4단계: 만들기 및 추적을 디코딩

이벤트를 사용 하 여 문제를 해결할 수 없으면 문제를 재현 하는 동안 추적 로그 (ETL 파일)를 만들 수 있으며 그런 다음 Microsoft 기호 서버에서 공용 기호를 사용 하 여 디코딩. 추적 로그는 User Profile Service을 수행 하 고 오류가 발생 한 위치를 파악 하는 데 도움이 하는 방법에 대 한 매우 구체적인 정보를 제공 합니다.

ETL 추적을 사용 하는 경우 가장 좋은 방법은 먼저 가능한 가장 작은 로그를 수집 하는 것입니다. 로그 디코드 되 면 오류에 대 한 로그를 검색 합니다.

만들기 및 사용자 프로필 서비스에 대 한 추적을 디코드 하는 방법은 다음과 같습니다.

1. 여기서 사용자는 문제가 로컬 Administrators 그룹의 구성원 인 계정을 사용 하는 컴퓨터에 로그온 합니다.
2. 관리자 권한 명령 프롬프트에서 다음 명령을 입력 위치 *\<경로\>* 로컬 폴더에 이전에 만든 예를 들어 c: 경로\\로그:
        
    ```PowerShell
    logman create trace -n RUP -o <Path>\RUP.etl -ets
    logman update RUP -p {eb7428f5-ab1f-4322-a4cc-1f1a9b2c5e98} 0x7FFFFFFF 0x7 -ets
    ```
3. 시작 화면에서 사용자 이름을 선택 하 고 선택한 **계정 전환**, 관리자를 기록할 필요가 있으므로 주의 해야 합니다. 원격 데스크톱을 사용 하는 경우에 사용자 세션을 설정 하려면 관리자 세션을 닫습니다.
4. 문제를 재현 합니다. 문제를 재현 하는 절차는 일반적으로 사용자를 로그인 문제를 발생 하는 사용자 또는 둘 다로 로그온 합니다.
5. 문제를 재현 한 후 로그온 로컬 관리자로 다시 합니다.
6. 관리자 권한 명령 프롬프트에서 ETL 파일에 로그를 저장 하려면 다음 명령을 실행 합니다.
  
    ```PowerShell
    logman stop -n RUP -ets
    ```
7. 현재 디렉터리에 알기 쉬운 파일로 ETL 파일을 내보내려면 다음 명령을 입력 (가능성이 홈 폴더 또는 % WINDIR %\\System32 폴더).
    
    ```PowerShell
    Tracerpt <path>\RUP.etl
    ```
8. 엽니다는 **Summary.txt** 파일 및 **Dumpfile.xml** 파일 (열 수 있습니다 보다 쉽게 로그의 전체 세부 정보를 보려면 Microsoft Excel에서). 포함 하는 이벤트를 검색할 **실패** 또는 **실패**; 포함 된 줄을 안전 하 게 무시할 수 있습니다는 **알 수 없는** 이벤트 이름입니다.

## <a name="more-information"></a>자세한 정보

* [로밍 사용자 프로필 배포](deploy-roaming-user-profiles.md)