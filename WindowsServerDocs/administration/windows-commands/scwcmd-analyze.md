---
title: Scwcmd 분석
description: '* * * *에 대 한 참조 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0259271b-be5b-48d7-a51d-8b9b6786efb4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 017363ff2a60f9348290813c357560fe9fe3ba2a
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82722157"
---
# <a name="scwcmd-analyze"></a>Scwcmd: 분석

> 적용 대상: Windows Server 2012 R2, Windows Server 2012

컴퓨터 정책을 준수 하는지 여부를 결정 합니다. .Xml 파일에 결과가 반환 됩니다. 컴퓨터 이름의 목록을 입력으로 받기도 합니다. 브라우저에서 결과 보려면 사용 하 여 **scwcmd 보기** 지정 **%windir%\security\msscw\TransformFiles\scwanalysis.xsl** .xsl 변환으로 합니다.

## <a name="syntax"></a>구문

```
scwcmd analyze [[[/m:<ComputerName> | /ou:<Ou>] /p:<Policy>] | /i:<ComputerList>] [/o:
<ResultDir>] [/u:<UserName>] [/pw:<Password>] [/t:<Threads>] [/l] [/e]
```

#### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|/m:\<ComputerName>|NetBIOS 이름, DNS 이름 또는 분석할 컴퓨터의 IP 주소를 지정 합니다. 하는 경우는 **/m** 매개 변수를 지정 하면 **/p** 매개 변수도 지정 해야 합니다.|
|/ou:\<ouname>|Active Directory 도메인 서비스에 조직 구성 단위 (OU)의 정규화 된 도메인 이름 (FQDN)을 지정합니다. 하는 경우는 **/ou** 매개 변수를 지정 하면 **/p** 매개 변수도 지정 해야 합니다. OU의 모든 컴퓨터는 해당된 정책에 대해 분석 됩니다.|
|/p:\<Policy>|분석을 수행 하는 데 사용할.xml 정책 파일의 경로 파일 이름을 지정 합니다.|
|/i:\<computerlist>|예상 되는 정책 파일과 함께 컴퓨터의 목록이 포함 된.xml 파일의 경로 파일 이름을 지정 합니다. .Xml 파일에 있는 모든 컴퓨터는 해당 정책 파일에 대해 분석 됩니다. 샘플.xml 파일은 %windir%\security\SampleMachineList.xml.|
|/o:\<resultdir>|경로 분석 결과 파일을 저장할 디렉터리를 지정 합니다. 기본값은 현재 디렉터리입니다.|
|/u:\<UserName>|원격 컴퓨터에서 분석을 수행할 때 사용 하는 대체 사용자 자격 증명을 지정 합니다. 기본값은 로그온 된 사용자입니다.|
|/pw:\<암호>|원격 컴퓨터에서 분석을 수행할 때 사용 하는 대체 사용자 자격 증명을 지정 합니다. 기본값은 로그온된 한 사용자의 암호입니다.|
|/t:\<스레드>|분석 하는 동안 유지 해야 하는 동시 처리 중인 분석 작업의 수를 지정 합니다 (DefaultValue 40, MinValue = = 1, MaxValue = 1000)입니다.|
|/l|분석 프로세스를 기록 하면 합니다. 분석 되 고 각 컴퓨터에 대해 하나의 로그 파일이 생성 됩니다. 로그 파일은 결과 파일과 동일한 디렉터리에 저장 됩니다. 사용 하 여 **/o** 결과 파일의 디렉터리를 지정 하는 옵션입니다.|
|/e|불일치가 발견 되는 경우 애플리케이션 이벤트 로그에 이벤트를 기록 합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명

Scwcmd.exe은 Windows Server 2008 R2, Windows Server 2008 또는 Windows Server 2003을 실행 하는 컴퓨터에서 사용할 수만 있습니다.

## <a name="examples"></a>예

파일 webpolicy.xml에 대 한 보안 정책을 분석 하려면 다음을 입력 합니다.
```
scwcmd analyze /p:webpolicy.xml

```
Webadmin 계정의 자격 증명을 사용 하 여 웹 서버에 대 한 파일 webpolicy.xml 이라는 컴퓨터의 보안 정책을 분석 하려면 다음을 입력 합니다.
```
scwcmd analyze /m:webserver /p:webpolicy.xml /u:webadmin

```
파일 webpolicy.xml 최대 100 개의 스레드를의 대 한 보안 정책 분석 결과 resultserver 공유에 대 한 결과 라는 이름의 파일에 출력을 입력 합니다.
```
scwcmd analyze /i:webpolicy.xml /t:100 /o:\\resultserver\results

```
보안 정책 파일 webpolicy.xml에 대해 WebServers OU에 대 한 DomainAdmin 자격 증명을 사용 하 여를 분석 하려면 다음을 입력 합니다.
```
scwcmd analyze /ou:OU=WebServers,DC=Marketing,DC=ABCCompany,DC=com /p:webpolicy.xml /u:DomainAdmin
```

## <a name="additional-references"></a>추가 참조

-   - [명령줄 구문 키](command-line-syntax-key.md)