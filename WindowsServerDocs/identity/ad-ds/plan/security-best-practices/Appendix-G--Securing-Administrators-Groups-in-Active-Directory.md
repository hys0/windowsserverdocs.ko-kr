---
ms.assetid: 4baefbd3-038f-44c0-85ba-f24e9722b757
title: 부록 G-Active Directory에서 관리자 그룹 보안
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: cdea04e211b1873ff51c4bc3dc9ff24e746ead69
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408649"
---
# <a name="appendix-g-securing-administrators-groups-in-active-directory"></a>부록 G: Active Directory에서 Administrators 그룹 보안

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012


## <a name="appendix-g-securing-administrators-groups-in-active-directory"></a>부록 G: Active Directory에서 Administrators 그룹 보안  
EA (Enterprise Admins) 및 DA (Domain Admins) 그룹의 경우와 마찬가지로 기본 제공 관리자 (BA) 그룹의 멤버 자격은 빌드 또는 재해 복구 시나리오 에서만 필요 합니다. [부록 D: 보안 기본 제공 관리자 계정 Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory.md)의 설명에 따라 보안이 설정 된 경우 도메인에 대 한 기본 제공 관리자 계정을 제외 하 고 Administrators 그룹에는 일상적인 사용자 계정이 없어야 합니다.  

관리자는 기본적으로 대부분의 각 도메인의 AD DS 개체의 소유자입니다. 이 그룹의 멤버 자격은 소유권 또는 개체의 소유권을 획득 하는 기능이 필요한 빌드 또는 재해 복구 시나리오에 필요할 수 있습니다. 또한 DAs 및 EAs에는 다양 한 해당 권한 및 관리자 그룹의 해당 기본 멤버 자격을 통해 권한을 상속합니다. Active Directory의 권한 있는 그룹에 대 한 기본 그룹 중첩은 수정할 수 없으며, 각 도메인의 관리자 그룹은 다음에 나오는 단계별 지침에 설명 된 대로 보안을 설정 해야 합니다.  

포리스트의 각 도메인에 있는 관리자 그룹의 경우:  

1.  [부록 D: 보안 기본 제공 관리자 계정 Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory.md)의 설명에 따라 보안이 설정 된 경우 도메인에 대 한 기본 제공 관리자 계정을 제외 하 고 Administrators 그룹에서 모든 구성원을 제거 합니다.  

2.  각 도메인의 구성원 서버 및 워크스테이션을 포함 하는 Ou에 연결 된 Gpo에서는 **컴퓨터 Configuration\Policies\Windows 설정 \ 사용자 권한 할당**의 다음 사용자 권한에 BA 그룹을 추가 해야 합니다.  

    -   네트워크에서 이 컴퓨터 액세스 거부  

    -   일괄 작업으로 로그온 거부  

    -   서비스로 로그온 거부  

3.  포리스트의 각 도메인에 있는 도메인 컨트롤러 OU에서 Administrators 그룹에는 다음 사용자 권한이 부여 되어야 합니다.  

    -   네트워크에서 이 컴퓨터 액세스  

    -   로컬 로그온 허용  

    -   원격 데스크톱 서비스를 통한 로그온 허용  

4.  감사 관리자 그룹의 구성원 또는 속성을 수정한 경우 경고를 보내도록 구성 되어야 합니다.  

#### <a name="step-by-step-instructions-for-removing-all-members-from-the-administrators-group"></a>관리자 그룹에서 모든 구성원을 제거 하는 방법에 대 한 단계별 지침  

1.  **서버 관리자**에서 **도구**를 클릭 하 **Active Directory 사용자 및 컴퓨터**를 클릭 합니다.  

2.  관리자 그룹에서 모든 구성원을 제거 하려면 다음 단계를 수행 합니다.  

    1.  **관리자** 그룹을 두 번 클릭 하 고 **구성원** 탭을 클릭 합니다.  

        ![보안 관리 그룹](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_79.gif)  

    2.  그룹의 구성원을 선택 하 고 **제거**, **예**를 차례로 클릭 한 다음 **확인**을 클릭 합니다.  

