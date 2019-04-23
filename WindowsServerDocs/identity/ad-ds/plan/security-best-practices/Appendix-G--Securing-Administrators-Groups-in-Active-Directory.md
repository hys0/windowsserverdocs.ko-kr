---
ms.assetid: 4baefbd3-038f-44c0-85ba-f24e9722b757
title: 부록 G-Active Directory에서 관리자 그룹의 보안 설정
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 2912dfc534d751d4aa121d238dffc36c07562d76
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59882714"
---
# <a name="appendix-g-securing-administrators-groups-in-active-directory"></a>부록 g: Active Directory에서 관리자 그룹의 보안 설정

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012


## <a name="appendix-g-securing-administrators-groups-in-active-directory"></a>부록 g: Active Directory에서 관리자 그룹의 보안 설정  
Enterprise Admins (EA) 및 도메인 관리자 (DA) 그룹을 사용 하는 경우에는 기본 제공 관리자 (BA) 그룹의 구성원 자격 빌드 또는 재해 복구 시나리오에만 받아야 합니다. 있어야 일상적인 사용자 계정이 없는 도메인에 대 한 기본 제공 관리자 계정 제외 하 고 Administrators 그룹의 경우에 설명 된 대로 보안이 설정 되었을 [부록 d: Active Directory에서 기본 제공 관리자 계정 보안](../../../ad-ds/plan/security-best-practices/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory.md)합니다.  

관리자는 기본적으로 대부분의 각 도메인의 AD DS 개체의 소유자입니다. 이 그룹의 멤버 소유권 또는 기능 개체의 소유권을 가질 필요는 빌드 또는 재해 복구 시나리오에 필요할 수 있습니다. 또한 DAs 및 EAs에는 다양 한 해당 권한 및 관리자 그룹의 해당 기본 멤버 자격을 통해 권한을 상속합니다. Active Directory에서 권한 있는 그룹에 대 한 중첩 하는 기본 그룹을 수정할 수 없습니다 하 고 각 도메인의 관리자 그룹 이어지는 단계별 지침에 설명 된 대로 보호 되어야 합니다.  

포리스트의 각 도메인의 관리자 그룹:  

1.  에 설명 된 대로 보안이 설정 되었습니다 제공 관리자 그룹의 도메인에 대 한 기본 제공 관리자 계정의 예외일 수 있음에서 모든 구성원을 제거 [부록 d: Active Directory에서 기본 제공 관리자 계정 보안](../../../ad-ds/plan/security-best-practices/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory.md)합니다.  

2.  구성원 서버 및 워크스테이션 각 도메인에 포함 된 Ou에 연결 된 Gpo, DA 그룹에 다음 사용자 권한을 추가 해야 합니다 **컴퓨터 구성 설정 \ 보안 설정 \ 로컬 정책 \ Policies\ 사용자 권한 할당**:  

    -   네트워크에서 이 컴퓨터 액세스 거부  

    -   일괄 작업으로 로그온 거부  

    -   서비스로 로그온 거부  

3.  포리스트의 각 도메인의 OU 도메인 컨트롤러에서 Administrators 그룹 다음 사용자 권한이 부여 해야 합니다.  

    -   네트워크에서 이 컴퓨터 액세스  

    -   로컬 로그온 허용  

    -   원격 데스크톱 서비스를 통한 로그온 허용  

4.  감사 관리자 그룹의 구성원 또는 속성을 수정한 경우 경고를 보내도록 구성 되어야 합니다.  

#### <a name="step-by-step-instructions-for-removing-all-members-from-the-administrators-group"></a>Administrators 그룹에서 모든 구성원을 제거 하기 위한 단계별 지침  

1.  **서버 관리자**, 클릭 **도구**를 클릭 하 고 **Active Directory Users and Computers**합니다.  

2.  관리자 그룹에서 모든 구성원을 제거 하려면 다음 단계를 수행 합니다.  

    1.  두 번 클릭 합니다 **관리자** 그룹을 클릭 합니다 **멤버** 탭 합니다.  

        ![보안 관리 그룹](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_79.gif)  

    2.  그룹의 멤버를 선택, 클릭 **제거할**, 클릭 **예**, 클릭 **확인**합니다.  

3.  Administrators 그룹의 모든 구성원을 제거할 때까지 2 단계를 반복 합니다.  

#### <a name="step-by-step-instructions-to-secure-administrators-groups-in-active-directory"></a>Active Directory에서 관리자 그룹을 보호 하기 위한 단계별 지침  

