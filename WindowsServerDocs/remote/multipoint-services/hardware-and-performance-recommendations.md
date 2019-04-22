---
title: 하드웨어 요구 사항 및 성능 권장 사항
description: 하드웨어 및 성능 요구 사항 및 MultiPoint 서비스에 대 한 권장 사항을 제공합니다
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 99a5c9c2-270f-4753-a28c-434882c03125
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: b47f4c224d4a4f6f4aa104b6d5ee5d93590ac0c4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59823394"
---
# <a name="hardware-requirements-and-performance-recommendations"></a>하드웨어 요구 사항 및 성능 권장 사항
이 항목에서는 MultiPoint 서비스 시스템을 실행 하 고 사용자 응용 프로그램 시나리오를 지원 하는 데 필요한 하드웨어를 설명 합니다. CPU, RAM 및 네트워크 대역폭 요구 사항에 직접 사용자 시나리오에는 영향을 줍니다.  

## <a name="optimize-multipoint-services-system-performance"></a>MultiPoint 서비스 시스템 성능 최적화  
MultiPoint 서비스 시스템의 성능은 직접 영향을 받습니다 CPU, GPU, 및 ram MultiPoint 서비스를 실행 하는 컴퓨터에서 사용할 수 있는 기능입니다.  
  
### <a name="applications-and-internet-content"></a>응용 프로그램 및 인터넷 콘텐츠  
MultiPoint 서비스는 공유 리소스 컴퓨팅 솔루션 이기 때문에 스테이션에서 실행 되는 응용 프로그램의 수와 형식 MultiPoint 서비스 시스템의 성능에 영향 수 있습니다. 시스템 계획할 때에 정기적으로 사용 되는 프로그램의 유형을 고려 하는 것이 반드시 합니다. 예를 들어 그래픽 위주 응용 프로그램을 워드 프로세서와 같은 응용 프로그램 보다 더 강력한 컴퓨터로 필요합니다. 그래픽 위주 응용 프로그램을 사용 하 여 컴퓨터를 오버 로드로 인해 발생할 전체 시스템 전체에 걸쳐 지연 문제입니다.  
  
응용 프로그램에서 액세스 되는 콘텐츠 형식의 시스템의 성능을도 영향을 줍니다. 여러 개의 스테이션에 완전 한 동영상 비디오와 같이 멀티미디어 콘텐츠 액세스 하려면 웹 브라우저를 사용 하는 경우 시스템 성능에 부정적인 영향을 하기 전에 더 적은 스테이션을 연결할 수 있습니다. 반대로, 여러 개의 스테이션을 사용 하는 웹 브라우저에 정적 웹 콘텐츠 액세스 하는 경우 성능에 큰 영향 없이 더 많은 스테이션을 연결할 수 있습니다.  
  
### <a name="hardware-recommendations"></a>하드웨어 권장 사항  
다양 한 부하에서 MultiPoint 서비스 시스템을 사용 하 여 적절 한 성능을 달성 하려면 계획 하 고 시스템을 테스트 하는 경우에 다음 표의 지침을 따르세요. 이러한 사항은 기본 forMultiPoint 서비스입니다. 실제 구성 크기 조정 시스템 구성를 실행 하는 워크 로드 및 하드웨어 기능에 따라 달라 집니다. 항상 응용 프로그램 및 하드웨어를 테스트 하 여 유효성을 검사 해야 합니다.  
  
> [!NOTE]  
> 2 C = 2 코어, 4 C = 4 코어, 6 C = 6 코어, MT = 다중 스레딩 합니다. 프로세서 속도 적어도 2.0 (ghz) 이어야 합니다.  
  
### <a name="minimum-recommended-hardware-for-running-default-multipoint-server-stations"></a>최소 하드웨어를 기본 MultiPoint Server 스테이션을 실행 하기 위한 것이 좋습니다.  
  
|응용 프로그램 시나리오|최대 5 개의 스테이션|6-8 스테이션|9-12 스테이션|13-16 스테이션|17 ~ 20 개의 스테이션|21 ~ 24 스테이션|  
|------------------------|----------------------|-------------------|------------------|-------------------|-------------------|-----------------|  
|**생산성**<br /><br />Office, 웹 검색, 기간 업무 응용 프로그램|CPU: 2C<br /><br />RAM: 2GB|CPU: 2C<br /><br />RAM: 4GB|CPU: 4C<br /><br />RAM: 6GB|CPU: 4C<br /><br />RAM: 8GB|CPU: C + MT 4 또는 6 C<br /><br />RAM: 10GB| CPU: 6C+MT<br /><br />RAM: 12GB|
|**혼합**<br /><br />Office, 웹 검색, 기간 업무 응용 프로그램 및 일부 사용자가 가끔 비디오 사용|CPU: 2C<br /><br />RAM: 2GB|CPU: 2C<br /><br />RAM: 4GB|CPU: 4C<br /><br />RAM: 6GB|CPU: C + MT 4 또는 6 C<br /><br />RAM: 8GB|CPU: 6C+MT<br /><br />RAM: 10GB| CPU: 6C+MT<br /><br />RAM: 12GB| 
|**많이 사용 되는 비디오**<br /><br />Office, 웹 검색, 기간 업무 응용 프로그램 및 모든 사용자가 자주 비디오 사용 **참고 합니다.** 비디오 테스트가 기본 해상도 360p H.264 비디오를 사용 하 여 수행 되었습니다.|CPU: 4C+MT<br /><br />RAM: 2GB|CPU: 6C+MT<br /><br />RAM: 4GB|CPU: 8C+MT<br /><br />RAM: 6GB|CPU: 12C+MT<br /><br />RAM: 8GB|CPU: 16C+MT<br /><br />RAM: 10GB<br /><br />-씬 클라이언트: RemoteFX<br />USB 비디오 좋지| CPU: 20C+MT<br /><br />RAM: 12GB<br /><br />-씬 클라이언트: RemoteFX<br />USB 비디오 좋지|   
  
## <a name="minimum-recommended-hardware-for-running-full-windows-10-virtual-desktops"></a>최소 하드웨어를 전체 Windows 10 가상 데스크톱을 실행 하기 위한 것이 좋습니다.  
각 스테이션에 대 한 전체 가상 운영 체제 인스턴스를 실행 스테이션 당 호스트 하드웨어 요구 사항을 더 높은 되므로 기본 MultiPoint 데스크톱 세션을 실행할 때 보다 더 많은 계산 리소스를 많이 사용 됩니다.  
  
1.  CPU: 1 코어 또는 스테이션 당 스레드  
  
2.  솔리드 스테이트 드라이브 (SSD)  
  
    1.  용량 > = 스테이션 당 20GB + 40GB WMS 호스트 운영 체제에 대 한  
  
    2.  임의 읽기/쓰기 IOPS > 스테이션 당 3 K =  
  
3.  RAM > = 스테이션 당 2GB + 2GB WMS 호스트 운영 체제에 대 한  
  
가상화 – SLAT 두 번째 수준 주소 변환 ()를 사용 하도록 구성 된 BIOS CPU 설정  
  
최상의 MultiPoint 서비스 하드웨어 요구 사항에 맞게 선택 하는 방법에 대 한 자세한 내용은 하드웨어 공급 업체에 문의 합니다.  