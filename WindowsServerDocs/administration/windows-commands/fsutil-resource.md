---
ms.assetid: b198d8ca-a5b7-430f-8911-5cbb9f50484c
title: Fsutil 리소스
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: 2013173978838764b2ff83a8b7cbc35adc485264
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80844096"
---
# <a name="fsutil-resource"></a>Fsutil 리소스
>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8, Windows Server 2008 R2, Windows 7, Windows 2008, Windows Vista

보조 트랜잭션 리소스 관리자를 만들고, 시작 또는 트랜잭션 리소스 관리자를 중지 하거나 트랜잭션 리소스 관리자에 대 한 정보를 표시 및 다음 동작을 수정:

-   기본 트랜잭션 리소스 관리자에서 다음 탑재 트랜잭션 메타 데이터를 정리 합니다 여부

-   가용성 보다 일관성 작업을 사용 하려면 지정된 된 트랜잭션 리소스 관리자

-   일관성 보다 가용성 작업을 사용 하려면 지정 된 트랜잭션 리소스 관리자

-   실행 중인 트랜잭션 리소스 관리자의 특징

이 명령을 사용 하는 방법의 예제를 보려면 [예제](#BKMK_examples) 합니다.

## <a name="syntax"></a>구문

```
fsutil resource [create] <RmRootPathname>
fsutil resource [info] <RmRootPathname>
fsutil resource [setautoreset] {true|false} <DefaultRmRootPathname>
fsutil resource [setavailable] <RmRootPathname>
fsutil resource [setconsistent] <RmRootPathname>
fsutil resource [setlog] [growth {<Containers> containers|<Percent> percent} <RmRootPathname>] [maxextents <Containers> <RmRootPathname>] [minextents <Containers> <RmRootPathname>] [mode {full|undo} <RmRootPathname>] [rename <RmRootPathname>] [shrink <percent> <RmRootPathname>] [size <Containers> <RmRootPathname>]
fsutil resource [start] <RmRootPathname> [<RmLogPathname> <TmLogPathname>
fsutil resource [stop] <RmRootPathname>
```

#### <a name="parameters"></a>매개 변수

|        매개 변수        |                                                                                                                                                                                                                                        설명                                                                                                                                                                                                                                         |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|         create          |                                                                                                                                                                                                                    보조 트랜잭션 리소스 관리자를 만듭니다.                                                                                                                                                                                                                     |
|    <RmRootPathname>     |                                                                                                                                                                                                        트랜잭션 리소스 관리자 루트 디렉터리 전체 경로 지정합니다.                                                                                                                                                                                                         |
|          info           |                                                                                                                                                                                                            지정 된 트랜잭션 리소스 관리자 정보를 표시 합니다.                                                                                                                                                                                                            |
|      setautoreset       | 기본 트랜잭션 리소스 관리자의 다음 탑재 트랜잭션 메타 데이터를 정리 합니다 있는지 여부를 지정 합니다.<p>-설정 된 **setautoreset** 매개 변수를 **true** 지정할 트랜잭션 리소스 관리자가 기본적으로 다음 탑재 트랜잭션 메타 데이터를 정리 합니다.<br />-설정 된 **setautoreset** 매개 변수를 **false** 지정 기본적으로 트랜잭션 리소스 관리자의 다음 탑재 트랜잭션 메타 데이터 정리 되지 것입니다. |
| <DefaultRmRootPathname> |                                                                                                                                                                                                                       드라이브 이름 뒤에 콜론을 지정 합니다.                                                                                                                                                                                                                        |
|      setavailable       |                                                                                                                                                                                                 트랜잭션 리소스 관리자를 일관성 보다 가용성을 선호를 지정 합니다.                                                                                                                                                                                                 |
|      setconsistent      |                                                                                                                                                                                                 트랜잭션 리소스 관리자 일관성 가용성 보다를 선호를 지정 합니다.                                                                                                                                                                                                 |
|         setlog          |                                                                                                                                                                                                  트랜잭션 리소스 관리자를 이미 실행 되 고 특성을 변경 합니다.                                                                                                                                                                                                  |
|         증가          |                                                                                                  트랜잭션 리소스 관리자 로그가 증가할 수 있는 크기를 지정 합니다.<p>증가 매개 변수는 다음과 같이 지정할 수 있습니다.<p>-형식을 사용 하는 컨테이너의 수: _컨테이너_**컨테이너**<br />-형식을 사용 하 여 백분율: _%_ **%**                                                                                                   |
|      <containers>       |                                                                                                                                                                                                      트랜잭션 리소스 관리자에서 사용 되는 데이터 개체를 지정 합니다.                                                                                                                                                                                                       |
|        maxextent        |                                                                                                                                                                                                컨테이너의 최대 수에 대 한 지정된 된 트랜잭션 리소스 관리자를 지정합니다.                                                                                                                                                                                                |
|        minextent        |                                                                                                                                                                                                컨테이너의 최소 수에 대 한 지정된 된 트랜잭션 리소스 관리자를 지정합니다.                                                                                                                                                                                                |
|  {전체 &#124; 실행 취소} 모드  |                                                                                                                                                                                        모든 트랜잭션을 기록할지 ( **full**) 아니면 롤백 이벤트만 기록할지 (**실행 취소**) 지정 합니다.                                                                                                                                                                                         |
|         이름 바꾸기          |                                                                                                                                                                                                                  트랜잭션 리소스 관리자에 대 한 GUID를 변경합니다.                                                                                                                                                                                                                  |
|         축소          |                                                                                                                                                                                              트랜잭션 리소스 관리자 로그 자동으로 줄일 수 있는 백분율을 지정 합니다.                                                                                                                                                                                              |
|          size           |                                                                                                                                                                                              트랜잭션 리소스 관리자의 크기를 지정된 된 수로 지정 *컨테이너*합니다.                                                                                                                                                                                               |
|          시작          |                                                                                                                                                                                                                    지정된 된 트랜잭션 리소스 관리자를 시작합니다.                                                                                                                                                                                                                    |
|          stop           |                                                                                                                                                                                                                    지정된 된 트랜잭션 리소스 관리자를 중지합니다.                                                                                                                                                                                                                     |

### <a name="examples"></a><a name="BKMK_examples"></a>예와
C:\test에서 지정 하는 트랜잭션 리소스 관리자의 로그를 설정 하려면 5 개의 컨테이너를 자동으로 증가 시키려면 다음을 입력 합니다.

```
fsutil resource setlog growth 5 containers c:test
```

C:\test에 지정 된 트랜잭션 리소스 관리자에 대 한 로그를 설정 하려면 2%의 자동 증가를 수행 하려면 다음을 입력 합니다.

```
fsutil resource setlog growth 2 percent c:test
```

트랜잭션 리소스 관리자 기본 C 드라이브에서 다음 탑재 트랜잭션 메타 데이터를 정리 합니다를 지정 하려면 다음을 입력 합니다.

```
fsutil resource setautoreset true c:\  
```

### <a name="additional-references"></a>추가 참조
- [명령줄 구문 키](command-line-syntax-key.md)

[Fsutil](Fsutil.md)

[트랜잭션 NTFS](https://go.microsoft.com/fwlink/?LinkID=165402)


