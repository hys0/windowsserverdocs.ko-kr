---
ms.assetid: ea015cbc-dea9-4c72-a9d8-d6c826d07608
title: "부록 H-로컬 관리자 계정 및 그룹 보안"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 222e6725456bb76267240467469e97c5b64fc888
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="appendix-h-securing-local-administrator-accounts-and-groups"></a>로컬 관리자 계정 및 그룹 부록 h: 보안

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012


## <a name="appendix-h-securing-local-administrator-accounts-and-groups"></a>로컬 관리자 계정 및 그룹 부록 h: 보안  
일반 지원에서 현재 Windows의 모든 버전에서 로컬 관리자 계정은 계정을 해시를 pass 및 기타 자격 증명 도용의 공격에 사용할 수 없게는 기본적으로 사용할 수 없습니다. 그러나 이전 운영 체제를 포함 하는 또는 로컬 관리자 계정을 설정 된 환경에서 이러한 계정은 사용할 수 앞에서 설명한 대로 워크스테이션과 회원 서버에 손상 전파 됩니다. 각 로컬 관리자 계정 및 그룹에 따라 단계별 지침에 설명 된 대로 확보 해야 합니다.  

보안 기본 관리자 (모음) 그룹에 고려 사항에 대 한 자세한 내용은 참조 [구현 최소 권한 관리 모델](../../../ad-ds/plan/security-best-practices/Implementing-Least-Privilege-Administrative-Models.md)합니다.  

#### <a name="controls-for-local-administrator-accounts"></a>로컬 관리자 계정에 대 한 컨트롤  
각 도메인에 숲에서 로컬 관리자 계정에 대해 다음 설정을 구성 해야 합니다.  

-   도메인 가입 시스템에서 도메인의 관리자 계정 사용을 제한 하는 Gpo 구성  
    -   다음 사용자 권리를 관리자 계정을 만들고 서버로 워크스테이션과 구성원 Ou 각 도메인에 연결 하는 하나 이상의 Gpo에서 추가 **컴퓨터 구성 보안 로컬 Settings\User 권한 할당**:  

        -   네트워크에서이 컴퓨터에 대 한 액세스 거부  

        -   로그온 일괄 작업으로 거부  

        -   로그온 서비스 거부  

        -   원격 데스크톱 서비스를 통해 로그온 거부  

#### <a name="step-by-step-instructions-to-secure-local-administrators-groups"></a>로컬 관리자가 그룹 보안에 대 한 단계별 지침  

###### <a name="configuring-gpos-to-restrict-administrator-account-on-domain-joined-systems"></a>도메인 가입 시스템 관리자 계정 제한 Gpo 구성  

1.  **서버 관리자**, 클릭 **도구**를 클릭 하 고 **그룹 정책 관리**합니다.  

2.  콘솔 트리에서 확장 <Forest>\Domains\\<Domain>, 선택한 다음 **그룹 정책 개체** (여기서 <Forest> 숲의 이름 및 <Domain> 그룹 정책 설정 도메인 이름입니다) 합니다.  

3.  콘솔 트리에서 마우스 오른쪽 단추로 클릭 **그룹 정책 개체**를 클릭 하 고 **새로**합니다.  

    ![보안 로컬 관리자 계정 및 그룹](media/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups/SAD_101.png)  

4.  에 **새 GPO** 대화 상자, 입력 ** <GPO Name> **, 클릭 하 고 **확인** (여기서 <GPO Name> 이 GPO 이름입니다).  

    ![보안 로컬 관리자 계정 및 그룹](media/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups/SAD_102.png)  

5.  세부 정보 창에서 마우스 오른쪽 단추로 클릭 ** <GPO Name> **를 클릭 하 고 **편집**합니다.  

6.  로 이동 **컴퓨터 구성 보안 로컬 정책**를 클릭 하 고 **사용자 권한 할당**합니다.  

    ![보안 로컬 관리자 계정 및 그룹](media/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups/SAD_103.png)  

