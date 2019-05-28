---
title: Windows Server 관련 문서에 필요한 메타 데이터 태그 추가
description: 정보 목록을 Windows Server 관련 문서 맨 메타 데이터 태그로 추가 해야 합니다. 필요한 태그를 보고와 팀 요구 사항에 따라 변경 될 수 있습니다.
author: eross-msft
ms.author: lizross
ms.date: 05/06/2019
ms.openlocfilehash: f7c514def1353d44386b1bc53c8cabffe1e31fda
ms.sourcegitcommit: 7e54a1bcd31cd2c6b18fd1f21b03f5cfb6165bf3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65461639"
---
# <a name="add-the-required-metadata-tags-to-your-windows-server-related-article"></a>Windows Server 관련 문서에 필요한 메타 데이터 태그 추가

모든 문서 맨 위에 있는 추적 및 SEO 목적을 위해 포함 해야 하는 특정 메타 데이터가 있습니다. 필요한 태그를 보고 요구 사항에 따라 변경 될 수 있습니다. 그러나 사용자 필드 추가/제거 하는 경우 알림을 받게 해야 합니다.

맨 위 및 맨 아래에 세 개의 하이픈 (-)를 포함 하 여 이렇게 표시 됩니다.

```markdown

---
title: The title of the article should go here. This is used in SEO and search results.

description: A description for the article should go here. This is used in search results, to provide users with information about whether the article has the information they’re looking for.

ms.prod: Use this specific text, windows-server-threshold

ms.reviewer: The Microsoft alias for the primary PM for the feature/functionality

author: Your GitHub alias

ms.author: Your Microsoft alias

manager: Your manager’s Microsoft alias

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