---
title: 가상 컴퓨터 자동 정품 인증
TOCTitle: Automatic VM Activation
description: Windows Server 2019, Windows Server 2016 및 Windows Server 2012 R2에서 Vm을 활성화 하는 방법
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: server-general
ms.tgt_pltfrm: na
ms.topic: article
author: lizap
ms.author: elizapo
ms.localizationpriority: medium
ms.openlocfilehash: 18e20433050371dc02782fb8630a885e53ae31ad
ms.sourcegitcommit: 2977c707a299929c6ab0d1e0adab2e1c644b8306
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63688701"
---
# <a name="automatic-virtual-machine-activation"></a>가상 컴퓨터 자동 정품 인증

> 적용 대상: Windows Server 2019, Windows Server Semi-Annual Channel, Windows Server 2016, Windows Server 2012 R2

AVMA(자동 가상 컴퓨터 정품 인증)는 Windows 제품이 제품 사용권 및 Microsoft 소프트웨어 사용 조건에 따라 사용되는지를 확인하도록 도와주는 구입 증명 메커니즘의 역할을 합니다.

AVMA를 사용하면 연결이 끊어진 환경에서도 각 개별 가상 컴퓨터의 제품 키를 관리할 필요 없이 적절하게 정품 인증된 Windows 서버에 가상 컴퓨터를 설치할 수 있습니다. AVMA는 라이선스가 부여된 가상화 서버에 가상 컴퓨터 정품 인증을 바인딩하고 시작 시 가상 컴퓨터를 정품 인증합니다. 또한 AVMA는 사용 현황에 대한 실시간 보고 및 가상 컴퓨터의 라이선스 상태에 대한 기록 데이터를 제공합니다. 보고 및 추적 데이터는 가상화 서버에서 사용할 수 있습니다.

## <a name="practical-applications"></a>유용한 팁

볼륨 라이선스 또는 OEM 라이선스를 통해 정품 인증된 가상화 서버에서 AVMA는 여러 가지 이점을 제공합니다.

서버 데이터 센터 관리자는 AVMA를 사용하여 다음을 수행할 수 있습니다.

  - 원격 위치에서 가상 컴퓨터 정품 인증

  - 인터넷 연결 여부에 관계없이 가상 컴퓨터 정품 인증

  - 가상화된 시스템에 대한 액세스 권한 없이도 가상화 서버에서 가상 컴퓨터 사용 현황 및 라이선스 추적

서버에서 읽을 스티커 및 관리할 제품 키가 없습니다. 가상 컴퓨터가 일련의 가상화 서버에서 마이그레이션된 경우에도 정품 인증되고 계속 작동합니다.

SPLA(Service Provider License Agreement) 파트너 및 기타 호스팅 공급자는 테넌트와 제품 키를 공유하거나 테넌트의 가상 컴퓨터에 액세스하지 않고도 가상 컴퓨터의 정품 인증을 수행할 수 있습니다. AVMA를 사용하면 테넌트의 작업에 영향을 주지 않고 가상 컴퓨터 정품 인증이 수행됩니다. 호스팅 공급자는 서버 로그를 사용하여 라이선스 준수를 확인하고 클라이언트 사용 기록을 추적할 수 있습니다.

## <a name="system-requirements"></a>시스템 요구 사항

AVMA에는 Windows Server 2019 Datacenter, Windows Server 2016 Datacenter, 또는 Windows Server 2012 R2를 실행 하는 Microsoft 가상화 서버가 필요 합니다. 

다른 버전 호스트를 활성화할 수 있는 게스트는 다음과 같습니다.

|서버 호스트 버전|Windows Server 2019|Windows Server 2016|Windows Server 2012 R2|
|-|-|-|-|
|Windows Server 2019|X|X|X|
|Windows Server 2016| |X|X|
|Windows Server 2012 R2| ||X|

이러한 모든 버전 (데이터 센터, 표준 또는 Essentials)를 활성화 하는 참고 합니다.

이 도구는 다른 가상화 서버 기술과 함께 작동 하지 않습니다.

## <a name="how-to-implement-avma"></a>AVMA를 구현하는 방법

1.  Windows Server Datacenter 가상화 서버에 설치 하 고 Microsoft Hyper-v 서버 역할을 구성 합니다. 자세한 내용은 [하이퍼-V 서버 설치](../virtualization/hyper-v/get-started/install-the-hyper-v-role-on-windows-server.md)합니다.

2.  [가상 머신 만들기](../virtualization/hyper-v/get-started/create-a-virtual-machine-in-hyper-v.md) 및 지원 되는 서버 운영 체제를 설치 합니다.

