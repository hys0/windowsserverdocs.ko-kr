---
ms.assetid: 5b2876ac-fe7d-4054-bfba-b692e57bc0d2
title: "부록 C-계정과 그룹 Active Directory에 보호"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: c1d29b61844428115f8b2d1f5d935f225a249659
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="appendix-c-protected-accounts-and-groups-in-active-directory"></a>부록 c: 보호 계정과 그룹 Active Directory에

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012


## <a name="appendix-c-protected-accounts-and-groups-in-active-directory"></a>부록 c: 보호 계정과 그룹 Active Directory에  
Active Directory 내에서 보호 된 계정 및 그룹 권한이 높은 계정과 그룹의 기본 설정으로 간주 됩니다. 대부분의 Active Directory 개체 위임된 관리자 (된 Active Directory 개체를 관리할 수 있는 위임된 권한이 있는 사용자), 그룹의 등록 예를 들어 변경 하려면 자체 수 있는 권한을 변경 하는 등의 개체의 사용 권한 변경할 수 있습니다.  

그러나 보호 계정 및 그룹으로 개체의 권한은 설정 되 고 자동 하면 개체 경우에 일관 되 게 개체 유지에 대 한 권한을 디렉터리 이동 하는 프로세스를 통해 적용 합니다. 누군가가 수동으로 보호 개체의 사용 권한 변경 내용, 하는 경우에 이렇게 권한을 기본값으로 신속 하 게 반환 됩니다.  

### <a name="protected-groups"></a>보호 되는 그룹  
다음 표에서 도메인 컨트롤러 운영 체제에서 나열 된 Active Directory에 보호 그룹 합니다.  

**보호 된 계정 및 운영 체제에 대 한 Active Directory에 그룹**  

|||||  
|-|-|-|-|  
|**Windows 2000 < s p 4**|**Windows 2000 s p 4-Windows Server 2003 RTM**|**Windows Server 2003 s p 1 +**|**Windows Server 2012, Windows Server 2008 R2, Windows Server 2008**|  
|관리자|계정에서|계정에서|계정에서|  
||관리자|관리자|관리자|  
||관리자|관리자|관리자|  
||백업 관리자|백업 관리자|백업 관리자|  
||인증 게시자|||  
|도메인 관리|도메인 관리|도메인 관리|도메인 관리|  
||도메인 컨트롤러|도메인 컨트롤러|도메인 컨트롤러|  
|엔터프라이즈 관리|엔터프라이즈 관리|엔터프라이즈 관리|엔터프라이즈 관리|  
||Krbtgt|Krbtgt|Krbtgt|  
||연산자 인쇄|연산자 인쇄|연산자 인쇄|  
||||읽기 도메인 컨트롤러|  
||복제|복제|복제|  
|스키마 관리|스키마 관리|스키마 관리|스키마 관리|  
||서버 연산자|서버 연산자|서버 연산자|  

#### <a name="adminsdholder"></a>AdminSDHolder  
AdminSDHolder 개체의 목적은 보호 계정과 도메인에 있는 그룹에 대 한 "템플릿" 사용 권한을 제공 합니다. 모든 Active Directory 도메인의 시스템 컨테이너 개체로 AdminSDHolder 자동으로 만들어집니다. 해당 경로의: **CN CN AdminSDHolder = = 시스템, DC < domain_component > = DC < domain_component > =? 합니다.**  

소유 하는 관리자가 그룹, Active Directory 도메인에 있는 대부분 개체 달리 AdminSDHolder 도메인 관리자 그룹 소유 합니다. 기본적으로 EAs 변경할 수 있는 도메인 AdminSDHolder 개체 도메인 도메인 관리자와 관리자가 그룹 처럼 합니다. 또한, AdminSDHolder의 기본 소유자는 도메인 도메인 관리자 그룹을 수 있지만 관리자 또는 Enterprise 관리자의 회원 개체의 소유권을 사용할 수 있습니다.  

#### <a name="sdprop"></a>SDProp  
SDProp은 도메인 PDC 에뮬레이터 (PDCE) 보유 하는 도메인 컨트롤러의 (기본적으로) 60 분 마다을 실행 하는 프로세스입니다. SDProp 보호 계정과 도메인에 있는 그룹에 대 한 권한 된 도메인의 AdminSDHolder 개체에 대 한 권한을 비교합니다. 보호 된 계정 및 그룹 중 하나에 대 한 권한을 AdminSDHolder 개체에 대 한 권한을 일치 하지 않는 경우 도메인의 AdminSDHolder 개체 일치 하도록 보호 계정과 그룹에 대 한 권한은 다시 설정 됩니다.  