3.  관리자 그룹의 모든 구성원이 제거 될 때까지 2 단계를 반복 합니다.  

#### <a name="step-by-step-instructions-to-secure-administrators-groups-in-active-directory"></a>Active Directory에서 관리자 그룹을 보호 하는 단계별 지침  

1.  **서버 관리자**에서 **도구**를 클릭 하 **그룹 정책 관리**를 클릭 합니다.  

2.  콘솔 트리에서 &lt;포리스트&gt;\Domains\\&lt;도메인&gt;을 확장 한 다음 **개체를 그룹 정책** 합니다. 여기서 &lt;포리스트&gt;는 포리스트의 이름이 고 &lt;도메인&gt;는 그룹 정책를 설정 하려는 도메인의 이름입니다.  

3.  콘솔 트리에서 **그룹 정책 개체**를 마우스 오른쪽 단추로 클릭 하 고 **새로 만들기**를 클릭 합니다.  

    ![보안 관리 그룹](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_80.gif)  

4.  **새 gpo** 대화 상자에서 <GPO Name>를 입력 하 고 **확인** 을 클릭 합니다. 여기서 *gpo 이름* 은이 GPO의 이름입니다.  

    ![보안 관리 그룹](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_81.gif)  

5.  세부 정보 창에서 **<GPO Name>** 을 마우스 오른쪽 단추로 클릭 하 고 **편집**을 클릭 합니다.  

6.  **Computer Configuration\Policies\Windows 설정 \ 로컬 정책**으로 이동 하 고 **사용자 권한 할당**을 클릭 합니다.  

    ![보안 관리 그룹](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_82.gif)  

7.  다음을 수행 하 여 Administrators 그룹의 구성원이 네트워크를 통해 구성원 서버 및 워크스테이션에 액세스 하지 못하도록 사용자 권한을 구성 합니다.  

    1.  **네트워크에서이 컴퓨터 액세스 거부** 를 두 번 클릭 하 고 **다음 정책 설정 정의**를 선택 합니다.  

    2.  **사용자 또는 그룹 추가** 를 클릭 하 고 **찾아보기**를 클릭 합니다.  

    3.  **관리자**를 입력 하 고 **이름 확인**을 클릭 한 다음 **확인**을 클릭 합니다.  

        ![보안 관리 그룹](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_83.gif)  

    4.  **확인**을 클릭 하 고 다시 **확인** 을 클릭 합니다.  

8.  다음을 수행 하 여 Administrators 그룹의 멤버가 일괄 작업으로 로그온 하지 못하도록 사용자 권한을 구성 합니다.  

    1.  **일괄 작업으로 로그온 거부** 를 두 번 클릭 하 고 **다음 정책 설정 정의**를 선택 합니다.  

    2.  **사용자 또는 그룹 추가** 를 클릭 하 고 **찾아보기**를 클릭 합니다.  

    3.  **관리자**를 입력 하 고 **이름 확인**을 클릭 한 다음 **확인**을 클릭 합니다.  

        ![보안 관리 그룹](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_84.gif)  

    4.  **확인**을 클릭 하 고 다시 **확인** 을 클릭 합니다.  

9. 관리자 그룹의 구성원이 다음을 수행 하 여 서비스로 로그온 하지 못하도록 사용자 권한을 구성 합니다.  

    1.  **서비스로 로그온 거부** 를 두 번 클릭 하 고 **다음 정책 설정 정의**를 선택 합니다.  

    2.  **사용자 또는 그룹 추가** 를 클릭 하 고 **찾아보기**를 클릭 합니다.  

    3.  **관리자**를 입력 하 고 **이름 확인**을 클릭 한 다음 **확인**을 클릭 합니다.  

        ![보안 관리 그룹](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_85.gif)  

    4.  **확인**을 클릭 하 고 다시 **확인** 을 클릭 합니다.  

