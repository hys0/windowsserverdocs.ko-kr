---
ms.assetid: 11f36f2b-9981-4da0-9e7c-4eca78035f37
title: 부록 D-Active Directory의 기본 제공 관리자 계정 보안
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 3e0060e4b732fe77de4371c7b84b77da21de9e20
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80821666"
---
# <a name="appendix-d-securing-built-in-administrator-accounts-in-active-directory"></a>부록 D: Active Directory의 기본 제공 관리자 계정 보안

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012


## <a name="appendix-d-securing-built-in-administrator-accounts-in-active-directory"></a>부록 D: Active Directory의 기본 제공 관리자 계정 보안  
Active Directory의 각 도메인의 관리자 계정이 도메인의 만들기의 일부로 만들어집니다. 이 계정은 기본적으로 도메인에 있는 Domain Admins 및 Administrators 그룹의 구성원이 고, 도메인이 포리스트 루트 도메인 인 경우 계정도 Enterprise Admins 그룹의 구성원 이기도 합니다.

도메인의 관리자 계정 사용은 초기 빌드 작업 및 재해 복구 시나리오에 대해서만 예약 해야 합니다. 다른 계정을 사용할 수 없는 경우 관리자 계정을 사용 하 여 복구에 영향을 미칠 수 있도록 하려면 포리스트의 모든 도메인에서 관리자 계정의 기본 멤버 자격을 변경 하면 안 됩니다. 대신, 다음 섹션에 설명 된 대로 포리스트의 각 도메인에서 관리자 계정을 보호 하 고 다음에 나오는 단계별 지침에 자세히 설명 합니다. 

> [!NOTE]
> 이 가이드에서는 계정을 사용 하지 않도록 설정 하는 것이 좋습니다. 이는 포리스트 복구 백서에서 기본 관리자 계정을 사용 하기 때문에 제거 되었습니다. 그 이유는 글로벌 카탈로그 서버 없이 로그온 할 수 있는 유일한 계정입니다.


#### <a name="controls-for-built-in-administrator-accounts"></a>기본 제공 관리자 계정에 대 한 컨트롤  
포리스트의 각 도메인에 기본 제공 관리자 계정이 있는 경우 다음 설정을 구성 해야 합니다.  

-   계정이 **중요 하 고** 계정에 대 한 위임 플래그를 설정할 수 없습니다.  

-   계정에 대 **한 대화형 로그온 플래그에 스마트 카드 필요를** 사용 하도록 설정 합니다.  

-   도메인에 가입 된 시스템에서 관리자 계정의 사용을 제한 하도록 Gpo를 구성 합니다.  

    -   사용자가 만들고 각 도메인의 워크스테이션 및 구성원 서버 Ou에 연결 하는 하나 이상의 Gpo에서 각 도메인의 관리자 계정을 **컴퓨터 Configuration\Policies\Windows 설정 \ 로컬 정책 \ 사용자 권한 할당**의 다음 사용자 권한에 추가 합니다.  

        -   네트워크에서 이 컴퓨터 액세스 거부  

        -   일괄 작업으로 로그온 거부  

        -   서비스로 로그온 거부  

        -   원격 데스크톱 서비스를 통한 로그온 거부  

> [!NOTE]  
> 이 설정에 계정을 추가 하는 경우 로컬 관리자 계정 또는 도메인 관리자 계정을 구성할 지 여부를 지정 해야 합니다. 예를 들어 이러한 거부 권한에 NWTRADERS 도메인의 관리자 계정을 추가 하려면 계정을 NWTRADERS\Administrator로 입력 하거나 NWTRADERS 도메인에 대 한 관리자 계정으로 이동 해야 합니다. 그룹 정책 개체 편집기의 이러한 사용자 권한 설정에 "관리자"를 입력 하는 경우 GPO가 적용 되는 각 컴퓨터에서 로컬 관리자 계정을 제한 합니다.
>   
> 구성원 서버 및 워크스테이션의 로컬 관리자 계정 도메인 기반 관리자 계정으로 같은 방식으로 제한 하는 것이 좋습니다. 따라서 일반적으로 추가 해야 포리스트의 각 도메인에 대 한 관리자 계정 및 로컬 컴퓨터에 대 한 관리자 계정을 이러한 사용자 권한 설정 합니다. 다음 스크린 샷에서 로컬 관리자 계정 및 도메인의 관리자 계정에서 이러한 계정에 필요 하지 않습니다는 로그온을 수행을 차단 하도록 이러한 사용자 권한 구성 예를 보여줍니다.  


