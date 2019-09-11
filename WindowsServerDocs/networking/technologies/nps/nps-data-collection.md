---
title: 네트워크 정책 서버 사용자 데이터 수집
description: Windows Server 2016의 네트워크 정책 서버에서 사용자를 인증 하는 데 사용 되는 정보입니다.
author: MicrosoftGuyJFlo
manager: mtillman
ms.author: joflore
ms.reviewer: richagi
ms.custom: it-pro
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: ''
ms.date: 05/01/2018
ms.openlocfilehash: cd145402ed70aa52da7188dee9dd64ce17fea155
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70871881"
---
# <a name="network-policy-server-user-data-collection"></a>네트워크 정책 서버 사용자 데이터 수집

이 문서에서는 제거할 이벤트의 NPS (네트워크 정책 서버)에서 수집 된 사용자 정보를 찾는 방법을 설명 합니다.

>[!Note]
>개인 데이터를 보거나 삭제 하는 데 관심이 있는 경우 [GDPR 사이트에 대 한 Windows 데이터 주체 요청](https://docs.microsoft.com/microsoft-365/compliance/gdpr-dsr-windows) 에서 Microsoft의 지침을 검토 하세요. GDPR에 대 한 일반 정보를 찾고 있는 경우 [서비스 신뢰 포털의 gdpr 섹션](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted)을 참조 하세요.

## <a name="information-collected-by-nps"></a>NPS에서 수집한 정보

- 타임 스탬프
- 이벤트 타임 스탬프
- Username
- 정규화 된 사용자 이름
- 클라이언트 IP 주소
- 클라이언트 공급 업체
- 클라이언트 이름
- 인증 형식
- RADIUS 프로토콜에 관련 된 기타 여러 필드

## <a name="gather-data-from-nps"></a>NPS에서 데이터 수집

계정 데이터를 사용 하도록 설정 하 고 구성 하는 경우 구성에 따라 SQL Server 또는 로그 파일에서 사용자의 NPS 인증 시도 기록을 가져올 수 있습니다. 

SQL Server에 대 한 회계 데이터가 구성 된 경우 User_Name = `'<username>'`인 모든 레코드를 쿼리 합니다.

로그 파일에 대해 계정 데이터가 구성 된 경우 로그 파일 `<username>` 을 검색 하 여 모든 로그 항목을 찾습니다.

네트워크 정책 및 액세스 서비스 이벤트 로그 항목은 계정 데이터로 중복 간주 되며 수집할 필요가 없습니다.

계정 데이터를 사용할 수 없는 경우를 검색 `<username>`하 여 네트워크 정책 및 액세스 서비스 이벤트 로그에서 사용자의 NPS 인증 시도 기록을 가져올 수 있습니다.
