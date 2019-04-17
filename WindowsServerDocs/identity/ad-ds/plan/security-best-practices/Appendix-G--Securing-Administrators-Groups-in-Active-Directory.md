---
ms.assetid: 4baefbd3-038f-44c0-85ba-f24e9722b757
title: "부록 Active Directory의 관리자가 그룹 보안-G"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 4cf89f7bf31ce848de384778b0213d0ddc822158
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="appendix-g-securing-administrators-groups-in-active-directory"></a>부록 g: 관리자가 그룹 Active Directory에 고정

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012


## <a name="appendix-g-securing-administrators-groups-in-active-directory"></a>부록 g: 관리자가 그룹 Active Directory에 고정  
엔터프라이즈 관리자 (EA) 및 도메인 관리자 (DA) 그룹 그대로 기본 제공 (모음) 관리자가 그룹의 회원 빌드 또는 장애 복구 경우에만 받아야 합니다. 없이 일상적인 사용자 계정에에서 있어야 도메인에 대 한 기본 제공 관리자 계정 따르는 관리자가 그룹에 설명 된 대로 보안이 설정 된 경우 [Active Directory에 부록 d: 보안 기본 제공 관리자 계정](../../../ad-ds/plan/security-best-practices/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory.md)합니다.  

관리자는 기본적으로, 대부분의 광고 DS 개체 각 도메인의 소유자는 합니다. 이 그룹의 회원 소유권 또는 개체의 소유권을 가져오는 기능 필요한가 빌드 또는 장애 복구 환경에서 필요할 수 있습니다. 또한 DAs 및 EAs 다양 한 자녀의 권한 및 관리자가 그룹에서 자신의 기본 멤버 자격 않아서 사용 권한을 상속합니다. 기본 그룹 중첩 Active Directory에 권한이 있는 그룹에 대 한 수정 해서는 안을 하 고 각 도메인 관리자가 그룹에 따라 단계별 지침에 설명 된 대로 확보 해야 합니다.  

각 도메인 숲에서 관리자가 그룹 다음과 같습니다.  

1.  그에 설명 된 대로 보안 제공 모든 구성원은 도메인에 대 한 기본 관리자 계정 제외 하 고 있는 관리자가 그룹에서 제거 [Active Directory에 부록 d: 보안 기본 제공 관리자 계정](../../../ad-ds/plan/security-best-practices/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory.md)합니다.  

2.  Ou 포함 된 각 도메인에 워크스테이션과 회원 서버에 연결 된 gpo, DA 그룹에서 다음 사용자 권한에 추가 해야 **컴퓨터 구성 보안 로컬 Policies\ 사용자 권한 할당**:  

    -   네트워크에서이 컴퓨터에 대 한 액세스 거부  

    -   로그온 일괄 작업으로 거부  

    -   로그온 서비스 거부  

3.  각 도메인 숲에서 OU 도메인 컨트롤러에서 관리자가 그룹 다음 사용자 권한은 부여 해야 합니다.  

    -   네트워크에서이 컴퓨터에 액세스  

    -   로컬 로그 허용  

    -   원격 데스크톱 서비스를 통해 로그온 허용  

4.  감사 속성 또는 관리자가 그룹의 회원 수정 되는 경우 알림을 보낼 구성 합니다.  

#### <a name="step-by-step-instructions-for-removing-all-members-from-the-administrators-group"></a>관리자가 그룹의 모든 구성원이 제거에 대 한 단계별 지침  

1.  **서버 관리자**, 클릭 **도구**를 클릭 하 고 **Active Directory 사용자와 컴퓨터**합니다.  

2.  관리자가 그룹의 모든 구성원이 제거 하려면 다음 단계를 수행 합니다.  

    1.  두 번 클릭는 **관리자** 그룹화 하 고 클릭는 **회원** 탭 합니다.  

        ![안전 하 게 관리 그룹](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_79.gif)  

    2.  그룹의 회원을 클릭 **제거**, 클릭 **예**를 클릭 하 고 **확인**합니다.  

3.  관리자가 그룹의 모든 구성원이 제거 될 때까지 2 단계를 반복 합니다.  

#### <a name="step-by-step-instructions-to-secure-administrators-groups-in-active-directory"></a>보안 Active Directory의 관리자가 그룹에 대 한 단계별 지침  

1.  **서버 관리자**, 클릭 **도구**를 클릭 하 고 **그룹 정책 관리**합니다.  