또한 권한을 상속 불가능 그룹과, 계정 보호에 계정 및 그룹 디렉터리의 다른 위치로 이동 하는 경우에 자녀가 권한을 상속 하지 않는 새로운 상위 개체를 의미 합니다. 부모 개체 사용 권한 변경 AdminSDHolder 권한이 변경 되지 않습니다 상속은 AdminSDHolder 개체에 사용할 수 없습니다.  

##### <a name="changing-sdprop-interval"></a>SDProp 간격을 변경  
일반적으로, 테스트 목적을 제외 하 고 있는 SDProp 실행 되며 언제 간격을 변경 필요가 없습니다. 도메인 PDCE에 SDProp 간격을 변경 하려는 경우 regedit 사용 하 여 추가 하거나 HKLM\SYSTEM\CurrentControlSet\Services\NTDS\Parameters AdminSDProtectFrequency DWORD 값을 수정할 수 있습니다.  

값은 7200 (2 시간에 1 분)를 60에서 초 됩니다. 변경 내용이 되돌리려면 60 분 간격으로 되돌리려면 SDProp 하면 AdminSDProtectFrequency 키를 삭제 합니다. 일반적으로 해야 하지 줄일 있습니다이 간격 프로덕션 도메인에 있는 lsass가 도메인 컨트롤러에서 처리 오버 강화 수 있습니다. 이 증가의 영향을 보호 되는 도메인의 개체의 수에 따라 달라 집니다.  

##### <a name="running-sdprop-manually"></a>수동으로 SDProp 실행  
더 나은 방법을 AdminSDHolder 변경 내용을 테스트 중이지만 SDProp 수동으로 실행 하는 작업를 즉시 실행 하도록 예정된 실행 영향을 주지 않습니다. 수동으로 SDProp 실행 하는 Windows Server 2008 실행 하는 도메인 컨트롤러에 약간 다르게 수행 이전 버전 Windows Server 2008 R2 또는 Windows Server 2012를 실행 하는 도메인 컨트롤러에는 것 보다.  

