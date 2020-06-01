---
title: Windows Server, 버전 2004의 새로운 기능
description: Windows Server, 버전 2004의 새로운 기능
ms.prod: windows-server
ms.technology: server-general
ms.topic: article
author: Heidilohr
ms.author: helohr
ms.date: 05/27/2020
ms.localizationpriority: high
ms.openlocfilehash: e0136dad7180e41f15ae6226008aa7580ec53283
ms.sourcegitcommit: c63672805c93d5bf2a9eb71b3e2de2df00194529
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/28/2020
ms.locfileid: "84124901"
---
# <a name="whats-new-in-windows-server-version-2004"></a>Windows Server, 버전 2004의 새로운 기능

>적용 대상: Windows Server(반기 채널)

Windows의 최신 기능을 알아보려면 [Windows Server의 새로운 기능](whats-new-in-windows-server.md)을 참조하세요. 이 항목에서는 Windows Server, 버전 2004의 새로운 기능 중 일부를 설명합니다.

## <a name="server-core-container-improvements"></a>Server Core 컨테이너 개선 사항

다운로드 속도와 성능을 향상시키기 위해 Server Core 컨테이너 이미지의 전체 크기를 줄였습니다. 다음과 같은 개선 사항이 포함되었습니다.

- Server Core 컨테이너 이미지에서 대부분의 NGEN 이미지를 제거하여 이미지 크기를 작게 만듭니다.
- Server Core 컨테이너 이미지를 기반으로 구축된 .NET Framework 런타임 이미지는 이제 ASP.NET 앱 및 Windows PowerShell 스크립트 성능에 맞게 최적화되었습니다.
- .NET 팀은 또한 각 NGEN 이미지의 사본이 하나만 있는지 확인하여 .NET Framework 이미지의 크기를 줄였습니다.

이러한 컨테이너의 크기를 보다 잘 이해하기 위해 다음 표에서는 [2020년 5월 월간 보안 업데이트](https://support.microsoft.com/help/4561769/windows-server-containers-for-may-2020)("5B" 업데이트라고 함)의 현재 컨테이너 버전을 이전 버전과 비교합니다.

| 컨테이너 버전 | 다운로드 크기 | 디스크의 크기 |
|---|---|---|
| Windows Server, 버전 1903 | 2.311GB | 5.1GB |
| Windows Server, 버전 1909 | 2.257GB | 4.97GB |
| Windows Server, 버전 2004 | 1.830GB | 3.98GB |

Windows Server 버전, 2004 업데이트에 대한 자세한 내용은 [블로그 게시물](https://techcommunity.microsoft.com/t5/containers/windows-server-version-2004-now-available/ba-p/1419194)을 참조하세요. 일반적으로 Windows 컨테이너 업데이트에 대한 자세한 내용은 [Windows Server 컨테이너 업데이트](/virtualization/windowscontainers/deploy-containers/update-containers/)를 참조하세요.
