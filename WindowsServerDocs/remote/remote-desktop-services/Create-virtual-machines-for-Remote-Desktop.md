---
title: 원격 데스크톱용 가상 컴퓨터 만들기
description: 원격 데스크톱 구성 요소를 호스트할 클라우드에서 Vm을 만듭니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 08/01/2016
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b0f62d6f-0915-44ca-afef-be44a922e20e
author: lizap
manager: dongill
ms.openlocfilehash: 5c61d9f08cb799d6a63a004bedab924a6ba37fdc
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446732"
---
# <a name="create-virtual-machines-for-remote-desktop"></a>원격 데스크톱용 가상 컴퓨터 만들기

>적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016

Windows Server 2016 역할, 서비스 및 데스크톱 호스팅 배포에 필요한 기능을 실행 하는 데 사용할 테 넌 트의 환경에서 가상 컴퓨터를 만들려면 다음 단계를 사용 합니다.   
  
기본 배포의이 예제에서는 가상 컴퓨터 3 개 생성 됩니다. RD (원격 데스크톱) 연결 브로커 및 라이선스 서버 역할 서비스 및 배포에 대 한 파일 공유를 하나의 가상 머신을 호스팅할 수 있습니다. 두 번째 가상 컴퓨터는 웹 액세스 및 RD 게이트웨이 역할 서비스를 호스팅합니다.  세 번째 가상 컴퓨터는 RD 세션 호스트 역할 서비스를 호스팅합니다. 소규모 배포에 대 한 AAD 앱 프록시를 사용 하 여 배포에서 모든 공용 끝점을 제거 하 고 단일 vm 역할 서비스를 모두 결합 하 여 VM 비용을 줄일 수 있습니다. 대규모 배포에 대 한 크기 조정을 더 나은 허용 하도록 개별 가상 머신에서 다양 한 역할 서비스를 설치할 수 있습니다.  
  
