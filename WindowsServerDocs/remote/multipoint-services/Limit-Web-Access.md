---
title: 웹 액세스 제한
description: MultiPoint 서비스에서 인터넷에 대 한 사용자 액세스를 제한 하는 방법을 알아봅니다.
ms.custom: na
ms.date: 07/08/2016
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 044f2fd5-5b87-42bb-ba0d-c06516ac48c8
author: lizap
manager: dongill
ms.author: elizapo
ms.openlocfilehash: 9f3524261e8e93439ff48a3e6666fa7680a76a29
ms.sourcegitcommit: ccec91c1d32a978159f9b8bb5e39ead5805c26c4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/19/2019
ms.locfileid: "71143741"
---
# <a name="limit-web-access"></a>웹 액세스 제한
개별 데스크톱에서 사용자 활동을 모니터링 하는 것 외에도, 관리자는 사용자를 제한할 수 있습니다 지정 된 웹 사이트에 대 한 사용자 액세스 허용 가능한 웹 사이트 및 사용자 액세스를 차단 하려는 웹 사이트를 지정 하 여.  
  
## <a name="to-limit-web-access-on-a-station"></a>스테이션에서 웹 액세스를 제한하려면  
  
1. 다중 포인트 대시보드에서에 **웹 제한** 탭을 클릭 하 여 **구성**. **Configure Web Limiting(웹 제한 구성)** 페이지가 열립니다. 사용자가 액세스할 수 있는 사이트가 나열됩니다.  
  
2. 웹 액세스를 제한하려는 사용자 스테이션의 미리 보기 이미지를 클릭합니다.  
  
3. **Selected Item Tasks(선택한 항목 작업)** 아래에서 **Limit web access on this station(이 스테이션에서 웹 액세스 제한)** 을 클릭합니다. **Configure Web Limiting(웹 제한 구성)** 페이지가 열립니다. 사용자가 액세스할 수 있는 사이트가 나열됩니다.  
  
4. 허용되는 사이트를 추가하려면 웹 주소를 입력하고 **추가**를 클릭합니다.  
  
   > [!NOTE]
   > 예를 들어 "Contoso.com"를 입력 하면 www\.contoso.com (예: www\.newpage.contoso.com)를 기준으로 하는 사이트를 허용 하거나 차단 합니다. "Contoso"를 입력 합니다 허용 하거나 모든 Contoso 관련 사이트 (contoso.com, contoso.uk, 등 포함)를 제한 합니다.  
  
5. 허용된 사이트 목록에서 웹 주소를 제거하려면 액세스 권한을 제거할 웹 주소를 클릭하고 **제거**를 클릭합니다.  
  
## <a name="to-limit-web-access-on-all-stations"></a>모든 스테이션에서 웹 액세스를 제한하려면  
  
1. 다중 포인트 대시보드에서에 **웹 제한** 탭을 클릭 하 여 시작\-메뉴 아래쪽 한 다음 클릭 **' 모든 데스크톱 '에 대 한 웹 액세스 제한**합니다.  
  
   **Configure Web Limiting(웹 제한 구성)** 페이지가 열립니다. 사용자가 액세스할 수 있는 사이트가 나열됩니다. 다음 중 하나를 수행합니다.  
  
2. 허용된 사이트를 추가하려면 **Allow only these sites(이러한 사이트만 허용)** 를 클릭하고 허용되는 웹 주소를 입력한 다음 **추가**를 클릭합니다.  
  
   사용자가 방문 하지 않으려는 사이트를 추가 하려면 **이러한 사이트만 허용**안 함을 클릭 하 고 사용자가 방문 하지 않을 웹 주소를 입력 한 다음 **추가**를 클릭 합니다.  
  
   > [!NOTE]
   > 예를 들어 "Contoso.com"를 입력 하면 www.contoso.com에 상대적인 사이트 (예: www\.newpage.contoso.com)를 허용 하거나 차단 합니다. "Contoso"를 입력 합니다 허용 하거나 모든 Contoso 관련 사이트 (contoso.com, contoso.uk, 등 포함)를 제한 합니다.  
  
3. 웹 주소를 허용되는 사이트 및 허용되지 않는 사이트 목록에서 제거하려면 웹 주소를 선택한 다음 **제거**를 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
[사용자 데스크톱 관리](manage-user-desktops-using-multipoint-dashboard.md)  
