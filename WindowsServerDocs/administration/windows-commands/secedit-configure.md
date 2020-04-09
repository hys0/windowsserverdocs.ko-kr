---
title: 'secedit: 구성'
description: '\* * * *에 대 한 Windows 명령 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a92e68ca-003c-4219-8655-0e7734f5fab3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 288886b486052fea62c7b89758890a664e1da0ce
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80834986"
---
# <a name="seceditconfigure"></a>secedit: 구성



데이터베이스에 저장 하는 보안 설정을 사용 하 여 현재 시스템 설정을 구성할 수 있습니다. 이 명령을 사용할 수 있는 방법을의 예 참조 [예제](#BKMK_Examples)합니다.

## <a name="syntax"></a>구문

```
Secedit /configure /db <database file name> [/cfg <configuration file name>] [/overwrite] [/areas SECURITYPOLICY | GROUP_MGMT | USER_RIGHTS | REGKEYS | FILESTORE | SERVICES] [/log <log file name>] [/quiet]
```

#### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|db|필수입니다.</br>저장된 된 구성을 포함 하는 데이터베이스의 경로 파일 이름을 지정 합니다.</br>파일 이름을 연결 된 보안 템플릿 (구성 파일에 표시 됨) 처럼 되지 않은 데이터베이스를 지정 하는 경우는 `/cfg \<configuration file name>` 명령줄 옵션 지정 해야 합니다.|
|cfg|(선택 사항)</br>분석을 위해 데이터베이스로 가져올 보안 서식 파일에 대 한 경로 파일 이름을 지정 합니다.</br>이 /cfg 옵션은 함께 사용할만 `/db \<database file name>` 매개 변수입니다. 지정 하지 않으면 데이터베이스에 이미 저장 된 모든 구성에 대해 분석이 수행 됩니다.|
|overwrite|(선택 사항)</br>/Cfg 매개 변수의 보안 템플릿을 템플릿 또는 저장 된 템플릿에 추가 하는 대신 데이터베이스에 저장 된 복합 서식 파일을 덮어써야 할지 여부를 지정 합니다.</br>이 명령줄 옵션 인 유효한 경우에는 `/cfg \<configuration file name>` 매개 변수에 사용 됩니다. 지정 하지 않으면 /cfg 매개 변수의 템플릿이 저장 된 템플릿에 추가 됩니다.|
|영역|(선택 사항)</br>시스템에 적용할 보안 영역을 지정 합니다. 이 매개 변수를 지정 하지 않으면 데이터베이스에 정의 된 모든 보안 설정은 시스템에 적용 됩니다. 여러 영역을 구성 하려면 각 영역을 공백으로 구분 합니다. 다음과 같은 보안 영역이 지원 됩니다.</br>-SecurityPolicy</br>    로컬 정책 및 도메인 정책에 대 한 계정 정책을 비롯 한 시스템 감사 정책, 보안 옵션 등에입니다.</br>-Group_Mgmt</br>    보안 서식 파일에 지정 된 모든 그룹에 대 한 제한 된 그룹 설정 합니다.</br>-User_Rights</br>    사용자 로그온 권한 및 권한 부여 합니다.</br>-RegKeys</br>    로컬 레지스트리 키의 보안입니다.</br>-파일 저장소</br>    로컬 파일 스토리지에 대 한 보안입니다.</br>-서비스</br>    정의 된 모든 서비스에 대 한 보안 합니다.|
|log|(선택 사항)</br>프로세스에 대 한 로그 파일의 경로 파일 이름을 지정합니다.|
|quiet|(선택 사항)</br>화면 및 로그 출력을 표시 하지 않습니다. 보안 구성 및 분석에 스냅인을 Microsoft Management Console (MMC)를 사용 하 여 분석 결과 보기 수 있습니다.|

## <a name="remarks"></a>주의

로그 파일에 대 한 경로를 지정 하지 않으면 기본 로그 파일 (*systemroot*\Users \*UserAccount<em>\My Documents\Security\Logs\*DatabaseName</em>)이 사용 됩니다.

Windows Server 2008 부터는 `Secedit /refreshpolicy` 바뀌었습니다 `gpupdate`합니다. 보안 설정을 새로 고치는 방법에 대 한 자세한 내용은 [Gpupdate](gpupdate.md)합니다.

## <a name="examples"></a><a name=BKMK_Examples></a>예와

보안 구성 및 분석 스냅인을 사용 하 여 만든 SecDbContoso.sdb 보안 데이터베이스에 보안 매개 변수에 대 한 분석을 수행 합니다. 직접 명령을 확인할 수 있도록 메시지를 표시 하는 SecAnalysisContosoFY11 올바르게 실행 파일에 출력 합니다.
```
Secedit /analyze /db C:\Security\FY11\SecDbContoso.sdb /log C:\Security\FY11\SecAnalysisContosoFY11.log
```
분석에서 일부 자질를 표시 하 여 보안 템플릿 SecContoso. i n s. 출력 메시지를 표시 하지 SecAnalysisContosoFY11 기존 파일을 전송 변경 내용을 통합을 다시 명령을 실행 합니다.
```
Secedit /configure /db C:\Security\FY11\SecDbContoso.sdb /cfg SecContoso.inf /overwrite /log C:\Security\FY11\SecAnalysisContosoFY11.xml /quiet
```

## <a name="additional-references"></a>추가 참조

-   [Secedit](secedit.md)
-   [Secedit:analyze](secedit-analyze.md)
-   - [명령줄 구문 키](command-line-syntax-key.md)