---
ms.assetid: 11f36f2b-9981-4da0-9e7c-4eca78035f37
title: 부록 D-Active Directory에서 기본 제공 관리자 계정 보안
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 51e503f55ee0fca1f1a53339de555fd213c69296
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59870684"
---
# <a name="appendix-d-securing-built-in-administrator-accounts-in-active-directory"></a>부록 D: Active Directory에서 기본 제공 관리자 계정 보안

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012


## <a name="appendix-d-securing-built-in-administrator-accounts-in-active-directory"></a>부록 D: Active Directory에서 기본 제공 관리자 계정 보안  
Active Directory의 각 도메인의 관리자 계정이 도메인의 만들기의 일부로 만들어집니다. 이 계정이 기본적으로 도메인의 Domain Admins 및 Administrators 그룹의 구성원 및 도메인 포리스트 루트 도메인 경우 계정이 Enterprise Admins 그룹의 구성원 이기도 합니다.

초기 빌드 활동 및 필요에 따라 재해 복구 시나리오에 대해서만 사용 하 여 도메인의 관리자 계정의 예약 되어야 합니다. 다른 계정을 사용할 수 있는 복구를 적용할 관리자 계정을 사용할 수 있도록 되도록 하지는 포리스트의 모든 도메인 관리자 계정의 기본 멤버 자격을 변경 해야 합니다. 대신, 다음 섹션에 설명 된 대로 포리스트의 각 도메인 관리자 계정을 보호 해야 하 고 이어지는 단계별 지침에 자세히 설명 합니다. 

> [!NOTE]
> 권장 계정 사용 하지 않도록 설정 하는 데이 가이드입니다. 이 포리스트 복구 백서로 제거 된 기본 관리자 계정을 사용 합니다. 이유는 글로벌 카탈로그 서버 없이 로그온을 허용 하는 유일한 계정입니다.


#### <a name="controls-for-built-in-administrator-accounts"></a>기본 제공 관리자 계정에 대 한 컨트롤  
포리스트의 각 도메인에 기본 제공 관리자 계정에 대 한 다음 설정을 구성 해야 합니다.  

-   사용 하도록 설정 합니다 **계정이 민감하여 위임할 수 없음** 계정에 대 한 플래그입니다.  

-   사용 하도록 설정 합니다 **대화형 로그온에 스마트 카드는** 계정에 대 한 플래그입니다.  

-   도메인에 가입 된 시스템에서 관리자 계정의 사용을 제한 하는 Gpo를 구성 합니다.  

    -   만들고 각 도메인의 Ou 워크스테이션 및 구성원 서버에 연결 하는 하나 이상의 Gpo에서 추가할 각 도메인의 관리자 계정에 다음과 같은 사용자 권한이 **컴퓨터 구성 설정 \ 보안 설정 \ 로컬 정책 \ 사용자 권한 할당**:  

        -   네트워크에서 이 컴퓨터 액세스 거부  

        -   일괄 작업으로 로그온 거부  

        -   서비스로 로그온 거부  

        -   원격 데스크톱 서비스를 통한 로그온 거부  

> [!NOTE]  
> 이 설정은 계정에 추가 하면 여부를 구성 하는 로컬 관리자 계정 또는 도메인 관리자 계정을 지정 해야 합니다. 예를 들어 이러한 NWTRADERS 도메인의 관리자 계정 거부를 추가 하려면 권한, 계정 NWTRADERS\Administrator, 또는 NWTRADERS 도메인에 대 한 관리자 계정에 검색으로 입력 해야 합니다. 이러한 사용자 권한 설정을 그룹 정책 개체 편집기에서 "관리자"를 입력 하는 경우 GPO를 적용할 각 컴퓨터의 로컬 관리자 계정을 제한 합니다.
>   
> 구성원 서버 및 워크스테이션의 로컬 관리자 계정 도메인 기반 관리자 계정으로 같은 방식으로 제한 하는 것이 좋습니다. 따라서 일반적으로 추가 해야 포리스트의 각 도메인에 대 한 관리자 계정 및 로컬 컴퓨터에 대 한 관리자 계정을 이러한 사용자 권한 설정 합니다. 다음 스크린 샷에서 로컬 관리자 계정 및 도메인의 관리자 계정에서 이러한 계정에 필요 하지 않습니다는 로그온을 수행을 차단 하도록 이러한 사용자 권한 구성 예를 보여줍니다.  