7.  로컬 관리자 계정을 다음을 수행 하 여 네트워크를 통해 워크스테이션과 회원 서버에 하지 않도록 하려면 사용자 권한을 구성 합니다.  

    1.  두 번 클릭 **네트워크에서이 컴퓨터에 대 한 액세스 거부** 선택한 **이 정책 설정 정의**합니다.  

    2.  클릭 **사용자 또는 그룹 추가**로컬 관리자 계정 사용자 이름을 입력 하 고 클릭 **확인**합니다. 사용자 이름이 됩니다 **관리자**, Windows가 설치 된 경우 기본 합니다.  

        ![보안 로컬 관리자 계정 및 그룹](media/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups/SAD_104.png)  

    3.  확인을 클릭 합니다.  

        > [!IMPORTANT]  
        > 이러한 설정을 관리자 계정을 추가 하면 도메인 관리자 계정 또는 로컬 관리자 계정의 계정의 레이블을 방식으로 구성 하 고 있는지 여부를 지정할 수 있습니다. 예를 들어, 이러한 TAILSPINTOYS 도메인 관리자 계정의 권한을 거부, TAILSPINTOYS 도메인에 대 한 관리자 계정에 찾아볼 것을 추가 하는 것 TAILSPINTOYS\Administrator로 표시 됩니다. 입력 하는 경우 **관리자** 이러한 사용자 권한 설정 그룹 정책 개체 편집기에서에서 제한 됩니다 앞에 설명 된 대로, GPO 적용 되는 각 컴퓨터에서 로컬 관리자 계정을 합니다.  

8.  로컬 관리자 계정을 다음을 수행 하 여 일괄 작업으로 로그온 하지 않도록 하려면 사용자 권한을 구성 합니다.  

    1.  두 번 클릭 **일괄 작업으로 로그온 거부** 선택한 **이 정책 설정 정의**합니다.  

    2.  클릭 **사용자 또는 그룹 추가**로컬 관리자 계정 사용자 이름을 입력 하 고 클릭 **확인**합니다. 사용자 이름이 됩니다 **관리자**, Windows가 설치 된 경우 기본 합니다.  

        ![보안 로컬 관리자 계정 및 그룹](media/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups/SAD_105.png)  

    3.  클릭 **확인**합니다.  

        > [!IMPORTANT]  
        > 이러한 설정을 관리자 계정을 추가 하면 도메인 관리자 계정 또는 로컬 관리자 계정의 계정의 레이블을 방식으로 구성 하 고 있는지 여부를 지정할 수 있습니다. 예를 들어, 이러한 TAILSPINTOYS 도메인 관리자 계정의 권한을 거부, TAILSPINTOYS 도메인에 대 한 관리자 계정에 찾아볼 것을 추가 하는 것 TAILSPINTOYS\Administrator로 표시 됩니다. 입력 하는 경우 **관리자** 이러한 사용자 권한 설정 그룹 정책 개체 편집기에서에서 제한 됩니다 앞에 설명 된 대로, GPO 적용 되는 각 컴퓨터에서 로컬 관리자 계정을 합니다.  

9. 로컬 관리자 계정을 다음을 수행 하 여 서비스 로그온 하지 않도록 하려면 사용자 권한을 구성 합니다.  

    1.  두 번 클릭 **로그온 서비스 거부** 선택한 **이 정책 설정 정의**합니다.  

    2.  클릭 **사용자 또는 그룹 추가**로컬 관리자 계정 사용자 이름을 입력 하 고 클릭 **확인**합니다. 사용자 이름이 됩니다 **관리자**, Windows가 설치 된 경우 기본 합니다.  

        ![보안 로컬 관리자 계정 및 그룹](media/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups/SAD_106.png)  

    3.  클릭 **확인**합니다.  

        > [!IMPORTANT]  
        > 이러한 설정을 관리자 계정을 추가 하면 도메인 관리자 계정 또는 로컬 관리자 계정의 계정의 레이블을 방식으로 구성 하 고 있는지 여부를 지정할 수 있습니다. 예를 들어, 이러한 TAILSPINTOYS 도메인 관리자 계정의 권한을 거부, TAILSPINTOYS 도메인에 대 한 관리자 계정에 찾아볼 것을 추가 하는 것 TAILSPINTOYS\Administrator로 표시 됩니다. 입력 하는 경우 **관리자** 이러한 사용자 권한 설정 그룹 정책 개체 편집기에서에서 제한 됩니다 앞에 설명 된 대로, GPO 적용 되는 각 컴퓨터에서 로컬 관리자 계정을 합니다.  

