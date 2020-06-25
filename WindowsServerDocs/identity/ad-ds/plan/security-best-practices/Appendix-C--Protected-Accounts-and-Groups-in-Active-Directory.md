---
ms.assetid: 5b2876ac-fe7d-4054-bfba-b692e57bc0d2
title: Active Directory의 부록 C 보호 된 계정 및 그룹
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 18a293f4ec7d96516bd89396c13562ba68dc471f
ms.sourcegitcommit: a1641b80c88205c0253f354f2d427d77bb879643
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85345437"
---
# <a name="appendix-c-protected-accounts-and-groups-in-active-directory"></a>부록 C: Active Directory의 보호된 계정 및 그룹

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

## <a name="appendix-c-protected-accounts-and-groups-in-active-directory"></a>부록 C: Active Directory의 보호된 계정 및 그룹

Active Directory 내에서 높은 권한 있는 계정 및 그룹의 기본 집합은 보호 된 계정 및 그룹으로 간주 됩니다. Active Directory에서 대부분의 개체를 사용 하는 경우 위임 된 관리자 (Active Directory 개체를 관리 하는 권한을 위임 받은 사용자)는 그룹의 멤버 자격을 변경할 수 있는 권한 변경을 포함 하 여 개체에 대 한 사용 권한을 변경할 수 있습니다 (예:).  

그러나 보호 된 계정 및 그룹을 사용 하는 경우 개체에 대 한 사용 권한이 디렉터리에서 이동 되더라도 개체에 대 한 사용 권한이 일관 되 게 유지 되도록 하는 자동 프로세스를 통해 개체의 사용 권한이 설정 되 고 적용 됩니다. 사용자가 보호 된 개체의 사용 권한을 수동으로 변경 하는 경우에도이 프로세스를 사용 하면 권한이 기본값으로 빠르게 반환 됩니다.  

### <a name="protected-groups"></a>보호 된 그룹

다음 표에는 도메인 컨트롤러 운영 체제에 나열 된 Active Directory의 보호 된 그룹이 포함 되어 있습니다.  

#### <a name="protected-accounts-and-groups-in-active-directory-by-operating-system"></a>운영 체제에서 Active Directory의 보호 된 계정 및 그룹

| Windows Server 2003 RTM | Windows Server 2003 SP1 이상 | Windows Server 2012, <br> Windows Server 2008 R2, <br> Windows Server 2008 | Windows Server 2016 |
| --- | --- | --- | --- |
|Account Operators|Account Operators|Account Operators|Account Operators|
|관리자|관리자|관리자|관리자|
|관리자|관리자|관리자|관리자|
|Backup Operators|Backup Operators|Backup Operators|Backup Operators|
|Cert Publishers|||
|도메인 관리자|도메인 관리자|도메인 관리자|도메인 관리자|
|도메인 컨트롤러 하나 이상|도메인 컨트롤러 하나 이상|도메인 컨트롤러 하나 이상|도메인 컨트롤러 하나 이상|
|엔터프라이즈 관리자|엔터프라이즈 관리자|엔터프라이즈 관리자|엔터프라이즈 관리자|
|Krbtgt|Krbtgt|Krbtgt|Krbtgt|
|Print Operators|Print Operators|Print Operators|Print Operators|
|||Read-only Domain Controllers|Read-only Domain Controllers|
|Replicator|Replicator|Replicator|Replicator|
|Schema Admins|Schema Admins|Schema Admins|Schema Admins|
|Server Operators|Server Operators|Server Operators|Server Operators|

#### <a name="adminsdholder"></a>AdminSDHolder

AdminSDHolder 개체의 목적은 도메인의 보호 된 계정 및 그룹에 대 한 "템플릿" 권한을 제공 하는 것입니다. AdminSDHolder는 모든 Active Directory 도메인의 시스템 컨테이너에 개체로 자동으로 생성 됩니다. 경로는 **cn = AdminSDHolder, cn = System, dc =<domain_component>, dc =<domain_component>?입니다** .  

Administrators 그룹에서 소유 하는 Active Directory 도메인의 대부분 개체와 달리 AdminSDHolder는 Domain Admins 그룹에서 소유 합니다. 기본적으로 EAs는 도메인의 도메인 관리자 및 관리자 그룹이 될 때 도메인의 모든 AdminSDHolder 개체를 변경할 수 있습니다. 또한 AdminSDHolder의 기본 소유자는 도메인의 Domain Admins 그룹 이지만 Administrators 또는 Enterprise Admins의 구성원은 개체의 소유권을 가져올 수 있습니다.  

#### <a name="sdprop"></a>SDProp

