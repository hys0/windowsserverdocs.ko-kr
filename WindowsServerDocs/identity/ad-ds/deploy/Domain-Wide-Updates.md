---
ms.assetid: 2a5d5271-6ac6-4c1b-b4ef-9b568932a55a
title: "Active Directory 전체 도메인 스키마 업데이트"
description: "전체 도메인 스키마 업데이트 adprep 수행한 /domainprep 도메인 컨트롤러를 홍보 하는 경우"
author: MicrosoftGuyJFlo
ms.author: joflore
manager: femila
ms.date: 07/14/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 59efb7c854b7f3693776bf9a1a371f98c2206d60
ms.sourcegitcommit: 79c1359232bece2e5c3ee5507f1e4bf19b44f487
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/19/2018
---
# <a name="domain-wide-schema-updates"></a>전체 도메인 스키마 업데이트

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

다음과 같은 변경 이해 하 고 도움이 수행 하는 adprep 스키마 업데이트에 대 한 준비를 집합을 검토할 수 /domainprep Windows Server에서 합니다. 

Adprep 명령 광고 DS 설치 하는 동안 필요에 따라 자동으로 실행 Windows Server 2012에서 시작 하세요. 자녀가 실행할 수도 별도로 광고 DS 설치 하기 전에 합니다. For more information, see [Running Adprep.exe](https://technet.microsoft.com/library/dd464018(v=ws.10).aspx).

For more information about how to interpret the access control entry (ACE) strings, see [ACE strings](https://msdn.microsoft.com/library/aa374928(VS.85).aspx). For more information about how to interpret the security ID (SID) strings, see [SID strings](https://msdn.microsoft.com/library/aa379602(VS.85).aspx).

## <a name="windows-server-semi-annual-channel-domain-wide-updates"></a>Windows Server (세미콜론 연간 채널): 도메인 전체 업데이트

수행 하는 작업 한 후 **도메인 준비** Windows Server 2016 (작업 89) 완료는 **수정** CN에 대 한 특성 = ActiveDirectoryUpdate, CN CN DomainUpdates = 시스템, DC = ForestRootDomain 개체로 설정 되어 = **16**합니다.

|작업 번호와 GUID|설명|사용 권한|
|------------------------------|---------------|--------------|---------------|
|**작업 89**: {A0C238BA-9E30-4EE6-80A6-43F731E9A5CD}|엔터프라이즈 키 관리자에 게 모든 권한을 부여 ACE 삭제 하 고 엔터프라이즈 키 관리자만 msdsKeyCredentialLink 특성을 통해 모든 권한을 부여 ACE 추가 합니다.|(A; 삭제 CI; RPWPCRLCLOCCDCRCWDWOSDDTSW; 됩니다. 엔터프라이즈 주요 관리자) <br /> <br />(OA; 추가 CI; RPWP; 5b47d60f-6090-40b2-9f37-2a4de88f3063, 엔터프라이즈 주요 관리자)|

## <a name="windows-server-2016-domain-wide-updates"></a>Windows Server 2016: 도메인 전체 업데이트

수행 하는 작업 한 후 **도메인 준비** Windows Server 2016 (작업 82 88) 완료는 **수정** 특성 CN에 대 한 CN ActiveDirectoryUpdate = CN DomainUpdates = 시스템, DC = ForestRootDomain 개체로 설정 되어 = **15**합니다.

|작업 번호와 GUID|설명|특성|사용 권한|
|------------------------------|---------------|--------------|---------------|
|**작업 82**: {83C53DA7-427E-47A4-A07A-A324598B88F7}|CN 만들기 = 루트 도메인에 컨테이너 키|-개체 클래스: 컨테이너<br />기능 설명: 주요 자격 증명 개체 기본 컨테이너<br />-ShowInAdvancedViewOnly: 진정한|(A; CI; RPWPCRLCLOCCDCRCWDWOSDDTSW; 됩니다. EA)<br />(A; CI; RPWPCRLCLOCCDCRCWDWOSDDTSW;, D )<br />(A; CI; RPWPCRLCLOCCDCRCWDWOSDDTSW; 됩니다. SY)<br />(A; CI; RPWPCRLCLOCCDCRCWDWOSDDTSW;, D D)<br />(A; CI; RPWPCRLCLOCCDCRCWDWOSDDTSW; 됩니다. 드)|
|**작업 83**: {C81FC9CC-0130-4FD1-B272-634D74818133}|모든 권한을 추가 CN ace 허용 = "rootdomain\Enterprise 키 관리자" 및 "domain\Key 관리자"에 대 한 컨테이너 키.|해당 없음|(A; CI; RPWPCRLCLOCCDCRCWDWOSDDTSW; 됩니다. 주요 관리자)<br />(A; CI; RPWPCRLCLOCCDCRCWDWOSDDTSW; 됩니다. 엔터프라이즈 주요 관리자)|
|**84 작업**: {E5F9E791-D96D-4FC9-93C9-D53E1DC439BA}|수정 otherWellKnownObjects 특성 CN 가리키도록 = 키 컨테이너 합니다.|-otherWellKnownObjects: B:32:683A24E2E8164BD3AF86AC3C2CF3F981:CN 키, %ws =|해당 없음|
|**작업 85**: {e6d5fd00-385d-4e65-b02d-9da3493ed850}|도메인 NC "domain\Key 관리자"를 허용 하도록 변경 하 고 "rootdomain\Enterprise 키 관리자"를 KeyCredentialLink 특성을 수정 하 합니다. |해당 없음|(OA; CI; RPWP; 5b47d60f-6090-40b2-9f37-2a4de88f3063, 주요 관리자)<br />(OA; CI; RPWP; 5b47d60f-6090-40b2-9f37-2a4de88f3063, 엔터프라이즈 키 관리자 루트 도메인 하지만 아닌은 도메인의 중단-527 SID가 확인할 수 있는 가짜 도메인 상대 ACE)|
|**작업 86**: {3a6b3fbf-3168-4312-a10d-dd5b3393952d}|DS 유효성을 검사-쓰기-컴퓨터 자동차 creator 소유자가 자신을 허용합니다|해당 없음|(OA; CIIO;SW;9b026da6-0d3c-465c-8bee-5199d7165cba;bf967a86-0de6-11d0-a285-00aa003049e2;PS)<br />(OA; CIIO;SW;9b026da6-0d3c-465c-8bee-5199d7165cba;bf967a86-0de6-11d0-a285-00aa003049e2;CO)|
|**작업 87**: {7F950403-0AB3-47F9-9730-5D7B0269F9BD}|잘못 된 도메인 상대 엔터프라이즈 키 관리자 그룹에 모든 권한을 부여 ACE 삭제 하 고 엔터프라이즈 키 관리자 그룹 모든 권한을 부여 ACE 추가 합니다. |해당 없음|(A; 삭제 CI; RPWPCRLCLOCCDCRCWDWOSDDTSW; 됩니다. 엔터프라이즈 주요 관리자)<br /> <br />(A; 추가 CI; RPWPCRLCLOCCDCRCWDWOSDDTSW; 됩니다. 엔터프라이즈 주요 관리자)|
|**작업 88**: {434bb40d-dbc9-4fe7-81d4-d57229f7b080}|도메인 NC 개체에서 "를 ExpirePasswordsOnSmartCardOnlyAccounts"을 추가 하 고 false 기본값 설정|해당 없음|해당 없음|

Windows Server 2016 도메인 컨트롤러 확장지 않습니다 및 에뮬레이터 FSMO PDC 역할은 후에 엔터프라이즈 키 관리자 및 키 관리자 그룹 생성 됩니다.

## <a name="windows-server-2012-r2-domain-wide-updates"></a>Windows Server 2012 r 2: 도메인 전체 업데이트

하 여 작업이 동일 하지만 **도메인 준비** Windows Server 2012 R2, 명령 완료 된 후에 **수정** CN에 대 한 특성 CN ActiveDirectoryUpdate = CN DomainUpdates = 시스템, DC = ForestRootDomain 개체로 설정 되어 = **10**합니다.

## <a name="windows-server-2012-domain-wide-updates"></a>Windows Server 2012: 도메인 전체 업데이트

수행 하는 작업 한 후 **도메인 준비** Windows Server 2012에 (작업 78, 79, 80 및 81) 완료는 **수정** CN에 대 한 특성 CN ActiveDirectoryUpdate = CN DomainUpdates = = 시스템, DC ForestRootDomain 개체로 설정 되어 = **9**합니다.

|작업 번호와 GUID|설명|특성|사용 권한|
|------------------------------|---------------|--------------|---------------|
|**작업 78**: {c3c927a6-cc1d-47c0-966b-be8f9b63d991}|잃게 CN TPM 디바이스에서 도메인 하는 파티션에 = 합니다.|개체 클래스: msTPM InformationObjectsContainer|해당 없음|
|**작업 79**: {54afcfb9-637a-4251-9f47-4d50e7021211}|TPM 서비스에 대 한 액세스를 제어 항목이 만들어집니다.|해당 없음|(OA; CIIO; WP;ea1b7b93-5e48-46d5-bc6c-4df4fda78a35;bf967a86-0de6-11d0-a285-00aa003049e2;PS)|
|**작업 80**: {f4728883-84dd-483c-9897-274f2ebcf11e}|"복제 DC" 확장 권한이 부여 **복제 가능한 도메인 컨트롤러** 그룹|해당 없음|(OA, CR; 3e0f7e18-2c7a-4c10-ba82-4d926db99a3e, *도메인 SID*-522)|
|**작업 81**: {ff4f9d27-7157-4cb0-80a9-5d6f2b14c8ff}|주 자체 MS-DS-Allowed-To-Act-On-Behalf-Of-Other-Identity 개체 권한을 부여 합니다.|해당 없음|(OA; CIOI; RPWP; 3f78c3e5-f79a-46bd-a0b8-9d18116ddc79, P)|
