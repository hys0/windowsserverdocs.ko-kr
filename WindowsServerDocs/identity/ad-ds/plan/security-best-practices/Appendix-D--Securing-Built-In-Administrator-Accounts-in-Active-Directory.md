---
ms.assetid: 11f36f2b-9981-4da0-9e7c-4eca78035f37
title: "부록 D-Active Directory에 기본 제공 관리자 계정 보안"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 2878e661e1bb93fcdc3161c46b73d8e4baec76d2
ms.sourcegitcommit: 2782a80a916f8432c030af76e860a72f08481899
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/13/2018
---
# <a name="appendix-d-securing-built-in-administrator-accounts-in-active-directory"></a>부록 d: Active Directory에 기본 제공 관리자 계정 보안

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012


## <a name="appendix-d-securing-built-in-administrator-accounts-in-active-directory"></a>부록 d: Active Directory에 기본 제공 관리자 계정 보안  
각 도메인 Active Directory에 관리자 계정 만들기 도메인의의 일환으로 만들어집니다. 이 계정 기본적으로 도메인에 있는 도메인 관리 및 관리자가 그룹의 회원 이며 도메인이 숲 루트 도메인 경우 계정을 Enterprise 관리자 그룹의 회원 이기도 합니다.

도메인의 관리자 계정 사용 하 여 초기 빌드 활동 하 고 예를 들어, 장애 복구 시나리오에 대해서만 예약 해야 합니다. 관리자 계정으로 다른 계정을 사용할 수 있는 영향을 복구를 사용할 수 있도록 하려면 관리자 계정을 도메인 숲에 기본 멤버 자격 하지 변경 해야 합니다. 대신 다음 섹션에 설명 된 대로 각 도메인 숲에서 관리자 계정을 보호 고 단계별 지침에 따라는에 자세히 설명 합니다. 

> [!NOTE]
> 이 가이드 계정을 비활성화 권장 하는 데 사용 합니다. 이 숲 복구 흰색 종이으로 제거 되었습니다 기본 관리자 계정을 사용 합니다. 글로벌 카탈로그 서버를 않고도 로그온 수 있는 유일한 계정 이유가입니다.


#### <a name="controls-for-built-in-administrator-accounts"></a>기본 제공 관리자 계정에 대 한 컨트롤  
각 사용자 숲 속의 도메인에 기본 제공 된 관리자 계정에 대해 다음 설정을 구성 해야 합니다.  

-   사용 하도록 설정의 **계정은 중요 한 위임 수 없는** 계정에 대해 플래그 합니다.  

-   사용 하도록 설정의 **스마트 카드 로그온 해야 합니다는** 계정에 대해 플래그.  

-   도메인 가입 시스템에서 관리자 계정을 사용을 제한 하는 Gpo 구성 합니다.  

    -   다음 사용자 권리를 각 도메인 관리자 계정을 만들고 서버로 워크스테이션과 구성원 Ou 각 도메인에 연결 하는 하나 이상의 Gpo에서 추가 **컴퓨터 구성 보안 로컬 Settings\User 권한 할당**:  

        -   네트워크에서이 컴퓨터에 대 한 액세스 거부  

        -   로그온 일괄 작업으로 거부  

        -   로그온 서비스 거부  

        -   원격 데스크톱 서비스를 통해 로그온 거부  

> [!NOTE]  
> 이 설정에 계정을 추가 하면 도메인 관리자 계정 또는 로컬 관리자 계정을 구성 하 고 있는지 여부를 지정 해야 합니다. 예를 들어, 거부 이러한 NWTRADERS 도메인 관리자 계정을 추가 하려면 권한, NWTRADERS\Administrator, 또는 NWTRADERS 도메인에 대 한 찾아보기 관리자 계정에 계정을 입력 해야 합니다. 그룹 정책 개체 편집기 이러한 사용자 권한 설정에서 "관리자"를 입력 하면 GPO 적용 되는 각 컴퓨터에서 로컬 관리자 계정을 제한 합니다.
>   
> 관리자 계정 도메인 기반와 같은 방식으로 로컬 관리자 계정 워크스테이션과 회원 서버에 대 한 제한 하는 것이 좋습니다. 따라서 일반적으로에 추가 해야 각 도메인 숲에 대해 관리자 계정과 로컬 컴퓨터에 대해 관리자 계정 이러한 사용자 권한 설정 합니다. 다음 스크린샷 구성 이러한 사용자 권한을 로컬 관리자 계정 및 해당이 계정에 대 한 필요 하지 않습니다 로그온에서 공연을 하는 도메인의 관리자 계정을 차단 하는 예를 나타냅니다.  