![기본 제공 관리자 계정 보안](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_23.gif)  

-   도메인 컨트롤러에서 관리자 계정 제한 하는 Gpo를 구성 합니다.  
    -   각 도메인의 관리자 계정에 다음과 같은 사용자 권한이에 추가할 OU 수정 해야 하는 도메인 컨트롤러에 연결 포리스트의 각 도메인에 기본 도메인 컨트롤러 GPO 또는 정책을 **컴퓨터 구성 \ 정책 설정 \ 보안 설정 \ 로컬 정책 \ 사용자 권한 할당**:   
        -   네트워크에서 이 컴퓨터 액세스 거부  

        -   일괄 작업으로 로그온 거부  

        -   서비스로 로그온 거부  

        -   원격 데스크톱 서비스를 통한 로그온 거부  

> [!NOTE]  
> 이러한 설정은 기본 제공 관리자 계정 도메인의 도메인 컨트롤러를 사용 하도록 설정 하는 경우 계정에서 로컬로 로그온 할 수 있지만 도메인 컨트롤러에 연결할 사용할 수 없습니다 확인 됩니다. 이 계정은 해야만 사용 하도록 설정 되어 재해 복구 시나리오에서 사용을 하기 때문에 하나 이상의 도메인 컨트롤러에 대 한 실제 액세스 된 사용할 수는 또는 도메인 컨트롤러를 원격으로 액세스할 수 있는 권한이 있는 다른 계정을 사용할 수 있도록으로 예상 됩니다.  

-   관리자 계정 감사 구성  

    각 도메인의 관리자 계정 보안을 한 옵션을 비활성화 하는 경우 계정에 대 한 변경 내용을 모니터링할 감사를 구성 해야 합니다. 계정이 활성화 되어, 암호를 재설정 또는 계정에 모든 수정 내용이 경고 사용자 또는 조직의 사고 대응 팀 외에도 Active Directory의 관리를 담당 하는 팀에 보내야 합니다.  

#### <a name="step-by-step-instructions-to-secure-built-in-administrator-accounts-in-active-directory"></a>Active Directory에서 기본 제공 관리자 계정을 보호 하기 위한 단계별 지침  

1.  **서버 관리자**, 클릭 **도구**를 클릭 하 고 **Active Directory Users and Computers**합니다.  

2.  다른 시스템에서 계정의 자격 증명을 사용 하 여 위임을 활용 하는 공격을 방지 하려면 다음 단계를 수행 합니다.  

    1.  마우스 오른쪽 단추로 클릭 합니다 **관리자** 계정 및 클릭 **속성**합니다.  

    2.  클릭 하 고 **계정** 탭 합니다.  

    3.  아래 **계정 옵션**를 선택 **계정이 민감하여 위임할 수 없음** 다음 스크린샷에 표시 된 대로 플래그를 클릭 **확인**합니다.  

        ![기본 제공 관리자 계정 보안](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_24.gif)  

3.  사용 하도록 설정 합니다 **대화형 로그온에 스마트 카드는** 계정 플래그, 다음 단계를 수행:  

    1.  마우스 오른쪽 단추로 클릭 합니다 **관리자** 선택한 계정 **속성**합니다.  

    2.  클릭 하 고 **계정** 탭 합니다.  

    3.  아래 **계정** 옵션을 선택 합니다 **대화형 로그온에 스마트 카드 필요** 다음 스크린샷에 표시 된 대로 플래그를 클릭 **확인**합니다.  

        ![기본 제공 관리자 계정 보안](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_25.gif) 

##### <a name="configuring-gpos-to-restrict-administrator-accounts-at-the-domain-level"></a>도메인 수준에서 관리자 계정 제한 하는 Gpo를 구성 합니다.  

