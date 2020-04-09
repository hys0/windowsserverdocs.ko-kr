---
title: 이벤트 ID 50 오류 메시지 문제 해결
description: 이벤트 ID 50 오류 메시지 문제를 해결 하는 방법을 설명 합니다.
author: Deland-Han
manager: dcscontentpm
ms.topic: article
ms.author: delhan
ms.date: 12/25/2019
ms.openlocfilehash: 7ce3551b60450a3720c9350b5c55f396368490c1
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80815236"
---
# <a name="troubleshoot-the-event-id-50-error-message"></a>이벤트 ID 50 오류 메시지 문제 해결

##  <a name="symptoms"></a>증상

정보를 실제 디스크에 기록 하는 경우 다음과 같은 두 이벤트 메시지가 시스템 이벤트 로그에 기록 될 수 있습니다. 

```
Event ID: 50 
Event Type: Warning 
Event Source: Ftdisk 
Description: {Lost Delayed-Write Data} The system was attempting to transfer file data from buffers to \Device\HarddiskVolume4. The write operation failed, and only some of the data may have been written to the file.
Data: 
0000: 00 00 04 00 02 00 56 00 
0008: 00 00 00 00 32 00 04 80 
0010: 00 00 00 00 00 00 00 00 
0018: 00 00 00 00 00 00 00 00 
0020: 00 00 00 00 00 00 00 00 
0028: 11 00 00 80 
```

```
Event ID: 26 
Event Type: Information
Event Source: Application Popup
Description: Windows - Delayed Write Failed : Windows was unable to save all the data for the file \Device\HarddiskVolume4\Program Files\Microsoft SQL Server\MSSQL$INSTANCETWO\LOG\ERRORLOG. The data has been lost. This error may be caused by a failure of your computer hardware or network connection.

Please try to save this file elsewhere.
```

이러한 이벤트 ID 메시지는 정확히 동일한 것을 의미 하며 동일한 이유로 생성 됩니다. 이 문서의 목적을 위해 이벤트 ID 50 메시지만 설명 되어 있습니다.

> [!NOTE] 
> 설명의 장치와 경로 및 특정 16 진수 데이터는 다를 수 있습니다. 

##  <a name="more-information"></a>자세한 내용

Windows에서 디스크에 정보를 쓰려고 할 때 일반 오류가 발생 하는 경우 이벤트 ID 50 메시지가 기록 됩니다. 이 오류는 Windows가 파일 시스템 캐시 관리자 (하드웨어 수준 캐시 아님)에서 실제 디스크로 데이터를 커밋하려고 할 때 발생 합니다. 이 동작은 Windows의 메모리 관리에 포함 됩니다. 예를 들어 프로그램에서 쓰기 요청을 보내는 경우 쓰기 요청이 캐시 관리자에 의해 캐시 되 고 프로그램에 쓰기가 성공적으로 완료 되었음을 지시 하는 것입니다. 나중에 캐시 관리자는 실제 디스크에 데이터를 지연 쓰려고 시도 합니다. Cache Manager에서 데이터를 디스크에 커밋하 려는 경우 데이터를 쓰는 동안 오류가 발생 하 고 데이터가 캐시에서 플러시되고 삭제 됩니다. 쓰기 후 캐싱은 시스템 성능을 향상 시키지만, 데이터 손실 및 볼륨 무결성 손실은 지연 된 쓰기 실패의 결과로 발생할 수 있습니다.

모든 i/o가 Cache Manager에 의해 버퍼링 되는 것은 아닙니다. 프로그램은 Cache Manager를 우회 하는 FILE_FLAG_NO_BUFFERING 플래그를 설정할 수 있습니다. SQL에서 데이터베이스에 대 한 중요 한 쓰기를 수행 하는 경우이 플래그는 트랜잭션이 디스크에 직접 완료 되도록 설정 됩니다. 예를 들어 로그 파일에 대 한 중요 하지 않은 쓰기는 버퍼링 된 i/o를 수행 하 여 전반적인 성능을 향상 시킵니다. 이벤트 ID 50 메시지는 버퍼링 되지 않은 i/o의 결과로 반환 되지 않습니다.

이벤트 ID 50 메시지에는 여러 가지 원본이 있습니다. 예를 들어 MRxSmb 원본에서 기록 된 이벤트 ID 50 메시지는 리디렉터에서 네트워크 연결에 문제가 있는 경우에 발생 합니다. 잘못 된 문제 해결 단계를 방지 하려면 이벤트 ID 50 메시지를 검토 하 여 디스크 i/o 문제를 참조 하 고이 문서를 적용 하는지 확인 합니다.

이벤트 ID 50 메시지는 이벤트 ID 9 및 이벤트 ID 11 메시지와 비슷합니다. 오류가 이벤트 ID 9 및 이벤트 id 11 메시지에 표시 된 오류 만큼 심각 하지는 않지만 이벤트 id 9 및 이벤트 ID 11 메시지에 대해 수행 하는 것과 동일한 문제 해결 기술을 이벤트 id 50 메시지에 사용할 수 있습니다. 그러나 스택의 모든 항목은 필터 드라이버 및 미니 포트 드라이버와 같은 손실 지연 쓰기를 유발할 수 있습니다. 

