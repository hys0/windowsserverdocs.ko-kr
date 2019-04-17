---
title: 자동 가상 컴퓨터 정품 인증
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
ms.openlocfilehash: 62873140c8e114ba537dc4fd3ff7c44868c33243
ms.sourcegitcommit: ca5c80bdb903b282e292488172a7cc92546574c0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2018
ms.locfileid: "4375490"
---
# 자동 가상 컴퓨터 정품 인증

> 적용 대상: Windows Server 2019, Windows Server 반기 채널, Windows Server 2016, Windows Server 2012 R2

자동 가상 컴퓨터 정품 인증 (AVMA) 제품 사용 권한 Microsoft 소프트웨어 사용 조건에 따라 사용 하는 Windows 제품을 보장 하기 위한 구입 증명 메커니즘으로 작동 합니다.

AVMA는 연결이 끊긴된 환경에도 각 개별 가상 컴퓨터에 대 한 제품 키를 관리 하지 않고도 제대로 활성화 된 Windows server에 가상 컴퓨터를 설치할 수 있습니다. AVMA 가상 컴퓨터 정품 인증을 사용이 허가 된 가상화 서버에 바인딩하고 시작할 때 가상 컴퓨터를 활성화 합니다. AVMA 사용 및 가상 컴퓨터의 라이선스 상태 기록 데이터에 대 한 실시간 보고를 제공 합니다. 보고 및 추적 데이터 가상화 서버에서 제공 됩니다.

## 유용한 팁

볼륨 라이선스 또는 OEM 라이선스를 사용 하 여 정품 인증 되는 가상화 서버에서 AVMA 여러 가지 이점을 제공 합니다.

서버 데이터 센터 관리자 AVMA를 사용 하 여 다음을 수행할 수 있습니다.

  - 원격 위치에서 가상 컴퓨터를 정품 인증

  - 가상 컴퓨터 또는 인터넷 연결 없이 활성화

  - 가상화 된 시스템에서 액세스 권한 없이 가상화 서버에서 가상 컴퓨터 사용 및 라이선스를 추적

제품 키를 관리 하 고 서버에서 읽을 수 없는 스티커 있습니다. 가상 컴퓨터는 활성화 되 고 계속 가상화 서버 배열에서 마이그레이션할 때 경우에 작동 합니다.

파트너 서비스 공급자 사용권 계약 (SPLA) 및 기타 호스팅 공급자를 테 넌 트를 사용 하 여 제품 키를 공유 하거나 액세스를 활성화 하는 테 넌 트의 가상 컴퓨터 없습니다. 가상 컴퓨터 정품 인증은 AVMA를 사용 하는 경우 테 넌 트에 투명 합니다. 호스팅 공급자 라이선스 규정 준수를 확인 하 고 클라이언트 사용 내용 추적 서버 로그를 사용할 수 있습니다.

## 시스템 요구 사항

AVMA는 Windows Server 2019 Datacenter, Windows Server 2016 Datacenter 또는 Windows Server 2012 R2를 실행 하는 Microsoft 가상화 서버에 필요 합니다. 

다른 버전 호스트를 활성화할 수 있는 게스트는 다음과 같습니다.

|서버 호스트 버전|Windows Server 2019|Windows Server 2016|Windows Server 2012 R2|
|-|-|-|-|
|Windows Server 2019|X|X|X|
|Windows Server 2016| |X|X|
|Windows Server 2012 R2| ||X|

참고 (Datacenter, Standard, 또는 필수 패키지) 모든 버전을 정품 인증 이러한 합니다.

이 도구는 다른 가상화 서버 기술과 함께 작동 하지 않습니다.

## AVMA를 구현 하는 방법

1.  Windows Server Datacenter 가상화 서버에 설치 하 고 Microsoft Hyper-v 서버 역할을 구성 합니다. 자세한 내용은 [Hyper-v 서버 설치](../virtualization/hyper-v/get-started/install-the-hyper-v-role-on-windows-server.md)를 참조 하세요.

2.  [가상 컴퓨터 만들기](../virtualization/hyper-v/get-started/create-a-virtual-machine-in-hyper-v.md) 및에 지원 되는 서버 운영 체제를 설치 합니다.

3.  가상 컴퓨터에서 AVMA 키를 설치 합니다. 관리자 권한 명령 프롬프트에서 다음 명령을 실행 합니다.
    
    ``` 
    slmgr /ipk <AVMA_key>  
    ```

가상 컴퓨터 가상화 서버에 대 한 라이선스에 자동으로 활성화 됩니다.


