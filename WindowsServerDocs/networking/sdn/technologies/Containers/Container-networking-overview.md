---
title: 컨테이너 네트워킹 개요
description: 이 항목은 Windows 컨테이너의 네트워킹 스택에 대 한 개요 이며 컨테이너 네트워크를 만들고 구성 하 고 관리 하는 방법에 대 한 추가 지침에 대 한 링크를 제공 합니다.
manager: ravirao
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 318659e5-e4a5-4e46-99d6-211dfc46f6b8
ms.author: lizross
author: jmesser81
ms.date: 09/04/2018
ms.openlocfilehash: e8ec74ff0ebf0f0cb87db4d79ed5d37583f9beb9
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80317259"
---
# <a name="container-networking-overview"></a>컨테이너 네트워킹 개요

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목에서는 Windows 컨테이너의 네트워킹 스택에 대 한 개요를 제공 하 고, 컨테이너 네트워크 만들기, 구성 및 관리에 대 한 추가 지침에 대 한 링크를 제공 합니다.

Windows Server 컨테이너는 동일한 컨테이너 호스트에서 실행 되는 다른 서비스와 응용 프로그램 또는 서비스를 구분 하는 간단한 운영 체제 가상화 방법입니다. Windows 컨테이너는 가상 컴퓨터와 유사 하 게 작동 합니다. 사용 하도록 설정 하면 각 컨테이너에는 가상 네트워크에 연결할 수 있는 운영 체제, 프로세스, 파일 시스템, 레지스트리 및 IP 주소에 대 한 별도의 뷰가 있습니다. 

Windows 컨테이너는 컨테이너 호스트와 호스트에서 실행 되는 모든 컨테이너와 커널을 공유 합니다. 공유 커널 공간 때문에 이러한 컨테이너에 동일한 커널 버전과 구성이 필요합니다. 컨테이너는 프로세스 및 네임 스페이스 격리 기술을 통해 응용 프로그램 격리를 제공 합니다.

>[!IMPORTANT]
>Windows 컨테이너는 악의적인 보안 경계를 제공 하지 않으므로 신뢰할 수 없는 코드를 분리 하는 데 사용 하면 안 됩니다. 

Windows 컨테이너를 사용 하 여 VM 호스트에서 하나 이상의 가상 컴퓨터를 만드는 Hyper-v 호스트를 배포할 수 있습니다. VM 호스트 내에서 컨테이너가 만들어지고 네트워킹 액세스는 가상 머신 내에서 실행 되는 가상 스위치를 통해 진행 됩니다. 리포지토리에 저장 된 재사용 가능한 이미지를 사용 하 여 운영 체제 및 서비스를 컨테이너에 배포할 수 있습니다. 각 컨테이너에는 가상 스위치에 연결 하 여 인바운드 및 아웃 바운드 트래픽을 전달 하는 가상 네트워크 어댑터가 있습니다. 컨테이너 끝점을 로컬 호스트 네트워크 (예: NAT), 실제 네트워크 또는 SDN 스택을 통해 만든 오버레이 가상 네트워크에 연결할 수 있습니다.

동일한 호스트의 컨테이너 간에 격리를 적용 하려면 각 Windows Server 및 Hyper-v 컨테이너에 대 한 네트워크 구획을 만듭니다. Windows Server 컨테이너는 호스트 vNIC를 사용하여 가상 스위치에 연결합니다. Hyper-V 컨테이너는 가상 VM NIC(유틸리티 VM에 노출되지 않음)를 사용하여 가상 스위치에 연결합니다. 

## <a name="related-topics"></a>관련 항목 

- [Windows 컨테이너 네트워킹](https://docs.microsoft.com/virtualization/windowscontainers/container-networking/architecture): 오버레이가 아닌/SDN 배포에 대 한 컨테이너 네트워크를 만들고 관리 하는 방법을 알아봅니다.

- [테 넌 트 가상 네트워크에 컨테이너 끝점 연결](../../manage/Connect-container-endpoints-to-a-Tenant-Virtual-Network.md): SDN을 사용 하 여 오버레이 가상 네트워크용 컨테이너 네트워크를 만들고 관리 하는 방법을 알아봅니다. 