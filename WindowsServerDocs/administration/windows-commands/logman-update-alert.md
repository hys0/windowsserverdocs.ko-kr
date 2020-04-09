---
title: logman 업데이트 경고
description: '\* * * *에 대 한 Windows 명령 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ede94a76-931c-40ed-9fda-6766bed8ff72 britw
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 13bd7fbef96b75d9308b1e2c8475389d10bbb921
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80840606"
---
# <a name="logman-update-alert"></a>logman 업데이트 경고

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

기존 경고 데이터 수집기의 속성을 업데이트 합니다.  

## <a name="syntax"></a>구문  
```  
logman update alert <[-n] <name>> [options]  
```  
### <a name="parameters"></a>매개 변수  

|                 매개 변수                  |                                                                               설명                                                                               |
|--------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                     /?                     |                                                                    도움말 상황에 맞는 표시 합니다.                                                                     |
|             -s <computer name>             |                                                          지정된 된 원격 컴퓨터에서 명령을 수행 합니다.                                                          |
|              -config <value>               |                                                         명령 옵션을 포함 하는 설정 파일을 지정 합니다.                                                         |
|                [-n] <name>                 |                                                                       대상 개체의 이름입니다.                                                                        |
|          -[-u < 사용자 [password] >           | 사용자 계정으로 실행을 지정합니다. 암호에 대 한 \*를 입력 하면 암호를 묻는 메시지가 생성 됩니다. 암호 프롬프트에서 입력할 때 암호 표시 되지 않습니다. |
| -m < [시작] [stop] [[시작] [stop] [...]] > |                                                예약 된 시작 시간 또는 종료 시간 대신 수동 시작 또는 중지로 변경 합니다.                                                 |
|             -rf < [[hh:] mm:] ss >             |                                                        지정 된 기간에 대 한 데이터 수집기를 실행 합니다.                                                         |
|     -b < M/d/yyyy h:mm: ss [AM (& a) #124; PM] >      |                                                              지정된 된 시간에 데이터 수집을 시작 합니다.                                                               |
|     -e < M/d/yyyy h:mm: ss [AM (& a) #124; PM] >      |                                                               지정된 된 시간에 대 한 데이터 수집을 종료 합니다.                                                                |
|             -si < [[hh:] mm:] ss >             |                                                 성능 카운터 데이터 수집기에 대 한 샘플 간격을 지정합니다.                                                  |
|           -o < 경로 & #124; dsn! 로그 >           |                                              SQL 데이터베이스에 출력 로그 파일 또는 DSN 및 로그 설정 이름을 지정 합니다.                                               |
|                   -[-]r                    |                                                  지정 된 시작 및 종료 시간에 매일 데이터 수집기를 반복 합니다.                                                  |
|                   -[-]a                    |                                                                     기존 로그 파일에 추가 합니다.                                                                     |
|                   -[-] ow                   |                                                                     기존 로그 파일을 덮어씁니다.                                                                     |
|        -[-v < nnnnnn & #124; mmddhhmm >        |                                                   로그 파일 이름 끝에 파일 버전 정보를 첨부 합니다.                                                   |
|               -[-] rc <task>                |                                                         지정 된 명령을 실행 될 때마다 로그가 닫힙니다.                                                          |
|              -[-] 최대 <value>               |                                                 최대 로그 파일 크기 (mb) 또는 SQL 로그에 대 한 레코드의 최대 수입니다.                                                  |
|           -[-] cnf < [[hh:] mm:] ss >           |     시간을 지정 하면 지정 된 시간이 경과 하는 경우 새 파일을 만듭니다. 시간을 지정 하지 않으면, 최대 크기를 초과 하는 경우 새 파일을 만듭니다.     |
|                     -y                     |                                                             메시지를 표시 하지 않고 모든 질문에 예로 답변 합니다.                                                              |
|               -cf <filename>               |                       수집할 성능 카운터를 나열 하는 파일을 지정 합니다. 파일에는 줄당 하나의 성능 카운터 이름을 포함 되어야 합니다.                        |
|                   -[-] el                   |                                                                이벤트 로그 보고를 사용 하지 않도록 설정 하거나 사용 합니다.                                                                 |
|     번째 < 임계값 [임계값 [...]] >      |                                                        카운터와 경고의 임계값을 지정 합니다.                                                        |
|              -[-] rdcs <name>               |                                                     경고가 발생할 때 시작 하도록 데이터 수집기 집합을 지정 합니다.                                                      |
|               -[-] tn <task>                |                                                             경고가 발생할 때 실행 되도록 작업을 지정 합니다.                                                              |
|            -[-] targ <argument>             |                                               -Tn를 사용 하 여 지정한 작업에 사용할 작업 인수를 지정 합니다.                                                |

## <a name="remarks"></a>주의  
[-] 나열 되는 위치는 추가 된-옵션을 부정 합니다.  
## <a name="examples"></a><a name=BKMK_examples></a>예와  
다음 예에서는 프로세서 (_Total) 카운터 그룹의 카운터% Processor time에 대 한 임계값을 40%로 설정 하 new_alert 기존 데이터 수집기를 업데이트 합니다.  
```  
logman update alert new_alert -th \Processor(_Total)\% Processor time>40  
```  
## <a name="additional-references"></a>추가 참조  
[logman](logman.md)  
[logman 경고 만들기](logman-create-alert.md)  
