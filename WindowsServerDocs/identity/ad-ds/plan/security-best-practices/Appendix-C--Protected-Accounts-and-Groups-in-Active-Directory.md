---
ms.assetid: 5b2876ac-fe7d-4054-bfba-b692e57bc0d2
title: 부록 C-보호 된 계정 및 Active Directory의 그룹
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 70e29ad42b57cf315c7179d6eea8220ad2bfab48
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59834704"
---
# <a name="appendix-c-protected-accounts-and-groups-in-active-directory"></a>부록 C: 보호 된 계정 및 Active Directory의 그룹

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

## <a name="appendix-c-protected-accounts-and-groups-in-active-directory"></a>부록 C: 보호 된 계정 및 Active Directory의 그룹

Active Directory 내에서 보호 된 계정 및 그룹 권한이 높은 계정 및 그룹의 기본 집합으로 간주 됩니다. Active Directory에서 대부분의 개체를 사용 하 여 위임 된 관리자 (위임 된 권한이 Active Directory 개체를 관리할 수 있는 사용자)의 구성원을 변경 하려면 자체를 허용 하도록 사용 권한을 변경 하는 등의 개체에 대 한 권한을 변경할 수 있습니다. 예를 들어 그룹입니다.  

그러나 보호 된 계정 및 그룹을 사용 하 여 개체의 사용 권한 설정 및 적용 하면 일관 된 개체가 있는 경우에 개체 계속에 대 한 권한을 디렉터리를 이동 하는 자동 프로세스를 통해. 누군가가 보호 된 개체의 사용 권한을 수동으로 변경, 경우에 이렇게 사용 권한이 기본값으로 신속 하 게 반환 됩니다.  

### <a name="protected-groups"></a>보호 된 그룹

다음 표에서 도메인 컨트롤러 운영 체제에서 나열 된 Active Directory의 보호 된 그룹을 보여 줍니다.  

#### <a name="protected-accounts-and-groups-in-active-directory-by-operating-system"></a>운영 체제에서 Active Directory의 보호 된 계정 및 그룹

| Windows Server 2003 RTM | Windows Server 2003 SP1+ | Windows Server 2012, <br> Windows Server 2008 R2, <br> Windows Server 2008 | Windows Server 2016 |
| --- | --- | --- | --- |
|Account Operators|Account Operators|Account Operators|Account Operators|
|관리자|관리자|관리자|관리자|
|Administrators|Administrators|Administrators|Administrators|
|Backup Operators|Backup Operators|Backup Operators|Backup Operators|
|Cert Publishers|||
|Domain Admins|Domain Admins|Domain Admins|Domain Admins|
|도메인 컨트롤러 하나 이상|도메인 컨트롤러 하나 이상|도메인 컨트롤러 하나 이상|도메인 컨트롤러 하나 이상|
|Enterprise Admins|Enterprise Admins|Enterprise Admins|Enterprise Admins|
||||엔터프라이즈 키 관리|
||||키 관리자|
|Krbtgt|Krbtgt|Krbtgt|Krbtgt|
|Print Operators|Print Operators|Print Operators|Print Operators|
|||Read-only Domain Controllers|Read-only Domain Controllers|
|Replicator|Replicator|Replicator|Replicator|
|Schema Admins|Schema Admins|Schema Admins|Schema Admins|
|Server Operators|Server Operators|Server Operators|Server Operators|

#### <a name="adminsdholder"></a>AdminSDHolder

AdminSDHolder 개체의 목적은 보호 된 계정 및 도메인에서 그룹에 대 한 "템플릿" 사용 권한을 제공 하는 것입니다. AdminSDHolder 개체의 모든 Active Directory 도메인 시스템 컨테이너에 자동으로 만들어집니다. 해당 경로: **CN=AdminSDHolder,CN=System,DC=<domain_component>,DC=<domain_component>?.**  

Active Directory 도메인의 소유 하는 Administrators 그룹, 대부분의 개체와 달리 AdminSDHolder는 Domain Admins 그룹에 의해 소유 됩니다. 기본적으로 eas에서는 변경할 수 모든 도메인의 AdminSDHolder 개체에 도메인의 Domain Admins 및 Administrators 그룹 수 있습니다. 또한 AdminSDHolder의 기본 소유자는 도메인의 Domain Admins 그룹, 관리자 또는 Enterprise Admins의 구성원 개체의 소유권을 걸릴 수 있습니다.  

#### <a name="sdprop"></a>SDProp