![기본 제공 된 관리자 계정 보안](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_23.gif)  

-   구성 Gpo 도메인 컨트롤러에 관리자 계정이 제한 하려면  
    -   각 도메인 숲에서 기본 도메인 컨트롤러 GPO 또는 정책을에 연결 된 도메인 컨트롤러에서 다음과 같은 사용자 권한에 각 도메인 관리자 계정을 추가 하려면 OU 수정 해야 **컴퓨터 구성 보안 로컬 Settings\User 권한 할당**:   
        -   네트워크에서이 컴퓨터에 대 한 액세스 거부  

        -   로그온 일괄 작업으로 거부  

        -   로그온 서비스 거부  

        -   원격 데스크톱 서비스를 통해 로그온 거부  

> [!NOTE]  
> 관리자 계정을 기본 제공 되는 도메인을 사용 하는 경우 해당 계정에 로그온 할 수 로컬로 도메인 컨트롤러에 있지만 도메인 컨트롤러에 연결할 사용할 수 없습니다 이러한 설정을 확인 됩니다 합니다. 이 계정을 사용 하도록 설정 및만 장애 복구 시나리오에서 사용 해야, 하기 때문에 것으로 예상 됩니다 하나 이상 도메인 컨트롤러에 물리적 액세스를 사용할 수 있는지 또는 다른 계정을 도메인 컨트롤러를 원격으로 액세스 권한이 있는 사용할 수 있습니다.  

-   관리자 계정 감사 구성  

    각 도메인 관리자 계정 보호를 비활성화 하면, 하는 경우 계정에 변경 내용을 모니터링할 감사 구성 해야 합니다. 계정을 사용 하도록 설정 하거나, 암호를 다시 설정 하거나 계정에는 다른 수정 사항이, 경고 사용자 또는 조직에서 사고 응답 팀 뿐 아니라 Active directory 관리 담당 팀에 전송 됩니다.  

#### <a name="step-by-step-instructions-to-secure-built-in-administrator-accounts-in-active-directory"></a>Active Directory에 기본 제공 관리자 계정 보안에 대 한 단계별 지침  

1.  **서버 관리자**, 클릭 **도구**를 클릭 하 고 **Active Directory 사용자와 컴퓨터**합니다.  

2.  다른 시스템에 계정 자격 증명을 사용 하 여 위임을 활용 하는 공격을 방지 하려면 다음 단계를 수행 합니다.  

    1.  마우스 오른쪽 단추로 클릭는 **관리자** 클릭 하 고 계정 **속성**합니다.  

    2.  클릭 하 고 **계정** 탭 합니다.  

    3.  아래에서 **계정 옵션**선택 **계정은 중요 한 위임 수 없습니다** 클릭 한 다음 화면에 표시 된 대로 플래그를 지정 **확인**합니다.  

        ![기본 제공 된 관리자 계정 보안](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_24.gif)  

3.  사용 하도록 설정 하려면는 **스마트 카드 로그온 해야 합니다는** 계정에 대해 플래그 지정, 다음 단계를 수행 합니다.  

    1.  마우스 오른쪽 단추로 클릭는 **관리자** 선택한 계정 **속성**합니다.  

    2.  클릭 하 고 **계정** 탭 합니다.  

    3.  아래에서 **계정** 옵션을 선택 하 고 있는 **스마트 카드 로그온 해야 합니다는** 클릭 한 다음 화면에 표시 된 대로 플래그를 지정 **확인**합니다.  

        ![기본 제공 된 관리자 계정 보안](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_25.gif) 

