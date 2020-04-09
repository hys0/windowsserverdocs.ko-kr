---
ms.assetid: 017b88a6-f29b-4787-99b6-b5c8eaf8c3df
title: 부록 F-Active Directory의 도메인 관리자 그룹 보안
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: d1df7403b7e50fa50894bb4dbaa0cac9c6f42727
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80821506"
---
# <a name="appendix-f-securing-domain-admins-groups-in-active-directory"></a>부록 F: Active Directory의 Domain Admins 그룹 보안

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012


## <a name="appendix-f-securing-domain-admins-groups-in-active-directory"></a>부록 F: Active Directory의 Domain Admins 그룹 보안  
EA (Enterprise Admins) 그룹의 경우와 마찬가지로, 도메인 관리자 (DA) 그룹의 구성원은 빌드 또는 재해 복구 시나리오에만 필요 합니다. 도메인에 대 한 기본 제공 관리자 계정을 제외 하 고 DA 그룹에는 일상적인 사용자 계정이 없어야 합니다 ( [부록 D: 보안 기본 제공 관리자 계정 Active Directory에](../../../ad-ds/plan/security-best-practices/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory.md)설명 된 대로 보안 된 경우).  

Domain Admins는 기본적으로 모든 구성원 서버 및 워크스테이션의 해당 도메인에 로컬 관리자 그룹의 구성원입니다. 지원 가능성 및 재해 복구를 위해이 기본 중첩을 수정 하면 안 됩니다. 구성원 서버의 로컬 관리자 그룹에서 도메인 관리자가 제거 된 경우 그룹은 각 구성원 서버 및 도메인의 워크스테이션에서 관리자 그룹에 추가 되어야 합니다. 아래의 단계별 지침에 설명 된 대로 각 도메인의 Domain Admins 그룹에 보안을 설정 해야 합니다.  

포리스트의 각 도메인에서 Domain Admins 그룹:  

1.  [부록 D: 보안 기본 제공 관리자 계정 Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory.md)의 설명에 따라 보안이 설정 된 경우 도메인에 대 한 기본 제공 관리자 계정을 제외 하 고 그룹에서 모든 구성원을 제거 합니다.  

2.  각 도메인의 구성원 서버 및 워크스테이션을 포함 하는 Ou에 연결 된 Gpo에서 DA 그룹을 **컴퓨터 Configuration\Policies\Windows 설정 \ 로컬 정책 \ 사용자 권한 할당**의 다음 사용자 권한에 추가 해야 합니다.  

    -   네트워크에서 이 컴퓨터 액세스 거부  

    -   일괄 작업으로 로그온 거부  

    -   서비스로 로그온 거부  

    -   로컬 로그온 거부  

    -   원격 데스크톱 서비스 사용자 권한을 통한 로그온 거부  

3.  Domain Admins 그룹의 속성 또는 멤버 자격이 수정 되 면 경고를 보내도록 감사를 구성 해야 합니다.  

#### <a name="step-by-step-instructions-for-removing-all-members-from-the-domain-admins-group"></a>Domain Admins 그룹에서 모든 구성원을 제거 하는 방법에 대 한 단계별 지침  

1.  **서버 관리자**에서 **도구**를 클릭 하 **Active Directory 사용자 및 컴퓨터**를 클릭 합니다.  

2.  DA 그룹에서 모든 구성원을 제거 하려면 다음 단계를 수행 합니다.  

    1.  **Domain Admins** 그룹을 두 번 클릭 하 고 **구성원** 탭을 클릭 합니다.  

        ![보안 도메인 관리자 그룹](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_62.gif)  

    2.  그룹의 구성원을 선택 하 고 **제거**, **예**를 차례로 클릭 한 다음 **확인**을 클릭 합니다.  

3.  DA 그룹의 모든 구성원이 제거 될 때까지 2 단계를 반복 합니다.  

#### <a name="step-by-step-instructions-to-secure-domain-admins-in-active-directory"></a>Active Directory에서 도메인 관리자를 보호 하는 단계별 지침  

