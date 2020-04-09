---
title: 테스트 랩 구성 단계
description: 이 항목은 테스트 랩 가이드-Windows Server 2016에 대 한 DirectAccess 멀티 사이트 배포 시연의 일부입니다.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-da
ms.topic: article
ms.assetid: dc7205b4-a822-4038-ab67-ec0a870737f2
ms.author: lizross
author: eross-msft
ms.openlocfilehash: c83d89cefe330a99777ea204f0aea417f5e03c33
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80861526"
---
# <a name="steps-for-configuring-the-test-lab"></a>테스트 랩 구성 단계

>적용 대상: Windows Server(반기 채널), Windows Server 2016

다음 단계에서는 원격 액세스 인프라를 구성 하 고, 원격 액세스 서버 및 클라이언트를 구성 하 고, 인터넷 및 Ho Et 서브넷에서 DirectAccess 연결을 테스트 하는 방법을 설명 합니다.  
  
이 테스트 랩 가이드에서는 다음 단계를 수행 하 여 멀티 사이트 원격 액세스 배포를 구축 합니다.  
  
-   [1 단계: 기본 구성을 완료](assetId:///9eb4a9ba-9118-4ea3-8963-e643ec81c3ed)합니다. [테스트 랩 가이드: IPv4 및 IPv6 혼합을 사용 하 여 DirectAccess 단일 서버 설정 시연](https://go.microsoft.com/fwlink/p/?LinkId=237004)의 모든 단계를 완료 합니다.  
  
-   [2 단계: ROUTER1을 설치 하 고 구성](assetId:///e4b1a298-d5b0-410e-970b-c5358a9378f9)합니다. ROUTER1은 Corpnet 및 Corpnet 서브넷 간의 라우팅 및 전달 기능을 제공 합니다.  
  
-   [3 단계: CLIENT2 설치 및 구성](assetId:///6cbee1b5-f6f6-443f-8fa9-31cc5c05a0ee) CLIENT2는 windows Server 2016, Windows Server 2012 R2 또는 Windows Server 2012 원격 액세스 배포의 이전 버전과의 호환성을 보여 주는 데 사용 되는 Windows 7 클라이언트 컴퓨터입니다.  
  
-   [4 단계: APP1 구성](assetId:///a0ee655e-c01e-4bf3-a7b3-064e9614f810) APP1를 기본 게이트웨이로 사용 하 고 2-d c 2를 대체 DNS 서버로 구성 합니다.  
  
-   [5 단계: DC1 구성](assetId:///205ca795-93ce-4e53-aa6b-b44c87f0e14a) 추가 Active Directory 사이트와 Windows 7 클라이언트 컴퓨터에 대 한 추가 보안 그룹을 사용 하 여 DC1을 구성 합니다.  
  
-   [6 단계: 2-DC1 설치 및 구성](assetId:///16752f61-edbf-4ff4-9d7a-e2077b66a127) 멀티 사이트 배포에는 두 개 이상의 도메인 및 사이트가 있습니다. 2-DC1은 corp2.corp.contoso.com 도메인에 대 한 도메인 컨트롤러 및 DNS 서비스를 제공 합니다.  
  
-   [7 단계: APP1을 설치 하 고 구성](assetId:///7d04b54e-590a-4d33-9766-415789859f29)합니다. 2-APP1는 2 Corpnet 네트워크의 웹 및 파일 서버입니다.  
  
-   [8 단계: INET1 구성](assetId:///8ecc0b63-8626-4939-8d26-3d51d051d231) INET1는이 테스트 랩 가이드에서 인터넷을 시뮬레이트합니다. 2-EDGE1의 공용 IP 주소로 확인 되는 DNS 항목을 구성 해야 합니다.  
  
-   [9 단계: EDGE1 구성](assetId:///562744dc-30f6-42fa-bd5f-60a013b2179e) EDGE1에서 2-Corpnet DNS 서버 및 라우팅을 구성 합니다.  
  
-   [10 단계: 2-EDGE1 설치 및 구성](assetId:///1938c4f3-ca96-475d-9f2e-6bea3b7a4130) 멀티 사이트 배포에는 두 개의 원격 액세스 서버가 필요 합니다. 2-EDGE1는 두 번째 도메인에 대 한 원격 액세스 서비스를 제공 합니다.  
  
-   [11 단계: 멀티 사이트 배포를 구성](assetId:///537e4b68-043f-49c9-94d8-15ce8c4b18e2)합니다. 원격 액세스 서버를 모두 구성한 후에는 멀티 사이트 배포를 구성할 수 있습니다.  
  
-   [12 단계: DirectAccess 연결을 테스트](assetId:///aa293b5d-4b6f-4004-95f3-0ab54804b15c)합니다. EDGE1 및 2 EDGE1를 통해 인터넷 서브넷의 클라이언트 컴퓨터에서 DirectAccess 연결을 테스트 합니다.  
  
-   [13 단계: NAT 장치 뒤에서 DirectAccess 연결을 테스트](assetId:///41f8195b-00a1-4991-9db8-3703514dbe0c)합니다. NAT 장치 뒤에서 DirectAccess 연결을 테스트 합니다.  
  
-   [14 단계: 구성 스냅숏 만들기](assetId:///7b56d5c9-c334-463e-9e29-d652ca110d84) 테스트 랩을 완료 한 후 나중에 다시 돌아가서 추가 시나리오를 테스트할 수 있도록 작동 하는 원격 액세스 멀티 사이트 배포의 스냅숏을 만듭니다.  
  