![기본 제공 관리자 계정 보안](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_23.gif)  

-   도메인 컨트롤러에서 관리자 계정을 제한 하도록 Gpo 구성  
    -   포리스트의 각 도메인에서 기본 도메인 컨트롤러 GPO 또는 도메인 컨트롤러 OU에 연결 된 정책을 수정 하 여 각 도메인의 관리자 계정을 **Computer Configuration\Policies\Windows 설정 \ 로컬 정책 \ 사용자 권한 할당**의 다음 사용자 권한에 추가 해야 합니다.   
        -   네트워크에서 이 컴퓨터 액세스 거부  

        -   일괄 작업으로 로그온 거부  

        -   서비스로 로그온 거부  

        -   원격 데스크톱 서비스를 통한 로그온 거부  

> [!NOTE]  
> 이러한 설정은 도메인의 기본 제공 관리자 계정을 도메인 컨트롤러에 연결 하는 데 사용할 수 없도록 합니다. 계정 (사용 하도록 설정 된 경우)은 도메인 컨트롤러에 로컬로 로그온 할 수 있습니다. 이 계정은 해야만 사용 하도록 설정 되어 재해 복구 시나리오에서 사용을 하기 때문에 하나 이상의 도메인 컨트롤러에 대 한 실제 액세스 된 사용할 수는 또는 도메인 컨트롤러를 원격으로 액세스할 수 있는 권한이 있는 다른 계정을 사용할 수 있도록으로 예상 됩니다.  

-   관리자 계정의 감사 구성  

    각 도메인의 관리자 계정 보안을 한 옵션을 비활성화 하는 경우 계정에 대 한 변경 내용을 모니터링할 감사를 구성 해야 합니다. 계정을 사용 하는 경우 암호를 다시 설정 하거나 계정에 대 한 다른 수정 작업을 수행 하면 조직의 인시던트 대응 팀 외에도 Active Directory 관리를 담당 하는 사용자 또는 팀에 게 경고를 전송 해야 합니다.  

#### <a name="step-by-step-instructions-to-secure-built-in-administrator-accounts-in-active-directory"></a>Active Directory에서 기본 제공 관리자 계정을 보호 하는 단계별 지침  

1.  **서버 관리자**에서 **도구**를 클릭 하 **Active Directory 사용자 및 컴퓨터**를 클릭 합니다.  

2.  위임을 활용 하 여 다른 시스템에서 계정의 자격 증명을 사용 하는 공격을 방지 하려면 다음 단계를 수행 합니다.  

    1.  **관리자** 계정을 마우스 오른쪽 단추로 클릭 하 고 **속성**을 클릭 합니다.  

    2.  클릭 하 고 **계정** 탭 합니다.  

    3.  **계정 옵션**에서 다음 스크린샷에 표시 된 것 처럼 **계정이 민감하여 위임할 수 없음** 플래그를 선택 하 고 **확인**을 클릭 합니다.  

        ![기본 제공 관리자 계정 보안](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_24.gif)  

3.  계정에 대 **한 대화형 로그온 플래그에 스마트 카드 필요** 를 사용 하도록 설정 하려면 다음 단계를 수행 합니다.  

    1.  **관리자** 계정을 마우스 오른쪽 단추로 클릭 하 고 **속성**을 선택 합니다.  

    2.  클릭 하 고 **계정** 탭 합니다.  

    3.  **계정** 옵션에서 다음 스크린샷에 표시 된 것 처럼 **대화형 로그온에 스마트 카드 필요** 플래그를 선택 하 고 **확인**을 클릭 합니다.  

        ![기본 제공 관리자 계정 보안](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_25.gif) 

##### <a name="configuring-gpos-to-restrict-administrator-accounts-at-the-domain-level"></a>도메인 수준에서 관리자 계정을 제한 하도록 Gpo 구성  

