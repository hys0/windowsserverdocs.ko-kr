---
title: 'secedit: 분석'
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3430cf9d-1411-48b1-b5a9-2e47701dc87f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 83f9e977a059e1a1f1b882d5a968054dacf6b3be
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70868872"
---
# <a name="seceditanalyze"></a>secedit: 분석



데이터베이스에 저장 된 초기 설정에 대 한 현재 시스템 설정을 분석할 수 있습니다. 이 명령을 사용할 수 있는 방법을의 예 참조 [예제](#BKMK_Examples)합니다.

## <a name="syntax"></a>구문

```
Secedit /analyze /db <database file name> [/cfg <configuration file name>] [/overwrite] [/log <log file name>] [/quiet}]
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|db|필수.</br>분석은 수행할 저장된 된 구성을 포함 하는 데이터베이스의 경로 파일 이름을 지정 합니다.</br>파일 이름을 연결 된 보안 템플릿 (구성 파일에 표시 됨) 처럼 되지 않은 데이터베이스를 지정 하는 경우는 `/cfg \<configuration file name>` 명령줄 옵션 지정 해야 합니다.|
|cfg|(선택 사항)</br>분석을 위해 데이터베이스로 가져올 보안 서식 파일에 대 한 경로 파일 이름을 지정 합니다.</br>이 /cfg 옵션은 함께 사용할만 `/db \<database file name>` 매개 변수입니다. 지정 하지 않으면 데이터베이스에 이미 저장 된 모든 구성에 대해 분석이 수행 됩니다.|
|overwrite|(선택 사항)</br>/Cfg 매개 변수의 보안 템플릿을 템플릿 또는 저장 된 템플릿에 추가 하는 대신 데이터베이스에 저장 된 복합 서식 파일을 덮어써야 할지 여부를 지정 합니다.</br>이 명령줄 옵션 인 유효한 경우에는 `/cfg \<configuration file name>` 매개 변수에 사용 됩니다. 지정 하지 않으면 /cfg 매개 변수의 템플릿이 저장 된 템플릿에 추가 됩니다.|
|log|(선택 사항)</br>프로세스에서 사용 될 로그 파일의 경로 파일 이름을 지정 합니다.|
|quiet|(선택 사항)</br>화면 출력을 표시 하지 않습니다. 보안 구성 및 분석에 스냅인을 Microsoft Management Console (MMC)를 사용 하 여 분석 결과 보기 수 있습니다.|

## <a name="remarks"></a>설명

분석 결과가 데이터베이스의 다른 영역에 저장 되 고 보안 구성 및 분석에 스냅인을 MMC에서 볼 수 있습니다.

로그 파일에 대 한 경로를 지정 하지 않으면 기본 로그 파일 (*systemroot*\Documents and Settings\*UserAccount<em>\My Documents\Security\Logs\*DatabaseName</em>)이 사용 됩니다.

Windows Server 2008에서 `Secedit /refreshpolicy` 바뀌었습니다 `gpupdate`합니다. 보안 설정을 새로 고치는 방법에 대 한 자세한 내용은 [Gpupdate](gpupdate.md)합니다.

## <a name="BKMK_Examples"></a>예와

보안 구성 및 분석 스냅인을 사용 하 여 만든 SecDbContoso.sdb 보안 데이터베이스에 보안 매개 변수에 대 한 분석을 수행 합니다. 직접 명령을 확인할 수 있도록 메시지를 표시 하는 SecAnalysisContosoFY11 올바르게 실행 파일에 출력 합니다.
```
Secedit /analyze /db C:\Security\FY11\SecDbContoso.sdb /log C:\Security\FY11\SecAnalysisContosoFY11.log
```
분석에서 일부 자질를 표시 하 여 보안 템플릿 SecContoso. i n s. 출력 메시지를 표시 하지 SecAnalysisContosoFY11 기존 파일을 전송 변경 내용을 통합을 다시 명령을 실행 합니다.
```
Secedit /analyze /db C:\Security\FY11\SecDbContoso.sdb /cfg SecContoso.inf /overwrite /log C:\Security\FY11\SecAnalysisContosoFY11.xml /quiet
```

#### <a name="additional-references"></a>추가 참조

-   [Secedit](secedit.md)
-   [명령줄 구문 키](command-line-syntax-key.md)