10. **그룹 정책 관리 편집기**종료 하려면 **파일**을 클릭 한 다음 **끝내기**를 클릭 합니다.  

11. **그룹 정책 관리**에서 다음을 수행 하 여 GPO를 구성원 서버 및 워크스테이션 ou에 연결 합니다.  

    1.  &lt;포리스트&gt;> \Domains\\&lt;도메인&gt;로 이동 합니다. 여기서 &lt;포리스트&gt;는 포리스트의 이름이 고 &lt;도메인&gt;는 그룹 정책를 설정 하려는 도메인의 이름입니다.  

    2.  GPO가 적용 될 OU를 마우스 오른쪽 단추로 클릭 하 고 **기존 Gpo 연결**을 클릭 합니다.  

        ![보안 관리 그룹](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_86.gif)  

    3.  방금 만든 GPO를 선택 하 고 **확인을**클릭 합니다.  

        ![보안 관리 그룹](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_87.gif)  

    4.  워크스테이션을 포함 하는 다른 모든 Ou에 대 한 링크를 만듭니다.  

    5.  구성원 서버가 포함 된 다른 모든 Ou에 대 한 링크를 만듭니다.  

        > [!IMPORTANT]  
        > 도메인 컨트롤러를 관리 하는 데 점프 서버를 사용 하 고 Active Directory 하는 경우 점프 서버가이 Gpo가 연결 되지 않은 OU에 있어야 합니다.  

        > [!NOTE]  
        > Gpo의 Administrators 그룹에 제한 사항이 구현 하는 경우 Windows 도메인의 관리자 그룹 외에도 컴퓨터의 로컬 관리자 그룹의 구성원에 게 설정을 적용 합니다. 따라서 관리자 그룹에서 제한을 구현할 때 주의 해야 합니다. Administrators 그룹의 구성원에 대 한 네트워크, 일괄 처리 및 서비스 로그온은 구현할 수 있는 모든 위치에 권장 되지만, 원격 데스크톱 서비스을 통해 로컬 로그온 또는 로그온을 제한 하지 않습니다. 이러한 로그온 유형은 차단 로컬 관리자 그룹의 구성원으로 컴퓨터의 합법적인 관리를 차단할 수 있습니다.  
        >   
        > 다음 스크린샷은 기본 제공 로컬 또는 도메인 관리자 그룹의 오용 외에도 기본 제공 로컬 및 도메인 관리자 계정의 오용을 차단 하는 구성 설정을 보여 줍니다. 이때는 **원격 데스크톱 서비스를 통한 로그온 거부** 사용자 권한을 포함 하 여이 설정에는 로컬 컴퓨터의 Administrators 그룹의 구성원 인 계정에 대 한 이러한 로그온 차단도 하기 때문에 관리자 그룹 포함 되지 않습니다. 컴퓨터의 서비스가이 섹션에 설명 된 권한 있는 그룹의 컨텍스트에서 실행 되도록 구성 된 경우 이러한 설정을 구현 하면 서비스와 응용 프로그램에 오류가 발생할 수 있습니다. 따라서이 섹션에서 권장 하는 모든와 마찬가지로 철저히 테스트 해야 적용 가능성에 대 한 설정을 사용자 환경에서.  

        ![보안 관리 그룹](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_88.gif)  

#### <a name="step-by-step-instructions-to-grant-user-rights-to-the-administrators-group"></a>관리자 그룹에 사용자 권한을 부여 하는 단계별 지침  

1.  **서버 관리자**에서 **도구**를 클릭 하 **그룹 정책 관리**를 클릭 합니다.  

2.  콘솔 트리에서 <Forest>\Domains\\<Domain>를 확장 한 다음 **개체를 그룹 정책** 합니다. 여기서 <Forest>는 포리스트의 이름이 고 <Domain>은 그룹 정책를 설정 하려는 도메인의 이름입니다.  

