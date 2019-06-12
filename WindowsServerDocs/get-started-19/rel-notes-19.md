---
title: 릴리스 정보-Windows Server 2019의 중요 한 문제
description: 충돌, 중단, 설치 오류 및 데이터 손실을 방지 하려면 해결 방법이 필요한 중요 한 문제 요약
ms.prod: windows-server-threshold
ms.technology: server-general
ms.topic: article
ms.assetid: 134aab85-664f-4d55-87ef-9e5fd098371f
author: jasongerend
ms.author: jgerend
manager: jasgroce
ms.localizationpriority: medium
ms.date: 06/07/2019
ms.openlocfilehash: 515255c301d343aa1b83bcfb506f2e3baa6ca969
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66810734"
---
# <a name="release-notes---important-issues-in-windows-server-2019"></a>릴리스 정보-Windows Server 2019의 중요 한 문제

>적용 대상: Windows Server 2019

이러한 릴리스 정보는 Windows Server 2019을 비롯해 운영 체제 방지 하거나 문제를 해결 하는 방법을 알고 있는 경우에 가장 중요 한 문제를 요약 합니다. 디자인별 변경 내용, 새 기능 및이 릴리스에서 수정 하는 방법에 대 한 내용은 [What's New in Windows Server 2019](whats-new-19.md) 및 특정 기능 팀의에서 공지 합니다. 달리 지정 하지 않으면 보고 된 각 문제는 모든 버전 및 Windows Server 2019의 설치 옵션에 적용 됩니다.  

이 문서는 계속해서 업데이트됩니다. 해결 방법이 필요한 중요한 문제가 발견되면 그 내용이 추가되고 새로운 해결 방법 및 수정 사항이 제공됩니다.  

## <a name="release-notes"></a>릴리스 정보

Windows Server 2019에 다음과 같은 알려진된 문제가 있습니다.

| Title         | 설명                            |
| -----         | -----------                            |
| 서버 설치 중 설치 옵션 메뉴 독일어 텍스트가 잘렸습니다 합니다. | 데스크톱 환경 설치 옵션에 대 한 설명을 누락 및 잘못 된 문자를 맨 끝에는 "를 설치 하려는 운영 체제 선택" 이라는 운영 체제 선택 창에 독일어 server 미디어에서 설치 프로그램을 실행 하는 경우 문장입니다. 표시 될 전체 독일어 텍스트가 다음과 같습니다.<br/>      <br/>`Durch diese Option wird die vollständige grafische Umgebung von Windows installiert, wodurch zusätzlicher Speicherplatz verbraucht wird. Sie kann hilfreich sein, wenn Sie den Windows-Desktop verwenden möchten oder über eine App verfügen, die die grafische Umgebung benötigt.` <br><br>이 공용 가용성의 Windows Server 2019, Windows Server, 1809, 버전 및 Microsoft Hyper-v Server 2019 때 해제 독일어 미디어에만 영향을 줍니다.|
| Windows Server 버전 1809 설치 하는 동안 잘못 된 Windows Server 브랜드 이미지 | Windows Server 버전 1809에 대 한 설치 환경을 중 몇 가지 초기에 배경 이미지 화면 표시 &quot;Windows Server 2019&quot;합니다.  Windows Server 버전 1709 및 1803를 사용 하 여이 단순히 나타나야 하는 대로 &quot;Windows Server&quot;합니다.  어디서 나 다른 제품에서 다른 영향은 없습니다 되며 Windows Server 2019 제품에 영향을 주지 않습니다.  문제는 설치 Windows Server 버전 1809, 볼륨 라이선스 서비스 센터에 액세스 하는 볼륨 라이선스 고객 에게만 제공 하는 동안이 이미지 제한 됩니다.<br/> |

### <a name="copyright"></a>저작권

이 문서는 "있는 그대로" 제공됩니다. URL 및 기타 인터넷 웹 사이트 참조를 포함하여 이 설명서의 내용 및 의견은 예고 없이 변경될 수 있습니다.  

이 설명서는 Microsoft 제품의 지적 재산에 대한 법적 권한을 제공하지 않습니다. 이 설명서는 내부 참조용으로만 복사 및 사용할 수 있습니다.

&copy; 2019 Microsoft Corporation. All rights reserved.  

Microsoft, Active Directory, Hyper-V, Windows 및 Windows Server는 미국, 대한민국 및/또는 기타 국가에서의 Microsoft Corporation 등록 상표 또는 상표입니다.  

이 제품에는 부분적으로 Independent JPEG Group의 작업을 기반으로 하는 그래픽 필터 소프트웨어가 포함되어 있습니다.  


1.0  
