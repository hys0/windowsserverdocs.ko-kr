---
title: DirectAccess 클러스터-NLB 테스트 랩 시나리오 개요
description: 이 항목은 일부 테스트 랩 가이드-Windows Server 2016 Windows NLB를 사용 하 여 클러스터에서 DirectAccess 시연
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cd1e9efd-19e9-49e7-8432-881f661c9792
ms.author: pashort
author: shortpatti
ms.openlocfilehash: a6d82713dfb12e6775402d29bfcebaa0ec8b066c
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67281549"
---
# <a name="overview-of-the-directaccess-cluster-nlb-test-lab-scenario"></a>DirectAccess 클러스터-NLB 테스트 랩 시나리오 개요

>적용 대상: Windows Server (반기 채널), Windows Server 2016

이 테스트 랩 시나리오에서 DirectAccess는 배포 됩니다.  
  
-   **DC1**도메인 컨트롤러로 구성 된-서버, 도메인 이름 시스템 (DNS) 서버 및 동적 호스트 구성 프로토콜 (DHCP) 서버.  
  
-   **EDGE1**-원격 액세스 서버 클러스터의 첫 번째 원격 액세스 서버로 구성 된 내부 네트워크에 서버. 이 서버에 두 네트워크 어댑터가; 내부 네트워크에 연결 된 하나 및 다른 외부 네트워크에 연결 합니다.  
  
-   **EDGE2**-서버의 내부 네트워크에 원격 액세스 서버 클러스터의 두 번째 원격 액세스 서버로 구성 됩니다. 이 서버에 두 네트워크 어댑터가; 내부 네트워크에 연결 된 하나 및 다른 외부 네트워크에 연결 합니다.  
  
-   **APP1**-웹 및 파일 서버 및 엔터프라이즈 루트 인증 기관 (CA)으로 구성 된 내부 네트워크의 서버  
  
-   **A p p 2**-IPv4 전용 웹 및 파일 서버 구성 된 내부 네트워크의 컴퓨터입니다. 이 컴퓨터는 NAT64/DNS64 기능을 강조 표시 하는 데 사용 됩니다.  
  
-   **INET1**-서버에 인터넷 DNS 및 DHCP 서버로 구성 됩니다.  
  
-   **NAT1**-클라이언트 컴퓨터는 네트워크 주소 변환기 (NAT) 장치 인터넷 연결 공유를 사용 하 여 구성 된 합니다.  
  
-   **CLIENT1**-클라이언트 컴퓨터는 내부 네트워크, 시뮬레이션된 된 인터넷 및 홈 네트워크 간에 이동 하는 경우 DirectAccess 연결을 테스트 하는 데 사용할 DirectAccess 클라이언트로 구성 합니다.  
  
테스트 랩 다음 시뮬레이션 하는 세 개의 서브넷 이루어져 있습니다.  
  
-   Homenet (192.168.137.0/24) 이라고 하는 홈 네트워크에서 NAT 인터넷에 연결  
  
-   외부 네트워크에서 인터넷 서브넷 (131.107.0.0/24)으로 표시 합니다.  
  
-   Corpnet 이라는 내부 네트워크 (10.0.0.0/24; 2001:db8:1:: / 64) 원격 액세스 서버에 의해 인터넷에서 분리 합니다.  
  
각 서브넷에 있는 컴퓨터는 다음 그림에 나와 있는 것 처럼 실제 또는 가상 허브나 스위치를 사용 하 여 연결 합니다.  
  
![테스트 랩 개요](../../../media/Overview-of-the-Test-Lab-Scenario_5/TLG_DA_Cluster.png)  
  


