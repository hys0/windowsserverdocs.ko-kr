---
ms.assetid: c20231dd-2b83-4494-9385-1172272e00d6
title: 기존 도메인을 업그레이드할지 또는 새 도메인을 배포할지 결정
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: e07965b079a953d062f5bdaaca8f9f9f32500610
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59851794"
---
# <a name="determining-whether-to-upgrade-existing-domains-or-deploy-new-domains"></a>기존 도메인을 업그레이드할지 또는 새 도메인을 배포할지 결정

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

디자인의 각 도메인에서 새 도메인을 갖게 됩니다 또는 기존 도메인을 업그레이드 합니다. 새 도메인으로 업그레이드 하지 않으면 기존 도메인에서 사용자를 이동 해야 합니다.  
  
계정을 도메인 간에 이동 최종 사용자에 게 영향을 줄 수 있습니다. 사용자가 새 도메인으로 이동 하거나 기존 도메인을 업그레이드 여부를 결정 하기 전에 도메인에 사용자를 이동 하는 비용에 대해 새 AD DS 도메인의 장기 관리 이점을 평가 합니다.  
  
Windows Server 2008 Active Directory 도메인을 업그레이드 하는 방법에 대 한 자세한 내용은 참조 하세요. [Windows Server 2008 및 Windows Server 2008 R2 AD DS 도메인에 Active Directory 도메인 업그레이드](https://technet.microsoft.com/library/cc731188.aspx)합니다.  
  
내부 및 포리스트 간에 AD DS 도메인 구조 변경 하는 방법에 대 한 자세한 내용은 Active Directory 마이그레이션 도구 버전 3.1을 참조 하세요. 마이그레이션 가이드 ([https://go.microsoft.com/fwlink/?LinkId=93678](https://go.microsoft.com/fwlink/?LinkId=93678)).  
  
신규 및 업그레이드 도메인에 대 한 계획을 문서화에 도움을 주는 워크시트에 대 한 작업 보조 기능에 대 한 Windows Server 2003 Deployment Kit에서 Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip 다운로드 ([ https://go.microsoft.com/fwlink/?LinkID=102558 ](https://go.microsoft.com/fwlink/?LinkID=102558)) 하 고 "도메인 계획" (DSSLOGI_5.doc)를 엽니다.  
  