SDProp는 도메인의 PDC 에뮬레이터 (PDCE)를 보유 하는 도메인 컨트롤러에서 60 분 마다 (기본적으로) 실행 되는 프로세스입니다. SDProp는 도메인의 AdminSDHolder 개체에 대 한 사용 권한을 보호 된 계정 및 도메인의 그룹에 대 한 권한과 비교 합니다. 보호 된 계정 및 그룹에 대 한 사용 권한이 AdminSDHolder 개체에 대 한 사용 권한과 일치 하지 않으면 보호 된 계정 및 그룹에 대 한 사용 권한이 도메인의 AdminSDHolder 개체와 일치 하도록 다시 설정 됩니다.  

또한 보호 된 그룹 및 계정에 대 한 사용 권한 상속이 사용 하지 않도록 설정 되어 있습니다. 즉, 계정 및 그룹이 디렉터리의 다른 위치로 이동 하더라도 새 부모 개체에서 사용 권한을 상속 하지 않습니다. 부모 개체에 대 한 사용 권한이 AdminSDHolder의 사용 권한을 변경 하지 않도록 AdminSDHolder 개체에 대 한 상속을 사용할 수 없습니다.  

##### <a name="changing-sdprop-interval"></a>SDProp 간격 변경

일반적으로 테스트 목적을 제외 하 고 SDProp가 실행 되는 간격을 변경할 필요가 없습니다. SDProp 간격을 변경 해야 하는 경우 도메인의 PDCE에서 regedit를 사용 하 여 Hklm\system\currentcontrolset\services\ntds\parameters에서 AdminSDProtectFrequency DWORD 값을 추가 하거나 수정 합니다.  

값의 범위는 60에서 7200 사이 (1 ~ 2 시간)입니다. 변경을 취소 하려면 AdminSDProtectFrequency 키를 삭제 합니다. 그러면 SDProp가 다시 60 분 간격으로 되돌아갑니다. 일반적으로 도메인 컨트롤러에서 LSASS 처리 오버 헤드를 늘릴 수 있으므로 프로덕션 도메인에서이 간격을 줄여야 하는 것은 아닙니다. 이러한 증가의 영향은 도메인에 있는 보호 된 개체의 수에 따라 달라 집니다.  

##### <a name="running-sdprop-manually"></a>수동으로 SDProp 실행

AdminSDHolder 변경을 테스트 하는 더 좋은 방법은 SDProp를 수동으로 실행 하는 것입니다. 이렇게 하면 작업이 즉시 실행 되지만 예약 된 실행에는 영향을 주지 않습니다. SDProp을 수동으로 실행 하는 것은 windows server 2008를 실행 하는 도메인 컨트롤러와 windows server 2012 또는 Windows Server 2008 r 2를 실행 하는 도메인 컨트롤러에 있는 것 보다 조금 다르게 수행 됩니다.  

