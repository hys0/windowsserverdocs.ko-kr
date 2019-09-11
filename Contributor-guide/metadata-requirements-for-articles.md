---
title: 필요한 메타 데이터 태그를 Windows Server 관련 문서에 추가 합니다.
description: Windows Server 관련 문서의 맨 위에 메타 데이터 태그로 추가 해야 하는 정보 목록입니다. 필요한 태그는 보고 및 팀 요구 사항에 따라 변경 될 수 있습니다.
author: eross-msft
ms.author: lizross
ms.date: 05/06/2019
ms.openlocfilehash: f0af6b48cd3fd28ae0a15752cb21bfe9a4abf14f
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70865085"
---
# <a name="add-the-required-metadata-tags-to-your-windows-server-related-article"></a>필요한 메타 데이터 태그를 Windows Server 관련 문서에 추가 합니다.

모든 문서 맨 위에는 추적 및 SEO 용도로 포함 되어야 하는 특정 메타 데이터가 있습니다. 필요한 태그는 보고 요구 사항에 따라 변경 될 수 있습니다. 그러나 필드를 추가/제거 해야 하는 경우 알림이 표시 됩니다.

위와 아래에 세 개의 하이픈 (---)을 포함 하 여 다음과 같이 표시 됩니다.

```markdown

---
title: The title of the article should go here. This is used in SEO and search results.

description: A description for the article should go here. This is used in search results, to provide users with information about whether the article has the information they're looking for.

ms.prod: Use this specific text, windows-server-threshold

ms.reviewer: The Microsoft alias for the primary PM for the feature/functionality

author: Your GitHub alias

ms.author: Your Microsoft alias

manager: Your manager's Microsoft alias

ms.topic: Type of article, including article, landing-page, get-started-article, or reference

ms.date: Date of change (MM/DD/YYYY)

---

```

## <a name="example"></a>예제

```markdown

---
title: What is Windows Admin Center?
description: Learn about the Windows Admin Center, a locally-deployed, browser-based management tool set that lets you manage your Windows Servers with no Azure or cloud dependency.
ms.prod: windows-server-threshold
ms.reviewer: alainch
author: danielle-github
ms.author: danielle
manager: alainch
ms.topic: article
ms.date: 07/06/2019
---

```