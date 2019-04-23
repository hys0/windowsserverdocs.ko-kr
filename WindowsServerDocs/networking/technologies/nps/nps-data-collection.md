---
title: 네트워크 정책 서버 사용자 데이터 수집
description: 정보는 Windows Server 2016에서 네트워크 정책 서버에서 사용자를 인증 하는 데 사용 됩니다.
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
ms.openlocfilehash: 5bddd22c9c2f954435cc6ce37347d18c76ee7de3
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59888744"
---
# <a name="network-policy-server-user-data-collection"></a>네트워크 정책 서버 사용자 데이터 수집

이 문서를 제거 하려는 경우에 네트워크 정책 서버 (NPS)에서 수집 된 사용자 정보를 찾는 방법을 설명 합니다.

>[!Note]
>보기 또는 개인 데이터를 삭제 하는 데 관심이 인 경우에 대 한 Microsoft의 지침을 검토 하세요 합니다 [GDPR에 대 한 Windows 데이터 주체 요청](https://docs.microsoft.com/microsoft-365/compliance/gdpr-dsr-windows) 사이트입니다. GDPR에 대 한 일반 정보를 찾으려는 경우 참조를 [Service Trust portal의 GDPR 섹션](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted)합니다.

## <a name="information-collected-by-nps"></a>NPS를 통해 수집 된 정보

- timestamp
- 이벤트 타임 스탬프
- Username
- 전체 정규화 된 사용자 이름
- 클라이언트 IP 주소
- 클라이언트 공급 업체
- 클라이언트 이름
- 인증 유형
- RADIUS 프로토콜과 관련 된 다른 다양 한 필드

## <a name="gather-data-from-nps"></a>NPS에서 데이터를 수집 합니다.

계정 데이터는 설정 되 고 구성 하는 경우 SQL Server 또는 구성에 따라 로그 파일에서 사용자의 NPS 인증 시도의 레코드를 가져올 수 있습니다. 

모든 쿼리는 User_Name 기록 계정 데이터를 SQL Server에 대 한 구성 된 경우 = `'<username>'`합니다.

계정 데이터를 로그 파일에 구성 된 경우 다음 로그 파일을 검색 합니다 `<username>` 모든 로그 항목을 찾으려고 합니다.

네트워크 정책 및 액세스 서비스 이벤트 로그 항목이 회계 데이터에 중복 된 것으로 간주 됩니다 및 수집할 필요가 없습니다.

계정 데이터를 사용 하지 않는 경우 사용자의 NPS 인증 시도의 레코드를 검색 하 여 네트워크 정책 및 액세스 서비스 이벤트 로그에서 가져올 수 있습니다는 `<username>`합니다.
