---
title: tapicfg
description: TAPI 응용 프로그램 디렉터리 파티션을 관리 하는 방법에 알아봅니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c0e642ce-5d98-4edb-9a65-1dff09aef4e1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 6e89b1e3d7638fbcbe0140658d2d2a9af1ccd852
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59886514"
---
# <a name="tapicfg"></a>tapicfg

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

만듭니다, 그리고 제거 또는 TAPI 응용 프로그램 디렉터리 파티션을 표시 하거나 기본 TAPI 응용 프로그램 디렉터리 파티션을 설정 합니다. TAPI 3.1 클라이언트를 찾아 TAPI 디렉터리와 통신 디렉터리 서비스 로케이터를 사용 하 여이 응용 프로그램 디렉터리 파티션에 정보를 사용할 수 있습니다. 사용할 수도 있습니다 **tapicfg** 만들거나 TAPI 클라이언트가 도메인의 TAPI 응용 프로그램 디렉터리 파티션을 효율적으로 찾을 수 있도록 하는 서비스 연결 지점을 제거 합니다. 자세한 내용은 설명을 참조 하십시오. 명령 구문을 보려면에서 명령을 클릭 합니다. 
-   [tapicfg install](#BKMK_install)
-   [tapicfg remove](#BKMK_remove)
-   [tapicfg publishscp](#BKMK_publishscp)
-   [tapicfg removescp](#BKMK_removescp)
-   [tapicfg show](#BKMK_show)
-   [tapicfg makedefault](#BKMK_makedefault)

## <a name="BKMK_install"></a>tapicfg install
TAPI 응용 프로그램 디렉터리 파티션을 만듭니다.

### <a name="syntax"></a>구문
```
tapicfg install /directory:<PartitionName> [/server:<DCName>] [/forcedefault]
```
### <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|/directory를 설치 합니다.\<PartitionName >|필수. TAPI 응용 프로그램 디렉터리 파티션 만들의 DNS 이름을 지정 합니다. 이 이름은 정규화 된 도메인 이름 이어야 합니다.|
|/server: \<DCName>|TAPI 응용 프로그램 디렉터리 파티션을 생성 된 도메인 컨트롤러의 DNS 이름을 지정 합니다. 도메인 컨트롤러의 이름을 지정 하지 않으면 로컬 컴퓨터의 이름이 사용 됩니다.|
|/forcedefault|이 디렉터리는 도메인에 대 한 기본 TAPI 응용 프로그램 디렉터리 파티션을 지정 합니다. 도메인에 여러 TAPI 응용 프로그램 디렉터리 파티션이 있을 수 있습니다.<br /><br />이 디렉터리 도메인에서 만든 첫 번째 TAPI 응용 프로그램 디렉터리 파티션에 이면 자동으로 사용 하는지 여부에 관계 없이 기본값으로 설정 됩니다는 **/forcedefault** 옵션입니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="BKMK_remove"></a>tapicfg 제거
TAPI 응용 프로그램 디렉터리 파티션을 제거합니다.

### <a name="syntax"></a>구문
```
tapicfg remove /directory:<PartitionName>
```
### <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|remove /directory:\<PartitionName>|필수. 제거할 TAPI 응용 프로그램 디렉터리 파티션의 DNS 이름을 지정 합니다. 참고가이 이름은 정규화 된 도메인 이름을 이어야 합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="BKMK_publishscp"></a>tapicfg publishscp
서비스 연결 지점 TAPI 응용 프로그램 디렉터리 파티션을 게시를 만듭니다.

### <a name="syntax"></a>구문
```
tapicfg publishscp /directory:<PartitionName> [/domain:<DomainName>] [/forcedefault]
```
### <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|publishscp /directory:\<PartitionName>|필수. 게시할 서비스 연결 지점 TAPI 응용 프로그램 디렉터리 파티션의 DNS 이름을 지정 합니다.|
|/domain:\<DomainName>|서비스 연결 지점이 있는 도메인의 DNS 이름을 만들도록 지정 합니다. 도메인 이름을 지정 하지 않으면 로컬 도메인 이름이 사용 됩니다.|
|/forcedefault|이 디렉터리는 도메인에 대 한 기본 TAPI 응용 프로그램 디렉터리 파티션을 지정 합니다. 도메인에 여러 TAPI 응용 프로그램 디렉터리 파티션이 있을 수 있습니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="BKMK_removescp"></a>tapicfg removescp
TAPI 응용 프로그램 디렉터리 파티션에 대 한 서비스 연결 지점을 제거합니다.

### <a name="syntax"></a>구문
```
tapicfg removescp /directory:<PartitionName> [/domain:<DomainName>]
```
### <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|removescp /directory:\<PartitionName>|필수 사항입니다. 서비스 연결 지점이 제거 되는 TAPI 응용 프로그램 디렉터리 파티션의 DNS 이름을 지정 합니다.|
|/domain: \<DomainName>|서비스 연결 지점 제거는 도메인의 DNS 이름을 지정 합니다. 도메인 이름을 지정 하지 않으면 로컬 도메인 이름이 사용 됩니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="BKMK_show"></a>tapicfg 표시
도메인의 이름 및 TAPI 응용 프로그램 디렉터리 파티션의 위치를 표시합니다.

### <a name="syntax"></a>구문
```
tapicfg show [/defaultonly][ /domain:<DomainName>]
```
### <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|/defaultonly|도메인의 이름 및 기본 TAPI 응용 프로그램 디렉터리 파티션만의 위치를 표시합니다.|
|/domain: \<DomainName>|TAPI 응용 프로그램 디렉터리 파티션을 표시 되는 도메인의 DNS 이름을 지정 합니다. 도메인 이름을 지정 하지 않으면 로컬 도메인 이름이 사용 됩니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="BKMK_makedefault"></a>tapicfg makedefault
도메인에 대 한 기본 TAPI 응용 프로그램 디렉터리 파티션을 설정합니다.

### <a name="syntax"></a>구문
```
tapicfg makedefault /directory:<PartitionName> [/domain:<DomainName>]  
```
### <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|makedefault /directory:\<PartitionName>|필수. TAPI 응용 프로그램 디렉터리 파티션에 도메인에 대 한 기본 파티션으로 설정의 DNS 이름을 지정 합니다. 참고가이 이름은 정규화 된 도메인 이름을 이어야 합니다. TAPI 응용 프로그램 디렉터리 파티션에 기본값으로 설정 된 도메인의 DNS 이름을 지정 합니다. 도메인 이름을 지정 하지 않으면 로컬 도메인 이름이 사용 됩니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명
하나를 실행 하려면 active directory의 Enterprise Admins 그룹의 멤버 여야 합니다 **tapicfg 설치** (TAPI 응용 프로그램 디렉터리 파티션을 만들려면) 또는 **tapicfg 제거** (TAPI 응용 프로그램을 제거 하려면 디렉터리 파티션)입니다.

이 명령줄 도구는 도메인의 구성원 인 모든 컴퓨터에서 실행할 수 있습니다.

만 국제 표준 문자나 유니코드 문자를 사용한 사용자 제공 텍스트 (예: TAPI 응용 프로그램 디렉터리 파티션, 서버 및 도메인 이름) 적절 한 글꼴 및 언어 지원이 설치 된 경우 올바르게 표시 됩니다.

여전히 ILS ILS 서버 또는 응용 프로그램 디렉터리 파티션을 TAPI Windows XP 또는 Windows Server 2003 운영 체제를 실행 하는 TAPI 클라이언트 쿼리할 수 있으므로 특정 응용 프로그램을 지원 하기 위해 필요한 경우 로케이터 ILS (인터넷 서비스) 서버, 조직에서 사용할 수 있습니다.

사용할 수 있습니다 **tapicfg** 만들거나 서비스 연결 지점을 제거 합니다. 어떤 이유 (예를 들어, 존재 하는 도메인 이름을 변경한 경우)에 대 한 TAPI 응용 프로그램 디렉터리 파티션 이름을 바꾸면, 기존 서비스 연결 지점을 제거 하 고 게시할 TAPI 응용 프로그램 디렉터리 파티션의 새 DNS 이름이 포함 된 새 프로필을 만듭니다. 그렇지 않으면, TAPI 클라이언트를 찾아 TAPI 응용 프로그램 디렉터리 파티션에 액세스할 수는 없습니다. (예를 들어 경우 특정 TAPI 응용 프로그램 디렉터리 파티션에 TAPI 데이터를 노출 하지 않으려는) 유지 관리 또는 보안 용도 대 한 서비스 연결 지점을 제거할 수도 있습니다.

## <a name="examples"></a>예
서버에서 명명 된 tapifiction.testdom.microsoft.com testdc.testdom.microsoft.com 이라는 새 도메인에 대 한 기본 TAPI 응용 프로그램 디렉터리 파티션을으로 설정한 다음 TAPI 응용 프로그램 디렉터리 파티션을 만들려면 다음을 입력 합니다.
```
tapicfg install /directory:tapifiction.testdom.microsoft.com /server:testdc.testdom.microsoft.com /forcedefault
```
새 도메인에 대 한 기본 TAPI 응용 프로그램 디렉터리 파티션의 이름의 표시 하려면 다음을 입력 합니다.
```
tapicfg show /defaultonly
```
## <a name="additional-references"></a>추가 참조
-   [명령줄 구문 키](command-line-syntax-key.md)