관련 된 "디스크" 오류 (이벤트 ID 9, 11, 51 오류 메시지 또는 기타 메시지로 표시 됨)와 연결 된 이진 데이터를 사용 하 여 문제를 쉽게 파악할 수 있습니다.

###  <a name="how-to-decode-the-data-section-of-an-event-id-50-event-message"></a>이벤트 ID 50 이벤트 메시지의 데이터 섹션을 디코딩하는 방법 

"요약" 섹션에 포함 된 이벤트 ID 50 메시지의 예제에서 데이터 섹션을 디코딩하는 경우 장치가 사용 중이 고 데이터가 손실 되었기 때문에 쓰기 작업을 수행 하지 못했음을 알 수 있습니다. 이 섹션에서는이 이벤트 ID 50 메시지를 디코딩하는 방법을 설명 합니다. 

다음 표에서는이 메시지의 각 오프셋이 나타내는 내용에 대해 설명 합니다. 

|OffsetLengthValues|길이|값|
|-----------|------------|---------|
|0x00|2|사용되지 않음|
|0x02|2|덤프 데이터 크기 = 0x0004|
|0x04|2|문자열 수 = 0x0002|
|0x06|2|문자열에 대 한 오프셋|
|0x08|2|이벤트 범주|
|0x0c|4|NTSTATUS 오류 코드 = 0x80040032 = IO_LOST_DELAYED_WRITE|
|0x10|8|사용되지 않음|
|0x18|8|사용되지 않음|
|0x20|8|사용되지 않음|
|0x28|4|NT 상태 오류 코드|

#### <a name="key-sections-to-decode"></a>디코딩할 키 섹션

**오류 코드**

"요약" 섹션의 예제에서 오류 코드는 두 번째 줄에 나열 됩니다. 이 줄은 "0008:"로 시작 하 고 마지막 4 바이트 (이 경우 0008:00 00 00 00 32 00 04 80)를 포함 합니다 .이 경우 오류 코드는 0x80040032입니다. 다음 코드는 오류 50에 대 한 코드 이며 모든 이벤트 ID 50 메시지에 대해 동일 합니다. IO_LOST_DELAYED_WRITEWARNINGNote 이벤트 ID 메시지의 16 진수 데이터를 상태 코드로 변환 하는 경우 값은 작은 endian 형식으로 표현 됩니다.

**대상 디스크**

이벤트 ID 메시지의 "설명" 섹션에서 드라이브에 나열 된 기호화 된 링크를 사용 하 여 쓰기를 시도 하는 디스크를 식별할 수 있습니다. 예: \Device\HarddiskVolume4. 드라이브를 식별 하는 방법에 대 한 자세한 내용은 다음 문서 번호를 클릭 하 여 Microsoft 기술 자료의 문서를 참조 하십시오. [159865](/EN-US/help/159865) 물리적 디스크 장치를 이벤트 메시지와 구분 하는 방법

**최종 상태 코드**

최종 상태 코드는 이벤트 ID 50 메시지의 가장 중요 한 정보입니다. I/o 요청이 발생 했을 때 반환 되는 오류 코드 이며 정보의 핵심 원본입니다. "요약" 섹션의 예제에서 최종 상태 코드는 "0028:"으로 시작 하 고이 줄에 4 개의 8 진수만 포함 하는 여섯 번째 줄 0x28에 나열 되어 있습니다. 

```
0028: 11 00 00 80 
```

이 경우 최종 상태는 0x80000011과 같습니다. 이 상태 코드는 STATUS_DEVICE_BUSY에 매핑되고 장치가 현재 사용 중임을 의미 합니다.

>[!NOTE] 
> 이벤트 ID 50 메시지의 16 진수 데이터를 상태 코드로 변환 하는 경우 값은 작은 endian 형식으로 표현 됩니다. 상태 코드는 관심이 있는 유일한 정보 이므로 바이트 대신 단어 형식으로 데이터를 보는 것이 더 쉬울 수 있습니다. 이렇게 하면 바이트가 올바른 형식이 되며 데이터를 신속 하 게 해석 하는 것이 더 쉬울 수 있습니다.

이렇게 하려면 **이벤트 속성** 창에서 **단어** 를 클릭 합니다. 데이터 단어 보기에서 "증상" 섹션의 예제는 다음과 같이 읽혀집니다. 

```
() Bytes (.) 
Words 0000: 00040000 00560002 00000000 80040032 0010: 00000000 00000000 00000000 00000000 0020: 00000000 00000000 80000011
```

Windows NT 상태 코드 목록을 가져오려면 NTSTATUS를 참조 하세요. Windows SDK (소프트웨어 개발자 키트)의 H.