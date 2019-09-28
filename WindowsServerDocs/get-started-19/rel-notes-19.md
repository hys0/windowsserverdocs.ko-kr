---
title: 릴리스 정보 - Windows Server 2019의 주요 문제점
description: 충돌, 중단, 설치 실패 및 데이터 손실 등을 방지하기 위한 해결책이 필요한 중요한 문제를 요약합니다.
ms.prod: windows-server
ms.technology: server-general
ms.topic: article
ms.assetid: 134aab85-664f-4d55-87ef-9e5fd098371f
author: jasongerend
ms.author: jgerend
manager: jasgroce
ms.localizationpriority: medium
ms.date: 06/07/2019
ms.openlocfilehash: 6f0a13401810adebb299f0b0c9607bfe58bb405d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71360806"
---
# <a name="release-notes---important-issues-in-windows-server-2019"></a>릴리스 정보 - Windows Server 2019의 주요 문제점

>적용 대상: Windows Server 2019

이러한 릴리스 정보에서는 문제를 방지하거나 해결하는 방법(알려진 경우)을 포함하여 Windows Server 2019 운영 체제의 가장 중요한 문제를 요약합니다. 이 릴리스의 계획된 변경 사항, 새로운 기능 및 해결 방법에 대한 자세한 내용은 [Windows Server 2019의 새로운 기능](whats-new-19.md) 및 해당하는 기능 팀의 공지를 참조하세요. 별도로 지정하지 않는 이상, 보고된 각 문제는 Windows Server 2019의 모든 버전 및 설치 옵션에 적용됩니다.  

이 문서는 계속해서 업데이트됩니다. 해결 방법이 필요한 중요한 문제가 발견되면 그 내용이 추가되고 새로운 해결 방법 및 수정 사항이 제공됩니다.  

## <a name="release-notes"></a>릴리스 정보

Windows Server 2019에는 다음과 같은 알려진 문제가 있습니다.

| 제목         | 설명                            |
| -----         | -----------                            |
| 서버 설치 중 설치 옵션 메뉴에서 독일어 텍스트가 잘림 | 독일어 서버 미디어에서 설치 프로그램을 실행하는 경우 “설치할 운영 체제 선택”이라고 표시되는 운영 체제 선택 창의 데스크톱 환경 설치 옵션에 대한 설명에서 문장 맨 끝의 문자가 누락되거나 올바르지 않게 표시됩니다. 표시되어야 하는 전체 독일어 텍스트는 다음과 같습니다.<br/>      <br/>`Durch diese Option wird die vollständige grafische Umgebung von Windows installiert, wodurch zusätzlicher Speicherplatz verbraucht wird. Sie kann hilfreich sein, wenn Sie den Windows-Desktop verwenden möchten oder über eine App verfügen, die die grafische Umgebung benötigt.` <br><br>이러한 문제는 Windows Server 2019, Windows Server, 버전 1809 및 Microsoft Hyper-V Server 2019의 일반 공급에서 출시된 독일어 미디어에만 영향을 줍니다.|
| Windows Server, 버전 1809를 설치하는 동안 Windows Server 브랜드 이미지가 올바르지 않음 | Windows Server, 버전 1809에 대한 설치 환경 동안, 일부 초기 화면의 배경 이미지에 &quot;Windows Server 2019&quot;가 표시됩니다.  Windows Server, 버전 1709 및 1803을 사용할 때처럼 단순히 &quot;Windows Server&quot;로 표시되어야 합니다.  제품의 다른 부분에는 영향을 미치지 않으며, Windows Server 2019 제품에도 영향을 주지 않습니다.  이 이슈는 Windows Server, 버전 1809의 설치 동안, 볼륨 라이선스 서비스 센터에 액세스하는 볼륨 라이선스 고객에게만 제공되는 이 단일 이미지로 제한됩니다.<br/> |

### <a name="copyright"></a>저작권

이 문서는 "있는 그대로" 제공됩니다. URL 및 다른 인터넷 웹 사이트 참조를 포함한 이 문서의 내용과 관점은 예고 없이 변경될 수 있습니다.  

이 문서는 귀하에게 Microsoft 제품의 지적 재산에 대한 어떠한 법적 권리도 제공하지 않습니다. 개인적인 목적과 참조용으로만 이 문서를 복사하고 사용할 수 있습니다.

&copy; 2019 Microsoft Corporation. All rights reserved.  

Microsoft, Active Directory, Hyper-V, Windows 및 Windows Server는 미국, 대한민국 및/또는 기타 국가에서의 Microsoft Corporation 등록 상표 또는 상표입니다.  

이 제품에는 부분적으로 Independent JPEG Group의 작업을 기반으로 하는 그래픽 필터 소프트웨어가 포함되어 있습니다.  


1.0  