10. 로컬 관리자 계정을 다음을 수행 하 여 원격 데스크톱 서비스를 통해 워크스테이션과 회원 서버에 액세스 하지 못하도록 사용자 권한을 구성 합니다.  

    1.  두 번 클릭 **로그온 원격 데스크톱 서비스를 통해 거부** 선택한 **이 정책 설정 정의**합니다.  

    2.  클릭 **사용자 또는 그룹 추가**로컬 관리자 계정 사용자 이름을 입력 하 고 클릭 **확인**합니다. 사용자 이름이 됩니다 **관리자**, Windows가 설치 된 경우 기본 합니다.  

        ![보안 로컬 관리자 계정 및 그룹](media/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups/SAD_107.png)  

    3.  클릭 **확인**합니다.  

        > [!IMPORTANT]  
        > 이러한 설정을 관리자 계정을 추가 하면 도메인 관리자 계정 또는 로컬 관리자 계정의 계정의 레이블을 방식으로 구성 하 고 있는지 여부를 지정할 수 있습니다. 예를 들어, 이러한 TAILSPINTOYS 도메인 관리자 계정의 권한을 거부, TAILSPINTOYS 도메인에 대 한 관리자 계정에 찾아볼 것을 추가 하는 것 TAILSPINTOYS\Administrator로 표시 됩니다. 입력 하는 경우 **관리자** 이러한 사용자 권한 설정 그룹 정책 개체 편집기에서에서 제한 됩니다 앞에 설명 된 대로, GPO 적용 되는 각 컴퓨터에서 로컬 관리자 계정을 합니다.  

11. 종료 하려면 **그룹 정책 편집기 관리**, 클릭 **파일**를 클릭 하 고 **종료**합니다.  

12. **그룹 정책 관리**, 다음을 수행 하 여 GPO 구성원 서버 및 Ou 워크스테이션을 연결 합니다.  

    1.  로 이동는 <Forest>\Domains\\<Domain> (여기서 <Forest> 숲의 이름 및 <Domain> 그룹 정책 설정 도메인 이름입니다) 합니다.  

    2.  OU GPO에 적용 되 고 클릭를 마우스 오른쪽 단추로 클릭 **기존 GPO 연결**합니다.  

        ![보안 로컬 관리자 계정 및 그룹](media/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups/SAD_108.png)  

    3.  사용자가 만든 GPO 선택 하 고 클릭 **확인**합니다.  

        ![보안 로컬 관리자 계정 및 그룹](media/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups/SAD_109.png)  

    4.  모든 일부 조직 구성 단위 워크스테이션 포함 된에 대 한 링크를 만듭니다.  

    5.  모든 일부 조직 구성 단위 구성원 서버를 포함 하는 링크를 만듭니다.  

#### <a name="verification-steps"></a>확인 단계  

##### <a name="verify-deny-access-to-this-computer-from-the-network-gpo-settings"></a>"액세스 거부가이 컴퓨터에는 네트워크에서" GPO 설정 확인  

모든 구성원이 서버 또는 (예: 점프 서버) GPO 변경 영향을 받지 않는 워크스테이션 구성원 서버 또는 워크스테이션 GPO 변경 사항을 영향을 받는 네트워크를 통해 액세스 하려고 합니다. 시스템 드라이브를 사용 하 여 지도를 시도 GPO 설정을 확인 하 고 **NET 사용** 명령 합니다.  

1.  구성원 서버 또는 GPO 변경 사항을 영향을 받지 않는 워크스테이션 로컬 로그온 합니다.  

