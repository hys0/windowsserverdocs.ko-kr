---
title: nlbmgr
description: 네트워크 부하 분산 관리자를 사용 하 여 단일 컴퓨터에서 네트워크 부하 분산 클러스터 및 모든 클러스터 호스트를 구성 하 고 관리 하는 데 도움이 되는 nlbmgr 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 89cb8590-b7cf-4a27-89fa-0fa62ea1a1ca
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 882d3540897214db2f3fa9d04a6f11fc76a76502
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85935531"
---
# <a name="nlbmgr"></a>nlbmgr

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

네트워크 부하 분산 관리자를 사용 하 여 단일 컴퓨터에서 네트워크 부하 분산 클러스터 및 모든 클러스터 호스트를 구성 하 고 관리 합니다. 또한이 명령을 사용 하 여 클러스터 구성을 다른 호스트로 복제할 수 있습니다.

**Systemroot\System32** 폴더에 설치 된 명령 **nlbmgr.exe**를 사용 하 여 명령줄에서 네트워크 부하 분산 관리자를 시작할 수 있습니다.

## <a name="syntax"></a>구문

```
nlbmgr [/noping][/hostlist <filename>][/autorefresh <interval>][/help | /?]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| /noping | WMI(Windows Management Instrumentation) (WMI)를 통해 연결을 시도 하기 전에 네트워크 부하 분산 관리자가 호스트를 ping 하지 못하도록 합니다. 모든 사용 가능한 네트워크 어댑터에서 제어 메시지 ICMP (Internet Protocol)를 사용 하지 않도록 설정한 경우이 옵션을 사용 합니다. 네트워크 부하 분산 관리자가 사용할 수 없는 호스트에 연결 하려고 시도 하는 경우이 옵션을 사용 하면 지연이 발생 합니다. |
| /hostlist`<filename>` | 파일 이름에 지정 된 호스트를 네트워크 부하 분산 관리자에 로드 합니다. |
| /autorefresh`<interval>` | 네트워크 부하 분산 관리자가 초당 호스트 및 클러스터 정보를 새로 고치도록 `<interval>` 합니다. 없는 간격을 지정 하는 경우 정보 60 초 마다 새로 고쳐집니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |
| /help | 명령 프롬프트에 도움말을 표시합니다. |

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [NetworkLoadBalancingClusters cmdlet 참조](https://docs.microsoft.com/powershell/module/networkloadbalancingclusters)