> [!WARNING]  
> 이 GPO 해야 있으므로 내장 된 Administrator 계정을 재해 복구 시나리오에도 사용할 수 없는 도메인 수준에서 연결 되지 않습니다.  

1.  **서버 관리자**, 클릭 **도구**를 클릭 하 고 **그룹 정책 관리**합니다.  

2.  콘솔 트리에서 <Forest>\Domains\\<Domain>를 차례로 **그룹 정책 개체** (여기서 <Forest> 포리스트의 이름 및 <Domain> 하려는 도메인의 이름 그룹 정책 만들기).  

3.  콘솔 트리에서 마우스 오른쪽 단추로 클릭 **그룹 정책 개체**, 클릭 **새로 만들기**합니다.  

    ![기본 제공 관리자 계정 보안](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_27.gif)  

4.  에 **새 GPO** 대화 상자에서 <GPO Name>, 클릭 **확인** (여기서 <GPO Name> 이 GPO의 이름입니다) 다음 스크린샷에 표시 된 대로 합니다.  

    ![기본 제공 관리자 계정 보안](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_28.gif)  

5.  세부 정보 창에서 마우스 오른쪽 단추로 클릭 <GPO Name>, 클릭 **편집**합니다.  

6.  이동할 **컴퓨터 구성 \ 정책 \ 로컬 정책**, 클릭 **사용자 권한 할당**합니다.  

    ![기본 제공 관리자 계정 보안](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_29.gif)  

7.  관리자 계정에서 다음을 수행 하 여 네트워크를 통해 멤버 서버 및 워크스테이션에 방지 하기 위해 사용자 권한을 구성 합니다.  

    1.  두 번 클릭 **네트워크에서이 컴퓨터 액세스 거부** 선택한 **이 정책 설정 정의**합니다.  

    2.  클릭 **사용자 또는 그룹 추가** 누릅니다 **찾아보기**합니다.  

    3.  형식 **관리자**, 클릭 **이름 확인**를 클릭 하 고 **확인**합니다. 계정에 표시 되는지 확인 <DomainName>다음 스크린샷에 표시 된 대로 \Username 형식입니다.  

        ![기본 제공 관리자 계정 보안](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_30.gif)  

    4.  클릭 **확인**, 및 **확인** 다시 합니다.  

8.  관리자 계정은 다음을 수행 하 여 일괄 작업으로 로그온 하지 못하도록 사용자 권한을 구성 합니다.  

    1.  두 번 클릭 **일괄 작업으로 로그온 거부** 선택한 **이 정책 설정 정의**합니다.  

    2.  클릭 **사용자 또는 그룹 추가** 누릅니다 **찾아보기**합니다.  

    3.  형식 **관리자**, 클릭 **이름 확인**를 클릭 하 고 **확인**합니다. 계정에 표시 되는지 확인 <DomainName>다음 스크린샷에 표시 된 대로 \Username 형식입니다.  

        ![기본 제공 관리자 계정 보안](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_31.gif)  

    4.  클릭 **확인**, 및 **확인** 다시 합니다.  

9. 관리자 계정은 다음을 수행 하 여 서비스로 로그온 하지 못하도록 사용자 권한을 구성 합니다.  

    1.  두 번 클릭 **서비스로 로그온 거부** 선택한 **이 정책 설정 정의**합니다.  

    2.  클릭 **사용자 또는 그룹 추가** 누릅니다 **찾아보기**합니다.  

    3.  형식 **관리자**, 클릭 **이름 확인**를 클릭 하 고 **확인**합니다. 계정에 표시 되는지 확인 <DomainName>다음 스크린샷에 표시 된 대로 \Username 형식입니다.  

        ![기본 제공 관리자 계정 보안](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_32.gif)  

    4.  클릭 **확인**, 및 **확인** 다시 합니다.  