3.  AVMA 키를 가상 컴퓨터에 설치합니다. 관리자 권한 명령 프롬프트에서 다음 명령을 실행합니다.
    
    ``` 
    slmgr /ipk <AVMA_key>  
    ```

가상 컴퓨터는 가상화 서버에 대해 자동으로 정품 인증됩니다.


> [!TIP]
> 모든 Unattend.exe 설정 파일에 AVMA 키를 사용할 수도 있습니다.


## <a name="avma-keys"></a>AVMA 키

Windows Server 2019에 대해 다음 AVMA 키를 사용할 수 있습니다.

|버전|   AVMA 키|
|-|-|
|Datacenter|    H3RNG-8C32Q-Q8FRX-6TDXV-WMBMW|
|Standard|  TNK62-RXVTB-4P47B-2D623-4GF74|
|Essentials|    2CTP7-NHT64-BP62M-FV6GG-HFV28|
 
Windows server, 버전 1809 다음 AVMA 키를 사용할 수 있습니다.

|버전|   AVMA 키|
|-|-|
|Datacenter|    H3RNG-8C32Q-Q8FRX-6TDXV-WMBMW|
|Standard|  TNK62-RXVTB-4P47B-2D623-4GF74|

Windows Server, 버전 1803 및 1709에 대 한 다음 AVMA 키를 사용할 수 있습니다.

|버전|AVMA 키|
|-|-|
|Datacenter|TMJ3Y-NTRTM-FJYXT-T22BY-CWG3J|
|Standard|C3RCX-M6NRP-6CXC9-TW2F2-4RHYD|


Windows Server 2016 용 다음 AVMA 키를 사용할 수 있습니다.

|버전|AVMA 키|
|-|-|
|Datacenter|TMJ3Y-NTRTM-FJYXT-T22BY-CWG3J|
|Standard|C3RCX-M6NRP-6CXC9-TW2F2-4RHYD|
|Essentials|B4YNW-62DX9-W8V6M-82649-MHBKQ|


다음 AVMA 키를 Windows Server 2012 R2에 사용할 수 있습니다.

|버전|AVMA 키|
|-|-|
|Datacenter|Y4TGP-NPTV9-HTC2H-7MGQ3-DV4TW|
|Standard|DBGBW-NPF86-BJVTX-K3WKJ-MTB6V|
|Essentials|K2XGM-NMBT3-2R6Q8-WF2FK-P36R2|

## <a name="reporting-and-tracking"></a>보고 및 추적

가상화 서버의 레지스트리(KVP)는 게스트 운영 체제에 대한 실시간 추적 데이터를 제공합니다. 레지스트리 키가 가상 컴퓨터와 함께 이동하기 때문에 라이선스 정보도 얻을 수 있습니다. KVP는 기본적으로 다음을 비롯한 가상 컴퓨터에 대한 정보를 반환합니다.

  - 정규화된 도메인 이름

  - 설치된 운영 체제 및 서비스 팩

  - 프로세서 아키텍처

  - IPv4 및 IPv6 네트워크 주소

  - RDP 주소

이 정보를 가져오는 방법에 대 한 자세한 내용은 참조 하세요. [Hyper-v 스크립트: KVP guestintrinsicexchangeitems](http://blogs.msdn.com/b/virtual_pc_guy/archive/2008/11/18/hyper-v-script-looking-at-kvp-guestintrinsicexchangeitems.aspx)합니다.


> [!NOTE]
> KVP 데이터는 보안이 유지되지 않습니다. 수정할 수 있으며 변경 내용이 모니터링되지 않습니다.



> [!IMPORTANT]
> AVMA 키가 다른 제품 키(정품, OEM 또는 볼륨 라이선스 키)로 대체된 경우에는 KVP 데이터가 제거됩니다.


AVMA 요청에 대한 기록 데이터는 가상화 서버의 로그 파일에서 확인할 수 있습니다(EventID 12310).

AVMA 정품 인증 프로세스는 다른 작업에 영향을 주지 않으므로 오류 메시지가 표시되지 않습니다. 그러나 가상 컴퓨터의 로그 파일에 다음 이벤트가 캡처됩니다(EventID 12309).

|알림|설명|
|-|-|
|AVMA 성공|가상 컴퓨터가 정품 인증되었습니다.|
|잘못된 호스트|가상화 서버가 응답하지 않습니다. 서버에서 지원되는 버전의 Windows를 실행하지 않는 경우에 발생할 수 있습니다.|
|잘못된 데이터|일반적으로 가상화 서버와 가상 컴퓨터 간의 통신 오류(주로 손상, 암호화 또는 데이터 불일치로 인해 발생)로 인해 발생합니다.|
|정품 인증 거부|AVMA ID가 일치하지 않아 가상화 서버에서 게스트 운영 체제를 정품 인증할 수 없습니다.|