> [!WARNING]  
> 이 GPO는 재해 복구 시나리오 에서도 기본 제공 관리자 계정을 사용할 수 없게 만들 수 있으므로 도메인 수준에서 연결 해서는 안 됩니다.  

1.  **서버 관리자**에서 **도구**를 클릭 하 **그룹 정책 관리**를 클릭 합니다.  

2.  콘솔 트리에서 <Forest>\Domains\\<Domain>를 확장 한 다음 **개체를 그룹 정책** 합니다. 여기서 <Forest>는 포리스트의 이름이 고 <Domain>은 그룹 정책를 만들려는 도메인의 이름입니다.  

3.  콘솔 트리에서 **그룹 정책 개체**를 마우스 오른쪽 단추로 클릭 하 고 **새로 만들기**를 클릭 합니다.  

    ![기본 제공 관리자 계정 보안](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_27.gif)  

4.  **새 gpo** 대화 상자에서 <GPO Name>를 입력 하 고 **확인** 을 클릭 합니다. 여기서 <GPO Name>은 다음 스크린샷에 표시 된 것과 같습니다.  

    ![기본 제공 관리자 계정 보안](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_28.gif)  

5.  세부 정보 창에서 <GPO Name>을 마우스 오른쪽 단추로 클릭 하 고 **편집**을 클릭 합니다.  

6.  **Computer Configuration\Policies\Windows 설정 \ 로컬 정책**으로 이동 하 고 **사용자 권한 할당**을 클릭 합니다.  

    ![기본 제공 관리자 계정 보안](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_29.gif)  

7.  다음을 수행 하 여 관리자 계정이 네트워크를 통해 구성원 서버 및 워크스테이션에 액세스 하지 못하도록 사용자 권한을 구성 합니다.  

    1.  **네트워크에서이 컴퓨터 액세스 거부** 를 두 번 클릭 하 고 **다음 정책 설정 정의**를 선택 합니다.  

    2.  **사용자 또는 그룹 추가** 를 클릭 하 고 **찾아보기**를 클릭 합니다.  

    3.  **관리자**를 입력 하 고 **이름 확인**을 클릭 한 다음 **확인**을 클릭 합니다. 다음 스크린샷에 표시 된 것 처럼 계정이 <DomainName>\Username 형식으로 표시 되는지 확인 합니다.  

        ![기본 제공 관리자 계정 보안](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_30.gif)  

    4.  **확인**을 클릭 하 고 다시 **확인** 을 클릭 합니다.  

8.  다음을 수행 하 여 관리자 계정이 일괄 작업으로 로그온 하지 못하도록 사용자 권한을 구성 합니다.  

    1.  **일괄 작업으로 로그온 거부** 를 두 번 클릭 하 고 **다음 정책 설정 정의**를 선택 합니다.  

    2.  **사용자 또는 그룹 추가** 를 클릭 하 고 **찾아보기**를 클릭 합니다.  

    3.  **관리자**를 입력 하 고 **이름 확인**을 클릭 한 다음 **확인**을 클릭 합니다. 다음 스크린샷에 표시 된 것 처럼 계정이 <DomainName>\Username 형식으로 표시 되는지 확인 합니다.  

        ![기본 제공 관리자 계정 보안](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_31.gif)  

    4.  **확인**을 클릭 하 고 다시 **확인** 을 클릭 합니다.  

9. 다음을 수행 하 여 관리자 계정이 서비스로 로그온 하지 못하도록 사용자 권한을 구성 합니다.  

    1.  **서비스로 로그온 거부** 를 두 번 클릭 하 고 **다음 정책 설정 정의**를 선택 합니다.  

    2.  **사용자 또는 그룹 추가** 를 클릭 하 고 **찾아보기**를 클릭 합니다.  

    3.  **관리자**를 입력 하 고 **이름 확인**을 클릭 한 다음 **확인**을 클릭 합니다. 다음 스크린샷에 표시 된 것 처럼 계정이 <DomainName>\Username 형식으로 표시 되는지 확인 합니다.  

        ![기본 제공 관리자 계정 보안](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_32.gif)  

    4.  **확인**을 클릭 하 고 다시 **확인** 을 클릭 합니다.  