10. BA 계정 다음을 수행 하 여 구성원 서버 및 워크스테이션을 통해 원격 데스크톱 서비스에 액세스 하지 못하도록 방지 하기 위해 사용자 권한을 구성 합니다.  

    1.  두 번 클릭 **원격 데스크톱 서비스를 통한 로그온 거부** 선택한 **이 정책 설정 정의**합니다.  

    2.  클릭 **사용자 또는 그룹 추가** 누릅니다 **찾아보기**합니다.  

    3.  형식 **관리자**, 클릭 **이름 확인**를 클릭 하 고 **확인**합니다. 계정에 표시 되는지 확인 <DomainName>다음 스크린샷에 표시 된 대로 \Username 형식입니다.  

        ![기본 제공 관리자 계정 보안](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_33.gif)  

    4.  클릭 **확인**, 및 **확인** 다시 합니다.  

11. 끝내려면 **그룹 정책 관리 편집기**, 클릭 **파일**, 클릭 **종료**합니다.  

12. **그룹 정책 관리**, 다음을 수행 하 여 Ou 워크스테이션 및 구성원 서버에 GPO을 연결 합니다.  

    1.  로 이동 합니다 <Forest>\Domains\\ <Domain> (여기서 <Forest> 포리스트의 이름 및 <Domain> 그룹 정책 설정 하려는 도메인의 이름입니다).  

    2.  GPO에 적용 됩니다을 클릭 하는 OU를 마우스 오른쪽 단추로 클릭 **기존 GPO 연결**합니다.  

        ![기본 제공 관리자 계정 보안](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_34.gif)  

    3.  사용자가 만든 GPO를 선택 하 고 클릭 **확인**합니다.  

        ![기본 제공 관리자 계정 보안](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_35.gif)  

    4.  워크스테이션을 포함 하는 다른 모든 Ou에 대 한 링크를 만듭니다.  

    5.  구성원 서버가 포함 된 다른 모든 Ou에 대 한 링크를 만듭니다.  

> [!IMPORTANT]  
> 이러한 설정에 관리자 계정에 추가 하면 로컬 관리자 계정 또는 도메인 관리자 계정을 계정 레이블을 지정 하는 방법으로 구성 하 고 있는지 여부를 지정할 수 있습니다. 예를 들어 이러한 명인 도메인의 관리자 계정 거부 권한 명인 도메인에 대 한 관리자 계정으로 이동 하는 추가 하려면 TAILSPINTOYS\Administrator로 표시 됩니다는 합니다. 이러한 사용자 권한 설정을 그룹 정책 개체 편집기에서 "관리자"를 입력 하는 경우 앞에서 설명한 대로, GPO 적용 되는 각 컴퓨터의 로컬 관리자 계정을 제한 합니다.  

#### <a name="verification-steps"></a>확인 단계  
여기에 설명 된 확인 단계에서는 Windows 8 및 Windows Server 2012에 따라 다릅니다.  

##### <a name="verify-smart-card-is-required-for-interactive-logon-account-option"></a>"스마트 카드는 대화형 로그온에 필요한" 확인 계정 옵션  

1.  구성원 서버 또는 워크스테이션 GPO 변경의 영향을 대화형으로 로그온 하려면 도메인에 도메인의 기본 제공 관리자 계정을 사용 하 여 시도 합니다. 로그온을 시도한 후에 다음과 유사한 대화 상자가 나타납니다.  

![기본 제공 관리자 계정 보안](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_36.gif)  

##### <a name="verify-account-is-disabled-account-option"></a>"계정 사용 안 함" 확인 계정 옵션  

1.  구성원 서버 또는 워크스테이션 GPO 변경의 영향을 대화형으로 로그온 하려면 도메인에 도메인의 기본 제공 관리자 계정을 사용 하 여 시도 합니다. 로그온을 시도한 후에 다음과 유사한 대화 상자가 나타납니다.  

![기본 제공 관리자 계정 보안](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_37.gif)  

##### <a name="verify-deny-access-to-this-computer-from-the-network-gpo-settings"></a>액세스 거부 "이이 컴퓨터에 네트워크에서" GPO 설정을 확인 합니다.  
구성원 서버 또는 워크스테이션 (예: 점프 서버) GPO 변경 내용의 영향을 받지 않는 구성원 서버 또는 워크스테이션 GPO 변경이 영향을 받는 네트워크를 통해 액세스 하려고 합니다. 시스템 드라이브를 사용 하 여 매핑할 시도 GPO 설정을 확인 하는 **NET USE** 다음 단계를 수행 하 여 명령:  