SDProp는 도메인의 PDC 에뮬레이터 (PDCE)를 보유 하는 도메인 컨트롤러에 기본적으로 60 분 마다 실행 하는 프로세스입니다. SDProp 보호 된 계정 및 도메인에서 그룹에 대 한 권한 사용 하 여 도메인의 AdminSDHolder 개체에 대 한 권한을 비교합니다. 보호 된 계정 및 그룹에 대 한 권한을 AdminSDHolder 개체에 대 한 권한을 일치 하지 않으면, 보호 된 계정 및 그룹에 대 한 권한은 도메인의 AdminSDHolder 개체의과 일치 하도록 다시 설정 됩니다.  

또한 사용 권한 상속이 비활성화 되어 보호 되는 그룹 및 계정에는 계정 및 그룹을 디렉터리에서 다른 위치로 이동, 경우에 해당 권한을 상속 하지 않는 새 부모 개체로에서 즉 있습니다. 부모 개체에 대 한 사용 권한 변경 AdminSDHolder의 권한은 변경 되지 않습니다 있도록 상속은 AdminSDHolder 개체에 사용할 수 없습니다.  

##### <a name="changing-sdprop-interval"></a>SDProp 간격 변경

일반적으로 테스트 목적으로 제외 하 고는 SDProp 실행 간격을 변경할 필요가 없습니다. 도메인에 대해 PDCE에 SDProp 간격을 변경 해야 할 경우 regedit를 사용 하 여 추가 하거나 HKLM\SYSTEM\CurrentControlSet\Services\NTDS\Parameters AdminSDProtectFrequency DWORD 값을 수정 합니다.  

값의 범위는 7200 (2 시간 1 분)에 60에서 초입니다. 변경 내용이 되돌리려면 60 분 간격으로 다시 되돌리려면 SDProp 그러면 AdminSDProtectFrequency 키를 삭제 합니다. 일반적으로 줄이지 않아야이 간격 프로덕션 도메인에 도메인 컨트롤러에서 처리 오버 헤드가 LSASS 강화 수 있습니다. 이 처럼 증가의 영향을 도메인에서 보호 되는 개체의 수에 따라 달라 집니다.  

##### <a name="running-sdprop-manually"></a>SDProp를 수동으로 실행

AdminSDHolder 변경 내용을 테스트에 더 나은 방법은 작업이 즉시 실행 되도록 있지만 예약 된 실행에 영향을 주지 않습니다 SDProp를 수동으로 실행 하는 것입니다. SDProp를 수동으로 실행 하는 것은 Windows Server 2008 실행 도메인 컨트롤러에서 약간 다르게 수행 되며 Windows Server 2012 또는 Windows Server 2008 R2를 실행 하는 도메인 컨트롤러에 있는 것 보다 이전입니다.  

