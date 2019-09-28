---
title: Scwcmd 구성
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6528b9dc-3d82-4228-b734-ed717458d74c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 43bd70c33294b09f63b9718e4c0f2cdc6cace156
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71384295"
---
# <a name="scwcmd-configure"></a>Scwcmd: 구성

> 적용 대상: Windows Server 2012 R2, Windows Server 2012

컴퓨터에는 SCW 보안 구성 마법사에서 생성 된 보안 정책을 적용합니다. 이 명령줄 도구는 입력으로 컴퓨터 이름 목록도 받아들입니다.

## <a name="syntax"></a>구문

```
scwcmd configure [[[/m:<ComputerName> | /ou:<OuName>] /p:<Policy>] | /i:<ComputerList>] [/u:<UserName>] [/pw:<Password>] [/t:<Threads>]
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|/m: \<ComputerName >|NetBIOS 이름, DNS 이름 또는 구성 하는 컴퓨터의 IP 주소를 지정 합니다. 하는 경우는 **/m** 매개 변수를 지정 하면 **/p** 매개 변수도 지정 해야 합니다.|
|/ou: \<OuName >|Active Directory 도메인 서비스에 조직 구성 단위 (OU)의 정규화 된 도메인 이름 (FQDN)을 지정합니다. 하는 경우는 **/ou** 매개 변수를 지정 하면 **/p** 매개 변수도 지정 해야 합니다. OU의 모든 컴퓨터는 지정 된 정책에 따라 분석 됩니다.|
|/p: \<Policy >|구성을 수행 하는 데 사용할.xml 정책 파일의 경로 파일 이름을 지정 합니다.|
|/i: \<ComputerList >|예상 되는 정책 파일과 함께 컴퓨터의 목록이 포함 된.xml 파일의 경로 파일 이름을 지정 합니다. .Xml 파일에 있는 모든 컴퓨터는 해당 정책 파일에 따라 구성 됩니다. 샘플.xml 파일은 %windir%\security\SampleMachineList.xml.|
|/u: \< 사용자 이름 >|원격 컴퓨터를 구성할 때 사용 하는 대체 사용자 자격 증명을 지정 합니다. 기본값은 로그온 된 사용자입니다.|
|/pw: \<Password >|원격 컴퓨터를 구성할 때 사용 하는 대체 사용자 자격 증명을 지정 합니다. 기본값은 로그온된 한 사용자의 암호입니다.|
|/t: \<Threads >|구성 프로세스 중에 유지 해야 하는 동시 처리 중인 구성 작업의 수를 지정 합니다 (DefaultValue 40, MinValue = = 1, MaxValue = 1000)입니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명

Scwcmd.exe은 Windows Server 2008 R2, Windows Server 2008 또는 Windows Server 2003을 실행 하는 컴퓨터에서 사용할 수만 있습니다.

## <a name="BKMK_Examples"></a>예와

파일 webpolicy.xml에 대 한 보안 정책을 구성 하려면 다음을 입력 합니다.
```
scwcmd configure /p:webpolicy.xml
```
컴퓨터에 대 한 보안 정책에 대해 파일 webpolicy.xml 172.16.0.0 webadmin 계정 자격 증명을 사용 하 여를 구성 하려면 다음을 입력 합니다.
```
scwcmd configure /m:172.16.0.0 /p:webpolicy.xml /u:webadmin
```
보안 정책에는 최대 100 개의 스레드 목록 campusmachines.xml에 있는 모든 컴퓨터를 구성 하려면 다음을 입력 합니다.
```
scwcmd configure /i:campusmachines.xml /t:100
```
DomainAdmin 계정의 자격 증명을 사용 하 여 파일 webpolicy.xml에 대해 WebServers OU의 모든 컴퓨터에는 보안 정책을 구성 하려면 다음을 입력 합니다.
```
scwcmd configure /ou:OU=WebServers,DC=Marketing,DC=ABCCompany,DC=com /p:webpolicy.xml /u:DomainAdmin
```

#### <a name="additional-references"></a>추가 참조

-   [명령줄 구문 키](command-line-syntax-key.md)