2.  콘솔 트리에서 확장 <Forest>\Domains\\<Domain>, 선택한 다음 **그룹 정책 개체** (여기서 <Forest> 숲의 이름 및 <Domain> 그룹 정책 설정 도메인 이름입니다) 합니다.  

3.  콘솔 트리에서 마우스 오른쪽 단추로 클릭 **그룹 정책 개체**를 클릭 하 고 **새로**합니다.  

    ![안전 하 게 관리 그룹](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_80.gif)  

4.  에 **새 GPO** 대화 상자, 입력 <GPO Name>, 클릭 하 고 **확인** (여기서 *GPO 이름* 이 GPO 이름입니다).  

    ![안전 하 게 관리 그룹](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_81.gif)  

5.  세부 정보 창에서 마우스 오른쪽 단추로 클릭 ** <GPO Name> **를 클릭 하 고 **편집**합니다.  

6.  로 이동 **컴퓨터 구성 보안 로컬 정책**를 클릭 하 고 **사용자 권한 할당**합니다.  

    ![안전 하 게 관리 그룹](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_82.gif)  

7.  관리자가 그룹의 회원 다음을 수행 하 여 네트워크를 통해 워크스테이션과 회원 서버에 하지 않도록 하려면 사용자 권한 구성 합니다.  

    1.  두 번 클릭 **네트워크에서이 컴퓨터에 대 한 액세스 거부** 선택한 **이 정책 설정 정의**합니다.  

    2.  클릭 **사용자 또는 그룹 추가** 클릭 **찾아보기**합니다.  

    3.  입력 **관리자**, 클릭 **이름 확인**를 클릭 하 고 **확인**합니다.  

        ![안전 하 게 관리 그룹](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_83.gif)  

    4.  클릭 **확인**, 및 **확인** 다시 합니다.  

8.  관리자가 그룹의 회원 다음을 수행 하 여 일괄 작업으로 로그온 하지 않도록 하려면 사용자 권한을 구성 합니다.  

    1.  두 번 클릭 **일괄 작업으로 로그온 거부** 선택한 **이 정책 설정 정의**합니다.  

    2.  클릭 **사용자 또는 그룹 추가** 클릭 **찾아보기**합니다.  

    3.  입력 **관리자**, 클릭 **이름 확인**를 클릭 하 고 **확인**합니다.  

        ![안전 하 게 관리 그룹](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_84.gif)  

    4.  클릭 **확인**, 및 **확인** 다시 합니다.  

9. 관리자가 그룹의 회원 다음을 수행 하 여 서비스 로그온 하지 않도록 하려면 사용자 권한을 구성 합니다.  

    1.  두 번 클릭 **로그온 서비스 거부** 선택한 **이 정책 설정 정의**합니다.  

    2.  클릭 **사용자 또는 그룹 추가** 클릭 **찾아보기**합니다.  

    3.  입력 **관리자**, 클릭 **이름 확인**를 클릭 하 고 **확인**합니다.  

        ![안전 하 게 관리 그룹](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_85.gif)  

    4.  클릭 **확인**, 및 **확인** 다시 합니다.  

10. 종료 하려면 **그룹 정책 편집기 관리**, 클릭 **파일**를 클릭 하 고 **종료**합니다.  