이 섹션에서 Windows Server 이미지를 기반으로 각 역할에 대 한 가상 머신을 배포 하는 데 필요한 단계를 간략하게 설명 합니다 [Microsoft Azure Marketplace](https://azure.microsoft.com/marketplace/)합니다. PowerShell을 요구 하는 사용자 지정 이미지에서 가상 컴퓨터를 만들 해야 할 경우 체크 아웃 [Resource Manager 및 PowerShell을 사용 하 여 Windows VM 만들기](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-ps-create/)합니다. 그런 다음 여기로 돌아와 파일 공유에 대 한 Azure 데이터 디스크를 연결 하 고 배포에 대 한 외부 URL을 입력 합니다.  
  
1. [Windows 가상 머신을 만드는](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-hero-tutorial/) RD 연결 브로커, RD 라이선스 서버 및 파일 서버를 호스트 합니다.  
  
   이러한 목적에는 다음 명명 규칙을 사용 했습니다.  
   - RD 연결 브로커, 라이선스 서버 및 파일 서버:   
       - VM: Contoso-Cb1  
       - 가용성 집합: CbAvSet    
   - RD 웹 액세스 및 RD 게이트웨이 서버:   
       - VM: Contoso-WebGw1  
       - 가용성 집합: WebGwAvSet  
          
   - RD 세션 호스트:   
       - VM: Contoso-Sh1  
       - 가용성 집합: ShAvSet  
          
   각 VM에는 동일한 리소스 그룹을 사용합니다.  
2. 만들기 및 사용자 프로필 디스크 (UPD) 공유에 대 한 Azure 데이터 디스크를 연결 합니다.  
   1.  Azure 포털에서 **찾아보기 > 리소스 그룹**, 배포에 대 한 리소스 그룹을 클릭 하 고 RD 연결 브로커 (예: Contoso-Cb1)에 대 한 만든 VM을 클릭 합니다.  
   2.  클릭 **설정 > 디스크 > 새 연결**합니다.  
   3.  이름 및 유형에 대 한 기본값을 적용 합니다.  
   4.  인증서 및 사용자 프로필 디스크를 포함 하 여 테 넌 트의 환경에 대 한 네트워크 공유를 저장할 수 있도록 충분히 큰 (GB)의 크기를 입력 합니다. 계획 하는 사용자 당 5GB를 대략적인 수 있습니다.  
   5.  위치 및 캐싱, 호스트에 대 한 기본값을 사용 하 고 클릭 **확인**합니다.  
3. 외부에서 배포에 액세스할 수는 외부 부하 분산 장치를 만듭니다.
   1. Azure 포털에서 **찾아보기 > 부하 분산 장치**를 클릭 하 고 **추가**합니다.
   2. 입력을 **이름을**를 선택 **공용** 으로 **형식** 부하 분산 장치를 적절 한 선택 **구독**,  **리소스 그룹**, 및 **위치**합니다.
   3. 선택 **공용 IP 주소 선택**를 **새로 만들기**는 이름을 입력 하 고 선택 **확인**합니다.
   4. 선택 **만들기** 부하 분산 장치를 만들려고 합니다.
4. 배포에 대 한 외부 부하 분산 장치 구성
   1. Azure 포털에서 **찾아보기 > 리소스 그룹**, 배포에 대 한 리소스 그룹을 클릭 하 고 배포에 대해 만든 부하 분산 장치를 클릭 합니다.
   2. 트래픽을 보낼 부하 분산 장치의 백 엔드 풀을 추가 합니다.
       1. 선택 **백 엔드 풀** 하 고 **추가**합니다.
       2. 입력을 **이름을** 선택한  **\+ 가상 머신 추가**합니다.
       3. 선택 **가용성 집합** 하 고 **WebGwAvSet**합니다.
       4. 선택 **Virtual machines**를 **Contoso WebGw1**를 **선택**를 **확인**, 및 **확인**합니다.
   3. 어떤 컴퓨터가 활성화 되어 알도록 부하 분산 장치 프로브를 추가 합니다.
       1. 선택 **프로브** 하 고 **추가**합니다.
       2. 입력을 **이름** (예: HTTPS)를 선택 **TCP**를 입력 **포트** 443, 선택한 **확인**합니다.
   4. 부하 분산 들어오는 트래픽을 분산 하는 규칙을 입력 합니다.
      1. 선택 **부하 분산 규칙** 고 **추가**
      2. 입력을 **이름** (예: HTTPS)를 선택 **TCP**, 및 443 모두에 대 한 합니다 **포트** 및 **백 엔드 포트**합니다.
          - Windows 10 및 Windows Server 2016 배포에 둡니다 **세션 지 속성** 으로 **없음**그렇지 않으면 선택 합니다 **클라이언트 IP**입니다.
      3. 선택 **확인** HTTPS 규칙을 허용 하도록 합니다.
      4. 선택 하 여 새 규칙을 만듭니다 **추가**합니다.
      5. 입력을 **이름** (예: UDP), 선택 **UDP**, 및 둘 다에 대해 3391를 <strong>포트 및 * * 백 엔드 포트</strong>합니다.
          - Windows 10 및 Windows Server 2016 배포를 둡니다 **세션 지 속성** 으로 **없음**그렇지 않으면 선택 합니다 **클라이언트 IP**합니다.
      6. 선택 **확인** UDP 규칙을 허용 하도록 합니다.
   5. Contoso WebGw1에 직접 연결할 인바운드 NAT 규칙을 입력 합니다.
       1. 선택 **인바운드 NAT 규칙** 하 고 **추가**합니다.
       2. 입력을 **이름** (예: RDP-Contoso-WebGw1)를 선택 **Customm** 서비스용 **TCP** 프로토콜에 대 한 14000에 대 한 입력 및 합니다 **포트**.
       3. 선택 **가상 머신을** 및 Contoso WebGw1 합니다.
       4. 선택 **사용자 지정** 포트 매핑에 대 한 3389를 입력 합니다 **Target port**, 선택한 **확인**.
5. 외부 액세스 배포에는 외부 URL/DNS 이름을 입력 합니다.  
   1.  Azure 포털에서 클릭 **찾아보기 > 리소스 그룹**, 배포에 대 한 리소스 그룹을 클릭 하 고 RD 웹 액세스 및 RD 게이트웨이를 만든 공용 IP 주소를 클릭 합니다.  
   2.  클릭 **Configuration**(예: contoso), DNS 이름 레이블을 입력 하 고 클릭 **저장**합니다. 이 DNS 이름 레이블 (contoso.westus.cloudapp.azure.com)는 RD 웹 액세스 및 RD 게이트웨이 서버에 연결 하는 데 사용할 수 있는 DNS 이름입니다.  