10. 다음을 수행 하 여 BA 계정이 원격 데스크톱 서비스 통해 구성원 서버 및 워크스테이션에 액세스 하지 못하도록 사용자 권한을 구성 합니다.  

    1.  **원격 데스크톱 서비스를 통한 로그온 거부** 를 두 번 클릭 하 고 **다음 정책 설정 정의**를 선택 합니다.  

    2.  **사용자 또는 그룹 추가** 를 클릭 하 고 **찾아보기**를 클릭 합니다.  

    3.  **관리자**를 입력 하 고 **이름 확인**을 클릭 한 다음 **확인**을 클릭 합니다. 다음 스크린샷에 표시 된 것 처럼 계정이 <DomainName>\Username 형식으로 표시 되는지 확인 합니다.  

        ![기본 제공 관리자 계정 보안](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_33.gif)  

    4.  **확인**을 클릭 하 고 다시 **확인** 을 클릭 합니다.  

11. **그룹 정책 관리 편집기**종료 하려면 **파일**을 클릭 한 다음 **끝내기**를 클릭 합니다.  

12. **그룹 정책 관리**에서 다음을 수행 하 여 GPO를 구성원 서버 및 워크스테이션 ou에 연결 합니다.  

    1.  <Forest>\Domains\\<Domain>으로 이동 합니다. 여기서 <Forest>는 포리스트의 이름이 고 <Domain>는 그룹 정책를 설정 하려는 도메인의 이름입니다.  

    2.  GPO가 적용 될 OU를 마우스 오른쪽 단추로 클릭 하 고 **기존 Gpo 연결**을 클릭 합니다.  

        ![기본 제공 관리자 계정 보안](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_34.gif)  

    3.  만든 GPO를 선택 하 고 **확인을**클릭 합니다.  

        ![기본 제공 관리자 계정 보안](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_35.gif)  

    4.  워크스테이션을 포함 하는 다른 모든 Ou에 대 한 링크를 만듭니다.  

    5.  구성원 서버가 포함 된 다른 모든 Ou에 대 한 링크를 만듭니다.  

> [!IMPORTANT]  
> 이러한 설정에 관리자 계정을 추가 하는 경우 계정에 레이블을 지정 하는 방법으로 로컬 관리자 계정 또는 도메인 관리자 계정을 구성할 지 여부를 지정 합니다. 예를 들어 이러한 거부 권한에 명인 도메인의 관리자 계정을 추가 하려면 TAILSPINTOYS\Administrator.로 표시 되는 명인 도메인에 대 한 관리자 계정을 찾습니다. 그룹 정책 개체 편집기의 이러한 사용자 권한 설정에 "관리자"를 입력 하는 경우 앞에서 설명한 대로 GPO가 적용 되는 각 컴퓨터에서 로컬 관리자 계정을 제한 합니다.  

#### <a name="verification-steps"></a>확인 단계  
여기에 설명 된 확인 단계는 Windows 8 및 Windows Server 2012에만 적용 됩니다.  

##### <a name="verify-smart-card-is-required-for-interactive-logon-account-option"></a>"대화형 로그온에 스마트 카드 필요" 계정 옵션 확인  

1.  GPO 변경의 영향을 받는 모든 구성원 서버 또는 워크스테이션에서 도메인의 기본 제공 관리자 계정을 사용 하 여 도메인에 대화형으로 로그온을 시도 합니다. 로그온을 시도한 후 다음과 유사한 대화 상자가 나타납니다.  

![기본 제공 관리자 계정 보안](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_36.gif)  

##### <a name="verify-account-is-disabled-account-option"></a>"계정이 사용 하지 않도록 설정 됨" 계정 옵션 확인  

1.  GPO 변경의 영향을 받는 모든 구성원 서버 또는 워크스테이션에서 도메인의 기본 제공 관리자 계정을 사용 하 여 도메인에 대화형으로 로그온을 시도 합니다. 로그온을 시도한 후 다음과 유사한 대화 상자가 나타납니다.  

![기본 제공 관리자 계정 보안](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_37.gif)  

