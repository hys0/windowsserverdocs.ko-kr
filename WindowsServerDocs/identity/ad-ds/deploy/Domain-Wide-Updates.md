---
ms.assetid: 2a5d5271-6ac6-4c1b-b4ef-9b568932a55a
title: Active Directory 도메인 전체 스키마 업데이트
description: Adprep /domainprep을 도메인 컨트롤러로 수준을 올릴 때 수행한 전체 도메인 스키마 업데이트
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 10/29/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 20598431b9c2376051247fd7ba14e33af00968cc
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59812324"
---
# <a name="domain-wide-schema-updates"></a>전체 도메인 스키마 업데이트

>적용 대상: Windows Server

변경 내용 이해 하 고 Windows Server에서 adprep /domainprep에서 수행 되는 스키마 업데이트를 준비 하는 데 다음 집합을 검토할 수 있습니다.

Adprep 명령은 Windows Server 2012부터, AD DS 설치 하는 동안 필요에 따라 자동으로 실행 됩니다. 또한 실행할 수 별도로 AD DS 설치 이전에 알려드립니다. 자세한 내용은 [Adprep.exe 실행](https://technet.microsoft.com/library/dd464018(v=ws.10).aspx)을 참조하십시오.

액세스 제어 항목 (ACE) 문자열을 해석 하는 방법에 대 한 자세한 내용은 참조 하세요. [ACE 문자열](https://msdn.microsoft.com/library/aa374928(VS.85).aspx)합니다. 보안 식별자 (SID) 문자열을 해석 하는 방법에 대 한 자세한 내용은 참조 하세요. [SID 문자열](https://msdn.microsoft.com/library/aa379602(VS.85).aspx)합니다.

## <a name="windows-server-semi-annual-channel-domain-wide-updates"></a>Windows Server (반기 채널): 전체 도메인 업데이트

수행 되는 작업을 수행한 후 **domainprep** Windows Server 2016의 (작업 89) 완료 합니다 **수정** CN 특성 ActiveDirectoryUpdate, CN = DomainUpdates, CN = System, DC = = 포리스트 루트 도메인 개체 설정할지 **16**합니다.

|작업 수 및 GUID|설명|사용 권한|
|------------------------------|---------------|--------------|---------------|
|**작업 89**: {A0C238BA-9E30-4EE6-80A6-43F731E9A5CD}|ACE 엔터프라이즈 키 관리에 모든 권한 부여를 삭제 하 고 엔터프라이즈 키 관리자를 완전히 제어할 msdsKeyCredentialLink 특성만 권한을 부여 하는 ACE를 추가 합니다.|(A; delete CI; RPWPCRLCLOCCDCRCWDWOSDDTSW;; 엔터프라이즈 키 관리) <br /> <br />(OA;를 추가 합니다. CI; RPWP; 5b47d60f-6090-40b2-9f37-2a4de88f3063; 엔터프라이즈 키 관리)|

## <a name="windows-server-2016-domain-wide-updates"></a>Windows Server 2016: 전체 도메인 업데이트

수행 되는 작업을 수행한 후 **domainprep** Windows Server 2016의 (작업 82 88) 완료 합니다 **수정** CN 특성 ActiveDirectoryUpdate, CN = DomainUpdates, CN = = 시스템, DC = 포리스트 루트 도메인 개체를 설정할지 **15**합니다.

|작업 수 및 GUID|설명|특성|사용 권한|
|------------------------------|---------------|--------------|---------------|
|**작업 82**: {83C53DA7-427E-47A4-A07A-A324598B88F7}|만들 CN = 도메인의 루트에서 키 컨테이너|-objectClass: 컨테이너<br />- description: 키 자격 증명 개체에 대 한 기본 컨테이너<br />- ShowInAdvancedViewOnly: TRUE|(A;CI;RPWPCRLCLOCCDCRCWDWOSDDTSW;;;EA)<br />(A;CI;RPWPCRLCLOCCDCRCWDWOSDDTSW;;;DA)<br />(A;CI;RPWPCRLCLOCCDCRCWDWOSDDTSW;;;SY)<br />(A;CI;RPWPCRLCLOCCDCRCWDWOSDDTSW;;;DD)<br />(A;CI;RPWPCRLCLOCCDCRCWDWOSDDTSW;;;ED)|
|**작업 83**: {C81FC9CC-0130-4FD1-B272-634D74818133}|모든 권한을 추가한 allow ace를 CN = "rootdomain\Enterprise 키 관리" 및 "domain\Key 관리자"에 대 한 키 컨테이너.|해당 사항 없음|(A; CI; RPWPCRLCLOCCDCRCWDWOSDDTSW;; 키 관리자)<br />(A;CI;RPWPCRLCLOCCDCRCWDWOSDDTSW;;;Enterprise Key Admins)|
|**작업 84**: {E5F9E791-D96D-4FC9-93C9-D53E1DC439BA}|CN를 가리키도록 otherWellKnownObjects 특성 수정 = 키 컨테이너입니다.|- otherWellKnownObjects: B:32:683A24E2E8164BD3AF86AC3C2CF3F981:CN=Keys,%ws|해당 사항 없음|
|**작업 85**: {e6d5fd00-385d-4e65-b02d-9da3493ed850}|NC "domain\Key 관리자"를 허용 하도록 도메인을 수정 하 고 "rootdomain\Enterprise 키 관리" Msds-keycredentiallink 특성을 수정 하 합니다. |해당 사항 없음|(OA; CI; RPWP; 5b47d60f-6090-40b2-9f37-2a4de88f3063; 키 관리자)<br />(OA; CI; RPWP; 5b47d60f-6090-40b2-9f37-2a4de88f3063; 루트 도메인에 있지만 루트가 아닌 도메인의 엔터프라이즈 키 관리는 가짜 도메인 관련 ACE가 확인할 수 없는-527 SID 사용 하 여 발생 한)|
|**작업 86**: {3a6b3fbf-3168-4312-a10d-dd5b3393952d}|DS-유효성 검사-쓰기-컴퓨터 자동차 작성자 소유자 및 자체에 부여|해당 사항 없음|(OA;CIIO;SW;9b026da6-0d3c-465c-8bee-5199d7165cba;bf967a86-0de6-11d0-a285-00aa003049e2;PS)<br />(OA;CIIO;SW;9b026da6-0d3c-465c-8bee-5199d7165cba;bf967a86-0de6-11d0-a285-00aa003049e2;CO)|
|**Operation 87**: {7F950403-0AB3-47F9-9730-5D7B0269F9BD}|잘못 된 도메인에 상대적인 엔터프라이즈 키 관리 그룹에 모든 권한을 부여 하는 ACE를 삭제 하 고 엔터프라이즈 키 관리 그룹에 모든 권한을 부여 하는 ACE를 추가 합니다. |해당 사항 없음|(A; delete CI; RPWPCRLCLOCCDCRCWDWOSDDTSW;; 엔터프라이즈 키 관리)<br /> <br />(A;를 추가 합니다. CI; RPWPCRLCLOCCDCRCWDWOSDDTSW;; 엔터프라이즈 키 관리)|
|**작업 88**: {434bb40d-dbc9-4fe7-81d4-d57229f7b080}|도메인 NC 개체에 "msDS-ExpirePasswordsOnSmartCardOnlyAccounts"를 추가 하 고 FALSE로 기본값 설정|해당 사항 없음|해당 사항 없음|

엔터프라이즈 키 관리 및 키 관리 그룹은 Windows Server 2016 도메인 컨트롤러가 승격 되어 PDC 에뮬레이터 FSMO 역할을 수행 후에 만들어집니다.

## <a name="windows-server-2012-r2-domain-wide-updates"></a>Windows Server 2012 R2: 전체 도메인 업데이트

작업을 수행 하지 하 여 있지만 **domainprep** Windows Server 2012 r2에서는 명령이 완료 되는 **수정** CN 특성 ActiveDirectoryUpdate, CN = DomainUpdates, CN = = 시스템, DC = 포리스트 루트 도메인 개체를 설정할지 **10**합니다.

## <a name="windows-server-2012-domain-wide-updates"></a>Windows Server 2012: 전체 도메인 업데이트

수행 하는 작업을 수행한 후 **domainprep** Windows Server 2012 (78, 79, 80 및 81 작업)를 완료 합니다 **수정** CN 특성 ActiveDirectoryUpdate, CN = DomainUpdates, = CN = System, DC = 포리스트 루트 도메인 개체를 설정할지 **9**합니다.

|작업 수 및 GUID|설명|특성|사용 권한|
|------------------------------|---------------|--------------|---------------|
|**작업 78**: {c3c927a6-cc1d-47c0-966b-be8f9b63d991}|만들 새 개체 CN = 도메인 파티션에 TPM 장치입니다.|개체 클래스: msTPM InformationObjectsContainer|해당 사항 없음|
|**작업 79**: {54afcfb9-637a-4251-9f47-4d50e7021211}|TPM 서비스에 대 한 액세스 제어 항목을 생성 합니다.|해당 사항 없음|(OA;CIIO;WP;ea1b7b93-5e48-46d5-bc6c-4df4fda78a35;bf967a86-0de6-11d0-a285-00aa003049e2;PS)|
|**작업 80**: {f4728883-84dd-483c-9897-274f2ebcf11e}|"복제 DC" 확장 권한이 부여 **Cloneable Domain Controllers** 그룹|해당 사항 없음|(OA;;CR;3e0f7e18-2c7a-4c10-ba82-4d926db99a3e;;*domain SID*-522)|
|**작업 81**: {ff4f9d27-7157-4cb0-80a9-5d6f2b14c8ff}|모든 개체에 대해 보안 주체가 셀프 ms-DS-Allowed-To-Act-On-Behalf-Of-Other-Identity 권한을 부여 합니다.|해당 사항 없음|(OA;CIOI;RPWP;3f78c3e5-f79a-46bd-a0b8-9d18116ddc79;;PS)|