1.  **서버 관리자**에서 **도구**를 클릭 하 **그룹 정책 관리**를 클릭 합니다.  

2.  콘솔 트리에서 \<포리스트\>\\\\도메인 \<도메인\>을 확장 한 다음 **개체를 그룹 정책** 합니다. 여기서 \<포리스트\>는 포리스트의 이름이 고 \<도메인\>는 그룹 정책를 설정 하려는 도메인의 이름입니다.  

3.  콘솔 트리에서 **그룹 정책 개체**를 마우스 오른쪽 단추로 클릭 하 고 **새로 만들기**를 클릭 합니다.  

    ![보안 도메인 관리자 그룹](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_63.gif)  

4.  **새 gpo** 대화 상자에서 gpo 이름\>\<을 입력 하 고 **확인** 을 클릭 합니다. 여기서 \<GPO 이름\>이 GPO의 이름입니다.  

    ![보안 도메인 관리자 그룹](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_64.gif)  

5.  세부 정보 창에서 GPO 이름\>\<을 마우스 오른쪽 단추로 클릭 하 고 **편집**을 클릭 합니다.  

6.  **Computer Configuration\Policies\Windows 설정 \ 로컬 정책**으로 이동 하 고 **사용자 권한 할당**을 클릭 합니다.  

    ![보안 도메인 관리자 그룹](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_65.gif)  

7.  다음을 수행 하 여 Domain Admins 그룹의 구성원이 네트워크를 통해 구성원 서버 및 워크스테이션에 액세스 하지 못하도록 사용자 권한을 구성 합니다.  

    1.  **네트워크에서이 컴퓨터 액세스 거부** 를 두 번 클릭 하 고 **다음 정책 설정 정의**를 선택 합니다.  

    2.  **사용자 또는 그룹 추가** 를 클릭 하 고 **찾아보기**를 클릭 합니다.  

    3.  **Domain Admins**를 입력 하 고 **이름 확인**을 클릭 한 다음 **확인**을 클릭 합니다.  

        ![보안 도메인 관리자 그룹](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_66.gif)  

    4.  **확인**을 클릭 하 고 다시 **확인** 을 클릭 합니다.  

8.  다음을 수행 하 여 DA 그룹의 구성원이 batch 작업으로 로그온 하지 못하도록 사용자 권한을 구성 합니다.  

    1.  **일괄 작업으로 로그온 거부** 를 두 번 클릭 하 고 **다음 정책 설정 정의**를 선택 합니다.  

    2.  **사용자 또는 그룹 추가** 를 클릭 하 고 **찾아보기**를 클릭 합니다.  

    3.  **Domain Admins**를 입력 하 고 **이름 확인**을 클릭 한 다음 **확인**을 클릭 합니다.  

        ![보안 도메인 관리자 그룹](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_67.gif)  

    4.  **확인**을 클릭 하 고 다시 **확인** 을 클릭 합니다.  

9. 다음을 수행 하 여 DA 그룹의 구성원이 서비스로 로그온 하지 못하도록 사용자 권한을 구성 합니다.  

    1.  **서비스로 로그온 거부** 를 두 번 클릭 하 고 **다음 정책 설정 정의**를 선택 합니다.  

    2.  **사용자 또는 그룹 추가** 를 클릭 하 고 **찾아보기**를 클릭 합니다.  

    3.  **Domain Admins**를 입력 하 고 **이름 확인**을 클릭 한 다음 **확인**을 클릭 합니다.  

        ![보안 도메인 관리자 그룹](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_68.gif)  

    4.  **확인**을 클릭 하 고 다시 **확인** 을 클릭 합니다.  