##### <a name="verify-deny-access-to-this-computer-from-the-network-gpo-settings"></a>"네트워크에서이 컴퓨터 액세스 거부" GPO 설정 확인  
GPO 변경의 영향을 받지 않는 구성원 서버 또는 워크스테이션 (예: 점프 서버)에서 GPO 변경의 영향을 받는 네트워크를 통해 구성원 서버 또는 워크스테이션에 대 한 액세스를 시도 합니다. GPO 설정을 확인 하려면 다음 단계를 수행 하 여 **NET use** 명령을 사용 하 여 시스템 드라이브를 매핑하려고 시도 합니다.  

1.  도메인의 기본 제공 관리자 계정을 사용 하 여 도메인에 로그온 합니다.  

2.  마우스를 사용 하 여 포인터를 화면의 오른쪽 위 또는 오른쪽 아래 모서리로 이동 합니다. **참 메뉴** 막대가 표시 되 면 **검색**을 클릭 합니다.  

3.  **검색** 상자에서 **명령 프롬프트**를 입력 하 고 **명령 프롬프트**를 마우스 오른쪽 단추로 클릭 한 다음 **관리자 권한으로 실행** 을 클릭 하 여 관리자 권한 명령 프롬프트를 엽니다.  

4.  권한 상승을 승인를 묻는 메시지가 나타나면 클릭 **예**합니다.  

    ![기본 제공 관리자 계정 보안](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_38.gif)  

5.  **명령 프롬프트** 창에서 **net use \\\\\<서버 이름\>\c $** 를 입력 합니다. 여기서 \<server name\>은 네트워크를 통해 액세스 하려는 구성원 서버 또는 워크스테이션의 이름입니다.  

6.  다음 스크린샷에서는 표시 되어야 하는 오류 메시지를 보여 줍니다.  

    ![기본 제공 관리자 계정 보안](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_39.gif)  

##### <a name="verify-deny-log-on-as-a-batch-job-gpo-settings"></a>"일괄 작업으로 로그온 거부" GPO 설정 확인  

GPO 변경의 영향을 받는 모든 구성원 서버 또는 워크스테이션에서 로컬로 로그온 합니다.  

###### <a name="create-a-batch-file"></a>배치 파일 만들기  

1.  마우스를 사용 하 여 포인터를 화면의 오른쪽 위 또는 오른쪽 아래 모서리로 이동 합니다. **참 메뉴** 막대가 표시 되 면 **검색**을 클릭 합니다.  

2.  **검색** 상자에 **notepad**를 입력 하 고 **notepad**를 클릭 합니다.  

3.  **메모장**에서 **dir c:** 를 입력 합니다.  

4.  **파일** 을 클릭 하 고 다른 **이름으로 저장**을 클릭 합니다.  

5.  **파일 이름** 필드에 **<Filename>** 을 입력 합니다. 여기서 <Filename>은 새 배치 파일의 이름입니다.  

###### <a name="schedule-a-task"></a>작업 예약  

1.  마우스를 사용 하 여 포인터를 화면의 오른쪽 위 또는 오른쪽 아래 모서리로 이동 합니다. **참 메뉴** 막대가 표시 되 면 **검색**을 클릭 합니다.  

2.  **검색** 상자에 **작업 스케줄러**를 입력 하 고 **작업 스케줄러**를 클릭 합니다.  

    > [!NOTE]  
    > Windows 8을 실행 하는 컴퓨터의 검색 상자에 **일정 작업**을 입력 하 고 **작업 예약**을 클릭 합니다.  

3.  **작업 스케줄러**에서 **작업**을 클릭 하 고 **작업 만들기**를 클릭 합니다.  

4.  **작업 만들기** 대화 상자에서 **<Task Name>** 를 입력 합니다. 여기서 **<Task Name>** 은 새 작업의 이름입니다.  

5.  **작업** 탭을 클릭 하 고 **새로 만들기**를 클릭 합니다.  

6.  **작업:** 에서 **프로그램 시작**을 선택 합니다.  

7.  **프로그램/스크립트:** 에서 **찾아보기**를 클릭 하 고 "배치 파일 만들기" 섹션에서 만든 배치 파일을 찾아서 선택한 다음 **열기**를 클릭 합니다.  

8.  **확인**을 클릭합니다.  

9. **일반** 탭을 클릭합니다.  

10. **보안** 옵션에서 **사용자 또는 그룹 변경**을 클릭 합니다.  

11. 도메인 수준에서 BA 계정의 이름을 입력 하 고 **이름 확인**을 클릭 한 다음 **확인**을 클릭 합니다.  

