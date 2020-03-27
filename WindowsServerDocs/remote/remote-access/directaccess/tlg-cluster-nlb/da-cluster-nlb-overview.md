---
title: DirectAccess 클러스터-NLB 테스트 랩 시나리오 개요
description: 이 항목은 테스트 랩 가이드-windows Server 2016 용 Windows NLB를 사용 하는 클러스터의 DirectAccess 시연에 포함 되어 있습니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cd1e9efd-19e9-49e7-8432-881f661c9792
ms.author: lizross
author: eross-msft
ms.openlocfilehash: abc3038cfe0dacb09c115f37289fe72f1c14b96d
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80308852"
---
# <a name="overview-of-the-directaccess-cluster-nlb-test-lab-scenario"></a>DirectAccess 클러스터-NLB 테스트 랩 시나리오 개요

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 테스트 랩 시나리오에서 DirectAccess는 배포 됩니다.  
  
-   **DC1**-도메인 컨트롤러, DNS (Domain Name System) 서버 및 DHCP (Dynamic Host Configuration Protocol) 서버로 구성 된 서버입니다.  
  
-   **EDGE1**-원격 액세스 서버 클러스터의 첫 번째 원격 액세스 서버로 구성 된 내부 네트워크의 서버입니다. 이 서버에는 두 개의 네트워크 어댑터가 있습니다. 하나는 내부 네트워크에 연결 되 고 다른 하나는 외부 네트워크에 연결 됩니다.  
  
-   **EDGE2**-원격 액세스 서버 클러스터의 두 번째 원격 액세스 서버로 구성 된 내부 네트워크의 서버입니다. 이 서버에는 두 개의 네트워크 어댑터가 있습니다. 하나는 내부 네트워크에 연결 되 고 다른 하나는 외부 네트워크에 연결 됩니다.  
  
-   **APP1**-웹 및 파일 서버로 구성 된 내부 네트워크의 서버 및 엔터프라이즈 루트 CA (인증 기관)로 서의 서버  
  
-   **A p p 2**-IPv4 전용 웹 및 파일 서버 구성 된 내부 네트워크의 컴퓨터입니다. 이 컴퓨터는 NAT64/DNS64 기능을 강조 표시 하는 데 사용 됩니다.  
  
-   **INET1**-서버에 인터넷 DNS 및 DHCP 서버로 구성 됩니다.  
  
-   **NAT1**-클라이언트 컴퓨터는 네트워크 주소 변환기 (NAT) 장치 인터넷 연결 공유를 사용 하 여 구성 된 합니다.  
  
-   **CLIENT1**-내부 네트워크, 시뮬레이트된 인터넷 및 홈 네트워크 간에 이동할 때 directaccess 연결을 테스트 하는 데 사용 되는 directaccess 클라이언트로 구성 된 클라이언트 컴퓨터입니다.  
  
테스트 랩은 다음을 시뮬레이트하는 세 개의 서브넷으로 구성 됩니다.  
  
-   Homenet (192.168.137.0/24) 이라고 하는 홈 네트워크에서 NAT 인터넷에 연결  
  
-   외부 네트워크에서 인터넷 서브넷 (131.107.0.0/24)으로 표시 합니다.  
  
-   원격 액세스 서버에서 인터넷을 통해 분리 된 Corpnet (10.0.0.0/24; 2001: db8:1::/64) 이라는 내부 네트워크  
  
각 서브넷에 있는 컴퓨터는 다음 그림에 나와 있는 것 처럼 실제 또는 가상 허브나 스위치를 사용 하 여 연결 합니다.  
  
![테스트 랩 개요](../../../media/Overview-of-the-Test-Lab-Scenario_5/TLG_DA_Cluster.png)  
  


