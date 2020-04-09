---
title: Windows에서 Hyper-v에 대 한 지원 되는 Linux 및 FreeBSD 가상 컴퓨터
description: 각 버전에 포함 된 Linux 통합 서비스 및 기능을 나열 합니다.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.topic: article
ms.assetid: 990ff94a-30fb-434b-b4a2-3804a5245ba6
author: shirgall
ms.author: kathydav
ms.date: 10/03/2016
ms.openlocfilehash: dff7a0f829f11a92f2c87305da806b9be43f42fe
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855946"
---
# <a name="supported-linux-and-freebsd-virtual-machines-for-hyper-v-on-windows"></a>Windows에서 Hyper-v에 대 한 지원 되는 Linux 및 FreeBSD 가상 컴퓨터

>적용 대상: Windows Server 2019, Windows Server 2016, Hyper-v 서버 2016, Windows Server 2012 R2, Hyper-v Server 2012 R2, Windows Server 2012, Hyper-v Server 2012, Windows Server 2008 R2, Windows 10, Windows 8.1, Windows 8, Windows 7.1, Windows 7

Hyper-v는 Linux 및 FreeBSD 가상 컴퓨터에 대 한 에뮬레이트된 및 하이퍼-V-특정 디바이스를 지원합니다. 에뮬레이트된 디바이스를 실행할 때 추가 소프트웨어는 설치 해야 합니다. 그러나 에뮬레이트된 장치 고성능을 제공 하지 않으면 및 Hyper-v 기술에서 제공 하는 풍부한 가상 컴퓨터 관리 인프라를 활용할 수 없습니다. 이 Hyper-v에서 제공 하는 모든 혜택을 완전 하 게 활용 하기 위해 Linux 및 FreeBSD 하이퍼-V-특정 디바이스를 사용 하 여 가장 좋습니다. 하이퍼-V-특정 디바이스를 실행 하는 데 필요한 드라이버의 컬렉션을 Integration Services LIS (Linux) 또는 FreeBSD Integration Services (BIS) 라고 합니다.

LIS는 Linux 커널에 추가한 하 고 새 릴리스를 위한 업데이트 됩니다. 하지만 최신 기능 향상 또는 수정 이전 커널에 따라 Linux 배포판 없을 수 있습니다. Microsoft는 이러한 이전 커널에 따라 일부 Linux 설치에 대 한 LIS 드라이버를 설치할 수 있는 다운로드를 제공 합니다. Linux Integration Services의 버전을 포함 하는 공급 업체, 이므로 설치에 해당 하는 경우 최신 버전 다운로드 가능한 버전의 LIS 설치 하는 최선의 합니다.

변경 내용은 LIS 기타 Linux 배포에 대 한 정기적으로 별도 다운로드 나 설치 없이가 필요 하므로 운영 체제 커널 및 애플리케이션에 통합 됩니다.

이전 FreeBSD 릴리스 (10.0) 앞에 대 한 Microsoft는 설치 가능한 BIS 드라이버 및 FreeBSD 가상 컴퓨터에 대 한 해당 디먼을 포함 하는 포트를 제공 합니다. 그 이상의 FreeBSD 버전에 대 한 BIS에 기본 제공 FreeBSD 운영 체제 이며 별도 다운로드 나 설치 없이 필수 FreeBSD 10.0에 필요한 KVP 포트 다운로드를 제외 하 고 있습니다.

> [!TIP]
> - 평가 센터에서 [Windows Server 2019](https://www.microsoft.com/evalcenter/evaluate-windows-server-2019) 를 다운로드 합니다.

이 콘텐츠의 목표 사용 하면 Hyper-v에서 Linux 또는 FreeBSD 배포 용이 하 게 하는 정보를 제공 하는 것입니다. 특정 세부 정보는 다음과 같습니다.

* Linux 배포판 또는 다운로드 및 설치 BIS 또는 LIS 드라이버 필요로 하는 FreeBSD 릴리스 합니다.

* Linux 배포판 또는 기본 제공 LIS 또는 BIS 드라이버가 포함 되어 있는 FreeBSD 릴리스 합니다.

* 주요 Linux 배포판 또는 FreeBSD 버전에서 기능을 나타내는 기능 배포 맵

* 알려진된 문제 및 각 배포 또는 버전에 대 한 대안입니다.

* 기능 각 LIS 또는 BIS 기능에 대해 설명 합니다.

**기능 및 기능에 대해 제안 하 시겠습니까?** 가 더 잘 우리가 수 있나요? [Windows Server 사용자 의견](https://windowsserver.uservoice.com/forums/295062-linux-support) 사이트를 사용 하 여 Hyper-v에서 Linux 및 FreeBSD Virtual Machines에 대 한 새로운 기능과 기능을 제안 하 고 다른 사용자에 게 제공 되는 내용을 확인할 수 있습니다.

## <a name="in-this-section"></a>이 섹션의 내용

* [Hyper-v에서 지원 되는 CentOS 및 Red Hat Enterprise Linux 가상 컴퓨터](Supported-CentOS-and-Red-Hat-Enterprise-Linux-virtual-machines-on-Hyper-V.md)

* [Hyper-V에서 지원되는 Debian 가상 머신](Supported-Debian-virtual-machines-on-Hyper-V.md)

* [Hyper-v에서 지원 되는 Oracle Linux 가상 컴퓨터](Supported-Oracle-Linux-virtual-machines-on-Hyper-V.md)

* [Hyper-v에서 지원 되는 SUSE 가상 컴퓨터](Supported-SUSE-virtual-machines-on-Hyper-V.md)

* [Hyper-v에서 지원 되는 Ubuntu 가상 머신](Supported-Ubuntu-virtual-machines-on-Hyper-V.md)

* [Hyper-v에서 지원 되는 FreeBSD 가상 컴퓨터](Supported-FreeBSD-virtual-machines-on-Hyper-V.md)

* [Hyper-v의 Linux 및 FreeBSD 가상 머신에 대 한 기능 설명](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md)

* [Hyper-v에서 Linux를 실행 하기 위한 모범 사례](Best-Practices-for-running-Linux-on-Hyper-V.md)

* [Hyper-v에서 FreeBSD 실행에 대 한 모범 사례](Best-practices-for-running-FreeBSD-on-Hyper-V.md)