3.  콘솔 트리에서 **그룹 정책 개체**를 마우스 오른쪽 단추로 클릭 하 고 **새로 만들기**를 클릭 합니다.  

    ![보안 관리 그룹](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_89.gif)  

4.  **새 gpo** 대화 상자에서 <GPO Name>를 입력 하 고 **확인** 을 클릭 합니다. 여기서 <GPO Name>는이 GPO의 이름입니다.  

    ![보안 관리 그룹](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_90.gif)  

5.  세부 정보 창에서 **<GPO Name>** 을 마우스 오른쪽 단추로 클릭 하 고 **편집**을 클릭 합니다.  

6.  **Computer Configuration\Policies\Windows 설정 \ 로컬 정책**으로 이동 하 고 **사용자 권한 할당**을 클릭 합니다.  

    ![보안 관리 그룹](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_91.gif)  

7.  다음을 수행 하 여 Administrators 그룹의 구성원이 네트워크를 통해 도메인 컨트롤러에 액세스할 수 있도록 사용자 권한을 구성 합니다.  

    1.  **네트워크에서이 컴퓨터 액세스를** 두 번 클릭 하 고 **다음 정책 설정 정의**를 선택 합니다.  

    2.  **사용자 또는 그룹 추가** 를 클릭 하 고 **찾아보기**를 클릭 합니다.  

    3.  **사용자 또는 그룹 추가** 를 클릭 하 고 **찾아보기**를 클릭 합니다.  

        ![보안 관리 그룹](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_92.gif)  

    4.  **확인**을 클릭 하 고 다시 **확인** 을 클릭 합니다.  

8.  다음을 수행 하 여 Administrators 그룹의 구성원이 로컬로 로그온 할 수 있도록 사용자 권한을 구성 합니다.  

    1.  **로컬 로그온 허용** 을 두 번 클릭 하 고 **다음 정책 설정 정의**를 선택 합니다.  

    2.  **사용자 또는 그룹 추가** 를 클릭 하 고 **찾아보기**를 클릭 합니다.  

    3.  **관리자**를 입력 하 고 **이름**확인을 클릭 한 다음 **확인**을 클릭 합니다.  

        ![보안 관리 그룹](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_93.gif)  

    4.  **확인**을 클릭 하 고 다시 **확인** 을 클릭 합니다.  

9. 다음을 수행 하 여 Administrators 그룹의 구성원이 원격 데스크톱 서비스를 통해 로그온 할 수 있도록 사용자 권한을 구성 합니다.  

    1.  **원격 데스크톱 서비스를 통한 로그온 허용** 을 두 번 클릭 하 고 **다음 정책 설정 정의**를 선택 합니다.  

    2.  **사용자 또는 그룹 추가** 를 클릭 하 고 **찾아보기**를 클릭 합니다.  

    3.  **관리자**를 입력 하 고 **이름 확인**을 클릭 한 다음 **확인**을 클릭 합니다.  

        ![보안 관리 그룹](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_94.gif)  

    4.  **확인**을 클릭 하 고 다시 **확인** 을 클릭 합니다.  

10. **그룹 정책 관리 편집기**종료 하려면 **파일**을 클릭 한 다음 **끝내기**를 클릭 합니다.  

11. **그룹 정책 관리**에서 다음을 수행 하 여 GPO를 도메인 컨트롤러 OU에 연결 합니다.  

    1.  <Forest>\Domains\\<Domain>으로 이동 합니다. 여기서 <Forest>는 포리스트의 이름이 고 <Domain>는 그룹 정책를 설정 하려는 도메인의 이름입니다.  

    2.  도메인 컨트롤러 OU를 마우스 오른쪽 단추로 클릭 하 고 **기존 GPO 연결**을 클릭 합니다.  

        ![보안 관리 그룹](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_95.gif)  

    3.  방금 만든 GPO를 선택 하 고 **확인을**클릭 합니다.  

        ![보안 관리 그룹](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_96.gif)  