> [!TIP]
> 모든 Unattend.exe 설치 파일의 AVMA 키를 사용할 수 있습니다.


## AVMA 키

Windows Server 2019에 대해 다음 AVMA 키를 사용할 수 있습니다.

|버전|   AVMA 키|
|-|-|
|Datacenter|    H3RNG-8C32Q-Q8FRX-6TDXV-WMBMW|
|Standard|  TNK62 RXVTB-4P47B-2 차원 623 4GF74|
|관련 자료|    2CTP7-NHT64-BP62M-FV6GG-HFV28|
 
Windows Server, 버전 1809에 다음 AVMA 키를 사용할 수 있습니다.

|버전|   AVMA 키|
|-|-|
|Datacenter|    H3RNG-8C32Q-Q8FRX-6TDXV-WMBMW|
|Standard|  TNK62 RXVTB-4P47B-2 차원 623 4GF74|

Windows Server, 버전 1803 및 1709에 다음 AVMA 키를 사용할 수 있습니다.

|버전|AVMA 키|
|-|-|
|Datacenter|TMJ3Y-NTRTM-FJYXT-T22BY-CWG3J|
|Standard|C3RCX-M6NRP-6CXC9-TW2F2-4RHYD|


Windows Server 2016에 대 한 다음 AVMA 키를 사용할 수 있습니다.

|버전|AVMA 키|
|-|-|
|Datacenter|TMJ3Y-NTRTM-FJYXT-T22BY-CWG3J|
|Standard|C3RCX-M6NRP-6CXC9-TW2F2-4RHYD|
|관련 자료|B4YNW-62DX9-W8V6M-82649-MHBKQ|


Windows Server 2012 R2에 대 한 다음 AVMA 키를 사용할 수 있습니다.

|버전|AVMA 키|
|-|-|
|Datacenter|Y4TGP-NPTV9-HTC2H-7MGQ3-DV4TW|
|Standard|DBGBW-NPF86-BJVTX-K3WKJ-MTB6V|
|관련 자료|K2XGM-NMBT3-2R6Q8-WF2FK-P36R2|

## 보고 및 추적

가상화 서버에서 레지스트리 (KVP)는 게스트 운영 체제에 대 한 실시간 추적 데이터를 제공합니다. 레지스트리 키를 가상 컴퓨터와 이동 하기 때문에 뿐만 아니라 라이선스 정보를 얻을 수 있습니다. 기본적으로는 KVP 다음을 포함 하는 가상 컴퓨터에 대 한 정보를 반환 합니다.

  - 정규화 된 도메인 이름

  - 운영 체제 및 서비스 팩 설치

  - 프로세서 아키텍처

  - IPv4 및 IPv6 네트워크 주소

  - RDP 주소

이 정보를 가져오는 방법에 대 한 자세한 내용은 참조 [Hyper-v 스크립트: KVP GuestIntrinsicExchangeItems 보면](http://blogs.msdn.com/b/virtual_pc_guy/archive/2008/11/18/hyper-v-script-looking-at-kvp-guestintrinsicexchangeitems.aspx).


> [!NOTE]
> KVP 데이터는 보호 되지 않습니다. 변경 내용에 대 한 모니터링 하지 않는 및 수정할 수 있습니다.



> [!IMPORTANT]
> AVMA 키는 다른 제품 키 (소매, OEM 또는 볼륨 라이선스 키)를 교체 하는 경우 KVP 데이터를 제거 해야 합니다.


AVMA 요청에 대 한 기록 데이터는 가상화 서버 (이벤트 Id 12310)의 로그 파일에서 사용할 수 있습니다.

AVMA 정품 인증 프로세스 투명 이기 때문에 오류 메시지가 표시 되지 않습니다. 그러나 다음 이벤트 (이벤트 Id 12309) 가상 컴퓨터에서 로그 파일에 캡처됩니다.

|알림|설명|
|-|-|
|AVMA 성공|가상 컴퓨터를 정품 인증 됩니다.|
|잘못 된 호스트|가상화 서버 응답 하지 않습니다. 이 서버에서 지원 되는 버전의 Windows 실행 중이지 않을 때 발생할 수 있습니다.|
|잘못 된 데이터|일반적으로에서 가상 컴퓨터를 손상, 암호화 또는 데이터 불일치 종종 인해 가상화 서버와 통신에 오류가 발생 합니다.|
|정품 인증 거부|가상화 서버 AVMA ID 일치 하지 않은 게스트 운영 체제를 활성화할 수 없습니다.|