12. **사용자의 로그온 여부에 관계 없이 실행** 을 선택 하 고 **암호를 저장 하지**않습니다. 작업은 로컬 컴퓨터 리소스에만 액세스할 수 있습니다.  

13. **확인**을 클릭합니다.  

14. 작업을 실행 하기 위한 사용자 계정 자격 증명을 요청 하는 대화 상자가 나타납니다.  

15. 자격 증명을 입력 한 후 **확인**을 클릭 합니다.  

16. 다음과 유사한 대화 상자가 표시 됩니다.  

    ![기본 제공 관리자 계정 보안](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_40.gif)  

##### <a name="verify-deny-log-on-as-a-service-gpo-settings"></a>"서비스로 로그온 거부" GPO 설정 확인  

1.  GPO 변경의 영향을 받는 모든 구성원 서버 또는 워크스테이션에서 로컬로 로그온 합니다.  

2.  마우스를 사용 하 여 포인터를 화면의 오른쪽 위 또는 오른쪽 아래 모서리로 이동 합니다. **참 메뉴** 막대가 표시 되 면 **검색**을 클릭 합니다.  

3.  **검색** 상자에 **서비스**를 입력 하 고 **서비스**를 클릭 합니다.  

4.  **인쇄 스풀러**를 찾아 두 번 클릭 합니다.  

5.  **로그온** 탭을 클릭합니다.  

6.  **다음으로 로그온:** 에서 **이 계정을**선택 합니다.  

7.  **찾아보기**를 클릭 하 고 도메인 수준에서 BA 계정 이름을 입력 하 고 **이름 확인**을 클릭 한 다음 **확인**을 클릭 합니다.  

8.  **암호:** 및 **암호 확인:** 에서 관리자 계정의 암호를 입력 하 고 **확인**을 클릭 합니다.  

9. **확인을** 세 번 더 클릭 합니다.  

10. **인쇄 스풀러 서비스** 를 마우스 오른쪽 단추로 클릭 하 고 **다시 시작**을 선택 합니다.  

11. 서비스가 다시 시작 되 면 다음과 유사한 대화 상자가 나타납니다.  

    ![기본 제공 관리자 계정 보안](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_41.gif)  

##### <a name="revert-changes-to-the-printer-spooler-service"></a>프린터 스풀러 서비스로 변경 내용 되돌리기  

1.  GPO 변경의 영향을 받는 모든 구성원 서버 또는 워크스테이션에서 로컬로 로그온 합니다.  

2.  마우스를 사용 하 여 포인터를 화면의 오른쪽 위 또는 오른쪽 아래 모서리로 이동 합니다. **참 메뉴** 막대가 표시 되 면 **검색**을 클릭 합니다.  

3.  **검색** 상자에 **서비스**를 입력 하 고 **서비스**를 클릭 합니다.  

4.  **인쇄 스풀러**를 찾아 두 번 클릭 합니다.  

5.  **로그온** 탭을 클릭합니다.  

6.  **다음으로 로그온:** 에서 **로컬 시스템** 계정을 선택 하 고 **확인**을 클릭 합니다.  

##### <a name="verify-deny-log-on-through-remote-desktop-services-gpo-settings"></a>"원격 데스크톱 서비스를 통한 로그온 거부" GPO 설정 확인

1.  마우스를 사용 하 여 포인터를 화면의 오른쪽 위 또는 오른쪽 아래 모서리로 이동 합니다. **참 메뉴** 막대가 표시 되 면 **검색**을 클릭 합니다.  

2.  **검색** 상자에 **원격 데스크톱 연결**을 입력 하 고 **원격 데스크톱 연결**를 클릭 합니다.  

3.  **컴퓨터** 필드에 연결 하려는 컴퓨터의 이름을 입력 하 고 **연결**을 클릭 합니다. (컴퓨터 이름 대신 IP 주소를 입력할 수도 있습니다.)  

4.  메시지가 표시 되 면 도메인 수준의 BA 계정 이름에 대 한 자격 증명을 제공 합니다.  

5.  다음과 유사한 대화 상자가 표시 됩니다.  

    ![기본 제공 관리자 계정 보안](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_42.gif)  