10. 다음을 수행 하 여 Domain Admins 그룹의 구성원이 구성원 서버 및 워크스테이션에 로컬로 로그온 하지 못하도록 사용자 권한을 구성 합니다.  

    1.  **로컬 로그온 거부** 를 두 번 클릭 하 고 **다음 정책 설정 정의**를 선택 합니다.  

    2.  **사용자 또는 그룹 추가** 를 클릭 하 고 **찾아보기**를 클릭 합니다.  

    3.  **Domain Admins**를 입력 하 고 **이름 확인**을 클릭 한 다음 **확인**을 클릭 합니다.  

        ![보안 도메인 관리자 그룹](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_69.gif)  

    4.  **확인**을 클릭 하 고 다시 **확인** 을 클릭 합니다.  

11. 다음을 수행 하 여 Domain Admins 그룹의 구성원이 원격 데스크톱 서비스를 통해 구성원 서버 및 워크스테이션에 액세스 하지 못하도록 사용자 권한을 구성 합니다.  

    1.  **원격 데스크톱 서비스를 통한 로그온 거부** 를 두 번 클릭 하 고 **다음 정책 설정 정의**를 선택 합니다.  

    2.  **사용자 또는 그룹 추가** 를 클릭 하 고 **찾아보기**를 클릭 합니다.  

    3.  **Domain Admins**를 입력 하 고 **이름 확인**을 클릭 한 다음 **확인**을 클릭 합니다.  

        ![보안 도메인 관리자 그룹](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_70.gif)  

    4.  **확인**을 클릭 하 고 다시 **확인** 을 클릭 합니다.  

12. **그룹 정책 관리 편집기**종료 하려면 **파일**을 클릭 한 다음 **끝내기**를 클릭 합니다.  

13. 그룹 정책 관리에서 다음을 수행 하 여 GPO를 구성원 서버 및 워크스테이션 Ou에 연결 합니다.  

    1.  \<포리스트\>\Domains\\\<도메인\>로 이동 합니다. 여기서 \<포리스트\>는 포리스트 이름이 고 \<도메인\>는 그룹 정책를 설정 하려는 도메인의 이름입니다.  

    2.  GPO가 적용 될 OU를 마우스 오른쪽 단추로 클릭 하 고 **기존 Gpo 연결**을 클릭 합니다.  

        ![보안 도메인 관리자 그룹](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_71.gif)  

    3.  방금 만든 GPO를 선택 하 고 **확인을**클릭 합니다.  

        ![보안 도메인 관리자 그룹](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_72.gif)  

    4.  워크스테이션을 포함 하는 다른 모든 Ou에 대 한 링크를 만듭니다.  

    5.  구성원 서버가 포함 된 다른 모든 Ou에 대 한 링크를 만듭니다.  

        > [!IMPORTANT]  
        > 도메인 컨트롤러를 관리 하는 데 점프 서버를 사용 하 고 Active Directory 하는 경우 점프 서버가이 Gpo가 연결 되지 않은 OU에 있어야 합니다.  

#### <a name="verification-steps"></a>확인 단계  

##### <a name="verify-deny-access-to-this-computer-from-the-network-gpo-settings"></a>"네트워크에서이 컴퓨터 액세스 거부" GPO 설정 확인  
GPO 변경의 영향을 받지 않는 구성원 서버 또는 워크스테이션 (예: "점프 서버")에서 GPO 변경의 영향을 받는 네트워크를 통해 구성원 서버 또는 워크스테이션에 액세스를 시도 합니다. GPO 설정을 확인 하려면 **NET use** 명령을 사용 하 여 시스템 드라이브를 매핑하려고 시도 합니다.  

1.  Domain Admins 그룹의 구성원 인 계정을 사용 하 여 로컬로 로그온 합니다.  

2.  마우스를 사용 하 여 포인터를 화면의 오른쪽 위 또는 오른쪽 아래 모서리로 이동 합니다. **참 메뉴** 막대가 표시 되 면 **검색**을 클릭 합니다.  

3.  **검색** 상자에서 **명령 프롬프트**를 입력 하 고 **명령 프롬프트**를 마우스 오른쪽 단추로 클릭 한 다음 **관리자 권한으로 실행** 을 클릭 하 여 관리자 권한 명령 프롬프트를 엽니다.  