1.  **서버 관리자**, 클릭 **도구**를 클릭 하 고 **그룹 정책 관리**합니다.  

2.  콘솔 트리에서 &lt;포리스트&gt;\Domains\\&lt;도메인&gt;를 차례로 **그룹 정책 개체** (여기서 &lt;포리스트&gt; 는 포리스트 이름 및 &lt;도메인&gt; 그룹 정책 설정 하려는 도메인의 이름입니다).  

3.  콘솔 트리에서 마우스 오른쪽 단추로 클릭 **그룹 정책 개체**, 클릭 **새로 만들기**합니다.  

    ![보안 관리 그룹](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_80.gif)  

4.  에 **새 GPO** 대화 상자에서 <GPO Name>, 클릭 **확인** (여기서 *GPO 이름* 이 GPO의 이름입니다).  

    ![보안 관리 그룹](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_81.gif)  

5.  세부 정보 창에서 마우스 오른쪽 단추로 클릭 **<GPO Name>**, 클릭 **편집**합니다.  

6.  이동할 **컴퓨터 구성 \ 정책 \ 로컬 정책**, 클릭 **사용자 권한 할당**합니다.  

    ![보안 관리 그룹](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_82.gif)  

7.  다음을 수행 하 여 네트워크를 통해 멤버 서버 및 워크스테이션에 관리자 그룹의 구성원을 방지 하기 위해 사용자 권한을 구성 합니다.  

    1.  두 번 클릭 **네트워크에서이 컴퓨터 액세스 거부** 선택한 **이 정책 설정 정의**합니다.  

    2.  클릭 **사용자 또는 그룹 추가** 누릅니다 **찾아보기**합니다.  

    3.  형식 **Administrators**, 클릭 **이름 확인**, 클릭 **확인**합니다.  

        ![보안 관리 그룹](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_83.gif)  

    4.  클릭 **확인**, 및 **확인** 다시 합니다.  

8.  다음을 수행 하 여 일괄 작업으로 로그온에서 Administrators 그룹의 멤버를 방지 하기 위해 사용자 권한을 구성 합니다.  

    1.  두 번 클릭 **일괄 작업으로 로그온 거부** 선택한 **이 정책 설정 정의**합니다.  

    2.  클릭 **사용자 또는 그룹 추가** 누릅니다 **찾아보기**합니다.  

    3.  형식 **Administrators**, 클릭 **이름 확인**, 클릭 **확인**합니다.  

        ![보안 관리 그룹](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_84.gif)  

    4.  클릭 **확인**, 및 **확인** 다시 합니다.  

9. 다음을 수행 하 여 서비스로 로그온에서 Administrators 그룹의 멤버를 방지 하기 위해 사용자 권한을 구성 합니다.  

    1.  두 번 클릭 **서비스로 로그온 거부** 선택한 **이 정책 설정 정의**합니다.  

    2.  클릭 **사용자 또는 그룹 추가** 누릅니다 **찾아보기**합니다.  

    3.  형식 **Administrators**, 클릭 **이름 확인**, 클릭 **확인**합니다.  

        ![보안 관리 그룹](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_85.gif)  

    4.  클릭 **확인**, 및 **확인** 다시 합니다.  

10. 끝내려면 **그룹 정책 관리 편집기**, 클릭 **파일**, 클릭 **종료**합니다.  