##### <a name="configuring-gpos-to-restrict-administrator-accounts-at-the-domain-level"></a>관리자 계정을 도메인 수준 제한 Gpo 구성  

> [!WARNING]  
> 기본 제공 된 관리자 계정으로 장애 복구 경우에도 사용할 수 없는 설정 수 있는 것 하기 때문에이 GPO 도메인 수준 하지 연결 해야 합니다.  

1.  **서버 관리자**, 클릭 **도구**를 클릭 하 고 **그룹 정책 관리**합니다.  

2.  콘솔 트리에서 확장 <Forest>\Domains\\<Domain>, 다음 **그룹 정책 개체** (위치 <Forest> 숲의 이름 및 <Domain> 그룹 정책 만들려는 도메인 이름입니다) 합니다.  

3.  콘솔 트리에서 마우스 오른쪽 단추로 클릭 **그룹 정책 개체**를 클릭 하 고 **새로**합니다.  

    ![기본 제공 된 관리자 계정 보안](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_27.gif)  

4.  **새 GPO** 대화 상자에서 입력 <GPO Name>, 클릭 **확인** (여기서 <GPO Name> 이 GPO 이름입니다) 다음 화면에 표시 된 대로 합니다.  

    ![기본 제공 된 관리자 계정 보안](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_28.gif)  

5.  세부 정보 창에서 마우스 오른쪽 단추로 클릭 <GPO Name>를 클릭 하 고 **편집**합니다.  

6.  로 이동 **컴퓨터 구성 보안 로컬 정책**를 클릭 하 고 **사용자 권한 할당**합니다.  

    ![기본 제공 된 관리자 계정 보안](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_29.gif)  

7.  관리자 계정을 다음을 수행 하 여 네트워크를 통해 워크스테이션과 회원 서버에 하지 않도록 하려면 사용자 권한 구성 합니다.  

    1.  두 번 클릭 **네트워크에서이 컴퓨터에 대 한 액세스 거부** 선택한 **이 정책 설정 정의**합니다.  

    2.  클릭 **사용자 또는 그룹 추가** 클릭 **찾아보기**합니다.  

    3.  입력 **관리자**, 클릭 **이름 확인**를 클릭 하 고 **확인**합니다. 계정이 표시 되는지 확인 <DomainName>다음 화면에 표시 된 대로 \Username 형식 있습니다.  

        ![기본 제공 된 관리자 계정 보안](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_30.gif)  

    4.  클릭 **확인**, 및 **확인** 다시 합니다.  

8.  관리자 계정을 다음을 수행 하 여 일괄 작업으로 로그온 하지 않도록 하려면 사용자 권한 구성 합니다.  

    1.  두 번 클릭 **일괄 작업으로 로그온 거부** 선택한 **이 정책 설정 정의**합니다.  

    2.  클릭 **사용자 또는 그룹 추가** 클릭 **찾아보기**합니다.  

    3.  입력 **관리자**, 클릭 **이름 확인**를 클릭 하 고 **확인**합니다. 계정이 표시 되는지 확인 <DomainName>다음 화면에 표시 된 대로 \Username 형식 있습니다.  

        ![기본 제공 된 관리자 계정 보안](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_31.gif)  

    4.  클릭 **확인**, 및 **확인** 다시 합니다.  

9. 관리자 계정을 다음을 수행 하 여 서비스 로그온 하지 않도록 하려면 사용자 권한 구성 합니다.  

    1.  두 번 클릭 **로그온 서비스 거부** 선택한 **이 정책 설정 정의**합니다.  

    2.  클릭 **사용자 또는 그룹 추가** 클릭 **찾아보기**합니다.  

    3.  입력 **관리자**, 클릭 **이름 확인**를 클릭 하 고 **확인**합니다. 계정이 표시 되는지 확인 <DomainName>다음 화면에 표시 된 대로 \Username 형식 있습니다.  

        ![기본 제공 된 관리자 계정 보안](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_32.gif)  

    4.  클릭 **확인**, 및 **확인** 다시 합니다.  