11. **그룹 정책 관리**, 다음을 수행 하 여 GPO 구성원 서버 및 Ou 워크스테이션을 연결 합니다.  

    1.  로 이동는 <Forest>\Domains\\<Domain> (여기서 <Forest> 숲의 이름 및 <Domain> 그룹 정책 설정 도메인 이름입니다) 합니다.  

    2.  OU GPO에 적용 되 고 클릭를 마우스 오른쪽 단추로 클릭 **기존 GPO 연결**합니다.  

        ![안전 하 게 관리 그룹](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_86.gif)  

    3.  방금 만든 GPO 선택 하 고 클릭 **확인**합니다.  

        ![안전 하 게 관리 그룹](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_87.gif)  

    4.  모든 일부 조직 구성 단위 워크스테이션 포함 된에 대 한 링크를 만듭니다.  

    5.  모든 일부 조직 구성 단위 구성원 서버를 포함 하는 링크를 만듭니다.  

        > [!IMPORTANT]  
        > 점프 서버 관리 도메인 컨트롤러 및 Active Directory를 사용 하는 경우 점프 서버가이 Gpo 연결 되지 않은에 있는지 확인 합니다.  

        > [!NOTE]  
        > Gpo 관리자가 그룹에서 제한을 구현 하는 경우 Windows는 컴퓨터의 도메인의 관리자가 그룹 뿐 아니라 로컬 관리자가 그룹의 회원 설정을 적용 합니다. 따라서의 관리자가 그룹 제한 구현 하는 경우 주의 사용 해야 합니다. 네트워크, 배치, 및 서비스 로그온 금지 관리자가 그룹의 회원은 어디 것은 구현 하는 것이 좋습니다, 있지만 로컬 로그온 이나 원격 데스크톱 서비스를 통해 로그온 제한 하지 않습니다. 이러한 로그온 형식을 차단 합법적 로컬 관리자가 그룹의 회원 하 여 컴퓨터 관리를 차단할 수 있습니다.  
        >   
        > 기본 제공 로컬 또는 도메인 관리자가 그룹의 오용 뿐 아니라 도메인 관리자 계정 동안의 다음 스크린샷 구성 설정을 내장의 오용 차단 하는 로컬 표시 됩니다. 하는 **로그온 원격 데스크톱 서비스를 통해 거부** 이 설정에 포함 되는 로컬 컴퓨터의 관리자가 그룹의 회원 계정에 대 한 이러한 로그온 차단할 수도 있으므로 사용자 권한 관리자가 그룹 포함 되지 않습니다. 컨텍스트의이 섹션에 설명 된 권한이 있는 그룹에서 실행 하도록 구성 된 컴퓨터에서 서비스 이러한 설정을 구현 발생할 수 있습니다 서비스와 응용 프로그램에 실패 합니다. 따라서이 섹션에서 권장 하는 모든와 같이 완전히 테스트 해야 적용에 대 한 설정을 귀하의 환경에 합니다.  

        ![안전 하 게 관리 그룹](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_88.gif)  

#### <a name="step-by-step-instructions-to-grant-user-rights-to-the-administrators-group"></a>관리자가 그룹에 권한 부여 사용자에 대 한 단계별 지침  

1.  **서버 관리자**, 클릭 **도구**를 클릭 하 고 **그룹 정책 관리**합니다.  

2.  콘솔 트리에서 확장 <Forest>\Domains\\<Domain>, 선택한 다음 **그룹 정책 개체** (여기서 <Forest> 숲의 이름 및 <Domain> 그룹 정책 설정 도메인 이름입니다) 합니다.  

3.  콘솔 트리에서 마우스 오른쪽 단추로 클릭 **그룹 정책 개체**를 클릭 하 고 **새로**합니다.  

    ![안전 하 게 관리 그룹](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_89.gif)  

4.  에 **새 GPO** 대화 상자, 입력 <GPO Name>, 클릭 하 고 **확인** (여기서 <GPO Name> 이 GPO 이름입니다).  

    ![안전 하 게 관리 그룹](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_90.gif)  

5.  세부 정보 창에서 마우스 오른쪽 단추로 클릭 ** <GPO Name> **를 클릭 하 고 **편집**합니다.  

6.  로 이동 **컴퓨터 구성 보안 로컬 정책**를 클릭 하 고 **사용자 권한 할당**합니다.  

    ![안전 하 게 관리 그룹](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_91.gif)  

7.  다음을 수행 하 여 네트워크를 통해 액세스 도메인 컨트롤러에 관리자가 그룹의 회원 수 있도록 사용자 권한을 구성 합니다.  

    1.  두 번 클릭 **네트워크에서이 컴퓨터에 대 한 액세스** 선택한 **이 정책 설정 정의**합니다.  

    2.  클릭 **사용자 또는 그룹 추가** 클릭 **찾아보기**합니다.  

    3.  클릭 **사용자 또는 그룹 추가** 클릭 **찾아보기**합니다.  

        ![안전 하 게 관리 그룹](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_92.gif)  

    4.  클릭 **확인**, 및 **확인** 다시 합니다.  

8.  관리자가 그룹의 회원 다음을 수행 하 여 로컬 로그온 할 수 있도록 사용자 권한을 구성 합니다.  

    1.  두 번 클릭 **로컬 로그온 허용** 선택한 **이 정책 설정 정의**합니다.  

    2.  클릭 **사용자 또는 그룹 추가** 클릭 **찾아보기**합니다.  

    3.  입력 **관리자**를 확인을 클릭 **이름을**를 클릭 하 고 **확인**합니다.  

        ![안전 하 게 관리 그룹](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_93.gif)  

    4.  클릭 **확인**, 및 **확인** 다시 합니다.  

