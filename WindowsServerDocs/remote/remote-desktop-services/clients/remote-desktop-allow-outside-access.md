---
title: 원격 데스크톱-네트워크 외부에서 PC에 대 한 액세스를 허용 합니다.
description: PC의 네트워크 외부에서 PC를 원격으로 액세스할 수 있는 옵션에 알아봅니다
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
author: haley-rowland
manager: dongill
ms.author: elizapo
ms.date: 04/04/2018
ms.localizationpriority: medium
ms.openlocfilehash: d77c362d9d06b70ad0747002ed8853a39e05b7ff
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59888154"
---
# <a name="remote-desktop---allow-access-to-your-pc-from-outside-your-pcs-network"></a>원격 데스크톱-PC의 네트워크 외부에서 PC에 대 한 액세스를 허용 합니다.

>적용 대상: Windows 10,  Windows Server 2016

원격 데스크톱 클라이언트를 사용 하 여 사용자 PC에 연결할 때 만들 피어-투-피어 연결 합니다. 즉, PC ("호스트" 라고도 함)에 대 한 직접 액세스 해야 합니다. PC에서 실행 되 고 네트워크 외부에서 PC에 연결 하는 경우에 액세스할 수 있도록 해야 합니다. 두 가지 옵션이 있습니다: 포트 전달을 사용 하거나 VPN을 설정 합니다.

## <a name="enable-port-forwarding-on-your-router"></a>라우터에서 포트 전달을 사용 하도록 설정

단순히 포트 전달을 포트 및 IP 주소에 액세스 하려면 PC의 라우터의 IP 주소 (공용 IP)에서 포트를 매핑합니다. 

포트 전달을 사용 하도록 설정 하는 것에 대 한 특정 단계 라우터의 지침은 온라인에서 검색 해야 하므로 사용 하는 라우터에 따라 달라 집니다. 에 대 한 일반적인 설명은 단계, 체크 아웃 [wikiHow 설정 구성 포트 전달 라우터에](https://www.wikihow.com/Set-Up-Port-Forwarding-on-a-Router)합니다.

포트를 매핑하기 전에 다음 해야 합니다.

- PC 내부 IP 주소: 찾는 위치 **설정 > 네트워크 및 인터넷 > 상태 > 네트워크 속성을 보려면**합니다. "작업" 상태를 사용 하 여 네트워크 구성을 찾아 다음 합니다 **IPv4 주소**합니다.

   ![운영 네트워크 구성](../media/rdclient-operational-network.png)

- 공용 IP 주소 (라우터의 IP). 여러 가지 방법으로이 찾으려면-검색할 수 있습니다 (Bing 이나 Google)에 "내 IP" 보거나 합니다 [Wi-fi 네트워크 속성](https://binged.it/2Gwob34) (Windows 10)에 대 한 합니다.
- 매핑되는 포트 번호입니다. 3389-이 대부분의 경우에서 원격 데스크톱 연결에서 사용 되는 기본 포트입니다.
- 라우터가에 대 한 관리자 액세스 합니다.  

   >[!WARNING]
   > 인터넷까지 PC를 열려는-강력한 암호가 PC에 대 한 설정 했는지 확인 합니다.

포트를 매핑한 후 라우터 (위의 두 번째 글머리)의 공용 IP 주소에 연결 하 여 로컬 네트워크 외부에서 호스트 PC에 연결할 수 있습니다.

라우터의 IP 주소를 변경할 수 있습니다-인터넷 서비스 공급자 (ISP)은 언제 든 지 새 IP를 할당할 수 있습니다. 이 문제를 방지 하려면 동적 DNS를 사용 하는 것이 좋습니다.-이렇게 하면 도메인 이름 대신 IP 주소를 기억 하기 쉬운를 사용 하 여 PC에 연결할 수 있습니다. 라우터가 자동으로 서비스를 업데이트 합니다 DDNS에 새 IP 주소로 변경 해야 합니다.

대부분의 라우터는 원본 IP 또는 원본 네트워크 포트 매핑을 사용할 수를 정의할 수 있습니다. 작업에서 연결 하려는 알고 있는 경우 회사 네트워크에 대 한 IP 주소를 추가할 수 있습니다 따라서 수 있는 전체 공용 인터넷에 포트를 열지 마십시오. 동적 IP 주소를 사용 하는 호스트에 연결 하는 데 사용할 경우 해당 특정 ISP의 전체 범위에서 액세스할 수 있도록 원본 제한을 설정 합니다.

설정 고려할 수도 있습니다는 [고정 IP 주소](/windows-hardware/customize/mobile/mcsf/enable-static-ip) pc 내부 IP 주소를 변경 하지 않습니다. 다음 라우터의 하면 포트 전달을 항상 올바른 IP 주소를 가리킵니다.


## <a name="use-a-vpn"></a>VPN을 사용 하 여

가상 사설망 (VPN)을 사용 하 여 로컬 영역 네트워크에 연결한 경우에 공용 인터넷에 PC를 열 필요가 없습니다. 대신, VPN에 연결할 때 RD 클라이언트는 동일한 네트워크의 일부가 되 고 사용자 PC에 액세스할 수 있으려면 처럼 작동 합니다. 사용 가능한 VPN 서비스는 여러 가지-찾아서 중 적합 한 사용할 수 있습니다.