10. 모음 계정 다음을 수행 하 여 원격 데스크톱 서비스를 통해 워크스테이션과 회원 서버에 액세스 하지 못하도록 사용자 권한을 구성 합니다.  

    1.  두 번 클릭 **로그온 원격 데스크톱 서비스를 통해 거부** 선택한 **이 정책 설정 정의**합니다.  

    2.  클릭 **사용자 또는 그룹 추가** 클릭 **찾아보기**합니다.  

    3.  입력 **관리자**, 클릭 **이름 확인**를 클릭 하 고 **확인**합니다. 계정이 표시 되는지 확인 <DomainName>다음 화면에 표시 된 대로 \Username 형식 있습니다.  

        ![기본 제공 된 관리자 계정 보안](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_33.gif)  

    4.  클릭 **확인**, 및 **확인** 다시 합니다.  

11. 종료 하려면 **그룹 정책 편집기 관리**, 클릭 **파일**를 클릭 하 고 **종료**합니다.  

12. **그룹 정책 관리**, 다음을 수행 하 여 GPO 구성원 서버 및 Ou 워크스테이션을 연결 합니다.  

    1.  로 이동는 <Forest>\Domains\\<Domain> (여기서 <Forest> 숲의 이름 및 <Domain> 그룹 정책 설정 도메인 이름입니다) 합니다.  

    2.  OU GPO에 적용 되 고 클릭를 마우스 오른쪽 단추로 클릭 **기존 GPO 연결**합니다.  

        ![기본 제공 된 관리자 계정 보안](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_34.gif)  

    3.  사용자가 만든 GPO 선택 하 고 클릭 **확인**합니다.  

        ![기본 제공 된 관리자 계정 보안](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_35.gif)  

    4.  모든 일부 조직 구성 단위 워크스테이션 포함 된에 대 한 링크를 만듭니다.  

    5.  모든 일부 조직 구성 단위 구성원 서버를 포함 하는 링크를 만듭니다.  

> [!IMPORTANT]  
> 이러한 설정을 관리자 계정을 추가 하면 도메인 관리자 계정 또는 로컬 관리자 계정의 계정의 레이블을 방식으로 구성 하 고 있는지 여부를 지정할 수 있습니다. 예를 들어, 이러한 TAILSPINTOYS 도메인 관리자 계정의 권한을 거부, TAILSPINTOYS 도메인에 대 한 관리자 계정에 찾아볼 것을 추가 하는 것 TAILSPINTOYS\Administrator로 표시 됩니다. 그룹 정책 개체 편집기 이러한 사용자 권한 설정에서 "관리자"를 입력 하면 앞에 설명 된 대로, GPO 적용 되는 각 컴퓨터에서 로컬 관리자 계정을 제한 합니다.  

#### <a name="verification-steps"></a>확인 단계  
여기 참조 확인 단계에 Windows 8 및 Windows Server 2012에 적용 됩니다.  

##### <a name="verify-smart-card-is-required-for-interactive-logon-account-option"></a>확인 "스마트 카드 로그온 해야 합니다"는 계정 옵션  

1.  모든 구성원이 서버 또는 워크스테이션 GPO 변경 영향을 대화형 도메인을 사용 하 여 로그온 도메인의 기본 제공 된 관리자 계정 하려고 합니다. 로그인에 사용한 후 다음과 비슷합니다 대화 상자가 나타나면 정상입니다.  

![기본 제공 된 관리자 계정 보안](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_36.gif)  

##### <a name="verify-account-is-disabled-account-option"></a>"계정이 비활성화" 확인 계정 옵션  

1.  모든 구성원이 서버 또는 워크스테이션 GPO 변경 영향을 대화형 도메인을 사용 하 여 로그온 도메인의 기본 제공 된 관리자 계정 하려고 합니다. 로그인에 사용한 후 다음과 비슷합니다 대화 상자가 나타나면 정상입니다.  

![기본 제공 된 관리자 계정 보안](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_37.gif)  

##### <a name="verify-deny-access-to-this-computer-from-the-network-gpo-settings"></a>"액세스 거부가이 컴퓨터에는 네트워크에서" GPO 설정 확인  
모든 구성원이 서버 또는 (예: 점프 서버) GPO 변경 영향을 받지 않는 워크스테이션 구성원 서버 또는 워크스테이션 GPO 변경 사항을 영향을 받는 네트워크를 통해 액세스 하려고 합니다. 시스템 드라이브를 사용 하 여 지도를 시도 GPO 설정을 확인 하 고 **NET 사용** 다음 단계를 수행 하 여 명령:  

