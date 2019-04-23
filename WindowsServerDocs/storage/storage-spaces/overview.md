---
title: 저장소 공간 개요
ms.prod: windows-server-threshold
ms.author: jgerend
ms.manager: dougkim
ms.technology: storage-file-systems
ms.topic: article
author: jasongerend
ms.date: 05/22/2018
ms.openlocfilehash: 9977bb35be3676e31cdcab7322b5b5a2cfc67609
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59832914"
---
# <a name="storage-spaces-overview"></a>저장소 공간 개요

저장소 공간에는 Windows 및 드라이브 오류 로부터 데이터를 보호 하는 데 도움이 되는 Windows Server 기술입니다. 개념적으로 RAID, 소프트웨어에 구현 하는 것이 비슷합니다. 3 개 이상의 드라이브를 저장소 풀으로 함께 그룹화 하 여 다음 해당 풀의 용량을 사용 하 여 저장소 공간을 만들 저장소 공간을 사용할 수 있습니다. 일반적으로 데이터의 추가 복사본을 저장이 있다면 드라이브 중 하나가 실패할 경우 여전히 데이터의 복사본을 그대로 유지 됩니다. 용량 부족을 실행 하는 경우 저장소 풀에 더 많은 드라이브 추가 합니다.

네 가지 주요 방법으로 저장소 공간을 사용 하려면:

- **Windows pc** -자세한 내용은 참조 하십시오 [Windows 10의 저장소 공간](http://windows.microsoft.com/en-us/windows-10/storage-spaces-windows-10)입니다.
- **단일 서버에서 모든 저장소를 사용 하 여 독립 실행형 서버당** -자세한 내용은 참조 하십시오 [독립 실행형 서버에서 저장소 공간 배포](deploy-standalone-storage-spaces.md)합니다.
- **각 클러스터 노드에서 로컬, 직접 연결 된 저장소를 사용 하 여 저장소 공간 다이렉트를 사용 하 여 클러스터 된 서버의** -자세한 내용은 참조 하십시오 [저장소 공간 다이렉트 개요](storage-spaces-direct-overview.md)합니다.
- **하나 이상의 공유 SAS 저장소 엔클로저 보유 모든 드라이브를 사용 하 여 클러스터 된 서버의** -자세한 내용은 참조 하십시오 [공유 SAS 개요를 사용 하 여 클러스터에 저장소 공간](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831739(v%3dws.11))입니다.