9. 관리자가 그룹의 회원 다음을 수행 하 여 원격 데스크톱 서비스를 통해 로그온 할 수 있도록 사용자 권한을 구성 합니다.  

    1.  두 번 클릭 **원격 데스크톱 서비스를 통해 로그온 허용** 선택한 **이 정책 설정 정의**합니다.  

    2.  클릭 **사용자 또는 그룹 추가** 클릭 **찾아보기**합니다.  

    3.  입력 **관리자**, 클릭 **이름 확인**를 클릭 하 고 **확인**합니다.  

        ![안전 하 게 관리 그룹](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_94.gif)  

    4.  클릭 **확인**, 및 **확인** 다시 합니다.  

10. 종료 하려면 **그룹 정책 편집기 관리**, 클릭 **파일**를 클릭 하 고 **종료**합니다.  

11. **그룹 정책 관리**, 다음을 수행 하 여 GPO OU 도메인 컨트롤러를 연결 합니다.  

    1.  로 이동는 <Forest>\Domains\\<Domain> (여기서 <Forest> 숲의 이름 및 <Domain> 그룹 정책 설정 도메인 이름입니다) 합니다.  

    2.  마우스 오른쪽 단추로 클릭 한 OU 도메인 컨트롤러 **기존 GPO 연결**합니다.  

        ![안전 하 게 관리 그룹](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_95.gif)  

    3.  방금 만든 GPO 선택 하 고 클릭 **확인**합니다.  

        ![안전 하 게 관리 그룹](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_96.gif)  

#### <a name="verification-steps"></a>확인 단계  

