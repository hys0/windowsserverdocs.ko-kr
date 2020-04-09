---
ms.assetid: 2a5d5271-6ac6-4c1b-b4ef-9b568932a55a
title: Active Directory 도메인 전체 스키마 업데이트
description: 도메인 컨트롤러의 수준을 올릴 때 adprep/domainprep에서 수행 하는 도메인 전체 스키마 업데이트
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 10/29/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 3b82958471e5292f202aa338aee7f4f5863459af
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80825216"
---
# <a name="domain-wide-schema-updates"></a>도메인 전체 스키마 업데이트

>Windows Server에 적용 됩니다.

다음 변경 내용 집합을 검토 하 여 Windows Server의 adprep/domainprep에서 수행 하는 스키마 업데이트를 이해 하 고 준비할 수 있습니다.

Windows Server 2012부터 Adprep 명령은 AD DS 설치 하는 동안 필요에 따라 자동으로 실행 됩니다. 또한 설치를 AD DS 하기 전에 별도로 실행할 수도 있습니다. 자세한 내용은 [Adprep.exe 실행](https://technet.microsoft.com/library/dd464018(v=ws.10).aspx)을 참조하십시오.

ACE (액세스 제어 항목) 문자열을 해석 하는 방법에 대 한 자세한 내용은 [ace 문자열](https://msdn.microsoft.com/library/aa374928(VS.85).aspx)을 참조 하세요. SID (보안 ID) 문자열을 해석 하는 방법에 대 한 자세한 내용은 [sid 문자열](https://msdn.microsoft.com/library/aa379602(VS.85).aspx)을 참조 하세요.

## <a name="windows-server-semi-annual-channel-domain-wide-updates"></a>Windows Server (반기 채널): 도메인 전체 업데이트

Windows Server 2016 (작업 89)에서 **domainprep** 에 의해 수행 된 작업이 완료 된 후 Cn = ACTIVEDIRECTORYUPDATE, Cn = domainupdates, Cn = SYSTEM, DC = ForestRootDomain 개체에 대 한 **수정** 특성은 **16**으로 설정 됩니다.

|작업 번호 및 GUID|설명|권한|
|------------------------------|---------------|--------------|---------------|
|**작업 89**: {A0C238BA-9E30-4EE6-80A6-43F731E9A5CD}|Enterprise Key Admins에 모든 권한을 부여 하는 ACE를 삭제 하 고 msdsKeyCredentialLink 특성에 대 한 모든 권한을 부여 하는 ACE를 추가 합니다.|Delete (A; CI RPWPCRLCLOCCDCRCWDWOSDDTSW;;; 엔터프라이즈 키 관리자) <br /> <br />추가 (OA; CI RPWP; 5b47d60f-6090-40b2-9f37-2a4de88f3063;; 엔터프라이즈 키 관리자)|

## <a name="windows-server-2016-domain-wide-updates"></a>Windows Server 2016: 도메인 전체 업데이트

Windows Server 2016 (operations 82-88)에서 **domainprep** 에 의해 수행 된 작업이 완료 된 후 Cn = ACTIVEDIRECTORYUPDATE, Cn = domainupdates, Cn = SYSTEM, DC = ForestRootDomain 개체에 대 한 **수정** 특성은 **15**로 설정 됩니다.

|작업 번호 및 GUID|설명|특성|권한|
|------------------------------|---------------|--------------|---------------|
|**작업 82**: {83C53DA7-427E-47A4-A07A-A324598B88F7}|도메인의 루트에 CN = Keys 컨테이너를 만듭니다.|-objectClass: 컨테이너<br />-description: 키 자격 증명 개체에 대 한 기본 컨테이너<br />-ShowInAdvancedViewOnly: TRUE|은 CI RPWPCRLCLOCCDCRCWDWOSDDTSW;;; E<br />은 CI RPWPCRLCLOCCDCRCWDWOSDDTSW;;D 은<br />은 CI RPWPCRLCLOCCDCRCWDWOSDDTSW;;; SY<br />은 CI RPWPCRLCLOCCDCRCWDWOSDDTSW;;D 2<br />은 CI RPWPCRLCLOCCDCRCWDWOSDDTSW;;; ED|
|**작업 83**: {C81FC9CC-0130-4FD1-B272-634D74818133}|"Domain\Key Admins" 및 "rootdomain\Enterprise Key Admins"에 대 한 모든 권한 ace를 CN = Keys 컨테이너에 추가 합니다.|N/A|은 CI RPWPCRLCLOCCDCRCWDWOSDDTSW;;; 키 관리자)<br />은 CI RPWPCRLCLOCCDCRCWDWOSDDTSW;;; 엔터프라이즈 키 관리자)|
|**작업 84**: {E5F9E791-D96D-4FC9-93C9-D53E1DC439BA}|CN = Keys 컨테이너를 가리키도록 otherWellKnownObjects 특성을 수정 합니다.|-otherWellKnownObjects: B:32:683A24E2E8164BD3AF86AC3C2CF3F981: CN = Keys,% ws|N/A|
|**작업 85**: {e6d5fd00-385d-4e65-b02d-9da3493ed850}|"Domain\Key Admins" 및 "rootdomain\Enterprise Key Admins"를 허용 하도록 도메인 NC를 수정 하 여의 msds-primary-computer-KeyCredentialLink 특성을 수정 합니다. |N/A|정부용 CI RPWP; 5b47d60f-6090-40b2-9f37-2a4de88f3063;; 키 관리자)<br />정부용 CI RPWP; 5b47d60f-6090-40b2-9f37-2a4de88f3063;; 엔터프라이즈 키 관리자가 루트 도메인에 있지만 루트가 아닌 도메인에 있는 위조 된 도메인 관련 ACE가 확인 되지 않은 527 SID로 생성 되었습니다.|
|**작업 86**: {3a6b3fbf-3168-4312-a10d-dd5b3393952d}|작성자 소유자 및 자신에 게 DS 유효성 검사-컴퓨터 자동차를 부여 합니다.|N/A|정부용 CIIO; SW; 9b026da6-0d3c-465c-8bee-5199d7165cba; bf967a86-0de6-11d0-a285-00aa003049e2; PS)<br />정부용 CIIO; SW; 9b026da6-0d3c-465c-8bee-5199d7165cba; bf967a86-0de6-11d0-a285-00aa003049e2; CO)|
|**작업 87**: {7F950403-0AB3-47F9-9730-5D7B0269F9BD}|잘못 된 도메인 관련 엔터프라이즈 키 관리자 그룹에 대 한 모든 권한을 부여 하는 ACE를 삭제 하 고 Enterprise Key Admins 그룹에 모든 권한을 부여 하는 ACE를 추가 합니다. |N/A|Delete (A; CI RPWPCRLCLOCCDCRCWDWOSDDTSW;;; 엔터프라이즈 키 관리자)<br /> <br />추가 (A; CI RPWPCRLCLOCCDCRCWDWOSDDTSW;;; 엔터프라이즈 키 관리자)|
|**작업 88**: {434bb40d-dbc9-4fe7-81d4-d57229f7b080}|도메인 NC 개체에 "의 msds-primary-computer-ExpirePasswordsOnSmartCardOnlyAccounts"를 추가 하 고 기본값을 FALSE로 설정 합니다.|N/A|N/A|

