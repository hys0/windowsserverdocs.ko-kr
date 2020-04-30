---
ms.assetid: 7530cafe-98d7-46c9-95d9-e49d39caa021
title: Windows 2000 조직에서 AD DS 배포
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 0a7dea03934a085961a8662f77b2c041b3040e17
ms.sourcegitcommit: 11421f4005f9f3a3f6c0db95b1836d0f765a9fa3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81624311"
---
# <a name="deploying-ad-ds-in-a-windows-2000-organization"></a>Windows 2000 조직에서 AD DS 배포

> 적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

조직에는 Windows 2000 Active Directory 현재 실행 중인 경우에 Windows Server 2008 도메인 컨트롤러의 운영 체제의 일부 또는 전부의 전체 업그레이드를 수행 하거나 또는 사용자 환경에 Windows Server 2008을 실행 하는 도메인 컨트롤러를 도입 하 여 Windows Server 2008 Active Directory 도메인 서비스 (AD DS)를 배포할 수 있습니다.

기존 Windows 2000 Active Directory 도메인에 Windows Server 2008을 실행 하는 도메인 컨트롤러를 추가 하기 전에 실행 해야 **adprep**, 명령줄 도구입니다. Adprep AD DS 스키마를 확장 하 고, 선택 된 개체의 기본 보안 설명자를 업데이트, 일부 애플리케이션에서 필요에 따라 새 디렉터리 개체를 추가 합니다. Adprep는 Windows Server 2008 설치 디스크 (\sources\adprep\adprep.exe)에 있습니다. 자세한 내용은 [Adprep](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/cc731728(v=ws.11))를 참조 하십시오.

> [!NOTE]
> 기존 Windows 2000 AD DS 도메인 컨트롤러를 Windows Server 2008의 전체 업그레이드를 수행 하려는 경우에 Windows Server 2003에 서버를 먼저 업그레이드 하 고 Windows Server 2008로 업그레이드 해야 합니다.

다음 그림에는 현재 실행 중인 Windows 2000 Active Directory 네트워크 환경에서 Windows Server 2008 AD DS를 배포 하기 위한 단계 보여 줍니다.

![windows 2000 조직에 배포](media/Deploying-AD-DS-in-a-Windows-2000-Organization/ee51218a-a858-49d9-8b99-9986679191c1.gif)

> [!NOTE]
> 도메인 또는 포리스트 기능 수준을 Windows Server 2008로 설정 하려는 경우 모든 도메인 컨트롤러 환경에서 Windows Server 2008 운영 체제를 실행 해야 합니다.

배포는 Windows Server 2008 AD DS의 일부로 Windows 2000 환경에서 업그레이드는 리소스 및 계정 도메인을 통합 인터포리스트 또는 포리스트 내 도메인 재구성 필요할 수 있습니다. 포리스트 간에 AD DS 도메인 구조 변경 해도 사용자 조직과 관련 된 관리 비용의 복잡성을 줄일 수 있습니다. 포리스트 내의 AD DS 도메인 구조 변경를 사용 하면 복제 트래픽을 줄이고 사용자 및 그룹 관리, 필요한 양을 줄이는의 그룹 정책 관리를 단순화 하 여 조직에 대 한 관리 오버 헤드를 줄입니다. 자세한 내용은 [ADMT Guide: Active Directory 도메인 마이그레이션 및 재구성](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc974332(v=ws.10))을 참조 하세요.

계획 및 현재 실행 중인 Windows 2000 Active Directory 조직에서 AD DS를 배포 하는 데 사용할 수 있는 세부 작업 목록은 참조 하십시오. [검사 목록: Windows 2000 조직에 AD DS 배포](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc732737(v=ws.10))합니다.