#### <a name="verification-steps"></a>확인 단계  

##### <a name="verify-deny-access-to-this-computer-from-the-network-gpo-settings"></a>"네트워크에서이 컴퓨터 액세스 거부" GPO 설정 확인  
GPO 변경의 영향을 받지 않는 구성원 서버 또는 워크스테이션 (예: "점프 서버")에서 GPO 변경의 영향을 받는 네트워크를 통해 구성원 서버 또는 워크스테이션에 액세스를 시도 합니다. GPO 설정을 확인 하려면 **NET use** 명령을 사용 하 여 시스템 드라이브를 매핑하려고 시도 합니다.  

1.  Administrators 그룹의 구성원 인 계정을 사용 하 여 로컬로 로그온 합니다.  

2.  마우스를 사용 하 여 포인터를 화면의 오른쪽 위 또는 오른쪽 아래 모서리로 이동 합니다. **참 메뉴** 막대가 표시 되 면 **검색**을 클릭 합니다.  

3.  **검색** 상자에서 **명령 프롬프트**를 입력 하 고 **명령 프롬프트**를 마우스 오른쪽 단추로 클릭 한 다음 **관리자 권한으로 실행** 을 클릭 하 여 관리자 권한 명령 프롬프트를 엽니다.  

4.  권한 상승을 승인를 묻는 메시지가 나타나면 클릭 **예**합니다.  

    ![보안 관리 그룹](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_97.gif)  

5.  **명령 프롬프트** 창에서 **net use \\\\\<서버 이름\>\c $** 를 입력 합니다. 여기서 \<server name\>은 네트워크를 통해 액세스 하려는 구성원 서버 또는 워크스테이션의 이름입니다.  

6.  다음 스크린샷은 표시 되어야 하는 오류 메시지를 보여 줍니다.  

    ![보안 관리 그룹](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_98.gif)  

##### <a name="verify-deny-log-on-as-a-batch-job-gpo-settings"></a>"일괄 작업으로 로그온 거부" GPO 설정 확인  
GPO 변경의 영향을 받는 모든 구성원 서버 또는 워크스테이션에서 로컬로 로그온 합니다.  

###### <a name="create-a-batch-file"></a>배치 파일 만들기  

1.  마우스를 사용 하 여 포인터를 화면의 오른쪽 위 또는 오른쪽 아래 모서리로 이동 합니다. **참 메뉴** 막대가 표시 되 면 **검색**을 클릭 합니다.  

2.  **검색** 상자에 **notepad**를 입력 하 고 **notepad**를 클릭 합니다.  

3.  **메모장**에서 **dir c:** 를 입력 합니다.  

4.  **파일**을 클릭 하 고 다른 **이름으로 저장**을 클릭 합니다.  

5.  **파일 이름** 필드에 **<Filename>** 을 입력 합니다. 여기서 <Filename>은 새 배치 파일의 이름입니다.  

###### <a name="schedule-a-task"></a>작업 예약  

1.  마우스를 사용 하 여 포인터를 화면의 오른쪽 위 또는 오른쪽 아래 모서리로 이동 합니다. **참 메뉴** 막대가 표시 되 면 **검색**을 클릭 합니다.  

2.  **검색** 상자에 **작업 스케줄러**를 입력 하 고 **작업 스케줄러**를 클릭 합니다.  

    > [!NOTE]  
    > Windows 8을 실행 하는 컴퓨터의 검색 상자에 일정 작업을 입력 하 고 작업 예약을 클릭 합니다.  

3.  **작업**을 클릭 하 고 **작업 만들기**를 클릭 합니다.  

4.  **작업 만들기** 대화 상자에서 **<Task Name>** 를 입력 합니다. 여기서 <Task Name>은 새 작업의 이름입니다.  