1.  관리자 계정 기본 제공 되는 도메인을 사용 하는 도메인 로그온 합니다.  

2.  마우스를 사용 하 여 포인터를 화면 오른쪽 위로 옮겼다가 또는 오른쪽 하단 모서리에 이동 합니다. 때는 **참** 클릭 표시줄이 나타날 **검색**합니다.  

3.  **검색** 상자에 입력 **명령 프롬프트**를 마우스 오른쪽 단추로 클릭 **명령 프롬프트**, 클릭 한 다음 **관리자 권한으로 실행** 관리자 권한 명령 프롬프트를 엽니다.  

4.  를 상승 승인 하 라는 메시지가 나타나면 클릭 **예**합니다.  

    ![기본 제공 된 관리자 계정 보안](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_38.gif)  

5.  에 **명령 프롬프트** 창, 입력 **사용 net \\\<Server Name>\c$**, 여기서 <Server Name> 구성원 서버 또는 워크스테이션 네트워크를 통해 액세스 하는 이름입니다.  

6.  다음 스크린샷 표시 되 고 오류 메시지가 표시 됩니다.  

    ![기본 제공 된 관리자 계정 보안](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_39.gif)  

##### <a name="verify-deny-log-on-as-a-batch-job-gpo-settings"></a>"로그온 거부 일괄 작업으로" GPO 설정 확인  

모든 구성원이 서버 또는 워크스테이션 GPO 변경 영향을 로컬로 로그온 합니다.  

###### <a name="create-a-batch-file"></a>배치 파일을 만들어  

1.  마우스를 사용 하 여 포인터를 화면 오른쪽 위로 옮겼다가 또는 오른쪽 하단 모서리에 이동 합니다. 때는 **참** 클릭 표시줄이 나타날 **검색**합니다.  

2.  에 **검색** 상자에 입력 **메모장**를 클릭 하 고 **메모장**합니다.  

3.  **메모장**, 입력 **디렉터리 c:**합니다.  

4.  클릭 **파일** 클릭 **다른 이름으로 저장**합니다.  

5.  **파일 이름** 필드를 입력 ** <Filename>.bat** (여기서 <Filename> 새 배치 파일 이름).  

###### <a name="schedule-a-task"></a>작업을 예약  

1.  마우스를 사용 하 여 포인터를 화면 오른쪽 위로 옮겼다가 또는 오른쪽 하단 모서리에 이동 합니다. 때는 **참** 클릭 표시줄이 나타날 **검색**합니다.  

2.  에 **검색** 상자에 입력 **작업 스케줄러**를 클릭 하 고 **작업 스케줄러**합니다.  

    > [!NOTE]  
    > 검색 상자에 Windows 8을 실행 하는 컴퓨터에서 입력 **작업을 예약**를 클릭 하 고 **작업을 예약**합니다.  

3.  **작업 스케줄러**, 클릭 **알림**를 클릭 하 고 **작업 만들기**합니다.  

4.  **작업 만들기** 대화 상자에서 입력 ** <Task Name> ** (여기서 ** <Task Name> ** 새 작업의 이름) 합니다.  

5.  클릭는 **작업** 탭 및 클릭 **새로**합니다.  

6.  아래에서 **알림:**선택 **프로그램 시작**합니다.  

7.  아래에서 **프로그램/스크립트:**, 클릭 **찾아보기**, 찾아 "배치 파일 만들기" 섹션에서 만든 배치 파일 선택한 클릭 **열기**합니다.  

8.  클릭 **확인**합니다.  

9. 클릭 하 고 **일반** 탭 합니다.  

10. 아래에서 **보안** 옵션을 클릭 **사용자 또는 그룹 변경**합니다.  

11. 도메인 수준 클릭에서 모음 계정의 이름을 입력 **이름 확인**를 클릭 하 고 **확인**합니다.  

