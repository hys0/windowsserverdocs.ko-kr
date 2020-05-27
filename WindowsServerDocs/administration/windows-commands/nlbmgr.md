---
title: nlbmgr
description: '* * * *에 대 한 참조 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 89cb8590-b7cf-4a27-89fa-0fa62ea1a1ca
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a055eb30984bd1832d84bce40607eb0722b175b2
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2020
ms.locfileid: "83820853"
---
# <a name="nlbmgr"></a>nlbmgr

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

네트워크 부하 분산 관리자를 사용 하 고 수 있으며 구성 단일 컴퓨터에서 네트워크 로드 균형 조정 클러스터 및 모든 클러스터 호스트를 관리할 다른 호스트에 클러스터 구성을 복제할 수도 있습니다. 명령줄 사용 하는 명령에서 네트워크 부하 분산 관리자를 시작할 수 있습니다 **nlbmgr.exe**, 에 설치 되는 **systemroot\System32** 폴더입니다.
## <a name="syntax"></a>구문
```
nlbmgr [/help] [/noping] [/hostlist <filename>] [/autorefresh <interval>]
```
#### <a name="parameters"></a>매개 변수

|        매개 변수        |                                                                                                                                                                                                설명                                                                                                                                                                                                |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|          /help          |                                                                                                                                                                                   명령 프롬프트에 도움말을 표시합니다.                                                                                                                                                                                    |
|         /noping         | Windows Management Instrumentation (WMI)을 통해 연락할 하려고 하기 전에 호스트를 ping에서 네트워크 부하 분산 관리자를 방지 합니다. 모든 사용 가능한 네트워크 어댑터에서 제어 메시지 ICMP (Internet Protocol)를 사용 하지 않도록 설정한 경우이 옵션을 사용 합니다. 네트워크 부하 분산 관리자를 사용할 수 있는 호스트에 연결 하려고 하는 경우이 옵션을 사용할 때 지연이 발생 합니다. |
|  /hostlist<filename>   |                                                                                                                                                                네트워크 로드 균형 조정 관리자 파일 이름에 지정 된 호스트를 로드 합니다.                                                                                                                                                                 |
| /autorefresh<interval> |                                                                                                          해당 호스트와 클러스터 정보를 새로 고치려면 네트워크 로드 균형 조정을 사용 하면 모든 <interval> 초입니다. 없는 간격을 지정 하는 경우 정보 60 초 마다 새로 고쳐집니다.                                                                                                          |
|           /?            |                                                                                                                                                                                   명령 프롬프트에 도움말을 표시합니다.                                                                                                                                                                                    |

## <a name="additional-references"></a>추가 참조
- [명령줄 구문 키](command-line-syntax-key.md)