2.  마우스를 사용 하 여 포인터를 화면 오른쪽 위로 옮겼다가 또는 오른쪽 하단 모서리에 이동 합니다. 때는 **참** 클릭 표시줄이 나타날 **검색**합니다.  

3.  **검색** 상자에 입력 **명령 프롬프트**를 마우스 오른쪽 단추로 클릭 **명령 프롬프트**, 클릭 한 다음 **관리자 권한으로 실행** 관리자 권한 명령 프롬프트를 엽니다.  

4.  를 상승 승인 하 라는 메시지가 나타나면 클릭 **예**합니다.  

    ![보안 로컬 관리자 계정 및 그룹](media/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups/SAD_110.png)  

5.  에 **명령 프롬프트** 창, 입력 **사용 net \\\<Server Name>\c$ 사용자:<Server Name>\Administrator**, 여기서 <Server Name> 구성원 서버 또는 워크스테이션 네트워크를 통해 액세스를 시도 하는 이름입니다.  

    > [!NOTE]  
    > 네트워크를 통해 액세스를 시도 하는 동일한 시스템 로컬 관리자 자격 증명 해야 합니다.  

6.  다음 스크린샷 표시 되 고 오류 메시지가 표시 됩니다.  

    ![보안 로컬 관리자 계정 및 그룹](media/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups/SAD_111.png)  

##### <a name="verify-deny-log-on-as-a-batch-job-gpo-settings"></a>"로그온 거부 일괄 작업으로" GPO 설정 확인  
모든 구성원이 서버 또는 워크스테이션 GPO 변경 영향을 로컬로 로그온 합니다.  

###### <a name="create-a-batch-file"></a>배치 파일을 만들어  

1.  마우스를 사용 하 여 포인터를 화면 오른쪽 위로 옮겼다가 또는 오른쪽 하단 모서리에 이동 합니다. 때는 **참** 클릭 표시줄이 나타날 **검색**합니다.  

2.  에 **검색** 상자에 입력 **메모장**를 클릭 하 고 **메모장**합니다.  

3.  **메모장**, 입력 **디렉터리 c:**합니다.  

4.  클릭 **파일**를 클릭 하 고 **다른 이름으로 저장**합니다.  

5.  에 **파일 이름** 상자에 입력 ** <Filename>.bat** (여기서 <Filename> 새 배치 파일 이름).  

###### <a name="schedule-a-task"></a>작업을 예약  

1.  마우스를 사용 하 여 포인터를 화면 오른쪽 위로 옮겼다가 또는 오른쪽 하단 모서리에 이동 합니다. 때는 **참** 클릭 표시줄이 나타날 **검색**합니다.  

2.  에 **검색** 상자 작업 스케줄러를 입력 하 고 클릭 **작업 스케줄러**합니다.  

    > [!NOTE]  
    > 컴퓨터에서 실행 중인 Windows 8에서는 **검색** 상자에 입력 **작업을 예약**를 클릭 하 고 **작업을 예약**합니다.  

3.  클릭 **알림**를 클릭 하 고 **작업 만들기**합니다.  

4.  **작업 만들기** 대화 상자에서 입력 ** <Task Name> ** (여기서 <Task Name> 새 작업의 이름) 합니다.  

5.  클릭는 **작업** 탭 및 클릭 **새로**합니다.  

6.  에 **알림** 필드를 클릭 **프로그램 시작**합니다.  

7.  에 **프로그램/스크립트** 필드를 클릭 **찾아보기**을 찾아에서 만든 배치 파일 선택는 **배치 파일을 만들어** 섹션을 클릭 **열기**합니다.  

8.  클릭 **확인**합니다.  

9. 클릭 하 고 **일반** 탭 합니다.  

10. 에 **보안 옵션** 필드를 클릭 **사용자 또는 그룹 변경**합니다.  

11. 로컬 관리자 계정 시스템의 이름을 입력을 클릭 **이름 확인**를 클릭 하 고 **확인**합니다.  

12. 선택 **사용자의 로그온 실행** 및 **암호를 저장 하지 않는**합니다. 작업 로컬 컴퓨터 리소스에 액세스할 수 있는 기간은 됩니다.  

