---
title: 테스트 랩 시나리오 개요
description: 이 항목은 테스트 랩 가이드-Windows Server 2016에 대 한 DirectAccess 멀티 사이트 배포 시연의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9afeced4-1a9b-4cb3-9fc4-d7e44c675755
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 8f58072fba266bb6f50b78785654a4748c1b8cb3
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80314643"
---
# <a name="overview-of-the-test-lab-scenario"></a>테스트 랩 시나리오 개요

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 테스트 랩 시나리오에서 DirectAccess는 배포 됩니다.  
  
-   **D c 1**-구성 된 서버를 도메인 컨트롤러로, DNS 서버 및 corp.contoso.com 도메인에 대 한 DHCP 서버입니다.  
  
-   **2-d c 1**-구성 된 서버를 도메인 컨트롤러 및 corp2.corp.contoso.com 도메인에 대 한 DNS 서버입니다.  
  
-   **EDGE1 및 2 EDGE1**-원격 액세스 서버로 구성 된 내부 네트워크에 두 명의 서버입니다. 각 서버에 두 개의 네트워크 어댑터가 있습니다. 내부 네트워크에 연결 된 하나 및 다른 외부 네트워크에 연결 합니다.  
  
-   **A p p 1 및 2-a p p 1**-웹 및 파일 서버로 구성 된 내부 네트워크에 두 명의 서버입니다.  
  
-   **A p p 2**-IPv4 전용 웹 및 파일 서버 구성 된 내부 네트워크의 컴퓨터입니다. 이 컴퓨터는 NAT64/DNS64 기능을 강조 표시 하는 데 사용 됩니다.  
  
-   **ROUTER1**-서버에 두 개의 회사 내부 네트워크 간의 라우팅을 제공 하도록 구성 됩니다.  
  
-   **INET1**-서버에 인터넷 DNS 및 DHCP 서버로 구성 됩니다.  
  
-   **NAT1**-클라이언트 컴퓨터는 네트워크 주소 변환기 (NAT) 장치 인터넷 연결 공유를 사용 하 여 구성 된 합니다.  
  
-   **CLIENT1 및 CLIENT2**-내부 네트워크, 시뮬레이션된 된 인터넷 및 홈 네트워크 간에 이동 하는 경우 DirectAccess 연결을 테스트 하는 DirectAccess 클라이언트로 구성 하는 두 클라이언트 컴퓨터입니다. **CLIENT2** 은 Windows 7&reg;  클라이언트입니다.  
  
테스트 랩 다음 시뮬레이션 하는 4 개의 서브넷 이루어져 있습니다.  
  
-   Homenet (192.168.137.0/24) 이라고 하는 홈 네트워크에서 NAT 인터넷에 연결  
  
-   외부 네트워크에서 인터넷 서브넷 (131.107.0.0/24)으로 표시 합니다.  
  
-   Corpnet 이라는 내부 네트워크 (10.0.0.0/24; 2001:db8:1:: / 64) EDGE1 원격 액세스 서버에 의해 인터넷에서 분리 합니다.  
  
-   내부 네트워크 라는 2 Corpnet1 (10.2.0.0/24; 2001:db8:2:: / 64) 2 EDGE1 원격 액세스 서버에 의해 인터넷에서 분리 합니다.  
  
각 서브넷에 있는 컴퓨터는 다음 그림에 나와 있는 것 처럼 실제 또는 가상 허브나 스위치를 사용 하 여 연결 합니다.  
  
![테스트 랩 개요](../../../media/Overview-of-the-Test-Lab-Scenario_4/TLG_DA_Multisite.png)  
  