11. **그룹 정책 관리**, 다음을 수행 하 여 Ou 워크스테이션 및 구성원 서버에 GPO을 연결 합니다.  

    1.  로 이동 합니다 &lt;포리스트&gt;> \Domains\\&lt;도메인&gt; (여기서 &lt;포리스트&gt; 포리스트의 이름 및 &lt;도메인&gt; 이름 도메인의 그룹 정책을 설정 하려면).  

    2.  GPO에 적용 됩니다을 클릭 하는 OU를 마우스 오른쪽 단추로 클릭 **기존 GPO 연결**합니다.  

        ![보안 관리 그룹](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_86.gif)  

    3.  방금 만든 GPO를 선택 하 고 클릭 **확인**합니다.  

        ![보안 관리 그룹](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_87.gif)  

    4.  워크스테이션을 포함 하는 다른 모든 Ou에 대 한 링크를 만듭니다.  

    5.  구성원 서버가 포함 된 다른 모든 Ou에 대 한 링크를 만듭니다.  

        > [!IMPORTANT]  
        > 점프 서버 도메인 컨트롤러와 Active Directory 관리를 사용 하는 경우이 Gpo 연결 되지 않은 OU에 점프 서버가 있는지는 확인 합니다.  

        > [!NOTE]  
        > Gpo의 Administrators 그룹에 제한 사항이 구현 하는 경우 Windows 도메인의 관리자 그룹 외에도 컴퓨터의 로컬 관리자 그룹의 구성원에 게 설정을 적용 합니다. 따라서 Administrators 그룹에 제한을 구현 하는 경우 주의 사용 해야 합니다. 로컬 로그온 이나 로그온 원격 데스크톱 서비스를 통해 Administrators 그룹의 멤버에 대 한 네트워크, 배치 및 서비스 로그온을 차단 하면 아무 곳에 나 것이 가능한 구현 하는 것이 좋습니다, 하지만 제한 하지 않습니다. 이러한 로그온 유형은 차단 로컬 관리자 그룹의 구성원으로 컴퓨터의 합법적인 관리를 차단할 수 있습니다.  
        >   
        > 기본 제공 로컬 또는 도메인 관리자 그룹의 오용 외에도 도메인 관리자 계정 및 다음 스크린 샷에서 구성 설정의 기본 제공 악용을 차단 하는 로컬 보여 줍니다. 이때는 **원격 데스크톱 서비스를 통한 로그온 거부** 사용자 권한을 포함 하 여이 설정에는 로컬 컴퓨터의 Administrators 그룹의 구성원 인 계정에 대 한 이러한 로그온 차단도 하기 때문에 관리자 그룹 포함 되지 않습니다. 서비스 및 응용 프로그램 서비스가 컴퓨터에서이 섹션에 설명 된 권한 있는 그룹의 컨텍스트에서 실행 되도록 구성 하는 경우 발생할 수 있습니다 이러한 설정을 구현 합니다. 따라서이 섹션에서 권장 하는 모든와 마찬가지로 철저히 테스트 해야 적용 가능성에 대 한 설정을 사용자 환경에서.  

        ![보안 관리 그룹](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_88.gif)  

#### <a name="step-by-step-instructions-to-grant-user-rights-to-the-administrators-group"></a>관리자 그룹에 권한 부여 사용자 권한에 대 한 단계별 지침  

1.  **서버 관리자**, 클릭 **도구**를 클릭 하 고 **그룹 정책 관리**합니다.  

2.  콘솔 트리에서 <Forest>\Domains\\<Domain>를 차례로 **그룹 정책 개체** (여기서 <Forest> 포리스트의 이름 및 <Domain> 하려는 도메인의 이름 그룹 정책 설정).  

3.  콘솔 트리에서 마우스 오른쪽 단추로 클릭 **그룹 정책 개체**, 클릭 **새로 만들기**합니다.  

    ![보안 관리 그룹](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_89.gif)  

4.  에 **새 GPO** 대화 상자에서 <GPO Name>, 클릭 **확인** (여기서 <GPO Name> 이 GPO의 이름입니다).  

    ![보안 관리 그룹](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_90.gif)  

5.  세부 정보 창에서 마우스 오른쪽 단추로 클릭 **<GPO Name>**, 클릭 **편집**합니다.  

6.  이동할 **컴퓨터 구성 \ 정책 \ 로컬 정책**, 클릭 **사용자 권한 할당**합니다.  

    ![보안 관리 그룹](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_91.gif)  

7.  다음을 수행 하 여 네트워크를 통해 컨트롤러에 액세스 하려면 도메인 관리자 그룹의 구성원을 허용 하도록 사용자 권한을 구성 합니다.  

    1.  두 번 클릭 **네트워크에서이 컴퓨터에 대 한 액세스** 선택한 **이 정책 설정 정의**합니다.  

    2.  클릭 **사용자 또는 그룹 추가** 누릅니다 **찾아보기**합니다.  

    3.  클릭 **사용자 또는 그룹 추가** 누릅니다 **찾아보기**합니다.  

        ![보안 관리 그룹](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_92.gif)  

    4.  클릭 **확인**, 및 **확인** 다시 합니다.  

8.  Administrators 그룹의 멤버는 다음을 수행 하 여 로컬로 로그온 할 수 있도록 사용자 권한을 구성 합니다.  

    1.  두 번 클릭 **로컬 로그온 허용** 선택한 **이 정책 설정 정의**합니다.  

    2.  클릭 **사용자 또는 그룹 추가** 누릅니다 **찾아보기**합니다.  

    3.  형식 **Administrators**, 확인을 클릭 **이름**, 클릭 **확인**합니다.  

        ![보안 관리 그룹](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_93.gif)  

    4.  클릭 **확인**, 및 **확인** 다시 합니다.  

