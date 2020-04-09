---
title: MultiPoint 서비스에서 RDP over LAN 연결 스테이션 설정
description: MultiPoint 서비스에서 RDP over LAN 시스템을 설정 하는 방법에 대해 알아봅니다.
ms.date: 07/22/2016
ms.prod: windows-server
ms.technology: multipoint-services
ms.topic: article
ms.assetid: 60e1a025-c2fb-4708-a3ff-c44c223a3224
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: 36aaa4c1571ff6dd48ae645b9c7b5746be7c1857
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80853906"
---
# <a name="set-up-an-rdp-over-lan-connected-station-in-multipoint-services"></a>MultiPoint 서비스에서 RDP over LAN 연결 스테이션 설정
RDP-LAN 연결 된 스테이션은 원격 데스크톱 프로토콜 (RDP)를 사용 하 여 LAN (local area network)에서 MultiPoint 서비스에 연결 하는 씬 클라이언트, 기존 데스크톱 또는 랩톱 컴퓨터입니다. 이 및 다른 스테이션 형식에 대 한 자세한 내용은 참조 [MultiPoint 스테이션](MultiPoint-services-Stations.md)합니다.  
  
## <a name="to-set-up-a-multipoint-station-using-a-computer-or-thin-client-on-a-lan"></a>LAN에서 컴퓨터 또는 씬 클라이언트를 사용 하 여 MultiPoint 스테이션을 설정 하려면  
  
1.  MultiPoint 서비스를 실행 하는 컴퓨터를 켭니다.  
  
2.  MultiPoint Server 컴퓨터가 스위치, 라우터 또는 기타 네트워킹 장치에 의해 LAN에 연결 되어 있고 적절 한 IP 주소를가지고 있는지 확인 합니다. 169.254 (APIPA 주소)로 시작 하는 IP 주소는 LAN 연결에 문제가 있거나 DHCP 서버에 연결할 수 없거나 제대로 작동 하지 않음을 나타낼 수 있습니다.  
  
3.  클라이언트 컴퓨터 또는 씬 클라이언트를 LAN에 연결 합니다.  
  
4.  클라이언트 컴퓨터 또는 씬 클라이언트를 켭니다.  
  
5.  클라이언트 컴퓨터 또는 씬 클라이언트에서 원격 데스크톱 연결 또는 동등한 응용 프로그램을 시작 하 고 MultiPoint 서비스를 실행 하는 컴퓨터의 이름 또는 IP 주소를 입력 합니다.

## <a name="set-up-a-windows-10-device-for-remote-management-by-using-connector-services"></a>커넥터 서비스를 사용 하 여 원격 관리를 위한 Windows 10 장치 설정
Windows 10을 실행 하는 PC 또는 랩톱은 다음을 수행 하는 동안 원격으로 관리할 수 있습니다.
- 커넥터 서비스가 사용 하도록 설정 되었습니다.  
- 컴퓨터가 MultiPoint server의 관리 되는 컴퓨터에 추가 되었습니다.  

Windows 10을 실행 하는 PC에서 다음 단계에 따라 MultiPoint Connector를 사용 하도록 설정 합니다.

1. 검색 상자에 "Windows 기능 사용/사용 안 함"을 입력 하 고 적절 한 검색 결과를 선택 합니다. 

2. 기능 목록에서 **MultiPoint Connector**를 사용 하도록 설정 합니다. 그러면 장치를 관리 하는 데 필요한 MultiPoint connector service가 활성화 됩니다. 

MultiPoint 서버에서 다음을 수행 합니다.
1. 다중 포인트 관리자를 열고 **개인용 컴퓨터 추가/제거** 또는 **multipoint 서비스 추가 또는 제거**를 선택 합니다.

2. 관리 하려는 원격 컴퓨터를 선택 하 고 **확인**을 클릭 합니다.  원격 컴퓨터에 대 한 관리자 자격 증명을 입력 하 라는 메시지가 표시 됩니다.  이 작업이 완료 되 면 MultiPoint 관리자 홈 탭에 원격 컴퓨터가 표시 됩니다.

성공적으로 설정 되 면 대시보드 관리자가 관리 되는 장치에서 작업 하는 사용자를 모니터링할 수 있습니다.

> [!IMPORTANT]  
> 관리 되는 Windows 10 장치를 모니터링할 때 서버 설정이 적절 하 게 변경 administratrive 사용자를 모니터링할 수 없습니다. [서버 설정 편집](Edit-Server-Settings.md) 을 참조 하세요.