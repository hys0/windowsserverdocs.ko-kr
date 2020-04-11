---
title: 원격 데스크톱 - 네트워크 외부에서 PC에 대한 액세스 허용
description: PC의 네트워크 외부에서 PC에 원격으로 액세스하기 위한 옵션에 대해 알아보기
ms.prod: windows-server
ms.technology: remote-desktop-services
ms.topic: article
author: haley-rowland
manager: dongill
ms.author: elizapo
ms.date: 04/04/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9cc1b7568006ef9e32132d772702212c5fd78ec4
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857426"
---
# <a name="remote-desktop---allow-access-to-your-pc-from-outside-your-pcs-network"></a>원격 데스크톱 - PC의 네트워크 외부에서 PC에 대한 액세스 허용

>적용 대상: Windows 10,  Windows Server 2016

원격 데스크톱 클라이언트를 사용하여 PC에 연결할 때 피어-투-피어 연결을 만들게 됩니다. 즉, PC(경우에 따라 "호스트"라고도 함)에 직접 액세스해야 합니다. PC가 실행 중인 네트워크의 외부에서 PC에 연결해야 하는 경우 해당 액세스를 사용하도록 설정해야 합니다. 포트 전달 사용 또는 VPN 설정 등, 몇 가지 옵션을 사용할 수 있습니다.

## <a name="enable-port-forwarding-on-your-router"></a>라우터에서 포트 전달 사용

포트 전달은 라우터의 IP 주소(공용 IP)에 있는 포트를 액세스하려는 PC의 포트 및 IP 주소에 간단히 매핑합니다. 

포트 전달을 사용하도록 설정하는 구체적인 단계는 사용 중인 라우터에 따라 다르므로, 온라인에서 라우터 지침을 검색해야 합니다. 단계에 대한 일반적인 설명을 보려면 [wiki - 라우터에서 포트 전달을 설정하는 방법](https://www.wikihow.com/Set-Up-Port-Forwarding-on-a-Router)을 참조하세요.

포트를 매핑하기 전에 다음이 필요합니다.

- PC 내부 IP 주소: **설정 > 네트워크 및 인터넷 > 상태 > 네트워크 속성 보기**에서 찾습니다. 상태가 "작동 가능"인 네트워크 구성을 찾아 **IPv4 주소**를 가져옵니다.

   ![작동 가능 네트워크 구성](../media/rdclient-operational-network.png)

- 공용 IP 주소(라우터의 IP). 이 주소는 여러 가지 방법으로 찾을 수 있습니다. Bing 또는 Google에서 "내 IP"를 검색하거나 [Wi-Fi 네트워크 속성](https://binged.it/2Gwob34)(Windows 10)을 확인합니다.
- 매핑되는 포트 번호. 대부분의 경우 3389입니다. 이 포트는 원격 데스크톱 연결에서 사용되는 기본 포트입니다.
- 라우터에 대한 관리자 액세스 권한.  

   >[!WARNING]
   > PC를 인터넷까지 열게 됩니다. 이 경우 PC에 대해 강력한 암호를 설정해야 합니다.

포트를 매핑한 후 라우터의 공용 IP 주소(위에서 두 번째 글머리 기호가 붙은 항목)에 연결하여 로컬 네트워크 외부에서 호스트 PC에 연결할 수 있습니다.

라우터의 IP 주소를 변경할 수 있습니다. ISP(인터넷 서비스 공급자)는 언제든지 새 IP를 할당할 수 있습니다. 이 문제를 방지하려면 동적 DNS를 사용하는 것이 좋습니다. 이렇게 하면 IP 주소 대신, 기억하기 쉬운 도메인 이름을 사용하여 PC에 연결할 수 있습니다. 라우터는 IP 주소를 변경해야 할 경우 새 IP 주소로 DDNS 서비스를 자동으로 업데이트합니다.

대부분의 라우터에서 포트 매핑을 사용할 수 있는 원본 IP 또는 원본 네트워크를 정의할 수 있습니다. 따라서 회사에서만 연결하는 경우 회사 네트워크의 IP 주소를 추가할 수 있습니다. 이렇게 하면 포트가 전체 공용 인터넷으로 열리지 않게 됩니다. 연결하는 데 사용하는 호스트가 동적 IP 주소를 사용하는 경우 원본 제한을 설정하여 해당 특정 ISP의 전체 범위에서 액세스할 수 있도록 합니다.

내부 IP 주소가 달라지지 않도록 PC에서 [고정 IP 주소](/windows-hardware/customize/mobile/mcsf/enable-static-ip)를 설정하는 것을 고려할 수도 있습니다. 이렇게 하면 라우터의 포트 전달이 항상 올바른 IP 주소를 가리킵니다.


## <a name="use-a-vpn"></a>VPN 사용

VPN(가상 사설망)을 사용하여 LAN(Local Area Network)에 연결하는 경우 공용 인터넷까지 PC를 열 필요가 없습니다. 대신, VPN에 연결할 때 RD 클라이언트는 동일한 네트워크에 속하고 PC에 액세스할 수 있는 것처럼 작동합니다. 사용 가능한 VPN 서비스는 다양합니다. 본인에게 가장 적합한 서비스를 찾아 사용할 수 있습니다.