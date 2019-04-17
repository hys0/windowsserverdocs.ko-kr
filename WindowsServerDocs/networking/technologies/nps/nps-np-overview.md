---
title: 네트워크 정책
description: 이 항목 네트워크 정책 서버 Windows Server 2016 대 한 네트워크 정책에 대 한 개요를 제공 하 고 NPS에 대 한 추가 지침은에 대 한 링크를 포함 합니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: e4a9b134-6d1d-40d7-a49c-5f46d5fdb419
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 7e1604f4839bd955e5ea10d9eafea5ef0c978977
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="network-policies"></a>네트워크 정책

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

이 항목에 대 한 개요 네트워크 정책 NPS에서 사용할 수 있습니다.

>[!NOTE]
>이 항목에서는 뿐만 아니라 다음 네트워크 정책 설명서를 사용할 수 있습니다.
> - [액세스 권한](nps-np-access.md)
> - [네트워크 정책을 구성합니다](nps-np-configure.md)

네트워크 정책은 집합 조건, 제한 및 연결 된 네트워크와는 하거나 수 연결할 수 없는 경우 권한이 있는 사용자 지정할 수 있도록 하는 설정입니다.

RADIUS(Remote Authentication Dial-In User Service) (RADIUS) 서버로 연결 요청을 처리할 때 NPS 연결 요청에 대해 인증과 인증을 수행 합니다. NPS 인증 과정에서 사용자 또는 네트워크에 연결 하는 컴퓨터의 id를 확인 합니다. 인증 과정에서 사용자 또는 컴퓨터에서 네트워크에 액세스할 수 있는지 여부를 확인 합니다.

이러한 확인을 수행 하기 NPS NPS 콘솔에서 구성 된 네트워크 정책 사용 합니다. NPS도 검사 하 여 사용자 계정을 Active Directory에 전화 속성&reg; 도메인 서비스 \ (AD DS \)에 권한을 부여 합니다.

## <a name="network-policies---an-ordered-set-of-rules"></a>네트워크 정책-는 일련의 규칙

네트워크 정책으로 규칙 볼 수 있습니다. 각 규칙 조건 및 설정의 설정을 있습니다. NPS 규칙 연결 요청 속성을 조건 비교합니다. 연결 요청 규칙와 일치 하는 경우 연결에 규칙에 정의 된 설정이 적용 됩니다.

여러 네트워크 정책 NPS에서 구성 된 일련의 규칙 됩니다. 일치 하는 발견 될 때까지 NPS 목록에서 다음 두 번째 및 등의 첫 번째 규칙에 대 한 각 연결 요청을 확인 합니다.

각 네트워크 정책에는 **정책 상태** 정책을 사용 하는 설정 수 있습니다. 네트워크 정책 해제 하면 연결이 요청을 승인 하는 경우 NPS 정책을 평가 하지 않습니다.

>[!NOTE]
>구성 해야 연결 요청을 승인 수행 하는 경우 네트워크 정책 평가할 NPS 하려는 경우는 **정책 상태** 정책을 선택 하 여 설정을 사용 확인란을 선택 합니다.

## <a name="network-policy-properties"></a>네트워크 속성 정책

아니요로 각 네트워크 정책에 대 한 속성 가지가 있습니다.

### <a name="overview"></a>개요

 이러한 속성 정책을 사용 가능 여부, 여부는 정책 하거나 거부 액세스 및 특정 네트워크 연결 방법 또는 네트워크 액세스 서버 (NAS) 형식의 연결 요청에 필요한 인지 지정할 수 있습니다. 또한 개요 속성의 사용자 계정 AD DS 전화 속성 무시 있는지 여부를 지정할 수 있습니다. 이 옵션을 선택 하는 경우 네트워크 정책에서 설정에 대해서만 연결이 권한이 있는지 확인 하려면 nps 사용 됩니다.


### <a name="conditions"></a>조건

 이러한 속성 연결 요청 네트워크 정책; 찾을 수 있도록 있어야 하는 조건 지정할 수 정책에서 구성 조건 연결 요청와 일치 하는 경우 네트워크 정책 연결에 지정 된 설정을 NPS에 적용 됩니다. 예를 들어, 조건 네트워크 정책으로 NAS IPv4 주소를 지정 하 고 NPS에서 지정된 된 IP 주소를 가진 NAS 연결 요청을 받으면 정책에 대 한 조건 연결 요청을 찾습니다. 


### <a name="constraints"></a>제한

 제한 된 연결 요청와 일치 하는 데 필요한 네트워크 정책 추가 매개 변수 합니다. 연결 요청에 따라 제한을 일치 하지 않으면, NPS 자동으로 요청을 거부 합니다. 일치 하지 않는 조건 네트워크 정책에서 NPS 응답 달리 제한을 일치 하지 않으면, NPS 요청을 거부 연결 추가 네트워크 정책을 평가 않고도 합니다.

### <a name="settings"></a>설정

 이러한 속성 네트워크 정책 조건과 정책에 대 한 모든 일치 하는 경우 NPS 연결 요청에 적용 되는 설정을 지정할 수 있습니다.

새 네트워크 정책 NPS 콘솔을 사용 하 여 추가 하면 새 네트워크 정책 마법사 사용 해야 합니다. 마법사를 사용 하 여 네트워크 정책을 만든 후 정책 속성을 가져오려면 NPS 콘솔에서 정책 두 번 클릭 하 여 정책을 지정할 수 있습니다.

지정 하는 구문 패턴와 일치 하는 몇 가지 특성 정책 네트워크에 대 한 참고 [NPS에서 사용 하 여 일반적인 표현](nps-crp-reg-expressions.md)합니다.

NPS에 대 한 자세한 내용은 참조 [네트워크 NPS 정책 서버 ()](nps-top.md)합니다.
