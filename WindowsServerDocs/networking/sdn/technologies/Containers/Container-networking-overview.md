---
title: 컨테이너 네트워킹 개요
description: 이 항목의 Windows 컨테이너에 대 한 네트워킹 스택 간략하게 설명 하 고 만들기, 구성 및 컨테이너 네트워크를 관리 하는 방법에 대 한 추가 설명서 링크가 포함 되어 있습니다.
manager: ravirao
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 318659e5-e4a5-4e46-99d6-211dfc46f6b8
ms.author: pashort
author: jmesser81
ms.date: 09/04/2018
ms.openlocfilehash: 72b1ac739d9012ac7b90e97abe22e5f321ddba63
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59886144"
---
# <a name="container-networking-overview"></a>컨테이너 네트워킹 개요

>적용 대상: Windows Server (반기 채널), Windows Server 2016

이 항목에서는 제공 네트워킹 스택의 개요 Windows 컨테이너에 대 한 및 만들기, 구성 및 컨테이너 네트워크를 관리 하는 방법에 대 한 추가 지침에 대 한 링크를 포함 하는 것입니다.

Windows Server 컨테이너는 동일한 컨테이너 호스트에서 실행 되는 다른 서비스에서 응용 프로그램 또는 서비스를 분리 하는 가벼운 운영 체제 가상화 방법입니다. Windows virtual machines에 비슷한 함수를 컨테이너입니다. 사용 하도록 설정 하면 각 컨테이너의 운영 체제, 프로세스, 파일 시스템, 레지스트리 및 가상 네트워크에 연결할 수 있는 IP 주소를 별도 보기를 있습니다. 

Windows 컨테이너를 컨테이너 호스트 및 호스트에서 실행 중인 모든 컨테이너와 커널을 공유 합니다. 공유 커널 공간 때문에 이러한 컨테이너에 동일한 커널 버전과 구성이 필요합니다. 컨테이너는 프로세스 및 네임 스페이스 격리 기술을 통해 응용 프로그램 격리를 제공합니다.

>[!IMPORTANT]
>Windows 컨테이너 악의적인 보안 경계를 제공 하지 않으며 신뢰할 수 없는 코드를 격리 하려면 쓰일 수 없습니다. 

Windows 컨테이너를 사용 하 여 VM 호스트에서 만든 하나 이상의 가상 컴퓨터를 Hyper-v 호스트를 배포할 수 있습니다. VM 호스트 내에서 컨테이너를 생성 하 고 네트워킹 대 한 액세스는 가상 컴퓨터 내에서 실행 되는 가상 스위치를 통해. 컨테이너에 운영 체제 및 서비스를 배포 하는 리포지토리에 저장 하는 재사용 가능한 이미지를 사용할 수 있습니다. 각 컨테이너 가상 네트워크 어댑터가 가상 스위치에 연결 하는 인바운드 및 아웃 바운드 트래픽을 전달 합니다. 컨테이너 끝점에는 로컬 호스트 네트워크 (예: NAT), 실제 네트워크 SDN 스택을 통해 만든 오버레이 가상 네트워크에 연결할 수 있습니다.

동일한 호스트에서 컨테이너 간에 격리를 적용 하는 것에 대 한 각 Windows Server 및 Hyper-v 컨테이너에 대 한 네트워크 구획을 만들 수 있습니다. Windows Server 컨테이너는 호스트 vNIC를 사용하여 가상 스위치에 연결합니다. Hyper-V 컨테이너는 가상 VM NIC(유틸리티 VM에 노출되지 않음)를 사용하여 가상 스위치에 연결합니다. 

## <a name="related-topics"></a>관련 항목 

- [Windows 컨테이너 네트워킹](https://docs.microsoft.com/virtualization/windowscontainers/container-networking/architecture): 컨테이너 네트워크 오버레이/SDN 아닌 배포에 대 한 만들기 및 관리 하는 방법에 알아봅니다.

- [테 넌 트 가상 네트워크에 컨테이너 끝점 연결](../../manage/Connect-container-endpoints-to-a-Tenant-Virtual-Network.md): SDN 사용 하 여 오버레이 가상 네트워크에 대 한 컨테이너 네트워크 만들기 및 관리 하는 방법에 알아봅니다. 