4.  권한 상승을 승인를 묻는 메시지가 나타나면 클릭 **예**합니다.  

    ![보안 도메인 관리자 그룹](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_73.gif)  

5.  **명령 프롬프트** 창에서 **net use \\\\\<서버 이름\>\c $** 를 입력 합니다. 여기서 \<server name\>은 네트워크를 통해 액세스 하려는 구성원 서버 또는 워크스테이션의 이름입니다.  

6.  다음 스크린샷은 표시 되어야 하는 오류 메시지를 보여 줍니다.  

    ![보안 도메인 관리자 그룹](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_74.gif)  

##### <a name="verify-deny-log-on-as-a-batch-job-gpo-settings"></a>"일괄 작업으로 로그온 거부" GPO 설정 확인  

GPO 변경의 영향을 받는 모든 구성원 서버 또는 워크스테이션에서 로컬로 로그온 합니다.  

###### <a name="create-a-batch-file"></a>배치 파일 만들기  

1.  마우스를 사용 하 여 포인터를 화면의 오른쪽 위 또는 오른쪽 아래 모서리로 이동 합니다. **참 메뉴** 막대가 표시 되 면 **검색**을 클릭 합니다.  

2.  **검색** 상자에 **notepad**를 입력 하 고 **notepad**를 클릭 합니다.  

3.  **메모장**에서 **dir c:** 를 입력 합니다.  

4.  **파일**을 클릭 하 고 다른 **이름으로 저장**을 클릭 합니다.  

5.  **파일** 이름 필드에 **\<filename\>** 을 입력 합니다. 여기서 \<filename\>은 새 배치 파일의 이름입니다.  

###### <a name="schedule-a-task"></a>작업 예약  

1.  마우스를 사용 하 여 포인터를 화면의 오른쪽 위 또는 오른쪽 아래 모서리로 이동 합니다. **참 메뉴** 막대가 표시 되 면 **검색**을 클릭 합니다.  

2.  **검색** 상자에 **작업 스케줄러**를 입력 하 고 **작업 스케줄러**를 클릭 합니다.  

    > [!NOTE]  
    > Windows 8을 실행 하는 컴퓨터의 **검색** 상자에 **일정 작업**을 입력 하 고 **작업 예약**을 클릭 합니다.  

3.  **작업 스케줄러** 메뉴 모음에서 **작업**을 클릭 하 고 **작업 만들기**를 클릭 합니다.  

4.  **작업 만들기** 대화 상자에서 **\<작업 이름\>** 을 입력 합니다. 여기서 \<작업 이름\>은 새 작업의 이름입니다.  

5.  **작업** 탭을 클릭 하 고 **새로 만들기**를 클릭 합니다.  

6.  **작업** 필드에서 **프로그램 시작**을 선택 합니다.  

7.  **프로그램/스크립트**에서 **찾아보기**를 클릭 하 고 **배치 파일 만들기** 섹션에서 만든 배치 파일을 찾아서 선택한 다음 **열기**를 클릭 합니다.  

8.  **확인**을 클릭합니다.  

9. **일반** 탭을 클릭합니다.  

10. **보안** 옵션에서 **사용자 또는 그룹 변경**을 클릭 합니다.  

11. Domain Admins 그룹의 구성원 인 계정의 이름을 입력 하 고 **이름 확인**을 클릭 한 다음 **확인**을 클릭 합니다.  

12. **사용자의 로그온 여부에 관계 없이 실행** 을 선택 하 고 **암호 저장 안 함**을 선택 합니다. 작업은 로컬 컴퓨터 리소스에만 액세스할 수 있습니다.  

13. **확인**을 클릭합니다.  

14. 작업을 실행 하기 위한 사용자 계정 자격 증명을 요청 하는 대화 상자가 나타납니다.  

15. 자격 증명을 입력 한 후 **확인**을 클릭 합니다.  

16. 다음과 유사한 대화 상자가 표시 됩니다.  

    ![보안 도메인 관리자 그룹](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_75.gif)  