##### <a name="verify-deny-access-to-this-computer-from-the-network-gpo-settings"></a>"액세스 거부가이 컴퓨터에는 네트워크에서" GPO 설정 확인  
모든 구성원이 서버 또는 (예: "점프 서버)" GPO 변경 영향을 받지 않는 워크스테이션 구성원 서버 또는 워크스테이션 GPO 변경 사항을 영향을 받는 네트워크를 통해 액세스 하려고 합니다. 시스템 드라이브를 사용 하 여 지도를 시도 GPO 설정을 확인 하 고 **NET 사용** 명령 합니다.  

1.  로컬 관리자가 그룹 구성원 계정을 사용 하 여 로그온 합니다.  

2.  마우스를 사용 하 여 포인터를 화면 오른쪽 위로 옮겼다가 또는 오른쪽 하단 모서리에 이동 합니다. 때는 **참** 클릭 표시줄이 나타날 **검색**합니다.  

3.  **검색** 상자에 입력 **명령 프롬프트**를 마우스 오른쪽 단추로 클릭 **명령 프롬프트**, 클릭 한 다음 **관리자 권한으로 실행** 관리자 권한 명령 프롬프트를 엽니다.  

4.  를 상승 승인 하 라는 메시지가 나타나면 클릭 **예**합니다.  

    ![안전 하 게 관리 그룹](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_97.gif)  

5.  에 **명령 프롬프트** 창, 입력 **사용 net \\\<Server Name>\c$**, 여기서 <Server Name> 구성원 서버 또는 워크스테이션 네트워크를 통해 액세스를 시도 하는 이름입니다.  

6.  다음 스크린샷 표시 되 고 오류 메시지가 표시 됩니다.  

    ![안전 하 게 관리 그룹](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_98.gif)  

##### <a name="verify-deny-log-on-as-a-batch-job-gpo-settings"></a>"로그온 거부 일괄 작업으로" GPO 설정 확인  
모든 구성원이 서버 또는 워크스테이션 GPO 변경 영향을 로컬로 로그온 합니다.  

###### <a name="create-a-batch-file"></a>배치 파일을 만들어  

1.  마우스를 사용 하 여 포인터를 화면 오른쪽 위로 옮겼다가 또는 오른쪽 하단 모서리에 이동 합니다. 때는 **참** 클릭 표시줄이 나타날 **검색**합니다.  

2.  에 **검색** 상자에 입력 **메모장**를 클릭 하 고 **메모장**합니다.  

3.  **메모장**, 입력 **디렉터리 c:**합니다.  

4.  클릭 **파일**를 클릭 하 고 **다른 이름으로 저장**합니다.  

5.  **파일 이름** 필드를 입력 ** <Filename>.bat** (여기서 <Filename> 새 배치 파일 이름).  

###### <a name="schedule-a-task"></a>작업을 예약  

1.  마우스를 사용 하 여 포인터를 화면 오른쪽 위로 옮겼다가 또는 오른쪽 하단 모서리에 이동 합니다. 때는 **참** 클릭 표시줄이 나타날 **검색**합니다.  

2.  에 **검색** 상자에 입력 **작업 스케줄러**를 클릭 하 고 **작업 스케줄러**합니다.  

    > [!NOTE]  
    > 검색 상자에 Windows 8을 실행 하는 컴퓨터에서 예약 작업을 입력 하 고 예약 작업을 누릅니다.  

3.  클릭 **알림**를 클릭 하 고 **작업 만들기**합니다.  

4.  **작업 만들기** 대화 상자에서 입력 ** <Task Name> ** (여기서 <Task Name> 새 작업의 이름) 합니다.  

5.  클릭는 **작업** 탭 및 클릭 **새로**합니다.  

6.  에 **알림** 필드를 **프로그램 시작**합니다.  

7.  에 **프로그램/스크립트** 필드를 클릭 **찾아보기**을 찾아에서 만든 배치 파일 선택는 **배치 파일을 만들어** 섹션을 클릭 **열기**합니다.  

8.  클릭 **확인**합니다.  

9. 클릭 하 고 **일반** 탭 합니다.  

10. 에 **보안 옵션** 필드를 클릭 **사용자 또는 그룹 변경**합니다.  

11. 관리자가 그룹의 회원은 계정의 이름을 입력 합니다 **이름 확인**를 클릭 하 고 **확인**합니다.  

12. 선택 **사용자가 로그인된 onor 여부 실행** 및 **암호를 저장 하지 않는**합니다. 작업 로컬 컴퓨터 리소스에 액세스할 수 있는 기간은 됩니다.  

13. 클릭 **확인**합니다.  

14. 작업을 실행 하 요청 하는 사용자 계정 자격 대화 상자가 표시 됩니다.  

15. 암호를 입력 한 후 클릭 **확인**합니다.  

16. 다음과 비슷합니다 대화 상자가 나타나면 정상입니다.  

    ![안전 하 게 관리 그룹](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_99.gif)  

##### <a name="verify-deny-log-on-as-a-service-gpo-settings"></a>"로그온 거부 as a service" GPO 설정 확인  

1.  모든 구성원이 서버 또는 워크스테이션 GPO 변경 영향을 로컬로 로그온 합니다.  

2.  마우스를 사용 하 여 포인터를 화면 오른쪽 위로 옮겼다가 또는 오른쪽 하단 모서리에 이동 합니다. 때는 **참** 클릭 표시줄이 나타날 **검색**합니다.  

3.  에 **검색** 상자에 입력 **서비스**를 클릭 하 고 **서비스**합니다.  

4.  찾아 두 번 클릭 **인쇄 스풀러**합니다.  

5.  클릭 하 고 **로그온** 탭 합니다.  

6.  에 **로 로그온** 필드를 **이 계정**합니다.  

7.  클릭 **찾아보기**, 관리자가 그룹의 회원은 계정의 이름을 입력 합니다 **이름 확인**를 클릭 하 고 **확인**합니다.  

8.  에 **암호** 및 **암호 확인** 필드를 입력 하 여 선택한 계정의 암호를 클릭 한 **확인**합니다.  

9. 클릭 **확인** 세 번 합니다.  

10. 마우스 오른쪽 단추로 클릭 **인쇄 스풀러** 클릭 **다시 시작**합니다.  

11. 서비스를 다시 시작 하면 다음과 비슷합니다 대화 상자가 나타나면 정상입니다.  

    ![안전 하 게 관리 그룹](media/Appendix-G--Securing-Administrators-Groups-in-Active-Directory/SAD_100.png)  

##### <a name="revert-changes-to-the-printer-spooler-service"></a>되돌리기 프린터 스풀러 서비스에 대 한 변경  

1.  모든 구성원이 서버 또는 워크스테이션 GPO 변경 영향을 로컬로 로그온 합니다.  

2.  마우스를 사용 하 여 포인터를 화면 오른쪽 위로 옮겼다가 또는 오른쪽 하단 모서리에 이동 합니다. 때는 **참** 클릭 표시줄이 나타날 **검색**합니다.  

3.  에 **검색** 상자에 입력 **서비스**를 클릭 하 고 **서비스**합니다.  

4.  찾아 두 번 클릭 **인쇄 스풀러**합니다.  

5.  클릭 하 고 **로그온** 탭 합니다.  

6.  에 **로 로그온** 필드를 클릭 **로컬 시스템** 계정, 클릭 한 **확인**합니다.  
