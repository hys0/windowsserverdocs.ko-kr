---
title: 저장소 공간 개요
ms.prod: windows-server
ms.author: jgerend
ms.manager: dougkim
ms.technology: storage-file-systems
ms.topic: article
author: jasongerend
ms.date: 05/22/2018
ms.openlocfilehash: cab92de2a96f1d44c8ad6a33e84aba08cad38837
ms.sourcegitcommit: 083ff9bed4867604dfe1cb42914550da05093d25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/14/2020
ms.locfileid: "75950246"
---
# <a name="storage-spaces-overview"></a>저장소 공간 개요

저장소 공간은 데이터를 드라이브 오류 로부터 보호 하는 데 도움이 되는 Windows 및 Windows Server의 기술입니다. 소프트웨어에 구현 된 RAID와 개념적으로 유사 합니다. 저장소 공간을 사용 하 여 3 개 이상의 드라이브를 저장소 풀로 그룹화 한 다음, 해당 풀의 용량을 사용 하 여 저장소 공간을 만들 수 있습니다. 이러한 데이터는 일반적으로 데이터의 추가 복사본을 저장 하므로 드라이브 중 하나에 오류가 발생 하면 데이터의 복사본도 그대로 유지 됩니다. 용량이 부족 한 경우 저장소 풀에 드라이브를 더 추가 하면 됩니다.

저장소 공간을 사용 하는 네 가지 주요 방법은 다음과 같습니다.

- **WINDOWS PC에서** -자세한 내용은 [Windows 10의 저장소 공간](https://windows.microsoft.com/windows-10/storage-spaces-windows-10)을 참조 하세요.
- **단일 서버에 모든 저장소를 포함 하는 독립 실행형 서버** -자세한 내용은 [독립 실행형 서버에 저장소 공간 배포](deploy-standalone-storage-spaces.md)를 참조 하세요.
- **각 클러스터 노드에 직접 연결 된 로컬 저장소와 스토리지 공간 다이렉트를 사용 하는 클러스터 된 서버** -자세한 정보는 [스토리지 공간 다이렉트 개요](storage-spaces-direct-overview.md)를 참조 하세요.
- **모든 드라이브를 보관 하는 하나 이상의 공유 SAS 저장소 엔클로저를 포함 하는 클러스터 된 서버** -자세한 내용은 [공유 sas를 사용 하는 클러스터의 저장소 공간 개요](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831739(v%3dws.11))를 참조 하세요.

