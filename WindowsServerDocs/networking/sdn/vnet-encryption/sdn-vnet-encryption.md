---
title: 가상 네트워크 암호화
description: "' 암호화 사용 합니다.'로 표시 하는 서브넷 내에서 서로 통신 하는 가상 컴퓨터 간에 가상 네트워크 트래픽의 암호화를 허용 하는 가상 네트워크 암호화"
manager: dougkim
ms.prod: windows-server-threshold
ms.technology: networking-hv-switch
ms.topic: get-started-article
ms.assetid: 7da0f509-7b02-4a0f-90fb-d97c83a2bc4e
ms.author: pashort
author: shortpatti
ms.date: 08/08/2018
ms.openlocfilehash: f2f50ae3146854e2ef6081b0c400a474b53dcf66
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59851084"
---
# <a name="virtual-network-encryption"></a>가상 네트워크 암호화

>적용 대상: Windows Server

' 암호화 사용 합니다.'로 표시 하는 서브넷 내에서 서로 통신 하는 가상 컴퓨터 간에 가상 네트워크 트래픽의 암호화를 허용 하는 가상 네트워크 암호화 또한 가상 서브넷의 DTLS(데이터그램 전송 계층 보안)를 활용하여 패킷을 암호화합니다. DTLS는 실제 네트워크에 액세스하는 누군가에 의한 도청, 변조 및 위조를 방지합니다.

가상 네트워크 암호화가 필요합니다.
- 암호화 인증서를 각 SDN 사용이 가능한 Hyper-v 호스트에 설치 합니다.
- 해당 인증서의 지문이 참조 네트워크 컨트롤러에서 사용 되는 자격 증명 개체입니다.
- 가상 네트워크 각각에서 구성 암호화를 요구 하는 서브넷을 포함 합니다.

서브넷에서 암호화를 사용 하도록 설정 하면 해당 서브넷 내의 모든 네트워크 트래픽은 일어날 수도 수 있습니다 하는 모든 응용 프로그램 수준 암호화 하는 것 외에도 자동으로 암호화 됩니다.  암호화 된 것으로 표시 하는 경우에, 서브넷 교차 하는 트래픽은 자동으로 암호화 되지 않은 전송 됩니다. 가상 네트워크 경계를 교차 하는 모든 트래픽은 전송 암호화 되지 않은 합니다.

>[!TIP]
>암호화 된 서브넷에만 통신 하도록 응용 프로그램을 제한 해야 하는 경우 액세스 제어 목록 (Acl)만 하 여 현재 서브넷 내의 통신을 허용 합니다. 자세한 내용은 [사용 하 여 액세스 제어 목록 (Acl) 데이터 센터 네트워크 트래픽 흐름을 관리 하려면](https://docs.microsoft.com/windows-server/networking/sdn/manage/use-acls-for-traffic-flow)합니다.

### <a name="next-steps"></a>다음 단계

[가상 네트워크에 대 한 암호화 구성](https://docs.microsoft.com/windows-server/networking/sdn/vnet-encryption/sdn-config-vnet-encryption)

