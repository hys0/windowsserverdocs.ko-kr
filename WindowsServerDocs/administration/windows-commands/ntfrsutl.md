---
title: ntfrsutl
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d7721a19-5a87-4ab6-b816-65d2da2c811f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e94d2b0a9ca764a6e8a25a087817598e3f158581
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66436406"
---
# <a name="ntfrsutl"></a>ntfrsutl

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

내부 테이블, 스레드 및 NT 파일 복제 서비스에 대 한 정보를 메모리 덤프 \(NTFRS\)합니다. 로컬 및 원격 서버에 대해 실행 됩니다. NTFRS 서비스 제어 관리자에 대 한 복구 설정이 \(SCM\) 찾고 컴퓨터에서 중요 한 로그 이벤트를 보관 하는 데 중요할 수 있습니다. 이 도구는 이러한 설정을 검토 하는 편리한 방법을 제공 합니다.   
  
## <a name="syntax"></a>구문  
  
```  
ntfrsutl[idtable|configtable|inlog|outlog][<computer>]  
ntfrsutl[memory|threads|stage][<computer>]  
ntfrsutl ds[<computer>]  
ntfrsutl [sets][<computer>]  
ntfrsutl [version][<computer>]  
ntfrsutl poll[/quickly[=[<N>]]][/slowly[=[<N>]]][/now][<computer>]  
```  
  
### <a name="parameters"></a>매개 변수  
  
|  매개 변수  |                                                                                                                                                                                                                                                                                                                                        설명                                                                                                                                                                                                                                                                                                                                         |
|-------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   idtable   |                                                                                                                                                                                                                                                                                                                                          ID 테이블                                                                                                                                                                                                                                                                                                                                          |
| 구성 테이블 |                                                                                                                                                                                                                                                                                                                                  FRS 구성 테이블                                                                                                                                                                                                                                                                                                                                   |
|    인 로그    |                                                                                                                                                                                                                                                                                                                                        인바운드 로그                                                                                                                                                                                                                                                                                                                                         |
|   아웃 로그    |                                                                                                                                                                                                                                                                                                                                        아웃 바운드 로그                                                                                                                                                                                                                                                                                                                                        |
| <computer>  |                                                                                                                                                                                                                                                                                                                                  컴퓨터를 지정합니다.                                                                                                                                                                                                                                                                                                                                   |
|   메모리    |                                                                                                                                                                                                                                                                                                                                        메모리 사용                                                                                                                                                                                                                                                                                                                                        |
|   스레드   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
|    stage(단계)    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
|     ds      |                                                                                                                                                                                                                                                                                                                         DS의 NTFRS 서비스의 뷰를 나열합니다.                                                                                                                                                                                                                                                                                                                          |
|    설정     |                                                                                                                                                                                                                                                                                                                             활성 복제 세트를 지정합니다.                                                                                                                                                                                                                                                                                                                              |
|   version   |                                                                                                                                                                                                                                                                                                                       API 및 NTFRS 서비스 버전을 지정합니다.                                                                                                                                                                                                                                                                                                                        |
|    설문 조사     | 현재 폴링 간격을 지정합니다.<br /><br />매개 변수:<br /><br /><ul><li>**\/신속 하 게** \[ **\=** \[ <N> \] \] \(신속 하 게 폴링합니다\)<br /><br /><ul><li>**신속 하 게** \- 구성은 rectrieved 안정 될 때까지 신속 하 게를 폴링합니다.</li><li>**신속 하 게\=**  \- 신속 하 게 기본 분 간격으로 폴링합니다.</li><li>**신속 하 게\=**  <N> \- 신속 하 게 폴링합니다 모든 *N* 분</li></ul></li><li>**\/느린** \[ **\=** \[ <N> \] \] \(느리게 폴링합니다\)<br /><br /><ul><li>**느린** \- 안정적인 구성을 검색할 때까지 천천히를 폴링합니다</li><li>**느린\=**  \- 느리게 기본 분 간격으로 폴링합니다</li><li>**느린\=**  <N> \- 신속 하 게 폴링합니다 모든 *N* 분</li></ul></li><li>**\/이제** \(이제 폴링합니다\)</li></ul> |
|     \/?     |                                                                                                                                                                                                                                                                                                                            명령 프롬프트에 도움말을 표시합니다.                                                                                                                                                                                                                                                                                                                            |
  
## <a name="BKMK_Examples"></a>예제  
확인 하려면 파일 복제에 대 한 폴링 간격:  
  
```  
C:\Program Files\SupportTools>ntfrsutl poll wrkstn-1  
```  
  
현재 NTFRS 응용 프로그램 인터페이스를 확인 하려면 \(API\) 버전:  
  
```  
C:\Program Files\SupportTools>ntfrsutl version  
```  
  
## <a name="additional-references"></a>추가 참조  
  
-   [명령줄 구문 키](command-line-syntax-key.md)  
  
  
  