엔터프라이즈 키 관리자 및 키 관리자 그룹은 Windows Server 2016 도메인 컨트롤러의 수준을 올린 후에만 생성 되며 PDC 에뮬레이터 FSMO 역할을 수행 합니다.

## <a name="windows-server-2012-r2-domain-wide-updates"></a>Windows Server 2012 R2: 도메인 전체 업데이트

Windows Server 2012 r 2의 **domainprep** 에서 작업을 수행 하지 않지만 명령이 완료 된 후 Cn = ACTIVEDIRECTORYUPDATE, Cn = domainupdates, Cn = SYSTEM, DC = ForestRootDomain 개체에 대 한 **수정** 특성은 **10**으로 설정 됩니다.

## <a name="windows-server-2012-domain-wide-updates"></a>Windows Server 2012: 도메인 전체 업데이트

Windows Server 2012 (operations 78, 79, 80 및 81)에서 **domainprep** 에 의해 수행 된 작업이 완료 된 후 Cn = ACTIVEDIRECTORYUPDATE, Cn = domainupdates, Cn = SYSTEM, DC = ForestRootDomain 개체에 대 한 **수정** 특성은 **9**로 설정 됩니다.

|작업 번호 및 GUID|설명|특성|권한|
|------------------------------|---------------|--------------|---------------|
|**작업 78**: {c3c927a6-cc1d-47c0-966b-be8f9b63d991}|도메인 파티션에 새 개체 CN = TPM 장치를 만듭니다.|개체 클래스: msTPM-InformationObjectsContainer|N/A|
|**작업 79**: {54afcfb9-637a-4251-9f47-4d50e7021211}|TPM 서비스에 대 한 액세스 제어 항목을 만들었습니다.|N/A|정부용 CIIO; WP; ea1b7b93-5e48-46d5-bc6c-4df4fda78a35; bf967a86-0de6-11d0-a285-00aa003049e2; PS)|
|**작업 80**: {f4728883-84dd-483c-9897-274f2ebcf11e}|**복제 가능 도메인 컨트롤러** 그룹에 "복제 DC" 확장 권한을 부여 합니다.|N/A|(OA;;) CR; 3e0f7e18-2c7a-4c10-ba82-4d926db99a3e;; *도메인 SID*-522)|
|**작업 81**: {ff4f9d27-7157-4cb0-80a9-5d6f2b14c8ff}|모든 개체의 주 서버에 대 한 다른 Id를 사용자 자신에 게 부여 합니다.|N/A|정부용 CIOI; RPWP; 3f78c3e5-f79a-46bd-a0b8-9d18116ddc79;; PS|