9. 사용자에 게 다음을 수행 하 여 원격 데스크톱 서비스를 통한 로그온 Administrators 그룹의 구성원이 수 있도록 권한을 구성 합니다.  

    1.  두 번 클릭 **원격 데스크톱 서비스를 통한 로그온 허용** 선택한 **이 정책 설정 정의**합니다.  

    2.  클릭 **사용자 또는 그룹 추가** 누릅니다 **찾아보기**합니다.  

    3.  형식 **Administrators**, 클릭 **이름 확인**, 클릭 **확인**합니다.  

        ![보안 관리 그룹](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_94.gif)  

    4.  클릭 **확인**, 및 **확인** 다시 합니다.  

10. 끝내려면 **그룹 정책 관리 편집기**, 클릭 **파일**, 클릭 **종료**합니다.  

11. **그룹 정책 관리**, 다음을 수행 하 여 도메인 컨트롤러 OU에 GPO을 연결 합니다.  

    1.  로 이동 합니다 <Forest>\Domains\\ <Domain> (여기서 <Forest> 포리스트의 이름 및 <Domain> 그룹 정책 설정 하려는 도메인의 이름입니다).  

    2.  도메인 컨트롤러 OU 및 클릭을 마우스 오른쪽 단추로 클릭 **기존 GPO 연결**합니다.  

        ![보안 관리 그룹](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_95.gif)  

    3.  방금 만든 GPO를 선택 하 고 클릭 **확인**합니다.  

        ![보안 관리 그룹](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_96.gif)  

#### <a name="verification-steps"></a>확인 단계  

##### <a name="verify-deny-access-to-this-computer-from-the-network-gpo-settings"></a>액세스 거부 "이이 컴퓨터에 네트워크에서" GPO 설정을 확인 합니다.  
구성원 서버 또는 워크스테이션 (예: "점프 서버") GPO 변경 내용의 영향을 받지 않는 구성원 서버 또는 워크스테이션 GPO 변경이 영향을 받는 네트워크를 통해 액세스 하려고 합니다. 시스템 드라이브를 사용 하 여 매핑할 시도 GPO 설정을 확인 하는 **NET USE** 명령입니다.  

1.  로컬 Administrators 그룹의 구성원 인 계정을 사용 하 여 로그온 합니다.  

2.  마우스를 사용 하 여 화면 오른쪽 상단 또는 오른쪽 아래 모퉁이에 포인터를 이동 합니다. 경우는 **참 메뉴** 표시줄에 표시 되 면 클릭 **검색**합니다.  

3.  에 **검색** 상자에 입력 **명령 프롬프트**를 마우스 오른쪽 단추로 클릭 **명령 프롬프트**를 클릭 하 고 **관리자 권한으로 실행** 열려면 관리자 권한 명령 프롬프트입니다.  

4.  권한 상승을 승인를 묻는 메시지가 나타나면 클릭 **예**합니다.  

    ![보안 관리 그룹](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_97.gif)  

5.  에 **명령 프롬프트** 창, 형식 **사용 하 여 net \\ \\ \<서버 이름\>\c$** 여기서 \<서버 이름을\> 는 구성원 서버 또는 네트워크를 통해 액세스를 시도 중인 워크스테이션의 이름입니다.  

6.  다음 스크린 샷에 표시 되는 오류 메시지를 표시 합니다.  

    ![보안 관리 그룹](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_98.gif)  

##### <a name="verify-deny-log-on-as-a-batch-job-gpo-settings"></a>"로그온 거부 일괄 작업으로" GPO 설정을 확인 합니다.  
구성원 서버 또는 GPO 변경의 영향을 받는 워크스테이션에서 로컬로 로그온 합니다.  

###### <a name="create-a-batch-file"></a>배치 파일을 만듭니다  

1.  마우스를 사용 하 여 화면 오른쪽 상단 또는 오른쪽 아래 모퉁이에 포인터를 이동 합니다. 경우는 **참 메뉴** 표시줄에 표시 되 면 클릭 **검색**합니다.  

2.  에 **검색** 상자에 입력 **메모장**를 클릭 하 고 **메모장**합니다.  

3.  **메모장**, 형식 **dir c:** 합니다.  

4.  클릭 **파일**, 클릭 **다른 이름으로 저장**합니다.  

5.  에 **파일 이름** 필드에 입력  **<Filename>.bat** (여기서 <Filename> 새 일괄 처리 파일의 이름입니다).  

###### <a name="schedule-a-task"></a>작업 예약  