1.  도메인의 기본 제공 관리자 계정을 사용 하 여 도메인에 로그온 합니다.  

2.  마우스를 사용 하 여 화면 오른쪽 상단 또는 오른쪽 아래 모퉁이에 포인터를 이동 합니다. 경우는 **참 메뉴** 표시줄에 표시 되 면 클릭 **검색**합니다.  

3.  에 **검색** 상자에 입력 **명령 프롬프트**를 마우스 오른쪽 단추로 클릭 **명령 프롬프트**를 클릭 하 고 **관리자 권한으로 실행** 열려면 관리자 권한 명령 프롬프트입니다.  

4.  권한 상승을 승인를 묻는 메시지가 나타나면 클릭 **예**합니다.  

    ![기본 제공 관리자 계정 보안](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_38.gif)  

5.  에 **명령 프롬프트** 창, 형식 **사용 하 여 net \\ \\ \<서버 이름\>\c$** 여기서 \<서버 이름을\> 는 구성원 서버 또는 네트워크를 통해 액세스 하려고 하는 워크스테이션의 이름입니다.  

6.  다음 스크린 샷에서 표시 되는 오류 메시지를 표시 합니다.  

    ![기본 제공 관리자 계정 보안](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_39.gif)  

##### <a name="verify-deny-log-on-as-a-batch-job-gpo-settings"></a>"로그온 거부 일괄 작업으로" GPO 설정을 확인 합니다.  

구성원 서버 또는 GPO 변경의 영향을 받는 워크스테이션에서 로컬로 로그온 합니다.  

###### <a name="create-a-batch-file"></a>배치 파일을 만듭니다  

1.  마우스를 사용 하 여 화면 오른쪽 상단 또는 오른쪽 아래 모퉁이에 포인터를 이동 합니다. 경우는 **참 메뉴** 표시줄에 표시 되 면 클릭 **검색**합니다.  

2.  에 **검색** 상자에 입력 **메모장**를 클릭 하 고 **메모장**합니다.  

3.  **메모장**, 형식 **dir c:** 합니다.  

4.  클릭 **파일** 누릅니다 **다른 이름으로 저장**합니다.  

5.  에 **Filename** 필드에 입력  **<Filename>.bat** (여기서 <Filename> 새 일괄 처리 파일의 이름입니다).  

###### <a name="schedule-a-task"></a>작업 예약  

1.  마우스를 사용 하 여 화면 오른쪽 상단 또는 오른쪽 아래 모퉁이에 포인터를 이동 합니다. 경우는 **참 메뉴** 표시줄에 표시 되 면 클릭 **검색**합니다.  

2.  에 **검색** 상자에 입력 **작업 스케줄러**를 클릭 하 고 **작업 스케줄러**합니다.  

    > [!NOTE]  
    > 검색 상자에 Windows 8을 실행 하는 컴퓨터에서 입력 **작업 일정**, 클릭 **작업을 예약**합니다.  

3.  **작업 스케줄러**, 클릭 **동작**를 클릭 하 고 **작업 만들기**합니다.  

4.  에 **작업 만들기** 대화 상자에서 **<Task Name>** (여기서 **<Task Name>** 새 작업의 이름입니다).  

5.  클릭 합니다 **동작** 탭을 클릭 **새로 만들기**합니다.  

6.  아래 **동작:** 를 선택 **프로그램을 시작할**합니다.  

7.  아래 **프로그램/스크립트:**, 클릭 **찾아보기**, "일괄 처리 파일 만들기" 섹션에서 만든 배치 파일을 찾아서 클릭 **열기**합니다.  

8.  **확인**을 클릭합니다.  

9. **일반** 탭을 클릭합니다.  

10. 아래 **Security** 옵션을 클릭 **사용자 또는 그룹 변경**합니다.  

11. 도메인 수준 클릭 BA 계정의 이름을 입력 **이름 확인**, 클릭 **확인**합니다.  

12. 선택 **사용자의 로그온 여부 실행** 하 고 **암호를 저장 하지 않는**합니다. 작업만 로컬 컴퓨터 리소스에 액세스할을 수 있습니다.  

