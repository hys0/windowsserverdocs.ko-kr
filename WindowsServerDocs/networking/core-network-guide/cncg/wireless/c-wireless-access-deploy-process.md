---
title: 무선 액세스 배포 프로세스
description: 이 항목은 Windows Server 2016 네트워킹 가이드 "배포 암호 기반 802.1 X 인증 된 무선 액세스"
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 2555f238-926e-4b20-9bfb-9774831062da
author: shortpatti
ms.author: pashort
ms.openlocfilehash: fcdbe796e4d530604dfec448e817eab877d34c4f
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="wireless-access-deployment-process"></a>무선 액세스 배포 프로세스

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

이러한 단계에서 무선 액세스를 배포 하는 프로세스 발생 합니다.

## <a name="stage-1--ap-deployment"></a>1 – AP 배포 단계

계획 배포 및 무선 클라이언트 연결 하 고 사용 하 여 Ap NPS로 구성 됩니다. Pre\ 중 기본 설정 및 네트워크 종속성을 따라 수 3에 무선 네트워크에 설치 하기 전에 Ap 설정을 구성 또는 설치 후 원격으로 구성할 수 있습니다.

## <a name="stage-2--ad-ds-group-configuration"></a>2-광고 DS 그룹 구성 단계

AD ds에서 무선 사용자가 하나 이상의 보안 그룹 만들어야 합니다.

그런 다음, 무선 네트워크에 액세스할 수 있는 사용자를 식별 합니다.

마지막으로, 사용자가 만든 무선 해당 사용자에 게 보안 그룹에 추가 합니다.

>[!NOTE]
>기본적으로는 **네트워크 액세스 권한을** 속성 전화에서 사용자 계정에서에서 설정을 설정으로 구성 되어 **NPS 네트워크 정책을 통해 액세스를 제어**합니다. 이 설정을 변경 하는 특정 이유를 않은 경우 기본 유지 하는 것이 좋습니다. 이렇게 하면 NPS에서 구성 된 네트워크 정책을 통해 네트워크 액세스를 제어할 수 있습니다.

## <a name="stage-3--group-policy-configuration"></a>그룹 정책 구성 – 3 단계

무선 네트워크를 구성 \ (IEEE 802.11\) 그룹 정책 편집기 관리 Microsoft Management Console \(MMC\)를 사용 하 여 그룹 정책 정책 확장 합니다.

Domain\ 구성원 컴퓨터에서 설정을 사용 하 여 무선 네트워크 정책에서 구성 하려면 그룹 정책을 적용 해야 합니다. 컴퓨터에서 도메인에 가입 먼저 되 면 자동 그룹 정책은 적용 됩니다. 그룹 정책을 변경 된 경우 새 설정은 자동으로 적용 됩니다.

- 그룹 정책 pre\ 결정 간격으로

- 도메인 사용자가 로그 오프 한 다음 네트워크에 다시 하는 경우

- 클라이언트 컴퓨터를 다시 시작 하 고 도메인에 로그온 하 여

또한 명령을 실행 하 여 컴퓨터에 로그온 한 상태를 복구 하려면 그룹 정책 하도록 할 수 있습니다 **gpupdate** 명령 프롬프트에 있습니다.

## <a name="stage-4--nps-server-configuration"></a>서버 구성 NPS-4 단계

사용 하 여 구성 마법사 NPS RADIUS 클라이언트로 무선 액세스 포인트를 추가 하려면 수 NPS 연결 요청을 처리할 때 사용 하는 네트워크 정책 만들 합니다.

마법사를 사용 하 여 네트워크 정책 만드는, PEAP EAP 유형 및 2 단계에서 만든 무선 사용자가 보안 그룹으로 지정 합니다.

## <a name="stage-5--deploy-wireless-clients"></a>배포 무선 클라이언트-5 단계

클라이언트 컴퓨터를 사용 하 여 네트워크에 연결 합니다.

유선된 LAN에 로그온 할 수 있는 도메인 구성원 컴퓨터에 대 한 그룹 정책 고치면 필요한 무선 구성 설정이 적용 자동으로 됩니다.

무선 네트워크에 있는 설정을 사용 하는 경우 \ (IEEE 802.11\) 때 내에 있으면 브로드캐스트 다양 한 후에 무선, domain\ 가입 컴퓨터는 무선 네트워크에 자동으로 자동으로 연결 하는 정책 무선 LAN 연결을 시도 합니다.

무선 네트워크에 연결할 사용자 도메인 사용자 이름 및 암호 자격 증명 메시지가 Windows에 의해 표시 되 면 에서만 제공 해야 합니다.

무선 액세스 배포를 계획 참조 [무선 액세스 배포 계획](d-wireless-access-planning.md)합니다.