이전 운영 체제에서 SDProp를 수동으로 실행 하는 절차는 [Microsoft 지원 문서 251343](https://support.microsoft.com/kb/251343)에 제공 되며, 다음은 이전 버전 이상의 운영 체제에 대 한 단계별 지침입니다. 두 경우 모두 Active Directory에서 rootDSE 개체에 연결 하 고 rootDSE 개체에 대해 null DN을 사용 하 여 수정 작업을 수행 하 고 작업 이름을 수정할 특성으로 지정 해야 합니다. RootDSE 개체의 수정 가능한 작업에 대 한 자세한 내용은 MSDN 웹 사이트에서 [Rootdse 수정 작업](https://msdn.microsoft.com/library/cc223297.aspx) 을 참조 하세요.  

###### <a name="running-sdprop-manually-in-windows-server-2008-or-earlier"></a>Windows Server 2008 이전 버전에서 수동으로 SDProp 실행

Ldp.exe를 사용 하거나 LDAP 수정 스크립트를 실행 하 여 SDProp를 강제로 실행할 수 있습니다. Ldp.exe를 사용 하 여 SDProp를 실행 하려면 도메인에서 AdminSDHolder 개체를 변경한 후 다음 단계를 수행 합니다.  

1. **Ldp.exe**를 시작 합니다.  
2. Ldp 대화 상자에서 **연결** 을 클릭 하 고 **연결**을 클릭 합니다.  

   ![보호 된 계정 및 그룹](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_9.gif)  

3. **연결** 대화 상자에서 PDCE (PDC 에뮬레이터) 역할을 보유 하는 도메인에 대 한 도메인 컨트롤러의 이름을 입력 하 고 **확인**을 클릭 합니다.  

   ![보호 된 계정 및 그룹](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_10.png)  

4. 다음 스크린샷에서 **Dn: (RootDSE)** 에 표시 된 대로 성공적으로 연결 되었는지 확인 하 고 **연결** 을 클릭 한 다음 **바인딩**을 클릭 합니다.  

   ![보호 된 계정 및 그룹](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_11.png)  

5. **바인딩** 대화 상자에서 rootDSE 개체를 수정할 수 있는 권한이 있는 사용자 계정의 자격 증명을 입력 합니다. 해당 사용자로 로그온 한 경우 현재 로그온 한 사용자 **로 바인딩** 을 선택할 수 있습니다. **확인을**클릭 합니다.  

   ![보호 된 계정 및 그룹](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_12.png)  

6. 바인딩 작업을 완료 한 후 **찾아보기**를 클릭 하 고 **수정**을 클릭 합니다.  

   ![보호 된 계정 및 그룹](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_13.png)  

7. **수정** 대화 상자에서 **DN** 필드를 비워 둡니다. **항목 편집 특성** 필드에 **fixupinheritance**를 입력 하 고 **값** 필드에 **예**를 입력 합니다. **Enter 키** 를 클릭 하 여 다음 스크린샷에서와 같이 **항목 목록을** 채웁니다.  

   ![보호 된 계정 및 그룹](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_14.gif)  

8. 채워진 수정 대화 상자에서 실행을 클릭 하 고 AdminSDHolder 개체에 대 한 변경 내용이 해당 개체에 표시 되는지 확인 합니다.  

> [!NOTE]  
> 지정 된 권한 없는 계정이 보호 된 그룹의 멤버 자격을 수정할 수 있도록 AdminSDHolder를 수정 하는 방법에 대 한 자세한 내용은 [부록 I: 보호 된 계정 및 그룹에 대 한 관리 계정 만들기 Active Directory](../../../ad-ds/manage/component-updates/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory.md)를 참조 하세요.  

LDIFDE 또는 스크립트를 통해 SDProp를 수동으로 실행 하려는 경우 다음과 같이 수정 항목을 만들 수 있습니다.  

![보호 된 계정 및 그룹](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_15.gif)  

###### <a name="running-sdprop-manually-in-windows-server-2012-or-windows-server-2008-r2"></a>Windows Server 2012 또는 Windows Server 2008 r 2에서 수동으로 SDProp 실행

Ldp.exe를 사용 하거나 LDAP 수정 스크립트를 실행 하 여 SDProp를 강제로 실행할 수도 있습니다. Ldp.exe를 사용 하 여 SDProp를 실행 하려면 도메인에서 AdminSDHolder 개체를 변경한 후 다음 단계를 수행 합니다.  

1. **Ldp.exe**를 시작 합니다.  

2. **Ldp** 대화 상자에서 **연결**을 클릭 하 고 **연결**을 클릭 합니다.  

   ![보호 된 계정 및 그룹](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_16.gif)  

3. **연결** 대화 상자에서 PDCE (PDC 에뮬레이터) 역할을 보유 하는 도메인에 대 한 도메인 컨트롤러의 이름을 입력 하 고 **확인**을 클릭 합니다.  

   ![보호 된 계정 및 그룹](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_17.gif)  

4. 다음 스크린샷에서 **Dn: (RootDSE)** 에 표시 된 대로 성공적으로 연결 되었는지 확인 하 고 **연결** 을 클릭 한 다음 **바인딩**을 클릭 합니다.  

   ![보호 된 계정 및 그룹](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_18.gif)  

5. **바인딩** 대화 상자에서 rootDSE 개체를 수정할 수 있는 권한이 있는 사용자 계정의 자격 증명을 입력 합니다. 해당 사용자로 로그온 한 경우 **현재 로그온 한 사용자로 바인딩**을 선택할 수 있습니다. **확인을**클릭 합니다.  

   ![보호 된 계정 및 그룹](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_19.gif)  

6. 바인딩 작업을 완료 한 후 **찾아보기**를 클릭 하 고 **수정**을 클릭 합니다.  

   ![보호 된 계정 및 그룹](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_20.gif)  

7. **수정** 대화 상자에서 **DN** 필드를 비워 둡니다. **항목 편집 특성** 필드에 **RunProtectAdminGroupsTask**를 입력 하 고 **값** 필드에 **1**을 입력 합니다. **Enter 키** 를 클릭 하 여 여기에 표시 된 대로 항목 목록을 채웁니다.  

   ![보호 된 계정 및 그룹](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_21.gif)  

8. 채워진 **수정** 대화 상자에서 **실행**을 클릭 하 고 AdminSDHolder 개체에 대 한 변경 내용이 해당 개체에 표시 되는지 확인 합니다.  

LDIFDE 또는 스크립트를 통해 SDProp를 수동으로 실행 하려는 경우 다음과 같이 수정 항목을 만들 수 있습니다.  

![보호 된 계정 및 그룹](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_22.gif)  
