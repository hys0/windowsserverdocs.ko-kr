---
title: 실제 컴퓨터 및 기본 스테이션 설정
description: 기본 스테이션을 MultiPoint 서비스에서 첫 번째 시스템을 설정 하는 방법 알아보기
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4e83b126-ce9a-4cd7-a0bd-6627c9e0f81b
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: 6569c4963d31b72216943bf29b71411e702caf84
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59812014"
---
# <a name="set-up-the-physical-computer-and-primary-station"></a>실제 컴퓨터 및 기본 스테이션 설정
MultiPoint 서비스를 설치 하기 전에 기본 스테이션 MultiPoint 서비스 시스템을 설정 해야 합니다. 로컬 영역 네트워크 (LAN)를 사용 하는 경우 컴퓨터를 LAN에 연결 합니다.  
  
A *스테이션* MultiPoint 서비스 액세스는 끝점입니다. 합니다 *기본 스테이션* 첫 번째 스테이션 MultiPoint 서비스를 시작할 때 시작 됩니다. 관리자는 액세스 시작 메뉴 및 설정에 사용할 수 있습니다. 시스템 구성에 대 한 액세스를 제공 하는 기본 스테이션 및 문제 해결 시작 하는 동안 전과 MultiPoint 서비스 에서만 사용할 수 있는 정보 시스템은 실행 됩니다. 시작 후 다른 스테이션와 마찬가지로 기본 스테이션을 사용할 수 있습니다.  
  
기본 스테이션 스테이션 직접 비디오를 연결 해야 합니다. 다음 절차에 필요한 하드웨어 MultiPoint 서비스 컴퓨터에 연결 하는 방법을 설명 합니다.  
  
스테이션에 대 한 자세한 내용은 참조 하세요. [MultiPoint 스테이션](multipoint-services-stations.md)합니다. 하드웨어 선택 도움말을 참조 하세요 [Your MultiPoint 서비스 시스템에 대 한 하드웨어 선택](Selecting-Hardware-for-Your-MultiPoint-services-System.md)합니다. 정보에 연결 하는 방법에 대 한 다른 스테이션 MultiPoint 서비스 형식, 참조 [추가 스테이션 MultiPoint 서비스 컴퓨터에 연결할](Attach-additional-stations-to-your-MultiPoint-services-computer.md)합니다.  
  
> [!NOTE]  
> 비디오 연결 스테이션을 만들려면 (예:는 영어 또는 스페인어 언어 키보드) 라틴어 키보드를 사용 해야 합니다.  
  
## <a name="to-set-up-your-primary-station"></a>에 기본 스테이션을 설정 하려면  
  
1.  MultiPoint 서비스를 실행 하는 컴퓨터의 연결 해제을 확인 합니다.  
  
2.  모니터의 전원 코드를 전원 콘센트에 연결 하 고 아래와 같이 모니터 케이블 비디오 디스플레이 포트를 컴퓨터에 연결 합니다.  
  
    ![USB 허브 기반 시스템에 대한 동영상 연결 이미지](./media/WMSVideoConnection.gif)  
  
3.  스테이션을 USB 키보드 및 마우스를 사용할 경우 다음 단계를 완료 합니다.  
  
    1.  아래와 같이 컴퓨터의 열려 있는 USB 포트에는 외부 USB 허브를 연결 합니다.  
  
        ![MultiPoint 서비스 USB 허브 연결 이미지](./media/WMSUSBHubConnection.gif)  
  
    2.  USB 키보드 및 마우스 USB 허브에 연결 합니다.  
  
        ![USB 허브 입력 장치 연결 이미지](./media/WMSUSBDeviceConnection.gif)  
  
        > [!NOTE]  
        > PS/2 포트 MultiPoint 서비스 컴퓨터에 있으면, 필요한 경우 사용할 수 ps/2 키보드와 마우스를 컴퓨터에 직접 연결 합니다. 그러나이 설치에 중요 한 제한 사항이 있습니다. 사용자 플래시 드라이브 ps/2 스테이션에서 및 오디오 장치, 웹 카메라를 사용할 수 없습니다.  
  
    3.  외부에서 전원이 공급 되는 허브를 사용 하는 경우 전원 콘센트에 허브의 전원 케이블을 연결 합니다.  
  
        > [!IMPORTANT]  
        > 전원이 켜진된 허브의 사용을 권장합니다. 언더 현재 상태에서 시스템 동작 오류가 발생할 수 있습니다.  
        >   
        > 사용자가 마우스 및 키보드는 컴퓨터의 USB 포트에 직접 하지 연결 해야 합니다. 이 방법은 여러 키보드 및 마우스를 동일한 스테이션 또는 스테이션이 없습니다의 잘못 된 연결을 전혀 발생할 가능성이 있습니다.  
  
        > [!NOTE]  
        > 시스템의 마더보드에 호스트 오디오 장치 MultiPoint 서비스 콘솔 모드일 때만 제공 됩니다. 외부 USB 허브를 사용 하는 장치에 대 한 중단 없이 오디오 허브에 연결 하는 USB 오디오 장치를 사용 해야 합니다.  
  
## <a name="to-connect-the-computer-to-the-lan"></a>LAN에 컴퓨터 연결  
  
-   LAN에 있는 경우 네트워크 케이블을 사용 하 여 네트워크에 컴퓨터를 연결 합니다.