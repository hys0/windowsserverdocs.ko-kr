---
title: ntfrsutl
description: '* * * *에 대 한 참조 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d7721a19-5a87-4ab6-b816-65d2da2c811f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 698237380d02fb1ceb4e738c6fb4f083dd31aef3
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82723460"
---
# <a name="ntfrsutl"></a>ntfrsutl

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

내부 테이블, 스레드 및 NT 파일 복제 서비스에 대 한 정보를 메모리 덤프 \(NTFRS\)합니다. 로컬 및 원격 서버에 대해 실행 됩니다. 컴퓨터에서 중요 한 로그 이벤트를 찾고 유지 \(하려면\) 서비스 제어 관리자 SCM의 NTFRS에 대 한 복구 설정이 중요할 수 있습니다. 이 도구는 이러한 설정을 검토 하는 편리한 방법을 제공 합니다.   
  
## <a name="syntax"></a>구문  
  
```  
ntfrsutl[idtable|configtable|inlog|outlog][<computer>]  
ntfrsutl[memory|threads|stage][<computer>]  
ntfrsutl ds[<computer>]  
ntfrsutl [sets][<computer>]  
ntfrsutl [version][<computer>]  
ntfrsutl poll[/quickly[=[<N>]]][/slowly[=[<N>]]][/now][<computer>]  
```  
  
#### <a name="parameters"></a>매개 변수  
  
|  매개 변수  |                                                                                                                                                                                                                                                                                                                                        설명                                                                                                                                                                                                                                                                                                                                         |
|-------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   idtable   |                                                                                                                                                                                                                                                                                                                                          ID 테이블                                                                                                                                                                                                                                                                                                                                          |
| 구성 테이블 |                                                                                                                                                                                                                                                                                                                                  FRS 구성 테이블                                                                                                                                                                                                                                                                                                                                   |
|    인 로그    |                                                                                                                                                                                                                                                                                                                                        인바운드 로그                                                                                                                                                                                                                                                                                                                                         |
|   아웃 로그    |                                                                                                                                                                                                                                                                                                                                        아웃 바운드 로그                                                                                                                                                                                                                                                                                                                                        |
| <computer>  |                                                                                                                                                                                                                                                                                                                                  컴퓨터를 지정합니다.                                                                                                                                                                                                                                                                                                                                   |
|   메모리    |                                                                                                                                                                                                                                                                                                                                        메모리 사용량                                                                                                                                                                                                                                                                                                                                        |
|   스레드   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
|    stage(단계)    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
|     ds      |                                                                                                                                                                                                                                                                                                                         DS의 NTFRS 서비스 보기를 나열 합니다.                                                                                                                                                                                                                                                                                                                          |
|    설정     |                                                                                                                                                                                                                                                                                                                             활성 복제 세트를 지정합니다.                                                                                                                                                                                                                                                                                                                              |
|   버전   |                                                                                                                                                                                                                                                                                                                       API 및 NTFRS 서비스 버전을 지정합니다.                                                                                                                                                                                                                                                                                                                        |
|    설문 조사     | 현재 폴링 간격을 지정합니다.<p>매개 변수<p><ul><li>**\/신속 하 게 신속 하 게 폴링** \[ **\=** \[ \] \( <N> \]  \)<p><ul><li>**신속 하 게** \- 구성은 rectrieved 안정 될 때까지 신속 하 게를 폴링합니다.</li><li>**신속 하 게\=** \- 신속 하 게 기본 분 간격으로 폴링합니다.</li><li>**신속 하 게\=**<N> \- 신속 하 게 폴링합니다 모든 *N* 분</li></ul></li><li>**\/느린 폴링** \[ **\=** \[ <N> \] \] \(\)<p><ul><li>**느린** \- 안정적인 구성을 검색할 때까지 천천히를 폴링합니다.</li><li>**느린\=** \- 느리게 기본 분 간격으로 폴링합니다</li><li>**느린\=**<N> \- 신속 하 게 폴링합니다 모든 *N* 분</li></ul></li><li>** \/지금** \(설문 조사\)</li></ul> |
|     \/?     |                                                                                                                                                                                                                                                                                                                            명령 프롬프트에 도움말을 표시합니다.                                                                                                                                                                                                                                                                                                                            |
  
## <a name="examples"></a>예  
확인 하려면 파일 복제에 대 한 폴링 간격:  
  
```  
C:\Program Files\SupportTools>ntfrsutl poll wrkstn-1  
```  
  
현재 NTFRS 애플리케이션 인터페이스를 확인 하려면 \(API\) 버전:  
  
```  
C:\Program Files\SupportTools>ntfrsutl version  
```  
  
## <a name="additional-references"></a>추가 참조  
  
-   - [명령줄 구문 키](command-line-syntax-key.md)  
  
  
  

