---
title: "Microsoft 온라인 백업 서비스 작업에 대 한 로그를 사용자 지정"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a7eafbb3-7728-487e-b287-90bbd6fee7f0
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: cd148e0e58cd80dbff7f7884ead95dc1e46b6257
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="customize-sign-up-for-microsoft-online-backup-service-task"></a>Microsoft 온라인 백업 서비스 작업에 대 한 로그를 사용자 지정

>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다.

기본적으로는 **Microsoft 온라인 백업 서비스에 대 한 등록할** 에서 작업의 **디바이스** 대시보드의 탭 Microsoft 온라인 백업 서비스 웹 사이트를 엽니다. 웹 사이트의 서비스에 대 한 정보를 제공 하 고 구독 서비스 하 고 필요한 소프트웨어를 다운로드 하는 데 도움이 됩니다.  
  
 사용자 지정할 수 있는 **Microsoft 온라인 백업 서비스에 대 한 등록할** 두 가지 방법으로 작업:  
  
-   기본 웹 사이트에 대 한 URL 사용자 지정 경험을 나타내는 URL 바꿀 수 있습니다. 기본 URL 바꾸려면 레지스트리 편집기를 열고 레지스트리 키를 만들: **를 Server\OnlineBackup\LinkUrl**, 고 사용자 정의 URL 키에 대 한 값으로 할당 합니다.  
  
-   작업을 숨길 수 있습니다. 작업을 숨기려면 레지스트리 편집기를 열고 레지스트리 키를 만들: **를 Server\OnlineBackup\OnlineBackupInstalled**합니다.  
  
## <a name="see-also"></a>참조 하십시오  
 [만들기 및 이미지를 사용자 지정](Creating-and-Customizing-the-Image.md)   
 [추가로 사용자 지정](Additional-Customizations.md)   
 [배포에 대 한 이미지를 준비 중](Preparing-the-Image-for-Deployment.md)   
 [고객 만족도 테스트합니다.](Testing-the-Customer-Experience.md)