12. 선택 **사용자의 로그온 실행** 및 **암호를 저장 하지 않는**합니다. 작업 로컬 컴퓨터 리소스에 액세스할 수 있는 기간은 됩니다.  

13. 클릭 **확인**합니다.  

14. 작업을 실행 하 요청 하는 사용자 계정 자격 대화 상자가 표시 됩니다.  

15. 자격 증명을 입력 한 후 클릭 **확인**합니다.  

16. 다음과 비슷합니다 대화 상자가 나타나면 정상입니다.  

    ![기본 제공 된 관리자 계정 보안](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_40.gif)  

##### <a name="verify-deny-log-on-as-a-service-gpo-settings"></a>"로그온 거부 as a service" GPO 설정 확인  

1.  모든 구성원이 서버 또는 워크스테이션 GPO 변경 영향을 로컬로 로그온 합니다.  

2.  마우스를 사용 하 여 포인터를 화면 오른쪽 위로 옮겼다가 또는 오른쪽 하단 모서리에 이동 합니다. 때는 **참** 클릭 표시줄이 나타날 **검색**합니다.  

3.  에 **검색** 상자에 입력 **서비스**를 클릭 하 고 **서비스**합니다.  

4.  찾아 두 번 클릭 **인쇄 스풀러**합니다.  

5.  클릭 하 고 **로그온** 탭 합니다.  

6.  아래에서 **로 로그온:**선택 **이 계정**합니다.  

7.  클릭 **찾아보기**도메인 수준 모음 계정의 이름을 입력을 클릭 **이름 확인**를 클릭 하 고 **확인**합니다.  

8.  아래에서 **암호:** 및 **암호 확인:**관리자 계정 암호를 입력 하 고 클릭 **확인**합니다.  

9. 클릭 **확인** 세 번 합니다.  

10. 마우스 오른쪽 단추로 클릭는 **인쇄 스풀러 서비스** 선택한 **다시 시작**합니다.  

11. 서비스를 다시 시작 하면 다음과 비슷합니다 대화 상자가 나타나면 정상입니다.  

    ![기본 제공 된 관리자 계정 보안](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_41.gif)  

##### <a name="revert-changes-to-the-printer-spooler-service"></a>되돌리기 프린터 스풀러 서비스에 대 한 변경  

1.  모든 구성원이 서버 또는 워크스테이션 GPO 변경 영향을 로컬로 로그온 합니다.  

2.  마우스를 사용 하 여 포인터를 화면 오른쪽 위로 옮겼다가 또는 오른쪽 하단 모서리에 이동 합니다. 때는 **참** 클릭 표시줄이 나타날 **검색**합니다.  

3.  에 **검색** 상자에 입력 **서비스**를 클릭 하 고 **서비스**합니다.  

4.  찾아 두 번 클릭 **인쇄 스풀러**합니다.  

5.  클릭 하 고 **로그온** 탭 합니다.  

6.  아래에서 **로 로그온:**는 **로컬 시스템** 계정, 클릭 한 **확인**합니다.  

##### <a name="verify-deny-log-on-through-remote-desktop-services-gpo-settings"></a>"로그온 거부 원격 데스크톱 서비스를 통해" GPO 설정 확인

1.  마우스를 사용 하 여 포인터를 화면 오른쪽 위로 옮겼다가 또는 오른쪽 하단 모서리에 이동 합니다. 때는 **참** 클릭 표시줄이 나타날 **검색**합니다.  

2.  에 **검색** 상자에 입력 **원격 데스크톱 연결**를 클릭 하 고 **원격 데스크톱 연결**합니다.  

3.  에 **컴퓨터** 필드를 클릭 하 고, 연결 하려는 컴퓨터의 이름을 입력 **연결**합니다. (입력할 수도 있습니다 컴퓨터 이름 대신 IP 주소 합니다.)  

4.  메시지가 표시 되 면 도메인 수준 모음 계정 이름에 대 한 자격 증명을 제공 합니다.  

5.  다음과 비슷합니다 대화 상자가 나타나면 정상입니다.  

    ![기본 제공 된 관리자 계정 보안](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_42.gif)  
