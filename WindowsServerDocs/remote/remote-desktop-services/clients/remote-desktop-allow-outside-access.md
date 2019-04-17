---
title: 원격 데스크톱-네트워크 외부에서 PC에 대 한 액세스를 허용 합니다.
description: 원격으로 PC의 네트워크 외부에서 PC에 액세스 하기 위한 옵션에 대 한 설명
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
ms.sourcegitcommit: 1533d994a6ddea54ac189ceb316b7d3c074307db
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/01/2018
ms.locfileid: "1708661"
---
# <a name="remote-desktop---allow-access-to-your-pc-from-outside-your-pcs-network"></a>원격 데스크톱-PC의 네트워크 외부에서 PC에 대 한 액세스를 허용 합니다.

>적용 대상: Windows, Windows Server 2016 10

원격 데스크톱 클라이언트를 사용 하 여 PC에 연결할 때에 피어-투-피어 연결을 만들려는 합니다. 즉, ("호스트"이 라고도 함) PC에 직접 액세스할 수 있어야 합니다. PC에서 실행 되 고 네트워크 외부에서 PC에 연결 해야 하는 경우 해당 액세스를 사용 하도록 설정 해야 합니다. 옵션의 몇: 포트 전달을 사용 하 여 또는 VPN을 설정 합니다.

## <a name="enable-port-forwarding-on-your-router"></a>라우터에서 포트 전달 사용

단순히 포트 전달에 액세스 하려면 PC의 IP 주소와 포트를 라우터의 IP 주소 (공용 IP)에서 포트를 매핑합니다. 

라우터의 지침에 대 한 온라인 검색을 수행 해야 하므로 사용 중인 라우터에서 포트 전달을 사용 하도록 설정 하는 것에 대 한 특정 단계에 따라 다릅니다. 단계에 대 한 일반적인 내용은 [wikiHow를 포트 착신 전환 설정에서 라우터를](https://www.wikihow.com/Set-Up-Port-Forwarding-on-a-Router)체크아웃 합니다.

포트를 매핑할 하기 전에 다음 필요 합니다.

- PC 내부 IP 주소:에서 **설정 > 네트워크 및 인터넷 > 상태 > 네트워크 속성을 볼**합니다. "작업" 상태와 네트워크 구성을 찾아 다음 **IPv4 주소**를 가져옵니다.

   ![운영 네트워크 구성](../media/rdclient-operational-network.png)

- 공용 IP 주소 (라우터의 IP). 여러 가지 방법으로이 찾을 수-(Bing 또는 Google)에 "내 IP"를 검색 하거나 (Windows 10)에 대 한 [Wi-fi 네트워크 속성](https://binged.it/2Gwob34) 을 볼 수 있습니다.
- 매핑 중인 포트 번호입니다. 이 3389-대부분의 경우에서 기본 포트가 원격 데스크톱 연결에서 사용 합니다.
- 라우터에서에 대 한 관리자 액세스 합니다.  

   >[!WARNING]
   > 인터넷 최대 PC를 열려는-PC에 대 한 설정 하는 강력한 암호 있는지 확인 합니다.

포트를 매핑한 후 라우터 (위의 두 번째 글머리)의 공용 IP 주소에 연결 하 여 로컬 네트워크 외부에서 PC 호스트에 연결할 수 있습니다.

라우터의 IP 주소를 변경할 수-인터넷 서비스 공급자 (ISP)은 언제 든 지 새 IP를 할당할 수 있습니다. 이 문제에 하는 것을 방지 하려면 동적 DNS를 사용 하는 것이 좋습니다.-이 도메인 이름, IP 주소 대신 기억 하기 쉬운를 사용 하 여 PC에 연결할 수 있습니다. 라우터 자동으로 업데이트 하는 DDNS 서비스를 사용 하 여 새 IP 주소와 해당 변경 해야 합니다.

대부분의 라우터를 사용 하면 어떤 원본 IP 또는 원본 네트워크 포트 매핑을 사용할 수 있습니다 정의할 수 있습니다. 하므로 작업에서 연결 하려는 알고 있는 경우 회사 네트워크에 대 한 IP 주소를 추가할 수 있습니다 수 있는 전체 공용 인터넷에 포트를 열지 마십시오. 연결을 사용 하는 호스트 동적 IP 주소를 사용 하는 경우 해당 특정 ISP의 전체 범위에서 액세스할 수 있도록 소스 제한을 설정 합니다.

또한 내부 IP 주소를 변경 하지 않도록 PC에서 [고정 IP 주소](/windows-hardware/customize/mobile/mcsf/enable-static-ip) 설정을 고려할 수 있습니다. 그 다음 라우터의 경우 포트 전달은 항상 올바른 IP 주소를 가리킵니다.


## <a name="use-a-vpn"></a>VPN을 사용 하 여

가상 사설망 (VPN)를 사용 하 여 로컬 영역 네트워크에 연결 하는 경우에 공용 인터넷 PC 열 필요가 없습니다. 대신, VPN에 연결 하면 RD 클라이언트는 동일한 네트워크의 일부인 하 고 PC에 액세스할 수와 동일 하 게 작동 합니다. 사용할 수 있는 다양 한 VPN 서비스-찾아 중 가장 적합 한 경우에 사용할 수 있습니다.