5.  **작업** 탭을 클릭 하 고 **새로 만들기**를 클릭 합니다.  

6.  **작업** 필드에서 **프로그램 시작**을 선택 합니다.  

7.  **프로그램/스크립트** 필드에서 **찾아보기**를 클릭 하 고 **배치 파일 만들기** 섹션에서 만든 배치 파일을 찾아서 선택한 다음 **열기**를 클릭 합니다.  

8.  **확인**을 클릭합니다.  

9. **일반** 탭을 클릭합니다.  

10. **보안 옵션** 필드에서 **사용자 또는 그룹 변경**을 클릭 합니다.  

11. Administrators 그룹의 구성원 인 계정의 이름을 입력 하 고 **이름 확인**을 클릭 한 다음 **확인**을 클릭 합니다.  

12. **사용자가 로그인 했는지 여부에 관계 없이 실행** 을 선택 하 고 **암호를 저장 하지**않습니다. 작업은 로컬 컴퓨터 리소스에만 액세스할 수 있습니다.  

13. **확인**을 클릭합니다.  

14. 작업을 실행 하기 위한 사용자 계정 자격 증명을 요청 하는 대화 상자가 나타납니다.  

15. 암호를 입력 한 후 **확인**을 클릭 합니다.  

16. 다음과 유사한 대화 상자가 표시 됩니다.  

    ![보안 관리 그룹](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_99.gif)  

##### <a name="verify-deny-log-on-as-a-service-gpo-settings"></a>"서비스로 로그온 거부" GPO 설정 확인  

1.  GPO 변경의 영향을 받는 모든 구성원 서버 또는 워크스테이션에서 로컬로 로그온 합니다.  

2.  마우스를 사용 하 여 포인터를 화면의 오른쪽 위 또는 오른쪽 아래 모서리로 이동 합니다. **참 메뉴** 막대가 표시 되 면 **검색**을 클릭 합니다.  

3.  **검색** 상자에 **서비스**를 입력 하 고 **서비스**를 클릭 합니다.  

4.  **인쇄 스풀러**를 찾아 두 번 클릭 합니다.  

5.  **로그온** 탭을 클릭합니다.  

6.  다음 **으로 로그온** 필드에서 **이 계정을**선택 합니다.  

7.  **찾아보기**를 클릭 하 고 Administrators 그룹의 구성원 인 계정의 이름을 입력 한 다음 **이름 확인**을 클릭 하 고 **확인**을 클릭 합니다.  

8.  **암호** 및 **암호 확인** 필드에 선택한 계정의 암호를 입력 하 고 **확인**을 클릭 합니다.  

9. **확인을** 세 번 더 클릭 합니다.  

10. **인쇄 스풀러** 를 마우스 오른쪽 단추로 클릭 하 고 **다시 시작**을 클릭 합니다.  

11. 서비스가 다시 시작 되 면 다음과 유사한 대화 상자가 나타납니다.  

    ![보안 관리 그룹](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_100.png)  

##### <a name="revert-changes-to-the-printer-spooler-service"></a>프린터 스풀러 서비스로 변경 내용 되돌리기  

1.  GPO 변경의 영향을 받는 모든 구성원 서버 또는 워크스테이션에서 로컬로 로그온 합니다.  

2.  마우스를 사용 하 여 포인터를 화면의 오른쪽 위 또는 오른쪽 아래 모서리로 이동 합니다. **참 메뉴** 막대가 표시 되 면 **검색**을 클릭 합니다.  

3.  **검색** 상자에 **서비스**를 입력 하 고 **서비스**를 클릭 합니다.  

4.  **인쇄 스풀러**를 찾아 두 번 클릭 합니다.  

5.  **로그온** 탭을 클릭합니다.  

6.  다음 **으로 로그온** 필드에서 **로컬 시스템** 계정을 클릭 하 고 **확인**을 클릭 합니다.  
