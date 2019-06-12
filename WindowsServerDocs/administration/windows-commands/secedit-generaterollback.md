---
title: secedit:generaterollback
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 385a6799-51a7-4fe3-bd73-10c7998b6680
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: aa655d80c2698430827ad814c2b476e526529323
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66441557"
---
# <a name="seceditgeneraterollback"></a>secedit:generaterollback



지정 된 구성 템플릿에 대 한 롤백 템플릿을 만들 수 있습니다. 이 명령을 사용할 수 있는 방법을의 예 참조 [예제](#BKMK_Examples)합니다.

## <a name="syntax"></a>구문

```
Secedit /generaterollback /db <database file name> /cfg <configuration file name> /rbk <rollback template file name> [log <log file name>] [/quiet]
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|db|필수.</br>분석은 수행할 저장된 된 구성을 포함 하는 데이터베이스의 경로 파일 이름을 지정 합니다.</br>파일 이름을 연결 된 보안 템플릿 (구성 파일에 표시 됨) 처럼 되지 않은 데이터베이스를 지정 하는 경우는 `/cfg \<configuration file name>` 명령줄 옵션 지정 해야 합니다.|
|cfg|필수.</br>분석을 위해 데이터베이스로 가져올 보안 서식 파일에 대 한 경로 파일 이름을 지정 합니다.</br>이 /cfg 옵션은 함께 사용할만 `/db \<database file name>` 매개 변수입니다. 지정 하지 않으면 데이터베이스에 이미 저장 된 모든 구성에 대해 분석이 수행 됩니다.|
|rbk|필수.</br>롤백 정보 기록 되는 보안 템플릿을 지정 합니다. 보안 템플릿 스냅인을 사용 하 여 보안 템플릿은 만듭니다. 이 명령을 사용 하 여 롤백 파일을 만들 수 있습니다.|
|log|(선택 사항)</br>프로세스에 대 한 로그 파일의 경로 파일 이름을 지정합니다.|
|quiet|(선택 사항)</br>화면 및 로그 출력을 표시 하지 않습니다. 보안 구성 및 분석에 스냅인을 Microsoft Management Console (MMC)를 사용 하 여 분석 결과 보기 수 있습니다.|

## <a name="remarks"></a>설명

로그 파일의 경로를 제공 하지 않으면, 기본 로그 파일 (*systemroot*\Users \*UserAccount<em>\My Documents\Security\Logs\*DatabaseName</em>.log) 사용 됩니다.

Windows Server 2008 부터는 `Secedit /refreshpolicy` 바뀌었습니다 `gpupdate`합니다. 보안 설정을 새로 고치는 방법에 대 한 자세한 내용은 [Gpupdate](gpupdate.md)합니다.

이 명령은 성공적으로 실행 "작업 완료 되었습니다." 상태는 및 로그 명시 된 보안 템플릿과 보안 정책 구성 간의 불일치만 합니다. 이러한 불일치는 scesrv.log에 나열 됩니다.

기존 롤백 템플릿을 지정 된 경우이 명령은 덮어씁니다. 이 명령을 사용 하 여 새 롤백 서식 파일을 만들 수 있습니다. 두 조건 중 하나에 대 한 추가 매개 변수 없이 필요 합니다.

## <a name="BKMK_Examples"></a>예제

보안 구성 및 분석 스냅인, SecTmplContoso.inf를 사용 하 여 보안 템플릿을 만든 후 원래 설정을 저장 하려면 rollback 구성 파일을 만듭니다. 동작 FY11 로그 파일을 작성 합니다.
```
Secedit /generaterollback /db C:\Security\FY11\SecDbContoso.sdb /cfg sectmplcontoso.inf /rbk sectmplcontosoRBK.inf /log C:\Security\FY11\SecAnalysisContosoFY11.log
```

#### <a name="additional-references"></a>추가 참조

-   [secedit](secedit.md)
-   [명령줄 구문 키](command-line-syntax-key.md)