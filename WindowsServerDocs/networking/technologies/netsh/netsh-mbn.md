---
title: MBN(모바일 광대역 네트워크)용 Netsh 명령
description: netsh mbn을 사용하여 모바일 광대역 설정 및 매개 변수를 쿼리하고 구성합니다.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
author: apdutta
ms.date: 02/20/2020
ms.openlocfilehash: 478f87db4d520a133b3d70c0ed2dbb4e91db60d9
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80853736"
---
# <a name="netsh-mbn-commands"></a>netsh mbn 명령


**netsh mbn**을 사용하여 모바일 광대역 설정 및 매개 변수를 쿼리하고 구성합니다.

> [!TIP]
> 다음을 사용하여 netsh mbn 명령에 대한 도움말을 볼 수 있습니다. 
>
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;netsh mbn /?

사용 가능한 netsh mbn 명령은 다음과 같습니다.

- [add](#add)
- [connect](#connect)
- [delete](#delete)
- [disconnect](#disconnect)
- [diagnose](#diagnose)
- [dump](#dump)
- [help](#help)
- [set](#set)
- [show](#show)

## <a name="add"></a>추가

구성 항목을 테이블에 추가합니다.

사용 가능한 netsh mbn add 명령은 다음과 같습니다.

- [dmprofile](#dmprofile)
- [profile](#profile)

### <a name="dmprofile"></a>dmprofile

DM 구성 프로필을 프로필 데이터 저장소에 추가합니다.

**구문**

```powershell
add dmprofile [interface=]<string> [name=]<string>
```

**매개 변수**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | 인터페이스 이름입니다. "netsh mbn show interface" 명령으로 표시되는 인터페이스 이름 중 하나입니다. | 필수 |
| **name**      | 프로필 XML 파일의 이름입니다. 프로필 데이터가 포함된 XML 파일의 이름입니다.     | 필수 |


**예제**

```powershell
add dmprofile interface="Cellular" name="Profile1.xml"
```


### <a name="profile"></a>profile

네트워크 프로필을 프로필 데이터 저장소에 추가합니다.

**구문**

```powershell
add profile [interface=]<string> [name=]<string>
```

**매개 변수**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | 인터페이스 이름입니다. "netsh mbn show interface" 명령으로 표시되는 인터페이스 이름 중 하나입니다. | 필수 |
| **name**      | 프로필 XML 파일의 이름입니다. 프로필 데이터가 포함된 XML 파일의 이름입니다.     | 필수 |


**예제**

```powershell
add profile interface="Cellular" name="Profile1.xml"
```


## <a name="connect"></a>connect

모바일 광대역 네트워크에 연결합니다.

**구문**

```powershell
connect [interface=]<string> [connmode=]tmp|name [name=]<string>
```

**매개 변수**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | 인터페이스 이름입니다. "netsh mbn show interface" 명령으로 표시되는 인터페이스 이름 중 하나입니다. | 필수 |
| **connmode**  | 연결 매개 변수를 제공하는 방법을 지정합니다. 프로필 XML을 사용하거나, 이전에 "netsh mbn add profile" 명령을 통해 이전에 모바일 광대역 프로필 데이터 저장소에 저장한 프로필 XML의 프로필 이름을 사용하여 연결을 요청할 수 있습니다. 전자의 경우 connmode 매개 변수는 값으로 "tmp"를 포함해야 합니다. 반면, 후자의 경우 "name"이어야 합니다.                                       | 필수 |
| **name**      | 프로필 XML 파일의 이름입니다. 프로필 데이터가 포함된 XML 파일의 이름입니다.     | 필수 |


**예제**

```powershell
connect interface="Cellular" connmode=tmp name=d:\profile.xml
connect interface="Cellular" connmode=name name=MyProfileName
```


## <a name="delete"></a>삭제

테이블에서 구성 항목을 추가합니다.

사용 가능한 netsh mbn delete 명령은 다음과 같습니다.

- [dmprofile](#dmprofile)
- [profile](#profile)

### <a name="dmprofile"></a>dmprofile

프로필 데이터 저장소에서 DM 구성 프로필을 삭제합니다.

**구문**

```powershell
delete dmprofile [interface=]<string> [name=]<string>
```

**매개 변수**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | 인터페이스 이름입니다. "netsh mbn show interface" 명령으로 표시되는 인터페이스 이름 중 하나입니다. | 필수 |
| **name**      | 프로필 XML 파일의 이름입니다. 프로필 데이터가 포함된 XML 파일의 이름입니다.     | 필수 |

**예제**

```powershell
delete dmprofile interface="Cellular" name="myProfileName"
```

### <a name="profile"></a>profile

프로필 데이터 저장소에서 네트워크 프로필을 삭제합니다.

**구문**

```powershell
delete profile [interface=]<string> [name=]<string>
```

**매개 변수**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | 인터페이스 이름입니다. "netsh mbn show interface" 명령으로 표시되는 인터페이스 이름 중 하나입니다. | 필수 |
| **name**      | 프로필 XML 파일의 이름입니다. 프로필 데이터가 포함된 XML 파일의 이름입니다.     | 필수 |


**예제**

```powershell
delete profile interface="Cellular" name="myProfileName"
```

## <a name="diagnose"></a>diagnose

기본 셀룰러 문제에 대한 진단을 실행합니다.

**구문**

```powershell
diagnose [interface=]<string>
```

**매개 변수**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | 인터페이스 이름입니다. "netsh mbn show interface" 명령으로 표시되는 인터페이스 이름 중 하나입니다. | 필수 |


**예제**

```powershell
diagnose interface="Cellular"
```


## <a name="disconnect"></a>연결 끊기

모바일 광대역 네트워크에서 연결을 끊습니다.

**구문**

```powershell
disconnect [interface=]<string>
```

**매개 변수**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | 인터페이스 이름입니다. "netsh mbn show interface" 명령으로 표시되는 인터페이스 이름 중 하나입니다. | 필수 |


**예제**

```powershell
disconnect interface="Cellular"
```


## <a name="dump"></a>dump

구성 스크립트를 표시합니다. 

현재 구성이 포함된 스크립트를 만듭니다.  파일에 저장되면 이 스크립트를 사용하여 변경된 구성 설정을 복원할 수 있습니다.

**구문**

```powershell
dump
```

## <a name="help"></a>도움말

명령 목록을 표시합니다.

**구문**

```powershell
help
```

## <a name="set"></a>설정

구성 정보를 설정합니다.

사용 가능한 netsh mbn set 명령은 다음과 같습니다.

- [acstate](#acstate)
- [dataenablement](#dataenablement)
- [dataroamcontrol](#dataroamcontrol)
- [enterpriseapnparams](#enterpriseapnparams)
- [highestconncategory](#highestconncategory)
- [powerstate](#powerstate)
- [profileparameter](#profileparameter)
- [slotmapping](#slotmapping)
- [tracing](#tracing)

### <a name="acstate"></a>acstate

지정한 인터페이스의 모바일 광대역 데이터 자동 연결 상태를 설정합니다.

**구문**

```powershell
set acstate [interface=]<string> [state=]autooff|autoon|manualoff|manualon
```

**매개 변수**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | 인터페이스 이름입니다. "netsh mbn show interface" 명령으로 표시되는 인터페이스 이름 중 하나입니다. | 필수 |
| **name**      | 설정할 자동 연결 상태입니다. 다음 값 중 하나입니다.<br>autooff: 자동 연결 토큰 끄기입니다.<br>autoon: 자동 연결 토큰 켜기입니다.<br>manualoff: 수동 연결 토큰 끄기입니다.<br>manualon: 수동 연결 토큰 켜기입니다. | 필수 |


**예제**

```powershell
set acstate interface="Cellular" state=autoon
```


### <a name="dataenablement"></a>dataenablement

지정한 프로필 세트 및 인터페이스의 모바일 광대역 데이터를 설정하거나 해제합니다.

**구문**

```powershell
set dataenablement [interface=]<string> [profileset=]internet|mms|all [mode=]yes|no
```

**매개 변수**

|                |                                                                                               |          |
|----------------|-----------------------------------------------------------------------------------------------|----------|
| **interface**  | 인터페이스 이름입니다. "netsh mbn show interface" 명령으로 표시되는 인터페이스 이름 중 하나입니다. | 필수 |
| **profileset** | 프로필 세트의 이름입니다.                                                                      | 필수 |
| **mode**       | 다음 값 중 하나입니다.<br>yes: 대상 프로필 세트를 사용하도록 설정합니다.<br>아니요: 대상 프로필 세트를 사용하지 않도록 설정합니다.| 필수 |


**예제**

```powershell
set dataenablement interface="Cellular" profileset=mms mode=yes
```


### <a name="dataroamcontrol"></a>dataroamcontrol

지정한 프로필 세트 및 인터페이스의 모바일 광대역 데이터 로밍 제어 상태를 설정합니다.

**구문**

```powershell
set dataroamcontrol [interface=]<string> [profileset=]internet|mms|all [state=]none|partner|all
```

**매개 변수**

|                |                                                                                               |          |
|----------------|-----------------------------------------------------------------------------------------------|----------|
| **interface**  | 인터페이스 이름입니다. "netsh mbn show interface" 명령으로 표시되는 인터페이스 이름 중 하나입니다. | 필수 |
| **profileset** | 프로필 세트의 이름입니다.                                                                      | 필수 |
| **mode**       | 다음 값 중 하나입니다.<br>none: 홈 통신 회사만<br>partner: 홈 및 파트너 통신 회사만<br>all: 홈, 파트너 및 로밍 통신 회사| 필수 |


**예제**

```powershell
set dataroamcontrol interface="Cellular" profileset=mms mode=partner
```


### <a name="enterpriseapnparams"></a>enterpriseapnparams

지정한 인터페이스의 모바일 광대역 데이터 enterpriseAPN 매개 변수를 설정합니다.

**구문**

```powershell
set enterpriseapnparams [interface=]<string> [allowusercontrol=]yes|no|nc [allowuserview=]yes|no|nc [profileaction=]add|delete|modify|nc
```

**매개 변수**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | 인터페이스 이름입니다. "netsh mbn show interface" 명령으로 표시되는 인터페이스 이름 중 하나입니다. | 필수 |
| **allowusercontrol** | 다음 값 중 하나입니다.<br>yes: 최종 사용자가 enterpriseAPN을 제어하도록 허용합니다.<br>no: 최종 사용자가 enterpriseAPN을 제어하도록 허용하지 않습니다.<br>nc: 변경되지 않습니다. | 필수 |
| **allowuserview** |다음 값 중 하나입니다.<br>yes: 최종 사용자가 enterpriseAPN을 보도록 허용합니다.<br>no: 최종 사용자가 enterpriseAPN을 보도록 허용하지 않습니다.<br>nc: 변경되지 않습니다. | 필수 |
| **profileaction** | 다음 값 중 하나입니다.<br>add: enterpriseAPN 프로필이 추가되었습니다.<br>delete: enterpriseAPN 프로필이 삭제되었습니다.<br>modify: enterpriseAPN 프로필이 수정되었습니다.<br>nc: 변경되지 않습니다. | 필수 |


**예제**

```powershell
set enterpriseapnparams interface="Cellular" profileset=mms mode=yes
```


### <a name="highestconncategory"></a>highestconncategory

지정한 인터페이스의 모바일 광대역 데이터 최고 연결 범주를 설정합니다.

**구문**

```powershell
set highestconncategory [interface=]<string> [highestcc=]admim|user|operator|device
```

**매개 변수**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | 인터페이스 이름입니다. "netsh mbn show interface" 명령으로 표시되는 인터페이스 이름 중 하나입니다. | 필수 |
| **highestcc** | 다음 값 중 하나입니다.<br>admin: 관리자가 프로비저닝한 프로필입니다.<br>user: 사용자가 프로비저닝한 프로필입니다.<br>operator: 운영자가 프로비저닝한 프로필입니다.<br>device: 디바이스에서 프로비저닝한 프로필입니다 | 필수 |


**예제**

```powershell
set highestconncategory interface="Cellular" highestcc=operator
```


### <a name="powerstate"></a>powerstate

지정된 인터페이스의 모바일 광대역 송수신 장치를 켜거나 끕니다.

**구문**

```powershell
set powerstate [interface=]<string> [state=]on|off
```

**매개 변수**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | 인터페이스 이름입니다. "netsh mbn show interface" 명령으로 표시되는 인터페이스 이름 중 하나입니다. | 필수 |
| **state**      | 다음 값 중 하나입니다.<br>on: 송수신 장치의 전원을 켭니다.<br>off: 송수신 장치의 전원을 끕니다. | 필수 |


**예제**

```powershell
set powerstate interface="Cellular" state=on
```


### <a name="profileparameter"></a>profileparameter

모바일 광대역 네트워크 프로필의 매개 변수를 설정합니다.

**구문**

```powershell
set profileparameter [name=]<string> [[interface=]<string>] [[cost]=default|unrestricted|fixed|variable]
```

**매개 변수**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **name**      | 수정할 프로필의 이름입니다. 인터페이스를 지정하면 해당 인터페이스의 프로필만 수정됩니다. | 필수 |
| **interface** | 인터페이스 이름입니다. "netsh mbn show interface" 명령으로 표시되는 인터페이스 이름 중 하나입니다. | 선택 |
| **cost**      | 프로필과 관련된 비용입니다.                                                             | 선택 |


**설명**

인터페이스 이름과 비용 사이에 하나 이상의 매개 변수를 지정해야 합니다.


**예제**

```powershell
set profileparameter name="profile 1" cost=default
```


### <a name="slotmapping"></a>slotmapping

지정한 인터페이스의 모바일 광대역 모뎀 슬롯 매핑을 설정합니다.

**구문**

```powershell
set slotmapping [interface=]<string> [slotindex=]<integer>
```

**매개 변수**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | 인터페이스 이름입니다. "netsh mbn show interface" 명령으로 표시되는 인터페이스 이름 중 하나입니다. | 필수 |
| **slotindex** | 설정할 슬롯 인덱스입니다.                                                                         | 필수 |


**예제**

```powershell
set slotmapping interface="Cellular" slotindex=1
```


### <a name="tracing"></a>tracing

추적을 사용하거나 사용하지 않도록 설정합니다.

**구문**

```powershell
set tracing [mode=]yes|no
```

**매개 변수**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **mode**      | 다음 값 중 하나입니다.<br>yes: 모바일 광대역 추적을 사용하도록 설정합니다.<br>아니요: 모바일 광대역 추적을 사용하지 않도록 설정합니다.     | 필수 |


**예제**

```powershell
set tracing mode=yes
```

## <a name="show"></a>show

모바일 광대역 네트워크 정보를 표시합니다.

사용 가능한 netsh mbn set 명령은 다음과 같습니다.

- [acstate](#acstate)
- [capability](#capability)
- [connection](#connection)
- [dataenablement](#dataenablement)
- [dataroamcontrol](#dataroamcontrol)
- [dmprofiles](#dmprofiles)
- [enterpriseapnparams](#enterpriseapnparams)
- [highestconncategory](#highestconncategory)
- [homeprovider](#homeprovider)
- [interfaces](#interfaces)
- [netlteattachinfo](#netlteattachinfo)
- [pin](#pin)
- [pinlist](#pinlist)
- [preferredproviders](#preferredproviders)
- [profiles](#profiles)
- [profilestate](#profilestate)
- [provisionedcontexts](#provisionedcontexts)
- [purpose](#purpose)
- [radio](#radio)
- [readyinfo](#readyinfo)
- [signal](#signal)
- [slotmapping](#slotmapping)
- [slotstatus](#slotstatus)
- [smsconfig](#smsconfig)
- [tracing](#tracing)
- [visibleproviders](#visibleproviders)

### <a name="acstate"></a>acstate  

지정한 인터페이스의 모바일 광대역 데이터 자동 연결 상태를 표시합니다.

**구문**

```powershell
show acstate [interface=]<string>
```

**매개 변수**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | 인터페이스 이름입니다. "netsh mbn show interface" 명령으로 표시되는 인터페이스 이름 중 하나입니다. | 필수 |


**예제**

```powershell
show acstate interface="Cellular"
```


### <a name="capability"></a>capability

지정한 인터페이스의 인터페이스 기능 정보를 표시합니다.

**구문**

```powershell
show capability [interface=]<string>
```

**매개 변수**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | 인터페이스 이름입니다. "netsh mbn show interface" 명령으로 표시되는 인터페이스 이름 중 하나입니다. | 필수 |


**예제**

```powershell
show capability interface="Cellular"
```


### <a name="connection"></a>connection

지정한 인터페이스의 현재 연결 정보를 표시합니다.

**구문**

```powershell
show connection [interface=]<string>
```

**매개 변수**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | 인터페이스 이름입니다. "netsh mbn show interface" 명령으로 표시되는 인터페이스 이름 중 하나입니다. | 필수 |


**예제**

```powershell
show connection interface="Cellular"
```


### <a name="dataenablement"></a>dataenablement

지정한 인터페이스의 모바일 광대역 데이터 사용 상태를 표시합니다.

**구문**

```powershell
show dataenablement [interface=]<string>
```

**매개 변수**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | 인터페이스 이름입니다. "netsh mbn show interface" 명령으로 표시되는 인터페이스 이름 중 하나입니다. | 필수 |


**예제**

```powershell
show dataenablement interface="Cellular"
```


### <a name="dataroamcontrol"></a>dataroamcontrol

지정한 인터페이스의 모바일 광대역 데이터 로밍 제어 상태를 표시합니다.

**구문**

```powershell
show dataroamcontrol [interface=]<string>
```

**매개 변수**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | 인터페이스 이름입니다. "netsh mbn show interface" 명령으로 표시되는 인터페이스 이름 중 하나입니다. | 필수 |


**예제**

```powershell
show dataroamcontrol interface="Cellular"
```


### <a name="dmprofiles"></a>dmprofiles

시스템에 구성되어 있는 DM 구성 프로필 목록을 표시합니다.

**구문**

```powershell
show dmprofiles [[name=]<string>] [[interface=]<string>]
```

**매개 변수**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **name**      | 표시할 프로필의 이름입니다.                                                               | 선택 |
| **interface** | 인터페이스 이름입니다. "netsh mbn show interface" 명령으로 표시되는 인터페이스 이름 중 하나입니다. | 선택 |

**설명**
    
프로필 데이터를 표시하거나 시스템의 프로필을 나열합니다.

프로필 이름을 지정하면 해당 프로필의 내용이 표시됩니다. 그렇지 않으면 인터페이스의 프로필이 나열됩니다.

인터페이스 이름을 지정하면 지정한 인터페이스의 해당 프로필만 나열됩니다. 그렇지 않으면 일치하는 첫 번째 프로필이 표시됩니다.

**예제**

```powershell
show dmprofiles name="profile 1" interface="Cellular"
show dmprofiles name="profile 2"
show dmprofiles
```


### <a name="enterpriseapnparams"></a>enterpriseapnparams

지정한 인터페이스의 모바일 광대역 데이터 enterpriseAPN 매개 변수를 표시합니다.

**구문**

```powershell
show enterpriseapnparams [interface=]<string>
```

**매개 변수**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | 인터페이스 이름입니다. "netsh mbn show interface" 명령으로 표시되는 인터페이스 이름 중 하나입니다. | 필수 |


**예제**

```powershell
show enterpriseapnparams interface="Cellular"
```


### <a name="highestconncategory"></a>highestconncategory

지정한 인터페이스의 모바일 광대역 데이터 최고 연결 범주를 표시합니다.

**구문**

```powershell
show highestconncategory [interface=]<string>
```

**매개 변수**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | 인터페이스 이름입니다. "netsh mbn show interface" 명령으로 표시되는 인터페이스 이름 중 하나입니다. | 필수 |


**예제**

```powershell
show highestconncategory interface="Cellular"
```


### <a name="homeprovider"></a>homeprovider

지정한 인터페이스의 홈 공급자 정보를 표시합니다.

**구문**

```powershell
show homeprovider [interface=]<string>
```

**매개 변수**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | 인터페이스 이름입니다. "netsh mbn show interface" 명령으로 표시되는 인터페이스 이름 중 하나입니다. | 필수 |


**예제**

```powershell
show homeprovider interface="Cellular"
```


### <a name="interfaces"></a>interfaces

시스템의 모바일 광대역 인터페이스 목록을 표시합니다. 이 명령에는 매개 변수가 없습니다.

**구문**

```powershell
show interfaces
```


### <a name="netlteattachinfo"></a>netlteattachinfo

지정한 인터페이스의 모바일 광대역 네트워크 LTE 연결 정보를 표시합니다.

**구문**

```powershell
show netlteattachinfo [interface=]<string>
```

**매개 변수**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | 인터페이스 이름입니다. "netsh mbn show interface" 명령으로 표시되는 인터페이스 이름 중 하나입니다. | 필수 |


**예제**

```powershell
show netlteattachinfo interface="Cellular"
```

### <a name="pin"></a>고정      

지정한 인터페이스의 PIN 정보를 표시합니다.

**구문**

```powershell
show pin [interface=]<string>
```

**매개 변수**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | 인터페이스 이름입니다. "netsh mbn show interface" 명령으로 표시되는 인터페이스 이름 중 하나입니다. | 필수 |


**예제**

```powershell
show pin interface="Cellular"
```


### <a name="pinlist"></a>pinlist  

지정한 인터페이스의 PIN 목록 정보를 표시합니다.

**구문**

```powershell
show pinlist [interface=]<string>
```

**매개 변수**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | 인터페이스 이름입니다. "netsh mbn show interface" 명령으로 표시되는 인터페이스 이름 중 하나입니다. | 필수 |


**예제**

```powershell
show pinlist interface="Cellular"
```


### <a name="preferredproviders"></a>preferredproviders

지정한 인터페이스의 기본 공급자 목록을 표시합니다.

**구문**

```powershell
show preferredproviders [interface=]<string>
```

**매개 변수**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | 인터페이스 이름입니다. "netsh mbn show interface" 명령으로 표시되는 인터페이스 이름 중 하나입니다. | 필수 |


**예제**

```powershell
show preferredproviders interface="Cellular"
```


### <a name="profiles"></a>profiles 

시스템에 구성되어 있는 프로필 목록을 표시합니다.

**구문**

```powershell
show profiles [[name=]<string>] [[interface=]<string>] [[purpose=]<string>]
```

**매개 변수**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **name**      | 표시할 프로필의 이름입니다.                                                               | 선택 |
| **interface** | 인터페이스 이름입니다. "netsh mbn show interface" 명령으로 표시되는 인터페이스 이름 중 하나입니다. | 선택 |
| **purpose**   | 용도 | 선택 |

**설명**

프로필 이름을 지정하면 해당 프로필의 내용이 표시됩니다. 그렇지 않으면 인터페이스의 프로필이 나열됩니다.

인터페이스 이름을 지정하면 지정한 인터페이스의 해당 프로필만 나열됩니다. 그렇지 않으면 일치하는 첫 번째 프로필이 표시됩니다.

용도가 제공되면 용도 GUID가 일치하는 프로필만 표시됩니다.  그렇지 않으면 프로필이 용도를 기준으로 필터링되지 않습니다.  문자열은 중괄호로 묶인 GUID이거나 internet, supl, mms, ims 또는 allhost라는 문자열 중 하나일 수 있습니다.
    
**예제**

```powershell
show profiles interface="Cellular" purpose="{00000000-0000-0000-0000-000000000000}"
show profiles name="profile 1" interface="Cellular"
show profiles name="profile 2"
show profiles
```

### <a name="profilestate"></a>profilestate

지정한 인터페이스의 모바일 광대역 프로필 상태를 표시합니다.

**구문**

```powershell
show profilestate [interface=]<string> [name=]<string>
```

**매개 변수**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | 인터페이스 이름입니다. "netsh mbn show interface" 명령으로 표시되는 인터페이스 이름 중 하나입니다. | 필수 |
| **name**      | 프로필 이름입니다. 표시할 상태가 있는 프로필의 이름입니다.            | 필수 |

**예제**

```powershell
show profilestate interface="Cellular" name="myProfileName"
```

### <a name="provisionedcontexts"></a>provisionedcontexts

지정한 인터페이스의 프로비저닝된 컨텍스트 정보를 표시합니다.

**구문**

```powershell
show provisionedcontexts [interface=]<string>
```

**매개 변수**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | 인터페이스 이름입니다. "netsh mbn show interface" 명령으로 표시되는 인터페이스 이름 중 하나입니다. | 필수 |


**예제**

```powershell
show provisionedcontexts interface="Cellular"
```


### <a name="purpose"></a>purpose  

디바이스의 프로필을 필터링하는 데 사용할 수 있는 용도 그룹 GUID를 표시합니다. 이 명령에는 매개 변수가 없습니다.

**구문**

```powershell
show purpose
```


### <a name="radio"></a>radio    

지정한 인터페이스의 송수신 장치 상태 정보를 표시합니다.

**구문**

```powershell
show radio [interface=]<string>
```

**매개 변수**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | 인터페이스 이름입니다. "netsh mbn show interface" 명령으로 표시되는 인터페이스 이름 중 하나입니다. | 필수 |


**예제**

```powershell
show radio interface="Cellular"
```


### <a name="readyinfo"></a>readyinfo

지정한 인터페이스의 준비 상태 정보를 표시합니다.

**구문**

```powershell
show readyinfo [interface=]<string>
```

**매개 변수**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | 인터페이스 이름입니다. "netsh mbn show interface" 명령으로 표시되는 인터페이스 이름 중 하나입니다. | 필수 |


**예제**

```powershell
show readyinfo interface="Cellular"
```


### <a name="signal"></a>signal   

지정한 인터페이스의 신호 정보를 표시합니다.

**구문**

```powershell
show signal [interface=]<string>
```

**매개 변수**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | 인터페이스 이름입니다. "netsh mbn show interface" 명령으로 표시되는 인터페이스 이름 중 하나입니다. | 필수 |


**예제**

```powershell
show signal interface="Cellular"
```


### <a name="slotmapping"></a>slotmapping

지정한 인터페이스의 모바일 광대역 모뎀 슬롯 매핑을 표시합니다.

**구문**

```powershell
show slotmapping [interface=]<string>
```

**매개 변수**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | 인터페이스 이름입니다. "netsh mbn show interface" 명령으로 표시되는 인터페이스 이름 중 하나입니다. | 필수 |


**예제**

```powershell
show slotmapping interface="Cellular"
```


### <a name="slotstatus"></a>slotstatus

지정한 인터페이스의 모바일 광대역 모뎀 슬롯 상태를 표시합니다.

**구문**

```powershell
show slotstatus [interface=]<string>
```

**매개 변수**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | 인터페이스 이름입니다. "netsh mbn show interface" 명령으로 표시되는 인터페이스 이름 중 하나입니다. | 필수 |


**예제**

```powershell
show slotstatus interface="Cellular"
```


### <a name="smsconfig"></a>smsconfig

지정한 인터페이스의 SMS 구성 정보를 표시합니다.

**구문**

```powershell
show smsconfig [interface=]<string>
```

**매개 변수**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | 인터페이스 이름입니다. "netsh mbn show interface" 명령으로 표시되는 인터페이스 이름 중 하나입니다. | 필수 |


**예제**

```powershell
show smsconfig interface="Cellular"
```


### <a name="tracing"></a>tracing  

모바일 광대역 추적 기능의 사용 여부를 표시합니다.

**구문**

```powershell
show tracing 
```


### <a name="visibleproviders"></a>visibleproviders

지정한 인터페이스의 표시 공급자 목록을 표시합니다.

**구문**

```powershell
show visibleproviders [interface=]<string>
```

**매개 변수**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | 인터페이스 이름입니다. "netsh mbn show interface" 명령으로 표시되는 인터페이스 이름 중 하나입니다. | 필수 |


**예제**

```powershell
show visibleproviders interface="Cellular"
```
