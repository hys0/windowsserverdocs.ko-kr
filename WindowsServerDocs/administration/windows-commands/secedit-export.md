---
title: 'secedit: 내보내기'
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 49a8b241-aa8c-45b7-844d-67a29fab708e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2aed2774bcba1ac3d5ba828901586acbbe24d255
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71384252"
---
# <a name="seceditexport"></a>secedit: 내보내기



보안 템플릿을 사용 하 여 구성 된 데이터베이스에 저장 된 보안 설정을 내보냅니다. 이 명령을 사용할 수 있는 방법을의 예 참조 [예제](#BKMK_Examples)합니다.

## <a name="syntax"></a>구문

```
Secedit /export /db <database file name> [/mergedpolicy] /cfg <configuration file name> [/areas [securitypolicy | group_mgmt | user_rights | regkeys | filestore | services]] [/log <log file name>] [/quiet]
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|db|필수.</br>분석은 수행할 저장된 된 구성을 포함 하는 데이터베이스의 경로 파일 이름을 지정 합니다.</br>파일 이름을 연결 된 보안 템플릿 (구성 파일에 표시 됨) 처럼 되지 않은 데이터베이스를 지정 하는 경우는 `/cfg \<configuration file name>` 명령줄 옵션 지정 해야 합니다.|
|mergedpolicy|(선택 사항)</br>병합 하 고 도메인 및 로컬 정책 보안 설정을 내보냅니다.|
|cfg|필수.</br>분석을 위해 데이터베이스로 가져올 보안 서식 파일에 대 한 경로 파일 이름을 지정 합니다.</br>이 /cfg 옵션은 함께 사용할만 `/db \<database file name>` 매개 변수입니다. 지정 하지 않으면 데이터베이스에 이미 저장 된 모든 구성에 대해 분석이 수행 됩니다.|
|영역|(선택 사항)</br>시스템에 적용할 보안 영역을 지정 합니다. 이 매개 변수를 지정 하지 않으면 데이터베이스에 정의 된 모든 보안 설정은 시스템에 적용 됩니다. 여러 영역을 구성 하려면 각 영역을 공백으로 구분 합니다. 다음과 같은 보안 영역이 지원 됩니다.</br>-SecurityPolicy</br>    로컬 정책 및 도메인 정책에 대 한 계정 정책을 비롯 한 시스템 감사 정책, 보안 옵션 등에입니다.</br>-Group_Mgmt</br>    보안 서식 파일에 지정 된 모든 그룹에 대 한 제한 된 그룹 설정 합니다.</br>-User_Rights</br>    사용자 로그온 권한 및 권한 부여 합니다.</br>-RegKeys</br>    로컬 레지스트리 키의 보안입니다.</br>-파일 저장소</br>    로컬 파일 저장소에 대 한 보안입니다.</br>-서비스</br>    정의 된 모든 서비스에 대 한 보안 합니다.|
|log|(선택 사항)</br>프로세스에 대 한 로그 파일의 경로 파일 이름을 지정합니다.|
|quiet|(선택 사항)</br>화면 및 로그 출력을 표시 하지 않습니다. 보안 구성 및 분석에 스냅인을 Microsoft Management Console (MMC)를 사용 하 여 분석 결과 보기 수 있습니다.|

## <a name="remarks"></a>설명

보안 정책 설정을 다른 컴퓨터로 가져올 뿐만 아니라 로컬 컴퓨터에 백업 하려면이 명령을 사용할 수 있습니다.

로그 파일에 대 한 경로를 지정 하지 않으면 기본 로그 파일 (*systemroot*\Documents and Settings\*UserAccount<em>\My Documents\Security\Logs\*DatabaseName</em>)이 사용 됩니다.

Windows Server 2008에서 `Secedit /refreshpolicy` 바뀌었습니다 `gpupdate`합니다. 보안 설정을 새로 고치는 방법에 대 한 자세한 내용은 [Gpupdate](gpupdate.md)합니다.

## <a name="BKMK_Examples"></a>예와

보안 데이터베이스와 도메인 보안 정책 inf 파일을 내보낸 다음 다른 컴퓨터의 보안 정책 설정을 복제 하려면 다른 데이터베이스에 해당 파일을 가져옵니다.
```
Secedit /export /db C:\Security\FY11\SecDbContoso.sdb /mergedpolicy /cfg SecContoso.inf /log C:\Security\FY11\SecAnalysisContosoFY11.log /quiet
```
다른 컴퓨터에서 다른 데이터베이스에 해당 파일을 가져옵니다.
```
Secedit /import /db C:\Security\FY12\SecDbContoso.sdb /cfg SecContoso.inf /log C:\Security\FY11\SecAnalysisContosoFY12.log /quiet
```

#### <a name="additional-references"></a>추가 참조

-   [Secedit:import](secedit-import.md)
-   [Secedit](secedit.md)
-   [명령줄 구문 키](command-line-syntax-key.md)