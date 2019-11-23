---
title: pnpunattend
description: 컴퓨터에서 장치 드라이버를 감사 하는 방법 및 자동 드라이버 설치를 수행 하는 방법을 알아봅니다.
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 77a6ab1ea45322e3c53e8b095c412cf8838be60d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71372274"
---
# <a name="pnpunattend"></a>pnpunattend

컴퓨터에서 장치 드라이버를 감사 하 고 무인 드라이버 설치를 수행 하거나, 설치 하지 않고 드라이버를 검색 하 고, 필요에 따라 명령줄에 결과를 보고 합니다. 특정 하드웨어 장치에 대 한 특정 드라이버의 설치를 지정 하려면이 명령을 사용 합니다. 설명 부분을 참조하세요.

## <a name="syntax"></a>구문

```
PnPUnattend.exe auditSystem [/help] [/?] [/h] [/s] [/L]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|auditSystem|온라인 드라이버 설치를 지정 합니다.</br>**Pnpunattend** 가 **/help** 또는 **/?** 를 사용 하 여 실행 되는 경우를 제외 하 고는 필수 항목입니다. 필요합니다.|
|/s|선택 사항. 를 설치 하지 않고 드라이버를 검색 하도록 지정 합니다.|
|/L|선택 사항. 명령 프롬프트에서이 명령에 대 한 로그 정보를 표시 하도록 지정 합니다.|
|/?|선택 사항. 명령 프롬프트에서이 명령에 대 한 도움말을 표시 합니다.|

## <a name="remarks"></a>설명

예비 준비가 필요 합니다. 이 명령을 사용 하기 전에 다음 작업을 완료 해야 합니다.

1. 설치 하려는 드라이버에 대 한 디렉터리를 만듭니다. 예를 들어 비디오 어댑터 드라이버용 **C:\vom\video** 에서 폴더를 만듭니다.
2. 장치에 대 한 드라이버 패키지를 다운로드 하 고 압축을 풉니다. 운영 체제 버전의 INF 파일을 포함 하는 하위 폴더의 내용 및 만든 비디오 폴더의 하위 폴더를 복사 합니다. 예를 들어 비디오 드라이버 파일을 C:\vom\videos에 복사 합니다.
3. 1 단계에서 만든 폴더에 시스템 환경 경로 변수를 추가 합니다 (예: **C:\vom\video**).
4. 다음 레지스트리 키를 만든 다음 만든 **Driverpaths** 키에 대해 **값 데이터** 를 **1**로 설정 합니다.
5. Windows® 7 **HKEY_LOCAL_Machine \Software\microsoft\windows NT\CurrentVersion\\** 레지스트리 경로를 탐색 한 다음 키를 만듭니다. **UnattendSettings\PnPUnattend\DriverPaths\\**
6. Windows Vista의 경우 레지스트리 경로 **HK_LM \Software\microsoft\windows NT\CurrentVersion\\** 으로 이동한 다음 keys = **\UnattendSettings\PnPUnattend\DriverPaths**를 만듭니다.

## <a name="examples"></a>예

다음 예제 명령은 **PNPUnattend** 을 사용 하 여 컴퓨터에서 가능한 드라이버 업데이트를 감사 한 다음 결과를 명령 프롬프트에 보고 하는 방법을 보여 줍니다.

```
pnpunattend auditsystem /s /l 
```

## <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)