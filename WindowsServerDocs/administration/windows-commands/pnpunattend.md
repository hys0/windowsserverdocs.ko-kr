---
title: pnpunattend
description: Pnpunattend 명령에 대 한 참조 항목으로, 컴퓨터의 장치 드라이버를 감사 하 고 자동 드라이버 설치를 수행 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4fa88932-cff0-4dfc-936c-98c0e3dfbeb8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 23456ec8f8fda5f84819a7105ee1f46814d2f806
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85472408"
---
# <a name="pnpunattend"></a>pnpunattend

컴퓨터에서 장치 드라이버를 감사 하 고 무인 드라이버 설치를 수행 하거나, 설치 하지 않고 드라이버를 검색 하 고, 필요에 따라 명령줄에 결과를 보고 합니다. 특정 하드웨어 장치에 대 한 특정 드라이버의 설치를 지정 하려면이 명령을 사용 합니다.

## <a name="prerequisites"></a>전제 조건

이전 버전의 Windows 운영 체제에서는 예비 준비가 필요 합니다. 이 명령을 사용 하기 전에 다음 작업을 완료 해야 합니다.

1. 설치 하려는 드라이버에 대 한 디렉터리를 만듭니다. 예를 들어 비디오 어댑터 드라이버용 **C:\vom\video** 에서 폴더를 만듭니다.

2. 장치에 대 한 드라이버 패키지를 다운로드 하 고 압축을 풉니다. 운영 체제 버전의 INF 파일을 포함 하는 하위 폴더의 내용 및 만든 비디오 폴더의 하위 폴더를 복사 합니다. 예를 들어 비디오 드라이버 파일을 **C:\vom\video**에 복사 합니다.

3. 1 단계에서 만든 폴더에 시스템 환경 경로 변수를 추가 합니다 (예: **C:\vom\video**).

4. 다음 레지스트리 키를 만든 다음 만든 **Driverpaths** 키에 대해 **값 데이터** 를 **1**로 설정 합니다.

5. Windows® 7 **HKEY_LOCAL_Machine \Software\microsoft\windows NT\CurrentVersion \\ **레지스트리 경로를 탐색 한 다음 키를 **만듭니다 \\ .**

## <a name="syntax"></a>구문

```
PnPUnattend.exe auditsystem [/help] [/?] [/h] [/s] [/l]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
|--|--|
| auditsystem | 온라인 드라이버 설치를 지정 합니다.<p>이 명령이 **/help** 또는 **/?** 를 사용 하 여 실행 되는 경우를 제외 하 고는 필수 항목입니다. 필요합니다. |
| /s | (선택 사항) 를 설치 하지 않고 드라이버를 검색 하도록 지정 합니다. |
| /l | (선택 사항) 명령 프롬프트에서이 명령에 대 한 로그 정보를 표시 하도록 지정 합니다. |
| `/? | /help` | (선택 사항) 명령 프롬프트에서이 명령에 대 한 도움말을 표시 합니다. |

### <a name="examples"></a>예제

**PNPUnattend.exe** 를 사용 하 여 컴퓨터에서 가능한 드라이버 업데이트를 감사 한 다음 결과를 명령 프롬프트에 보고 하는 방법을 보여 줍니다.

```
pnpunattend auditsystem /s /l
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
