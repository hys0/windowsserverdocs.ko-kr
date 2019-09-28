---
title: Sc 만들기
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 59416460-0661-4fef-85cc-73e9d8f4beb4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8ea8f1c33472b7ac95ec0282a50d902a9d7cf84d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71384366"
---
# <a name="sc-create"></a>Sc 만들기



서비스 제어 관리자 데이터베이스 및 레지스트리에서 하위 키와 서비스에 대 한 항목을 만듭니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
sc [<ServerName>] create [<ServiceName>] [type= {own | share | kernel | filesys | rec | interact type= {own | share}}] [start= {boot | system | auto | demand | disabled}] [error= {normal | severe | critical | ignore}] [binpath= <BinaryPathName>] [group= <LoadOrderGroup>] [tag= {yes | no}] [depend= <dependencies>] [obj= {<AccountName> | <ObjectName>}] [displayname= <DisplayName>] [password= <Password>]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<ServerName >|서비스 위치는 원격 서버의 이름을 지정 합니다. 이름에는 UNC (범용 명명 규칙) 형식을 사용 해야 합니다 (예: \\ @ no__t-1myserver). SC.exe를 로컬로 실행 하려면이 매개 변수를 생략 합니다.|
|\<ServiceName >|반환 된 서비스 이름을 지정는 **getkeyname** 작업 합니다.|
|type = {자체 \| 공유 \| 커널 \| filesys \| rec \| 상호 작용 형식 = {자체 \| 공유}}|서비스 유형을 지정합니다. 기본 설정은 **유형 = 직접**합니다.</br>**직접** -서비스가 자체 프로세스에서 실행 되도록 지정 합니다. 다른 서비스와 함께 실행 파일을 공유 하지 않습니다. 이것이 기본 설정입니다.</br>**공유** -서비스를 공유 프로세스로 실행 되도록 지정 합니다. 다른 서비스와 함께 실행 파일을 공유 합니다.</br>**커널** -드라이버를 지정 합니다.</br>**filesys** -파일 시스템 드라이버를 지정 합니다.</br>**rec** -(컴퓨터에 사용 되는 파일 시스템 식별) 하는 파일 시스템 인식 드라이버를 지정 합니다.</br>**상호 작용** -서비스 사용자 로부터 입력을 받고 바탕 화면에서 상호 작용할 수 있음을 지정 합니다. 대화형 서비스는 LocalSystem 계정에서 실행 되어야 합니다. 이 형식은와 함께에서 사용 해야 **유형 = 자체** 또는 **유형 = 공유**합니다. 사용 하 여 **유형 = 상호 작용** 자체적으로 "매개 변수가 잘못 되었습니다" 오류를 생성 합니다.|
|start = {boot \| 시스템 \| 자동 \| 수요 \| 사용 안 함}|서비스 시작 유형을 지정합니다. 기본 설정은 **시작 요청 =** 합니다.</br>**부팅** -부팅 로더에 의해 로드 된 장치 드라이버를 지정 합니다.</br>**시스템** -커널 초기화 중에 시작 되는 장치 드라이버를 지정 합니다.</br>**자동** -컴퓨터를 다시 시작 될 때마다 자동으로 시작 하는 서비스를 지정 합니다. 컴퓨터에 로그온 한 경우에 서비스가 실행 되는 참고 합니다.</br>**필요 시** -수동으로 시작 해야 하는 서비스를 지정 합니다. 이 기본값을 사용 하는 경우 **시작 =** 지정 되지 않았습니다.</br>**사용 하지 않도록 설정** -시작할 수 없는 서비스를 지정 합니다. 사용할 수 없는 서비스를 시작 하려면 시작 유형을 다른 값을 변경 합니다.|
|오류 = {normal \| 심각 \| 중요 \| 무시}|컴퓨터를 시작할 때 서비스가 실패 하는 경우 오류의 심각도 지정 합니다. 기본 설정은 **오류 일반 =** 합니다.</br>**일반** -지정 된 오류가 기록 됩니다. 서비스를 시작 하지 못했음을 알리는 메시지 상자가 표시 됩니다. 시작 프로세스를 계속 합니다. 이것이 기본 설정입니다.</br>**심각한** -오류 (가능한 경우) 기록 되는지 지정 합니다. 컴퓨터가는 마지막으로 성공한 구성으로 다시 시작 하려고 합니다. 이 컴퓨터를 다시 시작할 수 없게 될 수 있습니다 없지만 서비스 수 있습니다 하지 실행할 수 있습니다.</br>**critical** -가능한 경우 오류를 기록 하도록 지정 합니다. 컴퓨터가는 마지막으로 성공한 구성으로 다시 시작 하려고 합니다. 마지막으로 성공한 구성에 실패 하면 시작도 실패 하 고 부팅 프로세스 중지 오류를 중단 합니다.</br>**무시** -지정 하는 오류를 기록 하 고 시작을 계속 합니다. 이벤트 로그에 오류를 기록 하는 것 외에는 사용자에 게 알림이 제공 되지 않습니다.|
|binpath = \<BinaryPathName >|서비스 이진 파일에 대 한 경로 지정합니다. 에 대 한 기본값이 없으면 **binpath =** , 이 문자열을 제공 해야 합니다.|
|group = \<LoadOrderGroup >|이 서비스가 멤버인 그룹의 이름을 지정 합니다. 그룹 목록에서 레지스트리에 저장 된 **HKLM\System\CurrentControlSet\Control\ServiceGroupOrder** 하위 키입니다. 기본값은 null입니다.|
|tag = {yes \| no}|TagID을 여부 지정 CreateService 호출에서 가져옵니다. 태그는 부팅 시작 및 시스템 시작 드라이버에만 사용 됩니다.|
|종속 = \<dependencies >|서비스 또는이 서비스를 시작 하기 전에 시작 해야 하는 그룹의 이름을 지정 합니다. 이름은은 슬래시 (/)로 구분 됩니다.|
|obj = {\<AccountName > \| \<ObjectName >}|서비스를 실행 또는 드라이버를 실행할 Windows 드라이버 개체의 이름을 지정 계정의 이름을 지정 합니다.|
|displayname = \<DisplayName >|서비스를 식별 하 여 사용자 인터페이스 프로그램에서 사용할 수 있는 친숙 한 이름을 지정 합니다.|
|password = \<Password >|암호를 지정합니다. LocalSystem 아닌 다른 계정을 사용 하는 경우 이것이 필요 합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명

-   각 명령줄 옵션에 대 한 등호 일부인 옵션 이름입니다.
-   옵션 및 해당 값 사이 공백을 않습니다 (예를 들어 **유형 = 직접**합니다. 공간을 생략 하면 작업이 실패 합니다.

## <a name="BKMK_examples"></a>예와

다음 예제에서는 사용 하는 방법을 보여는 **sc 만들** 명령:
```
sc \\myserver create NewService binpath= c:\windows\system32\NewServ.exe
sc create NewService binpath= c:\windows\system32\NewServ.exe type= share start= auto depend= "+TDI NetBIOS"
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)