##### <a name="verify-deny-log-on-as-a-service-gpo-settings"></a>"서비스로 로그온 거부" GPO 설정 확인  

1.  GPO 변경의 영향을 받는 모든 구성원 서버 또는 워크스테이션에서 로컬로 로그온 합니다.  

2.  마우스를 사용 하 여 포인터를 화면의 오른쪽 위 또는 오른쪽 아래 모서리로 이동 합니다. **참 메뉴** 막대가 표시 되 면 **검색**을 클릭 합니다.  

3.  **검색** 상자에 **서비스**를 입력 하 고 **서비스**를 클릭 합니다.  

4.  **인쇄 스풀러**를 찾아 두 번 클릭 합니다.  

5.  **로그온** 탭을 클릭합니다.  

6.  다음 계정 **으로 로그온**에서 **이 계정** 옵션을 선택 합니다.  

7.  **찾아보기**를 클릭 하 고 Domain Admins 그룹의 구성원 인 계정의 이름을 입력 한 다음 **이름 확인**을 클릭 하 고 **확인**을 클릭 합니다.  

8.  **암호** 및 **암호 확인**에서 선택한 계정의 암호를 입력 하 고 **확인**을 클릭 합니다.  

9. **확인을** 세 번 더 클릭 합니다.  

10. **인쇄 스풀러** 를 마우스 오른쪽 단추로 클릭 하 고 **다시 시작**을 클릭 합니다.  

11. 서비스가 다시 시작 되 면 다음과 유사한 대화 상자가 나타납니다.  

    ![보안 도메인 관리자 그룹](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_76.gif)  

##### <a name="revert-changes-to-the-printer-spooler-service"></a>프린터 스풀러 서비스로 변경 내용 되돌리기  

1.  GPO 변경의 영향을 받는 모든 구성원 서버 또는 워크스테이션에서 로컬로 로그온 합니다.  

2.  마우스를 사용 하 여 포인터를 화면의 오른쪽 위 또는 오른쪽 아래 모서리로 이동 합니다. **참 메뉴** 막대가 표시 되 면 **검색**을 클릭 합니다.  

3.  **검색** 상자에 **서비스**를 입력 하 고 **서비스**를 클릭 합니다.  

4.  **인쇄 스풀러**를 찾아 두 번 클릭 합니다.  

5.  **로그온** 탭을 클릭합니다.  

6.  다음 **으로 로그온**에서 **로컬 시스템** 계정을 선택 하 고 **확인**을 클릭 합니다.  

##### <a name="verify-deny-log-on-locally-gpo-settings"></a>"로컬 로그온 거부" GPO 설정 확인  

1.  GPO 변경의 영향을 받는 모든 구성원 서버 또는 워크스테이션에서 Domain Admins 그룹의 구성원 인 계정을 사용 하 여 로컬 로그온을 시도 합니다. 다음과 유사한 대화 상자가 표시 됩니다.  

    ![보안 도메인 관리자 그룹](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_77.gif)  

##### <a name="verify-deny-log-on-through-remote-desktop-services-gpo-settings"></a>"원격 데스크톱 서비스를 통한 로그온 거부" GPO 설정 확인    
1.  마우스를 사용 하 여 포인터를 화면의 오른쪽 위 또는 오른쪽 아래 모서리로 이동 합니다. **참 메뉴** 막대가 표시 되 면 **검색**을 클릭 합니다.  

2.  **검색** 상자에 **원격 데스크톱 연결**을 입력 하 고 **원격 데스크톱 연결**를 클릭 합니다.  

3.  **컴퓨터** 필드에 연결 하려는 컴퓨터의 이름을 입력 하 고 **연결**을 클릭 합니다. (컴퓨터 이름 대신 IP 주소를 입력할 수도 있습니다.)  

4.  메시지가 표시 되 면 Domain Admins 그룹의 구성원 인 계정에 대 한 자격 증명을 제공 합니다.  

5.  다음과 유사한 대화 상자가 표시 됩니다.  

    ![보안 도메인 관리자 그룹](media/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory/SAD_78.gif)  