이전 운영 체제에서 수동으로 SDProp 실행 절차에 제공 됩니다 [Microsoft 지원 문서 251343](https://support.microsoft.com/kb/251343), 다음은 이전 및 최신 운영 체제에 대 한 단계별 지침입니다. 두 경우 모두 rootDSE Active Directory 개체에 연결 하 고 수정 특성으로 작업의 이름을 지정 하 rootDSE 개체 null DN와 수정 작업을 수행 해야 합니다. RootDSE 개체에 수정할 수 있는 작업에 대 한 자세한 내용은 참조 [rootDSE 수정 작업](https://msdn.microsoft.com/library/cc223297.aspx) MSDN 웹 사이트에서 합니다.  

###### <a name="running-sdprop-manually-in-windows-server-2008-or-earlier"></a>Windows Server 2008 또는 그 이전에 수동으로 실행 SDProp  
LDAP 수정 스크립트 실행 하거나 Ldp.exe 사용 하 여 실행 하는 SDProp 할 수 있습니다. Ldp.exe 사용 하 여 SDProp를 실행 하려면 변경 도메인에 있는 AdminSDHolder 개체를 수행한 후 다음 단계를 수행 합니다.  

1.  시작 **Ldp.exe**합니다.  

2.  클릭 **연결** Ldp 대화 상자 및 클릭 **연결**합니다.  

    ![계정 보호 및 그룹](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_9.gif)  

3.  에 **연결** 대화 상자의 에뮬레이터 PDC (PDCE) 역할 도메인에 대 한 도메인 컨트롤러의 이름을 입력 하 고 클릭 **확인**합니다.  

    ![계정 보호 및 그룹](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_10.png)  

4.  사용자가 연결 되어 있는지 확인 성공적으로 표시 된 대로 **Dn: (RootDSE)** 클릭 한 다음 화면에 **연결** 클릭 **연결**합니다.  

    ![계정 보호 및 그룹](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_11.png)  

5.  에 **연결** 대화 상자에 rootDSE 개체를 수정할 수 있는 권한이 있는 사용자 계정 자격 증명을 입력 합니다. (경우 해당 사용자로 로그온 선택할 수 있습니다 **로 연결** 사용자에 현재 로그온 합니다.) 클릭 **확인**합니다.  

    ![계정 보호 및 그룹](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_12.png)  

6.  Bind 작업을 완료 한 후 클릭 **찾아보기**를 클릭 하 고 **수정**합니다.  

    ![계정 보호 및 그룹](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_13.png)  

7.  에 **수정** 남겨 대화 상자에서 **DN** 필드를 비워 합니다. 에 **항목 특성 편집** 필드를 입력 **FixUpInheritance**의 **값** 필드를 입력 **예**합니다. 클릭 **Enter** 채우려면는 **항목 목록** 다음 화면에 표시 된 대로 합니다.  

    ![계정 보호 및 그룹](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_14.gif)  

8.  밀도가 높은 수정 대화 상자에서 실행을 클릭 하 고 AdminSDHolder 개체를 변경한 해당 개체에서는 나타나지 있는지 확인 합니다.  

> [!NOTE]  
> 지정 된 권한 없는 계정을 보호 그룹의 회원 수정할 수 있도록 AdminSDHolder 수정에 대 한 내용은 [부록 i: 관리 계정 만들기 보호 계정과 Active Directory에 있는 그룹에 대 한](../../../ad-ds/manage/component-updates/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory.md)합니다.  

LDIFDE 또는 스크립트 통해 수동으로 SDProp 실행 하려는 경우 다음과 같이 수정 항목을 만들 수 있습니다.  

![계정 보호 및 그룹](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_15.gif)  

###### <a name="running-sdprop-manually-in-windows-server-2012-or-windows-server-2008-r2"></a>Windows Server 2008 R2 또는 Windows Server 2012에서 수동으로 SDProp 실행  
LDAP 수정 스크립트 실행 하거나 Ldp.exe 사용 하 여 실행 하는 SDProp 할 수 있습니다. Ldp.exe 사용 하 여 SDProp를 실행 하려면 변경 도메인에 있는 AdminSDHolder 개체를 수행한 후 다음 단계를 수행 합니다.  

1.  시작 **Ldp.exe**합니다.  

2.  **Ldp** 대화 상자를 클릭 **연결**를 클릭 하 고 **연결**합니다.  

    ![계정 보호 및 그룹](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_16.gif)  

3.  에 **연결** 대화 상자의 에뮬레이터 PDC (PDCE) 역할 도메인에 대 한 도메인 컨트롤러의 이름을 입력 하 고 클릭 **확인**합니다.  

    ![계정 보호 및 그룹](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_17.gif)  

4.  사용자가 연결 되어 있는지 확인 성공적으로 표시 된 대로 **Dn: (RootDSE)** 클릭 한 다음 화면에 **연결** 클릭 **연결**합니다.  

    ![계정 보호 및 그룹](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_18.gif)  

5.  에 **연결** 대화 상자에 rootDSE 개체를 수정할 수 있는 권한이 있는 사용자 계정 자격 증명을 입력 합니다. (선택 수 있는 경우 해당 사용자로 로그온 **Bind 현재 로그온 한 사용자**.) 클릭 **확인**합니다.  

    ![계정 보호 및 그룹](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_19.gif)  

6.  Bind 작업을 완료 한 후 클릭 **찾아보기**를 클릭 하 고 **수정**합니다.  

    ![계정 보호 및 그룹](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_20.gif)  

7.  에 **수정** 남겨 대화 상자에서 **DN** 필드를 비워 합니다. 에 **항목 특성 편집** 필드를 입력 **RunProtectAdminGroupsTask**의 **값** 필드를 입력 **1**합니다. 클릭 **Enter** 다음과 같이 항목 목록을 채웁니다.  

    ![계정 보호 및 그룹](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_21.gif)  

8.  고 밀도가 높은에서 **수정** 대화 상자를 클릭 **실행**, AdminSDHolder 개체를 변경한 해당 개체에서는 나타나지 있는지 확인 합니다.  

LDIFDE 또는 스크립트 통해 수동으로 SDProp 실행 하려는 경우 다음과 같이 수정 항목을 만들 수 있습니다.  

![계정 보호 및 그룹](media/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory/SAD_22.gif)  
