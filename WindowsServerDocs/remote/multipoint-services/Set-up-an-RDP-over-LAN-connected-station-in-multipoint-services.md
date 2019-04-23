---
title: MultiPoint 서비스에는 RDP-조치-LAN 연결 된 스테이션을 설정
description: MultiPoint 서비스에서 RDP-조치-LAN 시스템을 설정 하는 방법 알아보기
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 60e1a025-c2fb-4708-a3ff-c44c223a3224
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: 8d2f1644918f1a581c1bcab181cd084e12c6b576
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59843704"
---
# <a name="set-up-an-rdp-over-lan-connected-station-in-multipoint-services"></a>MultiPoint 서비스에는 RDP-조치-LAN 연결 된 스테이션을 설정
RDP-조치-LAN 연결 된 스테이션에는 씬 클라이언트, 기존의 데스크톱 또는 원격 데스크톱 프로토콜 (RDP)를 사용 하 여 MultiPoint 서비스 로컬 영역 네트워크 (LAN) 연결 하는 랩톱 컴퓨터입니다. 이 및 다른 스테이션 형식에 대 한 자세한 내용은 참조 [MultiPoint 스테이션](MultiPoint-services-Stations.md)합니다.  
  
## <a name="to-set-up-a-multipoint-station-using-a-computer-or-thin-client-on-a-lan"></a>LAN에서 컴퓨터 또는 씬 클라이언트를 사용 하 여 MultiPoint 스테이션을 설정 하려면  
  
1.  MultiPoint 서비스를 실행 하는 컴퓨터를 켭니다.  
  
2.  MultiPoint Server 컴퓨터 스위치, 라우터 또는 기타 네트워킹 장치에서 LAN에 연결 되어 있고 적절 한 IP 주소를 확인 합니다. (169.254 (APIPA 주소)를 사용 하 여 시작 하는 IP 주소를 나타낼 수 있습니다 LAN 연결을 사용 하 여 문제가 발생 하거나는 DHCP 서버에 연결할 수 없습니다 올바르게 작동 하지 않습니다.)  
  
3.  클라이언트 컴퓨터 또는 씬 클라이언트 LAN에 연결 합니다.  
  
4.  클라이언트 컴퓨터 또는 씬 클라이언트를 설정 합니다.  
  
5.  클라이언트 컴퓨터 또는 씬 클라이언트에서 원격 데스크톱 연결 또는 동등한 응용 프로그램을 시작 하 고 이름 또는 MultiPoint 서비스를 실행 하는 컴퓨터의 IP 주소를 입력 합니다.

## <a name="set-up-a-windows-10-device-for-remote-management-by-using-connector-services"></a>커넥터 서비스를 사용 하 여 원격 관리를 위한 Windows 10 장치 설정
모든 PC 또는 Windows 10을 실행 하는 랩톱을 원격으로 관리할 수 있다면:
- 커넥터 서비스가 사용 하도록 설정  
- MultiPoint 서버에서 관리 되는 컴퓨터에 컴퓨터 추가 되었습니다.  

Windows 10을 실행 하는 PC에서 MultiPoint 커넥터를 사용 하도록 설정 하려면 다음이 단계를 수행 합니다.

1. 검색 상자에 "Turn Windows 기능 사용 / 해제"를 입력 하 고 적절 한 검색 결과 선택 합니다. 

2. 기능 목록에서 사용 하도록 설정 **다중 포인트 커넥터**합니다. 이렇게 하면 장치를 관리 하는 데 필요한 MultiPoint 커넥터 서비스가 활성화 됩니다. 

MultiPoint 서버:
1. 다중 포인트 관리자를 열고 선택 **개인용 컴퓨터 추가 또는 제거** 하거나 **추가 / 제거 MultiPoint 서비스**합니다.

2. 관리 하 고 클릭 하려는 원격 컴퓨터 선택 **확인**합니다.  원격 컴퓨터에서 관리자 자격 증명에 대 한 라는 메시지가 표시 됩니다.  이 작업이 완료 되 면 원격 컴퓨터 다중 포인트 관리자 홈 탭에 표시 됩니다.

경우 성공적으로 집합 대시보드 관리자를 모니터링할 수 있습니다 관리 되는 장치에서 작업 하는 사용자.

> [!IMPORTANT]  
> 관리 되는 모니터링 하는 경우 Windows 10 장치 administratrive 사용자 설정이 적절 하 게 변경 된 서버를 제외 하 고 모니터링할 수 없습니다. 참조 [서버 설정 편집](Edit-Server-Settings.md)