이전 운영 체제에서 SDProp를 수동으로 실행 하는 절차에 나와 [Microsoft 지원 문서 251343](https://support.microsoft.com/kb/251343), 다음은 이전 버전과 최신 운영 체제에 대 한 단계별 지침 및 합니다. 두 경우 모두에서 Active Directory에서 rootDSE 개체에 연결 하 고 수정할 특성으로 작업의 이름을 지정 rootDSE 개체에 대 한 null DN 사용 하 여 수정 작업을 수행 합니다. RootDSE 개체에서 수정할 수 있는 작업에 대 한 자세한 내용은 참조 하세요. [rootDSE 수정 작업](https://msdn.microsoft.com/library/cc223297.aspx) MSDN 웹 사이트입니다.  

###### <a name="running-sdprop-manually-in-windows-server-2008-or-earlier"></a>Windows Server 2008 또는 이전에 수동으로 실행 SDProp

Ldp.exe를 사용 하 여 또는 LDAP 수정 스크립트를 실행 하 여를 실행 하는 SDProp를 강제로 수 있습니다. Ldp.exe를 사용 하 여 SDProp를 실행 하려면 도메인의 AdminSDHolder 개체에 변경 내용을 수행한 후 다음 단계를 수행 합니다.  

1. 시작할 **Ldp.exe**합니다.  
2. 클릭 **연결** Ldp 대화 상자를 클릭 **Connect**합니다.  

   ![보호 된 계정 및 그룹](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_9.gif)  

3. 에 **Connect** 대화 상자, PDC 에뮬레이터 (PDCE) 역할을 보유 하는 도메인에 대 한 도메인 컨트롤러의 이름을 입력 하 고, 클릭 **확인**합니다.  

   ![보호 된 계정 및 그룹](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_10.png)  

4. 표시 된 대로 성공적으로 연결 확인 **Dn: (RootDSE)**  클릭 한 다음 스크린 샷에서 **연결** 클릭 **바인딩할**합니다.  

   ![보호 된 계정 및 그룹](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_11.png)  

5. 에 **바인딩** 대화 상자, rootDSE 개체를 수정할 수 있는 권한을 가진 사용자 계정의 자격 증명을 입력 합니다. (해당 사용자로 로그온 하는 경우 선택할 수 있습니다 **으로 바인딩하고** 현재 로그온 한 사용자입니다.) **확인**을 클릭합니다.  

   ![보호 된 계정 및 그룹](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_12.png)  

6. 바인딩 작업을 완료 한 후 클릭 **찾아보기**, 클릭 **수정**합니다.  

   ![보호 된 계정 및 그룹](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_13.png)  

7. 에 **수정** 대화 상자에서를 **DN** 필드를 비워 합니다. 에 **항목 편집 특성** 필드에 입력 **FixUpInheritance**, 및를 **값** 필드에 입력 **예**합니다. 클릭 **Enter** 채우는 합니다 **항목 목록** 다음 스크린 샷과 같이 합니다.  

   ![보호 된 계정 및 그룹](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_14.gif)  

8. 채워진된 수정 대화 상자에서 실행을 클릭 하 고 해당 개체에 AdminSDHolder 개체에 대 한 변경 내용을 표시를 확인 합니다.  

> [!NOTE]  
> 지정 된 특권된 계정 보호 그룹의 구성원을 수정할 수 있도록 AdminSDHolder를 수정 하는 방법에 대 한 내용은 [부록 i: 계정 및 Active Directory에서 그룹 보호에 대 한 관리 계정을 만드는](../../../ad-ds/manage/component-updates/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory.md)합니다.  

LDIFDE 또는 스크립트를 통해 SDProp를 수동으로 실행 하려는 경우에 다음과 같이 수정 항목을 만들 수 있습니다.  

![보호 된 계정 및 그룹](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_15.gif)  

###### <a name="running-sdprop-manually-in-windows-server-2012-or-windows-server-2008-r2"></a>Windows Server 2012 또는 Windows Server 2008 R2에서 SDProp를 수동으로 실행

Ldp.exe를 사용 하 여 또는 LDAP 수정 스크립트를 실행 하 여를 실행 하는 SDProp를 강제로 수도 있습니다. Ldp.exe를 사용 하 여 SDProp를 실행 하려면 도메인의 AdminSDHolder 개체에 변경 내용을 수행한 후 다음 단계를 수행 합니다.  

1. 시작할 **Ldp.exe**합니다.  

2. 에 **Ldp** 대화 상자, 클릭 **연결**, 클릭 **연결**합니다.  

   ![보호 된 계정 및 그룹](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_16.gif)  

3. 에 **Connect** 대화 상자, PDC 에뮬레이터 (PDCE) 역할을 보유 하는 도메인에 대 한 도메인 컨트롤러의 이름을 입력 하 고, 클릭 **확인**합니다.  

   ![보호 된 계정 및 그룹](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_17.gif)  

4. 표시 된 대로 성공적으로 연결 확인 **Dn: (RootDSE)**  클릭 한 다음 스크린 샷에서 **연결** 클릭 **바인딩할**합니다.  

   ![보호 된 계정 및 그룹](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_18.gif)  

5. 에 **바인딩** 대화 상자, rootDSE 개체를 수정할 수 있는 권한을 가진 사용자 계정의 자격 증명을 입력 합니다. (해당 사용자로 로그온 하는 경우 선택할 수 있습니다 **현재 로그온 한 사용자의 바인딩**.) **확인**을 클릭합니다.  

   ![보호 된 계정 및 그룹](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_19.gif)  

6. 바인딩 작업을 완료 한 후 클릭 **찾아보기**, 클릭 **수정**합니다.  

   ![보호 된 계정 및 그룹](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_20.gif)  

7. 에 **수정** 대화 상자에서를 **DN** 필드를 비워 합니다. 에 **항목 편집 특성** 필드에 입력 **RunProtectAdminGroupsTask**, 및를 **값** 필드에 입력 **1**합니다. 클릭 **Enter** 다음과 같이 항목 목록을 채우는 데 있습니다.  

   ![보호 된 계정 및 그룹](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_21.gif)  

8. 채워진 **수정** 대화 상자, 클릭 **실행**, AdminSDHolder 개체에 대 한 변경 내용을 해당 개체에 표시를 확인 합니다.  

LDIFDE 또는 스크립트를 통해 SDProp를 수동으로 실행 하려는 경우에 다음과 같이 수정 항목을 만들 수 있습니다.  

![보호 된 계정 및 그룹](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_22.gif)  