13. 클릭 **확인**합니다.  

14. 작업을 실행 하 요청 하는 사용자 계정 자격 대화 상자가 표시 됩니다.  

15. 자격 증명을 입력 한 후 클릭 **확인**합니다.  

16. 다음과 비슷합니다 대화 상자가 나타나면 정상입니다.  

    ![보안 로컬 관리자 계정 및 그룹](media/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups/SAD_112.png)  

###### <a name="verify-deny-log-on-as-a-service-gpo-settings"></a>"로그온 거부 as a service" GPO 설정 확인  

1.  모든 구성원이 서버 또는 워크스테이션 GPO 변경 영향을 로컬로 로그온 합니다.  

2.  마우스를 사용 하 여 포인터를 화면 오른쪽 위로 옮겼다가 또는 오른쪽 하단 모서리에 이동 합니다. 때는 **참** 클릭 표시줄이 나타날 **검색**합니다.  

3.  에 **검색** 상자에 입력 **서비스**를 클릭 하 고 **서비스**합니다.  

4.  찾아 두 번 클릭 **인쇄 스풀러**합니다.  

5.  클릭 하 고 **로그온** 탭 합니다.  

6.  **로 로그온** 필드를 클릭 **이 계정**합니다.  

7.  클릭 **찾아보기**로컬 관리자 계정을 시스템의 입력을 클릭 **이름 확인**를 클릭 하 고 **확인**합니다.  

8.  에 **암호** 및 **암호 확인** 필드를 입력 하 여 선택한 계정의 암호를 클릭 한 **확인**합니다.  

9. 클릭 **확인** 세 번 합니다.  

10. 마우스 오른쪽 단추로 클릭 **인쇄 스풀러** 클릭 **다시 시작**합니다.  

11. 서비스를 다시 시작 하면 다음과 비슷합니다 대화 상자가 나타나면 정상입니다.  

    ![보안 로컬 관리자 계정 및 그룹](media/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups/SAD_113.png)  

###### <a name="revert-changes-to-the-printer-spooler-service"></a>되돌리기 프린터 스풀러 서비스에 대 한 변경  

1.  모든 구성원이 서버 또는 워크스테이션 GPO 변경 영향을 로컬로 로그온 합니다.  

2.  마우스를 사용 하 여 포인터를 화면 오른쪽 위로 옮겼다가 또는 오른쪽 하단 모서리에 이동 합니다. 때는 **참** 클릭 표시줄이 나타날 **검색**합니다.  

3.  에 **검색** 상자에 입력 **서비스**를 클릭 하 고 **서비스**합니다.  

4.  찾아 두 번 클릭 **인쇄 스풀러**합니다.  

5.  클릭 하 고 **로그온** 탭 합니다.  

6.  에 **로 로그온**: 필드를 **로컬 Systemaccount**를 클릭 하 고 **확인**합니다.  

###### <a name="verify-deny-log-on-through-remote-desktop-services-gpo-settings"></a>"로그온 거부 원격 데스크톱 서비스를 통해" GPO 설정 확인  

1.  마우스를 사용 하 여 포인터를 화면 오른쪽 위로 옮겼다가 또는 오른쪽 하단 모서리에 이동 합니다. 때는 **참** 클릭 표시줄이 나타날 **검색**합니다.  

2.  에 **검색** 상자에 입력 **원격 데스크톱 연결**를 클릭 하 고 **원격 데스크톱 연결**합니다.  

3.  에 **컴퓨터** 필드를 클릭 하 고, 연결 하려는 컴퓨터의 이름을 입력 **연결**합니다. (입력할 수도 있습니다 컴퓨터 이름 대신 IP 주소 합니다.)  

4.  시스템의 지역에 대 한 메시지가 표시 되 면 제공 자격 증명 **관리자** 계정 합니다.  

5.  다음과 비슷합니다 대화 상자가 나타나면 정상입니다.  

    ![보안 로컬 관리자 계정 및 그룹](media/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups/SAD_114.png)  
