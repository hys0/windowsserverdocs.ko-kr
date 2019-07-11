---
ms.assetid: f052dfcd-dace-4485-8d0a-cc7df5cf3751
title: Active Directory 도메인 서비스 개요
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: ed8a22881cd20633e6fcd61b146f3b0aad7a757b
ms.sourcegitcommit: be243a92f09048ca80f85d71555ea6ee3751d712
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67792276"
---
# <a name="active-directory-domain-services-overview"></a>Active Directory 도메인 서비스 개요

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012


디렉터리에는 네트워크의 개체에 대 한 정보를 저장 하는 계층 구조입니다. Active Directory Domain Services (AD DS)와 같은 디렉터리 서비스, 디렉터리 데이터를 저장 하 고 네트워크 사용자 및 관리자에 게이 데이터를 사용할 수 있도록 하기 위한 메서드를 제공 합니다. 예를 들어 AD DS 이름, 암호, 전화 번호 및 등과 같은 사용자 계정에 대 한 정보를 저장 하 고이 정보에 액세스 하려면 동일한 네트워크에 다른 권한 있는 사용자를 사용 하도록 설정 합니다.

Active Directory 네트워크에서 개체에 대 한 정보를 저장 하 고이 정보를 더 쉽게 찾아서 사용 하는 관리자와 사용자. Active Directory 디렉터리 정보의 논리, 계층적 조직에 대 한 기준으로 구조화 된 데이터 저장소를 사용합니다.

Active Directory 개체에 대 한 정보를 포함 하는이 데이터 저장소에 디렉터리 라고도 합니다. 일반적으로 이러한 개체는 서버, 볼륨, 프린터 및 네트워크 사용자 및 컴퓨터 계정을 같은 공유 리소스를 포함 합니다. Active Directory 데이터 저장소에 대 한 자세한 내용은 참조 하세요. [디렉터리 데이터 저장소](https://technet.microsoft.com/library/cc736627(v=ws.10).aspx)합니다.

보안은 로그온 인증과 액세스 제어 디렉터리에 있는 개체를 통해 Active Directory와 통합 됩니다. 단일 네트워크 로그온을 사용 하 여 디렉터리 데이터 및 해당 네트워크 전체에 걸쳐 조직 관리자가 관리할 수 있습니다 및 인증 된 네트워크 사용자 네트워크에 있는 모든 리소스에 액세스할 수 있습니다. 정책 기반 관리를 사용하면 가장 복잡한 네트워크조차 쉽게 관리할 수 있습니다. Active Directory 보안에 대 한 자세한 내용은 참조 하세요. [보안 개요](../../plan/security-best-practices/best-practices-for-securing-active-directory.md)합니다.

Active Directory에 포함 됩니다.
* 규칙 집합 **스키마**개체의 클래스를 정의 하 고 특성에 포함 된 디렉터리, 제약 조건 및 이러한 개체의 인스턴스 및 해당 이름의 형식에 대 한 제한입니다. 스키마에 대 한 자세한 내용은 스키마를 참조 하세요.


* A **글로벌 카탈로그** 디렉터리의 모든 개체에 대 한 정보를 포함 하는 합니다. 이렇게 하면 사용자와 관리자 정보를 찾는 디렉터리에 관계 없이 디렉터리에 있는 도메인의 실제 데이터를 포함 합니다. 글로벌 카탈로그에 대 한 자세한 내용은 글로벌 카탈로그의 역할을 참조 하세요.


* A **쿼리와 인덱스 메커니즘**개체 및 해당 속성 게시 및 네트워크 사용자 또는 응용 프로그램에서 찾을 수 있도록 합니다. 디렉터리를 쿼리 하는 방법에 대 한 자세한 내용은 디렉터리 정보 찾기을 참조 하세요.


* A **복제 서비스** 네트워크를 통해 디렉터리 데이터를 배포 하는 합니다. 도메인의 모든 도메인 컨트롤러 복제에 참여 하 고 해당 도메인에 대 한 모든 디렉터리 정보의 전체 복사본을 포함 합니다. 디렉터리 데이터에 대한 변경 내용은 모두 도메인의 모든 도메인 컨트롤러에 복제됩니다. Active Directory 복제에 대 한 자세한 내용은 복제 개요를 참조 하세요.

## <a name="understanding-active-directory"></a>Active Directory 이해
 이 섹션에서는 핵심 Active Directory 개념에 대 한 링크를 제공 합니다.
 
* [Active Directory 구조와 저장소 기술](https://technet.microsoft.com/library/cc759186(v=ws.10).aspx)
* [도메인 컨트롤러 역할](https://technet.microsoft.com/library/cc786438(v=ws.10).aspx) 
* [Active Directory 스키마](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771796(v=ws.10))
* [트러스트 이해](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771568(v=ws.10)) 
* [Active Directory 복제 토폴로지](https://technet.microsoft.com/library/cc786438(v=ws.10).aspx) 
* [Active Directory 검색 및 게시 기술](https://technet.microsoft.com/library/cc775686(v=ws.10).aspx) 
* [그룹 정책 및 DNS를 사용 하 여 상호 운용](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd197486(v=ws.10))
* [스키마 이해](https://technet.microsoft.com/library/cc759402(v=ws.10).aspx) 

Active Directory 개념의 자세한 목록은 참조 하세요 [이해 Active Directory](https://technet.microsoft.com/library/cc781408(v=ws.10).aspx)합니다. 


