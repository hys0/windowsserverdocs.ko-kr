---
title: 암호화 Virtual Network
description: 가상 네트워크 암호화를 사용 하면 ' 암호화 사용 '으로 표시 된 서브넷 내에서 서로 통신 하는 가상 컴퓨터 간의 가상 네트워크 트래픽 암호화가 가능 합니다.
manager: dougkim
ms.prod: windows-server
ms.technology: networking-hv-switch
ms.topic: get-started-article
ms.assetid: 7da0f509-7b02-4a0f-90fb-d97c83a2bc4e
ms.author: pashort
author: shortpatti
ms.date: 08/08/2018
ms.openlocfilehash: 7ecb2a1373efcf15aada451313e334e210c76d1e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71355530"
---
# <a name="virtual-network-encryption"></a>암호화 Virtual Network

>적용 대상: Windows Server

가상 네트워크 암호화를 사용 하면 ' 암호화 사용 '으로 표시 된 서브넷 내에서 서로 통신 하는 가상 컴퓨터 간의 가상 네트워크 트래픽 암호화가 가능 합니다. 또한 가상 서브넷의 DTLS(데이터그램 전송 계층 보안)를 활용하여 패킷을 암호화합니다. DTLS는 실제 네트워크에 액세스하는 누군가에 의한 도청, 변조 및 위조를 방지합니다.

가상 네트워크 암호화에는 다음이 필요 합니다.
- 각 SDN 사용 Hyper-v 호스트에 암호화 인증서가 설치 되어 있어야 합니다.
- 네트워크 컨트롤러에서 해당 인증서의 지문을 참조 하는 자격 증명 개체입니다.
- 각 가상 네트워크에 대 한 구성에는 암호화를 요구 하는 서브넷이 포함 됩니다.

서브넷에서 암호화를 사용 하도록 설정 하면 해당 서브넷 내의 모든 네트워크 트래픽이 자동으로 암호화 되며, 응용 프로그램 수준 암호화도 함께 수행 될 수 있습니다.  암호화 된 것으로 표시 된 경우에도 서브넷 간에 교차 하는 트래픽은 암호화 되지 않은 상태로 자동 전송 됩니다. 가상 네트워크 경계를 교차 하는 모든 트래픽은 암호화 되지 않은 상태로 전송 됩니다.

>[!TIP]
>암호화 된 서브넷 에서만 통신 하도록 응용 프로그램을 제한 해야 하는 경우에는 현재 서브넷 내에서 통신을 허용 하는 데만 Access Control 목록 (Acl)을 사용할 수 있습니다. 자세한 내용은 [데이터 센터 네트워크 트래픽 흐름을 관리 하기 위해 acl (Access Control 목록) 사용](https://docs.microsoft.com/windows-server/networking/sdn/manage/use-acls-for-traffic-flow)을 참조 하세요.

### <a name="next-steps"></a>다음 단계

[가상 네트워크에 대 한 암호화 구성](https://docs.microsoft.com/windows-server/networking/sdn/vnet-encryption/sdn-config-vnet-encryption)

