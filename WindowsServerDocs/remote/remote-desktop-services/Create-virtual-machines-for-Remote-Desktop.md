---
title: 원격 데스크톱용 가상 컴퓨터 만들기
description: 클라우드에서 원격 데스크톱 구성 요소를 호스팅할 VM을 만듭니다.
ms.prod: windows-server
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 08/01/2016
ms.topic: article
ms.assetid: b0f62d6f-0915-44ca-afef-be44a922e20e
author: lizap
manager: dongill
ms.openlocfilehash: fa17c472e3311e4e34ac7b2176d0045886463274
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80818466"
---
# <a name="create-virtual-machines-for-remote-desktop"></a>원격 데스크톱용 가상 컴퓨터 만들기

>적용 대상: Windows Server(반기 채널), Windows Server 2019, Windows Server 2016

데스크톱 호스팅 배포에 필요한 Windows Server 2016 역할, 서비스 및 기능을 실행하는 데 사용할 테넌트 환경의 가상 머신을 만들려면 다음 단계를 따르세요.   
  
이 기본 배포 예에서는 최소 3개의 가상 머신이 생성됩니다. 첫 번째 가상 머신은 원격 데스크톱(RD) 연결 브로커 및 라이선스 서버 역할 서비스와 배포의 파일 공유를 호스팅합니다. 두 번째 가상 머신은 RD 게이트웨이 및 웹 액세스 역할 서비스를 호스팅합니다.  세 번째 가상 머신은 RD 세션 호스트 역할 서비스를 호스팅합니다. 매우 작은 배포의 경우 AAD 앱 프록시를 사용하여 배포의 모든 공용 엔드포인트를 제거하고 모든 역할 서비스를 단일 VM에 결합하면 VM 비용을 줄일 수 있습니다. 대규모 배포의 경우 개별 가상 머신에 다양한 역할 서비스를 설치하면 더 원활하게 규모를 조정할 수 있습니다.  
  
