---
title: MultiPoint 서비스 소개
description: MultiPoint 서비스를 여러 사용자가 시스템을 공유할 수 있도록 하는 방법 간략하게 설명
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1cbef744-4661-4ba9-9e2b-0bbd8854fd5c
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: 86d240092282e7cc29eebe638e5a97312e22baff
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59844214"
---
# <a name="introducing-multipoint-services"></a>MultiPoint 서비스 소개
Windows Server 2016에서 multiPoint 서비스 역할에서는 여러 사용자가, 각각 고유한 독립적 이며 친숙 한 Windows 환경을 컴퓨터로 동시에 공유 합니다. 여러 가지 방법으로 사용자가 세션에 액세스할 수 있습니다. 첫 번째 방법은 remoting을 사용 하 여 서버에는 [원격 데스크톱 앱](../remote-desktop-services/clients/remote-desktop-clients.md) 모든 장치를 사용 하 여 합니다. 두 번째 방법은 실제 스테이션 스테이션 MultiPoint 서버에 연결을 통해:  
  
-   컴퓨터의 비디오 포트에 직접  
  
-   유사한 USB-이더넷 장치 뿐만 아니라 특수 USB 제로 클라이언트 (다기능 USB 허브 라고도 함)를 통해.  
  
-   로컬 영역 네트워크 (LAN)를 통해  
  
이러한 각 방법에서 자세히 설명 되어 [MultiPoint 서비스 스테이션](MultiPoint-services-Stations.md) 이 문서의 뒷부분에 나오는.  
  
이 문서에서는 MultiPoint 서비스 배포를 계획할 때 고려해 야 할 다음 요인:  
  
-   어떤 유형의 MultiPoint 서비스 시스템을 사용 하는 데스크톱의 경우: 세션, 가상 머신 또는 Windows Pc 필요 한가요?  
  
-   [MultiPoint 서비스 시스템에 대 한 하드웨어 선택](Selecting-Hardware-for-Your-MultiPoint-services-System.md): 어떤 하드웨어 결정 해야?  
  
-   [하드웨어 요구 사항 및 성능 권장 사항](Hardware-Requirements-and-Performance-Recommendations.md): 어떤 하드웨어 MultiPoint 서비스에 대 한 필요한은 무엇입니까?  
  
-   [MultiPoint 서비스 사이트 계획](MultiPoint-services-Site-Planning.md): MultiPoint 서비스 및 해당 스테이션 실행 하는 컴퓨터가 배치 될 위치, 및가 수 구성 방법?  
  
-   [네트워크 고려 사항 및 사용자 계정](Network-Considerations-and-User-Accounts.md): MultiPoint 서비스 시스템에 배포 된 네트워킹 환경 사용자 계정을 관리 하는 방법으로 발생할 수 있습니다. 네트워킹 환경 이란? 사용자 계정은 어떻게 관리할 수 있습니까?  
  
-   [MultiPoint 서비스를 사용 하 여 파일 저장](Storing-Files-with-MultiPoint-services.md): 사용자 파일 저장 위치는, 및 해당 액세스 되는 방법을?  
  
-   [배포 전 검사 목록](Predeployment-Checklist.md)  