13. **확인**을 클릭합니다.  

14. 요청 사용자 계정 작업을 실행 하려면 자격 증명 대화 상자가 표시 됩니다.  

15. 자격 증명을 입력 한 후 클릭 **확인**합니다.  

16. 다음과 유사한 대화 상자가 표시 됩니다.  

    ![기본 제공 관리자 계정 보안](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_40.gif)  

##### <a name="verify-deny-log-on-as-a-service-gpo-settings"></a>GPO 설정을 "로그온 거부 as a service"를 확인 합니다.  

1.  구성원 서버 또는 GPO 변경의 영향을 받는 워크스테이션에서 로컬로 로그온 합니다.  

2.  마우스를 사용 하 여 화면 오른쪽 상단 또는 오른쪽 아래 모퉁이에 포인터를 이동 합니다. 경우는 **참 메뉴** 표시줄에 표시 되 면 클릭 **검색**합니다.  

3.  에 **검색** 상자에 입력 **services**, 클릭 **서비스**합니다.  

4.  찾아 두 번 클릭 **인쇄 스풀러**합니다.  

5.  **로그온** 탭을 클릭합니다.  

6.  아래 **계정으로 로그온:** 를 선택 **이 계정은**합니다.  

7.  클릭 **찾아보기**, 도메인 수준에서 BA 계정의 이름을 입력, 클릭 **이름 확인**를 클릭 하 고 **확인**합니다.  

8.  아래 **암호:** 하 고 **암호 확인:** 관리자 계정의 암호를 입력 하 고 클릭 **확인**합니다.  

9. 클릭 **확인** 3 회 더 합니다.  

10. 마우스 오른쪽 단추로 클릭 합니다 **인쇄 스풀러 서비스가** 선택한 **다시 시작**합니다.  

11. 서비스를 다시 시작할 때 다음과 유사한 대화 상자가 표시 됩니다.  

    ![기본 제공 관리자 계정 보안](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_41.gif)  

##### <a name="revert-changes-to-the-printer-spooler-service"></a>프린터 스풀러 서비스에 대 한 변경 내용 되돌리기  

1.  구성원 서버 또는 GPO 변경의 영향을 받는 워크스테이션에서 로컬로 로그온 합니다.  

2.  마우스를 사용 하 여 화면 오른쪽 상단 또는 오른쪽 아래 모퉁이에 포인터를 이동 합니다. 경우는 **참 메뉴** 표시줄에 표시 되 면 클릭 **검색**합니다.  

3.  에 **검색** 상자에 입력 **services**, 클릭 **서비스**합니다.  

4.  찾아 두 번 클릭 **인쇄 스풀러**합니다.  

5.  **로그온** 탭을 클릭합니다.  

6.  아래 **계정으로 로그온:** 를 선택 합니다 **로컬 시스템** 를 고려 하 고 클릭 **확인**.  

##### <a name="verify-deny-log-on-through-remote-desktop-services-gpo-settings"></a>GPO 설정 "에서 원격 데스크톱 서비스를 통한 로그온을 거부"를 확인 합니다.

1.  마우스를 사용 하 여 화면 오른쪽 상단 또는 오른쪽 아래 모퉁이에 포인터를 이동 합니다. 경우는 **참 메뉴** 표시줄에 표시 되 면 클릭 **검색**합니다.  

2.  에 **검색** 상자에 입력 **원격 데스크톱 연결**를 클릭 하 고 **원격 데스크톱 연결**합니다.  

3.  에 **컴퓨터** 필드에 연결 하 고 클릭 하려는 컴퓨터의 이름을 입력 합니다 **Connect**합니다. (입력할 수도 있습니다 컴퓨터 이름 대신 IP 주소입니다.)  

4.  대화 상자가 나타나면 도메인 수준에서 BA 계정의 이름에 대 한 자격 증명을 제공 합니다.  

5.  다음과 유사한 대화 상자가 표시 됩니다.  

    ![기본 제공 관리자 계정 보안](media/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory/SAD_42.gif)  
