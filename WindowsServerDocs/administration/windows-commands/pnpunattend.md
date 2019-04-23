---
title: pnpunattend
description: 드라이버 자동 설치를 수행할 수 있을 뿐만 아니라 컴퓨터에서 장치 드라이버를 감사 하는 방법에 알아봅니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4fa88932-cff0-4dfc-936c-98c0e3dfbeb8 britw
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 7aa09636f8c23678f003bfa5ebf8be164e7fc683
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59879524"
---
# <a name="pnpunattend"></a>pnpunattend

장치 드라이버에 대 한 컴퓨터 감사 무인된 드라이버 설치를 수행할 또는 검색 드라이버를 설치 하지 않고 하 고, 필요에 따라 명령줄에 결과 보고 합니다. 이 명령을 사용 하 여 특정 하드웨어 장치에 대 한 특정 드라이버의 설치를 지정 합니다. 설명 부분을 참조하세요.

## <a name="syntax"></a>구문

```
PnPUnattend.exe auditSystem [/help] [/?] [/h] [/s] [/L]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|auditSystem|온라인 설치를 지정합니다.</br>필요한 경우 제외 **pnpunattend** 중 하나를 사용 하 여 실행 합니다 **/help** 또는 **/?** 필요합니다.|
|/s|(선택 사항) 드라이버를 설치 하지 않고 검색 하도록 지정 합니다.|
|/L|(선택 사항) 명령 프롬프트에서이 명령에 대 한 로그 정보를 표시 하도록 지정 합니다.|
|/?|(선택 사항) 명령 프롬프트에서이 명령에 대 한 도움말을 표시 합니다.|

## <a name="remarks"></a>설명

사전 준비가 필요 합니다. 이 명령을 사용 하기 전에 다음 작업을 완료 해야 합니다.

1.  설치 하려는 드라이버에 대 한 디렉터리를 만듭니다. 예를 들어 있는 폴더를 만듭니다 **C:\Drivers\Video** 비디오 어댑터 드라이버에 대 한 합니다.
2.  다운로드 하 고 장치에 대 한 드라이버 패키지를 추출 합니다. 운영 체제의 버전에 대 한 INF 파일이 포함 된 하위 폴더 및 하위 폴더의 내용을 사용자가 만든 비디오 폴더로 복사 합니다. 예를 들어 C:\Drivers\Video에 비디오 드라이버 파일을 복사 합니다.
3.  예를 들어, 1 단계에서에서 만든 폴더를 path 시스템 환경 변수를 추가 **C:\Drivers\Video**합니다.
4.  다음 레지스트리 키를 만듭니다 한 후는 **DriverPaths** 키를 만드는 설정 합니다 **값 데이터** 에 **1**.
-   에 대 한 Windows® 7 이동 레지스트리 경로: **하기 위해 HKEY_LOCAL_Machine\Software\Microsoft\Windows NT\CurrentVersion\** 를 만든 다음 키 및: **UnattendSettings\PnPUnattend\DriverPaths\**
-   Windows Vista에 대 한 레지스트리 경로 탐색: **HK_LM\Software\Microsoft\Windows 찾습니다\** 를 만든 다음 키 및 = **\UnattendSettings\PnPUnattend\DriverPaths** .

## <a name="examples"></a>예

다음 예제에서는 명령을 사용 하는 방법을 보여 줍니다 합니다 **PNPUnattend.exe** 가능한 드라이버 업데이트에 대 한 컴퓨터를 감사 하 고 다음 명령 프롬프트에 결과 보고 합니다.

```
pnpunattend auditsystem /s /l 
```

## <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)