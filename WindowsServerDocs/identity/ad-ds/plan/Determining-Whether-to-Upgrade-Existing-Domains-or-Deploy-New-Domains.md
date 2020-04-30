---
ms.assetid: c20231dd-2b83-4494-9385-1172272e00d6
title: 기존 도메인을 업그레이드할지 또는 새 도메인을 배포할지 결정
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 60f3dca9f4930fe9d1a717d741a818194a3db0f0
ms.sourcegitcommit: 11421f4005f9f3a3f6c0db95b1836d0f765a9fa3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81624281"
---
# <a name="determining-whether-to-upgrade-existing-domains-or-deploy-new-domains"></a>기존 도메인을 업그레이드할지 또는 새 도메인을 배포할지 결정

> 적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

디자인의 각 도메인은 새 도메인 또는 업그레이드 된 기존 도메인입니다. 업그레이드 하지 않은 기존 도메인의 사용자는 새 도메인으로 이동 해야 합니다.

도메인 간에 계정을 이동 하면 최종 사용자에 게 영향을 줄 수 있습니다. 사용자를 새 도메인으로 이동할지 아니면 기존 도메인을 업그레이드할지를 결정 하기 전에 사용자를 도메인으로 이동 하는 비용을 기준으로 새 AD DS 도메인의 장기 관리 혜택을 평가 합니다.

Active Directory 도메인을 Windows Server 2008로 업그레이드 하는 방법에 대 한 자세한 내용은 [Windows server 2008 및 Windows server 2008 R2 AD DS 도메인으로 Active Directory 도메인 업그레이드](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731188(v=ws.10))를 참조 하세요.

포리스트 내 및 포리스트 간 AD DS 도메인 구조 변경에 대 한 자세한 내용은 [ADMT Guide: Active Directory 도메인 마이그레이션 및 재구성](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc974332(v=ws.10))을 참조 하세요.

새 도메인 및 업그레이드 된 도메인에 대 한 계획을 문서화 하는 데 도움이 되는 워크시트의 경우 [Windows Server 2003 배포 키트의 작업 지원](https://microsoft.com/download/details.aspx?id=9608) 에서 Job_Aids_Designing_and_Deploying_Directory_and_Security_Services .zip을 다운로드 하 고 "도메인 계획" (DSSLOGI_5)을 엽니다.
