---
title: logman 업데이트 카운터
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 607df6d5-876c-428d-a0b3-f59cb244e2ce britw
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9a6ab1f75892bf8473714e0201c2a6db25cad426
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59866774"
---
# <a name="logman-update-counter"></a>logman 업데이트 카운터

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

기존 카운터 데이터 수집기의 속성을 업데이트 합니다.  
  
## <a name="syntax"></a>구문  
```  
logman update counter <[-n] <name>> [options]  
```  
## <a name="parameters"></a>매개 변수  
|매개 변수|설명|  
|-------|--------|  
|/?|도움말 상황에 맞는 표시 합니다.|  
|-s <computer name>|지정된 된 원격 컴퓨터에서 명령을 수행 합니다.|  
|-config <value>|명령 옵션을 포함 하는 설정 파일을 지정 합니다.|  
|[-n] <name>|대상 개체의 이름입니다.|  
|-f < bin &#124, bincirc &#124, csv 및 #124; tsv &#124, sql >|데이터 수집기에 대 한 로그 형식을 지정합니다.|  
|-[-u < 사용자 [password] >|사용자 계정으로 실행을 지정합니다. 입력 한 * 암호에 대 한 프롬프트를 생성 하는 암호에 대 한 합니다. 암호 프롬프트에서 입력할 때 암호 표시 되지 않습니다.|  
|-m < [시작] [stop] [[시작] [stop] [...]] >|수동 시작 변경 하거나 예약된 된 시작 또는 끝 시간 대신 중지 합니다.|  
|-rf < [[hh:] mm:] ss >|지정 된 기간에 대 한 데이터 수집기를 실행 합니다.|  
|-b < M/d/yyyy h:mm: ss [AM&#124;PM] >|지정된 된 시간에 데이터 수집을 시작 합니다.|  
|-e < M/d/yyyy h:mm: ss [AM&#124;PM] >|지정된 된 시간에 대 한 데이터 수집을 종료 합니다.|  
|-si < [[hh:] mm:] ss >|성능 카운터 데이터 수집기에 대 한 샘플 간격을 지정합니다.|  
|-o < 경로 &#124; dsn! 로그 >|SQL 데이터베이스에 출력 로그 파일 또는 DSN 및 로그 설정 이름을 지정 합니다.|  
|-[-]r|지정 된 시작 및 종료 시간에 매일 데이터 수집기를 반복 합니다.|  
|-[-]a|기존 로그 파일을 추가 합니다.|  
|-[-] ow|기존 로그 파일을 덮어씁니다.|  
|-[-v < nnnnnn &#124; mmddhhmm >|파일 버전 정보를 로그 파일 이름 끝에 연결 합니다.|  
|-[-]rc <task>|지정 된 명령을 실행 될 때마다 로그가 닫힙니다.|  
|-[-] 최대 <value>|최대 로그 파일 크기 (mb) 또는 SQL 로그에 대 한 레코드의 최대 수입니다.|  
|-[-] cnf < [[hh:] mm:] ss >|시간을 지정 하면 지정 된 시간이 경과 하는 경우 새 파일을 만듭니다. 시간을 지정 하지 않으면, 최대 크기를 초과 하는 경우 새 파일을 만듭니다.|  
|-y|메시지를 표시 하지 않고 모든 질문에 예로 답변 합니다.|  
|-cf <filename>|수집할 성능 카운터를 나열 하는 파일을 지정 합니다. 파일에는 줄당 하나의 성능 카운터 이름을 포함 되어야 합니다.|  
|-c <path [path [ ]]>|수집할 성능 카운터를 지정 합니다.|  
|-sc <value>|성능 카운터 데이터 수집기와 함께 수집 하는 샘플의 최대 수를 지정 합니다.|  
## <a name="remarks"></a>설명  
[-] 나열 되는 위치는 추가 된-옵션을 부정 합니다.  
## <a name="BKMK_examples"></a>예제  
다음 명령은 10과 CSV로 로그 형식 및 형식 mmddhhmm의 로그 파일 이름에 추가 버전 관리를 샘플 간격을 변경 하는 데이터 수집기 perf_log를 업데이트 합니다.  
```  
logman update perf_log -si 10 -f csv -v mmddhhmm  
```  
#### <a name="additional-references"></a>추가 참조  
[logman](logman.md)  
[logman 카운터 만들기](logman-create-counter.md)  