1.  마우스를 사용 하 여 화면 오른쪽 상단 또는 오른쪽 아래 모퉁이에 포인터를 이동 합니다. 경우는 **참 메뉴** 표시줄에 표시 되 면 클릭 **검색**합니다.  

2.  에 **검색** 상자에 입력 **작업 스케줄러**를 클릭 하 고 **작업 스케줄러**합니다.  

    > [!NOTE]  
    > 검색 상자에 Windows 8을 실행 하는 컴퓨터에서 작업 예약를 입력 하 고 일정 작업을 클릭 합니다.  

3.  클릭 **동작**, 클릭 **작업 만들기**합니다.  

4.  에 **작업 만들기** 대화 상자에서 **<Task Name>** (여기서 <Task Name> 새 작업의 이름입니다).  

5.  클릭 합니다 **동작** 탭을 클릭 **새로 만들기**합니다.  

6.  에 **동작** 필드를 선택한 **프로그램을 시작할**합니다.  

7.  에 **프로그램/스크립트** 필드를 클릭 **찾아보기**을 찾아에서 생성 된 일괄 처리 파일을 선택 합니다 **배치 파일을 만듭니다** 섹션을 클릭 **열기**.  

8.  **확인**을 클릭합니다.  

9. **일반** 탭을 클릭합니다.  

10. 에 **보안 옵션** 필드, 클릭 **사용자 또는 그룹 변경**합니다.  

11. Administrators 그룹의 구성원 인 계정의 이름을 입력, 클릭 **이름 확인**, 클릭 **확인**합니다.  

12. 선택 **사용자가 로그인된 onor 든 상관 없이 실행할** 하 고 **암호를 저장 하지 않는**합니다. 작업만 로컬 컴퓨터 리소스에 액세스할을 수 있습니다.  

13. **확인**을 클릭합니다.  

14. 요청 사용자 계정 작업을 실행 하려면 자격 증명 대화 상자가 표시 됩니다.  

15. 암호를 입력 한 후 클릭 **확인**합니다.  

16. 다음과 유사한 대화 상자가 표시 됩니다.  

    ![보안 관리 그룹](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_99.gif)  

##### <a name="verify-deny-log-on-as-a-service-gpo-settings"></a>GPO 설정을 "로그온 거부 as a service"를 확인 합니다.  

1.  구성원 서버 또는 GPO 변경의 영향을 받는 워크스테이션에서 로컬로 로그온 합니다.  

2.  마우스를 사용 하 여 화면 오른쪽 상단 또는 오른쪽 아래 모퉁이에 포인터를 이동 합니다. 경우는 **참 메뉴** 표시줄에 표시 되 면 클릭 **검색**합니다.  

3.  에 **검색** 상자에 입력 **services**, 클릭 **서비스**합니다.  

4.  찾아 두 번 클릭 **인쇄 스풀러**합니다.  

5.  **로그온** 탭을 클릭합니다.  

6.  에 **로 로그온** 필드를 선택한 **이 계정은**합니다.  

7.  클릭 **찾아보기**Administrators 그룹의 구성원 인 계정의 이름을 입력, 클릭 **이름 확인**를 클릭 하 고 **확인**합니다.  

8.  에 **암호** 하 고 **암호 확인** 필드는 선택한 계정의 암호를 입력 하 고 클릭 **확인**합니다.  

9. 클릭 **확인** 3 회 더 합니다.  

10. 마우스 오른쪽 단추로 클릭 **인쇄 스풀러** 누릅니다 **다시 시작**합니다.  

11. 서비스를 다시 시작할 때 다음과 유사한 대화 상자가 표시 됩니다.  

    ![보안 관리 그룹](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_100.png)  

##### <a name="revert-changes-to-the-printer-spooler-service"></a>프린터 스풀러 서비스에 대 한 변경 내용 되돌리기  

1.  구성원 서버 또는 GPO 변경의 영향을 받는 워크스테이션에서 로컬로 로그온 합니다.  

2.  마우스를 사용 하 여 화면 오른쪽 상단 또는 오른쪽 아래 모퉁이에 포인터를 이동 합니다. 경우는 **참 메뉴** 표시줄에 표시 되 면 클릭 **검색**합니다.  

3.  에 **검색** 상자에 입력 **services**, 클릭 **서비스**합니다.  

4.  찾아 두 번 클릭 **인쇄 스풀러**합니다.  

5.  **로그온** 탭을 클릭합니다.  

6.  에 **로 로그온** 필드를 클릭 **로컬 시스템** 계정 및 클릭 **확인**합니다.  
