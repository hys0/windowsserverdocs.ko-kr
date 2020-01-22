---
title: 원격 데스크톱 워크로드
description: 원격 데스크톱에서 관리하는 가상 머신의 다양한 워크로드 유형에 대해 간략히 설명합니다.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: helohr
ms.date: 12/02/2019
ms.tgt_pltfrm: na
ms.topic: article
author: Heidilohr
manager: lizross
ms.openlocfilehash: 693d1abd91fbfa2d44a6af42dd9f5338bd461927
ms.sourcegitcommit: 76469d1b7465800315eaca3e0c7f0438fc3939ed
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/13/2020
ms.locfileid: "75919950"
---
# <a name="remote-desktop-workloads"></a>원격 데스크톱 워크로드

사용자는 원격 데스크톱 서비스 또는 Windows Virtual Desktop에서 관리하는 가상 머신에서 다양한 유형의 워크로드를 실행할 수 있습니다. 각 유형의 사용자의 예상된 필요에 따라 배포 크기를 조정 합니다. 다음 표에서는 필요한 가상 머신의 크기를 예측하는 데 도움이 되는 다양한 워크로드 유형의 예를 보여 줍니다. 가상 머신이 설정되면 해당 가상 머신의 실제 사용량을 지속적으로 모니터링하고 이에 따라 크기를 조정해야 합니다. 더 크거나 작은 가상 머신이 필요한 경우 Azure에서 기존 배포를 쉽게 확장하거나 축소할 수 있습니다.

다음 표에서는 각 워크로드에 대해 설명합니다. "사용자 예"는 각 워크로드에 가장 적합할 수 있는 사용자의 유형입니다. "앱 예"는 각 워크로드에 가장 효율적으로 작동하는 앱의 종류입니다.

| 워크로드 유형 | 사용자 예 | 예제 앱 |
| --- | --- | --- |
| Light | 기본 데이터 항목 작업을 수행하는 사용자 | 데이터베이스 항목 애플리케이션, 명령줄 인터페이스 |
| 보통 | 컨설턴트 및 시장 연구자 | 데이터베이스 항목 애플리케이션, 명령줄 인터페이스, Microsoft Word, 정적 웹 페이지 |
| Heavy | 소프트웨어 엔지니어, 콘텐츠 작성자 | 데이터베이스 항목 애플리케이션, 명령줄 인터페이스, Microsoft Word, 정적 웹 페이지, Microsoft Outlook, Microsoft PowerPoint, 동적 웹 페이지 |
| 고급 | 그래픽 디자이너, 3D 모델 작성자, 기계 학습 연구자 | 데이터베이스 항목 애플리케이션, 명령줄 인터페이스, Microsoft Word, 정적 웹 페이지, Microsoft Outlook, Microsoft PowerPoint, 동적 웹 페이지, Adobe Photoshop, Adobe Illustrator, CAD(Computer-Aided Design), CAM(Computer-Aided Manufacturing) |

크기 조정 추천 사항에 대한 자세한 내용은 [가상 머신 크기 조정 지침](virtual-machine-recs.md)을 참조하세요.