이 섹션에서는 [Microsoft Azure Marketplace](https://azure.microsoft.com/marketplace/)의 Windows Server 이미지에 따라 각 역할의 가상 머신을 배포하는 데 필요한 단계를 간략히 설명합니다. PowerShell이 필요한 사용자 지정 이미지로 가상 머신을 만들어야 하는 경우 [Resource Manager 및 PowerShell로 Windows VM 만들기](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-ps-create/)를 확인하세요. 그런 다음, 여기로 돌아와서 파일 공유의 Azure 데이터 디스크를 연결하고 배포의 외부 URL을 입력합니다.  
  
1. RD 연결 브로커, RD 라이선스 서버 및 파일 서버를 호스팅할 [Windows 가상 머신을 생성](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-hero-tutorial/)합니다.  
  
   이 경우 다음과 같은 명명 규칙을 사용합니다.  
   - RD 연결 브로커, 라이선스 서버 및 파일 서버:   
       - VM: Contoso-Cb1  
       - 가용성 세트: CbAvSet    
   - RD 웹 액세스 및 RD 게이트웨이 서버:   
       - VM: Contoso-WebGw1  
       - 가용성 세트: WebGwAvSet  
          
   - RD 세션 호스트:   
       - VM: Contoso-Sh1  
       - 가용성 세트: ShAvSet  
          
   각 VM은 동일한 리소스 그룹을 사용합니다.  
2. 사용자 프로필 디스크(UPD) 공유의 Azure 데이터 디스크를 만들고 연결합니다.  
   1.  Azure Portal에서 **찾아보기 > 리소스 그룹**을 클릭하고 배포를 위한 리소스 그룹을 클릭한 다음, RD 연결 브로커용으로 생성된 VM(예: Contoso-Cb1)을 클릭합니다.  
   2.  **설정 > 디스크 > 새 디스크 연결**을 클릭합니다.  
   3.  이름 및 유형에 기본값을 적용합니다.  
   4.  사용자 프로필 디스크 및 인증서를 포함한 테넌트의 환경에 네트워크 공유를 유지하기에 충분한 크기(GB)를 입력합니다. 사용하려고 계획 중인 사용자당 약 5GB를 추산하면 됩니다.  
   5.  위치 및 호스트 캐싱에 기본값을 적용한 후 **확인**을 클릭합니다.  
3. 외부에서 배포에 액세스하는 데 사용할 외부 부하 분산 장치를 만듭니다.
   1. Azure Portal에서 **찾아보기 > 부하 분산 장치**를 클릭한 후 **추가**를 클릭합니다.
   2. **이름**을 입력하고 부하 분산 장치의 **유형**에 **공개**를 선택한 후 적절한 **구독**, **리소스 그룹** 및 **위치**를 선택합니다.
   3. **공개 IP 주소 선택**, **새로 만들기**를 선택하고 이름을 입력한 후 **확인**을 선택합니다.
   4. **만들기**를 선택하여 부하 분산 장치를 만듭니다.
4. 배포의 외부 부하 분산 장치 구성
   1. Azure Portal에서 **찾아보기 > 리소스 그룹**, 배포의 리소스 그룹, 배포용으로 만든 부하 분산 장치를 차례로 클릭합니다.
   2. 트래픽을 보낼 부하 분산 장치의 백 엔드 풀을 추가합니다.
       1. **백 엔드 풀** 및 **추가**를 선택합니다.
       2. **이름**을 입력하고 **\+ 가상 머신 추가**를 선택합니다.
       3. **가용성 세트** 및 **WebGwAvSet**를 선택합니다.
       4. **가상 머신**, **Contoso-WebGw1**, **선택**, **확인**, **확인**을 차례로 선택합니다.
   3. 부하 분산 장치가 활성 상태의 머신을 알 수 있도록 프로브를 추가합니다.
       1. **프로브** 및 **추가**를 선택합니다.
       2. **이름**(예: HTTPS)을 입력하고 **TCP**를 선택한 후 **포트** 443을 입력하고 **확인**을 선택합니다.
   4. 수신 트래픽을 분산하는 데 사용할 부하 분산 규칙을 입력합니다.
      1. **부하 분산 규칙** 및 **추가**를 선택합니다.
      2. **이름**(예: HTTPS)을 입력하고 **포트** 및 **백 엔드 포트** 모두에 **TCP** 및 443을 선택합니다.
          - Windows 10 및 Windows Server 2016 배포의 경우 **세션 지속성**을 **없음**으로 유지하고, 그렇지 않을 경우 **클라이언트 IP**를 선택합니다.
      3. **확인**을 선택하여 HTTPS 규칙을 수락합니다.
      4. **추가**를 선택하여 새 규칙을 만듭니다.
      5. **이름**(예: UDP)을 입력하고 <strong>포트 및 **백 엔드 포트</strong> 모두에 **UDP** 및 3391을 선택합니다.
          - Windows 10 및 Windows Server 2016 배포의 경우 **세션 지속성**을 **없음**으로 유지하고, 그렇지 않을 경우 **클라이언트 IP**를 선택합니다.
      6. **확인**을 선택하여 UDP 규칙을 수락합니다.
   5. Contoso-WebGw1에 직접 연결하는 데 사용할 인바운드 NAT 규칙을 입력합니다.
       1. **인바운드 NAT 규칙** 및 **추가**를 선택합니다.
       2. **이름**(예: RDP-Contoso-WebGw1)을 입력하고, 서비스에 **사용자 지정**, 프로토콜에 **TCP**를 선택하고, **포트**에 14000을 입력합니다.
       3. **가상 머신 선택** 및 Contoso-WebGw1을 선택합니다.
       4. 포트 매핑에 **사용자 지정**을 선택하고, **대상 포트**에 3389를 입력하고, **확인**을 선택합니다.
5. 외부에서 배포에 액세스하는 데 사용할 배포의 외부 URL/DNS 이름을 입력합니다.  
   1.  Azure Portal에서 **찾아보기 > 리소스 그룹**, 배포의 리소스 그룹, RD 웹 액세스 및 RD 게이트웨이용으로 만든 공개 IP 주소를 차례로 클릭합니다.  
   2.  **구성**을 클릭하고, DNS 이름 레이블(예: contoso)을 입력한 후 **저장**을 클릭합니다. 이 DNS 이름 레이블(contoso.westus.cloudapp.azure.com)은 웹 액세스 및 RD 게이트웨이 서버에 연결하는 데 사용할 DNS 이름입니다.  

