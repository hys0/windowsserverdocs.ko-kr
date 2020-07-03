---
title: msdt
description: 명령 줄 또는 자동화 된 스크립트의 일부로 문제 해결 팩을 호출 하 고 사용자 입력 없이 추가 옵션을 사용 하도록 설정 하는 msdt 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ead1b672-a120-4e16-94aa-a8e13602c1d0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 99ba1320171e4e305209f06fbee617e54c979d30
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85925026"
---
# <a name="msdt"></a>msdt

명령줄에서 또는 자동화 된 스크립트의 일부로 문제 해결 팩을 호출 하 고 사용자 입력 없이 추가 옵션을 활성화 합니다.

## <a name="syntax"></a>구문

```
msdt </id <name> | /path <name> | /cab < name>> <</parameter> [options] … <parameter> [options]>>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| 더불어`<packagename>` | 실행할 진단 패키지를 지정 합니다. 사용 가능한 패키지 목록은 [사용 가능한 문제 해결 팩](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/ee424379(v=ws.11)#available-troubleshooting-packs)을 참조 하세요. |
| /path`<directory|.diagpkg file|.diagcfg file>` | 진단 패키지의 전체 경로를 지정 합니다. 디렉터리를 지정 하는 경우 디렉터리는 진단 패키지를 포함 해야 합니다. **/Path** 매개 변수는 * */id * *, **/dci**또는 **/cab** 매개 변수와 함께 사용할 수 없습니다. |                                                                                   |
| /dci`<passkey>` | 암호 필드를 인시던트의 합니다. 이 매개 변수는 지원 공급자가 암호를 제공한 경우에만 사용 됩니다. |
| /dt`<directory>` | 지정 된 디렉터리에 문제 해결 기록을 표시 합니다. 진단 결과는 사용자의 **%LOCALAPPDATA%\Diagnostics** 또는 **%LOCALAPPDATA%\ElevatedDiagnostics** 디렉터리에 저장 됩니다. |
| /af`<answerfile>` | 하나 이상의 진단 상호 작용에 대 한 응답을 포함 하는 XML 형식의 응답 파일을 지정 합니다. |
| /su`<ownerHWND>` | 부모 콘솔 창 핸들 (HWND)에서 지정 된 창에 문제 해결 팩 모달을 사용 합니다 (10 진수). 이 매개 변수는 일반적으로 문제 해결 팩을 실행 하는 응용 프로그램에서 사용 됩니다. 콘솔 창 핸들을 가져오는 방법에 대 한 자세한 내용은 [콘솔 창 핸들을 가져오는 방법 (HWND)](https://support.microsoft.com/help/124103/how-to-obtain-a-console-window-handle-hwnd)을 참조 하세요. |
| /moreoptions`<true|false>` | 사용자가 추가 옵션을 탐색 하려고 하는지 여부를 묻는 최종 문제 해결 화면을 사용 하도록 설정 (true) 하거나 표시 하지 않습니다. 이 매개 변수는 일반적으로 운영 체제에 포함 되지 않은 문제 해결사에서 문제 해결 팩을 시작할 때 사용 됩니다. |
| /param returns`<parameters>` | 응답 파일과 비슷하게 명령줄에서 상호 작용 응답의 집합을 지정 합니다. 이 매개 변수는 일반적으로 TSP Designer를 사용 하 여 만든 pack 문제 해결의 컨텍스트 내에서 사용 되지 않습니다. 사용자 지정 매개 변수를 개발 하는 방법에 대 한 자세한 내용은 [Windows 문제 해결 플랫폼](https://docs.microsoft.com/previous-versions/windows/desktop/wintt/windows-troubleshooting-toolkit-portal)을 참조 하세요. |
| /advanced | 문제 해결 팩이 시작 될 때 기본적으로 시작 페이지의 고급 링크를 확장 합니다. |
| / 사용자 지정 | 사용자에 게 적용 하기 전에 가능한 해결 방법을 확인 하는 메시지를 표시 합니다. |

### <a name="return-codes"></a>반환 코드

문제 해결 팩은 각각 특정 기술 문제를 설명 하는 근본 원인 집합을 구성 합니다. 문제 해결 팩 작업을 완료 한 후에는 각 근본 원인을 해결 됨, 수정 되지 않음, 검색 됨 (수정할 수 제외) 또는 찾을 수 없음 상태를 반환 합니다. 문제 해결사 사용자 인터페이스에서 보고 되는 특정 결과 외에도 문제 해결 엔진은 문제 해결사가 원래 문제를 해결 했는지 여부를 설명 하는 결과의 코드를 일반적인 용어로 반환 합니다. 코드는 다음과 같습니다.

| 코드 | 설명 |
| ---- | ----------- |
| -1 | **중단:** 문제 해결 작업이 완료 되기 전에 문제 해결사가 닫혔습니다. |
| 0 | **수정 됨:** 문제 해결사는 근본 원인을 하나 이상 파악 하 고 해결 했지만 근본 원인은 고정 되지 않음 상태로 유지 되지 않습니다. |
| 1 | **있지만 수정 되지 않음:** 문제 해결사가 수정 되지 않은 상태로 남아 있는 하나 이상의 근본 원인을 식별 했습니다. 이 코드는 다른 근본 원인이 수정 된 경우에도 반환 됩니다. |
| 2 | **찾을 수 없음:** 문제 해결사에서 근본 원인을 확인 하지 못했습니다. |

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [사용 가능한 문제 해결 팩](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/ee424379(v=ws.11)#available-troubleshooting-packs)

- [TroubleshootingPack Powershell 참조](https://docs.microsoft.com/powershell/module/troubleshootingpack/?view=win10-ps)