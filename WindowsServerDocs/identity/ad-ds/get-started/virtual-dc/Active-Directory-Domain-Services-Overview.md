---
ms.assetid: f052dfcd-dace-4485-8d0a-cc7df5cf3751
title: Active Directory 도메인 서비스 개요
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 84ce4986d27884f817eb5e632ac8dc1c5a22b922
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71390484"
---
# <a name="active-directory-domain-services-overview"></a>Active Directory 도메인 서비스 개요

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012


디렉터리는 네트워크의 개체에 대 한 정보를 저장 하는 계층 구조입니다. Active Directory Domain Services (AD DS)와 같은 디렉터리 서비스는 디렉터리 데이터를 저장 하 고이 데이터를 네트워크 사용자 및 관리자가 사용할 수 있도록 하는 방법을 제공 합니다. 예를 들어 AD DS은 이름, 암호, 전화 번호 등의 사용자 계정에 대 한 정보를 저장 하 고, 동일한 네트워크에 있는 다른 권한 있는 사용자가이 정보에 액세스할 수 있도록 합니다.

Active Directory는 네트워크의 개체에 대 한 정보를 저장 하 고 관리자와 사용자가이 정보를 쉽게 찾아서 사용할 수 있도록 합니다. Active Directory는 구조화 된 데이터 저장소를 디렉터리 정보의 논리적 계층 구조에 대 한 기준으로 사용 합니다.

이 데이터 저장소 (디렉터리 라고도 함)에는 Active Directory 개체에 대 한 정보가 포함 되어 있습니다. 일반적으로 이러한 개체에는 서버, 볼륨, 프린터, 네트워크 사용자 및 컴퓨터 계정 등의 공유 리소스가 포함 됩니다. Active Directory 데이터 저장소에 대 한 자세한 내용은 [디렉터리 데이터 저장소](https://technet.microsoft.com/library/cc736627(v=ws.10).aspx)를 참조 하세요.

보안은 디렉터리의 개체에 대 한 로그온 인증 및 액세스 제어를 통해 Active Directory와 통합 됩니다. 관리자는 단일 네트워크 로그온을 통해 네트워크에서 디렉터리 데이터 및 조직을 관리할 수 있으며, 권한 있는 네트워크 사용자는 네트워크의 모든 위치에서 리소스에 액세스할 수 있습니다. 정책 기반 관리를 사용하면 가장 복잡한 네트워크조차 쉽게 관리할 수 있습니다. Active Directory 보안에 대 한 자세한 내용은 [보안 개요](../../plan/security-best-practices/best-practices-for-securing-active-directory.md)를 참조 하세요.

Active Directory에도 다음이 포함 됩니다.
* 디렉터리에 포함 된 개체 및 특성의 클래스, 이러한 개체의 인스턴스에 대 한 제약 조건 및 제한 및 이름의 형식을 정의 하는 규칙 집합 ( **스키마**)입니다. 스키마에 대 한 자세한 내용은 스키마를 참조 하십시오.


* 디렉터리의 모든 개체에 대 한 정보를 포함 하는 **글로벌 카탈로그** 입니다. 이를 통해 사용자와 관리자는 디렉터리의 어떤 도메인에 실제로 데이터가 포함 되는지에 관계 없이 디렉터리 정보를 찾을 수 있습니다. 글로벌 카탈로그에 대 한 자세한 내용은 글로벌 카탈로그의 역할을 참조 하세요.


* 네트워크 사용자 또는 응용 프로그램에서 개체와 해당 속성을 게시 하 고 찾을 수 있도록 하는 **쿼리 및 인덱스 메커니즘**입니다. 디렉터리를 쿼리 하는 방법에 대 한 자세한 내용은 디렉터리 정보 찾기를 참조 하세요.


* 네트워크를 통해 디렉터리 데이터를 배포 하는 **복제 서비스** 입니다. 도메인의 모든 도메인 컨트롤러는 복제에 참여 하 고 해당 도메인에 대 한 모든 디렉터리 정보의 전체 복사본을 포함 합니다. 디렉터리 데이터에 대한 변경 내용은 모두 도메인의 모든 도메인 컨트롤러에 복제됩니다. Active Directory 복제에 대 한 자세한 내용은 복제 개요를 참조 하세요.

## <a name="understanding-active-directory"></a>Active Directory 이해
 이 섹션에서는 핵심 Active Directory 개념에 대 한 링크를 제공 합니다.
 
* [Active Directory 구조 및 저장소 기술](https://technet.microsoft.com/library/cc759186(v=ws.10).aspx)
* [도메인 컨트롤러 역할](https://technet.microsoft.com/library/cc786438(v=ws.10).aspx) 
* [Active Directory 스키마](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771796(v=ws.10))
* [트러스트 이해](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771568(v=ws.10)) 
* [Active Directory 복제 기술](https://technet.microsoft.com/library/cc786438(v=ws.10).aspx) 
* [Active Directory 검색 및 게시 기술](https://technet.microsoft.com/library/cc775686(v=ws.10).aspx) 
* [DNS 및 그룹 정책 상호 운용](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd197486(v=ws.10))
* [스키마 이해](https://technet.microsoft.com/library/cc759402(v=ws.10).aspx) 

Active Directory 개념에 대 한 자세한 목록은 [Active Directory 이해](https://technet.microsoft.com/library/cc781408(v=ws.10).aspx)를 참조 하세요. 


