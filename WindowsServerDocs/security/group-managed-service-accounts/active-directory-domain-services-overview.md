---
title: "Active Directory Domain Services 개요"
description: "Windows Server 보안"
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.service: na
ms.suite: na
ms.technology: security-auditing
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6cfe9479-5d17-41d5-939a-891e5233fdca
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 3d0e849edbff3a481ffd28f83d7f14089030920d
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/17/2017
---
# <a name="active-directory-domain-services-overview"></a>Active Directory Domain Services 개요

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016
  
디렉터리는 소식 개체에 대 한 정보를 네트워크에 저장 합니다. 디렉터리 서비스를 Active Directory Domain Services (AD DS) 등 디렉터리 데이터를 저장 하 고 네트워크 사용자에 게와 관리자에 게이 데이터를 사용할 수 있게 하는 방법을 제공 합니다. 예를 들어, AD DS 이름, 암호, 전화 번호 등의 사용자 계정에 대 한 정보를 저장 및 사용 하면 다른 같은 네트워크에 사용자가이 정보에 액세스 합니다.  
  
Active Directory 개체에 대 한 정보를 네트워크에 저장 하 고이 정보를 더 쉽게 찾아 사용할 관리자와 사용자가 있습니다. Active Directory 기준으로 디렉터리 정보의 논리, 계층 조직에 대 한 구조적된 데이터 저장소를 사용 합니다.  
  
이 데이터 저장소 디렉터리 라고도 Active Directory 개체로 대 한 정보를 포함 합니다. 이러한 물체는 일반적으로 공유 리소스와 같은 서버, 볼륨, 프린터 및 네트워크 컴퓨터와 사용자 계정 포함 됩니다. Active Directory 데이터 저장소에 대 한 자세한 내용은 참조 [디렉터리 데이터 저장소](https://technet.microsoft.com/library/cc736627(v=ws.10).aspx)합니다.  
  
보안 Active Directory 개체 디렉터리에 액세스 제어 로그온 인증을 통해 통합 되어 있습니다. 단일 네트워크 로그온 디렉터리 데이터와 해당 네트워크를 통해 조직 관리자가 관리할 수 있으며 네트워크 권한이 있는 사용자가 네트워크에서 아무 곳 이나 리소스에 액세스할 수 있습니다. 정책 기반 관리 가장 복잡 한 네트워크 관리를 줄일 수 있습니다. 보안 개요 Active Directory 보안에 대 한 자세한 내용은 참조 합니다.  
  
Active Directory 포함 되어 있습니다.  
* 여러 가지 규칙 **스키마**, 개체 클래스 정의 하 및에 포함 된 특성 디렉터리, 제약 및 이러한 물체 인스턴스 및의 이름 형식에 대 한 제한을 합니다. 스키마 스키마에 대 한 자세한 내용은 참조 합니다.  
  
  
* A **드** 모든 개체 디렉터리에 대 한 정보가 포함 된 합니다. 이렇게 하면 사용자와 정보를 찾는 디렉터리에 관계 없이 디렉터리에는 도메인의 실제로 데이터가 관리자입니다. 드에 대 한 자세한 내용은 참조 드의 역할을 합니다.  
  
  
* A **쿼리 및 색인 메커니즘**개체 및 속성 게시 있고 네트워크 사용자에 게 또는 응용 프로그램에서 찾을 수 있도록 합니다. 디렉터리를 쿼리에 대 한 자세한 내용은 디렉터리 정보 찾기 참조 합니다.  
  
  
* A **복제 서비스** 디렉터리 데이터를 배포 하는 네트워크를 통해 합니다. 도메인에 있는 모든 도메인 컨트롤러 복제에 참여 하 고 자녀가 도메인에 대 한 모든 디렉터리 정보의 전체 복사본을 포함 합니다. 도메인에 있는 모든 도메인 컨트롤러에 디렉터리 데이터를 변경한 복제 됩니다. 복제 개요 복제 Active Directory에 대 한 자세한 내용은 참조 합니다.  
  
## <a name="understanding-active-directory"></a>이해 Active Directory  
 이 섹션의 핵심 Active Directory 개념에 대 한 링크를 제공합니다.  
   
* [저장소 기술과 active Directory 구조](https://technet.microsoft.com/library/cc759186(v=ws.10).aspx)  
* [도메인 컨트롤러 역할](https://technet.microsoft.com/library/cc786438(v=ws.10).aspx)   
* Active Directory 스키마   
* [이해 신뢰](https://technet.microsoft.com/library/cc771294(v=ws.10).aspx)   
* [Active Directory 복제 기술](https://technet.microsoft.com/library/cc786438(v=ws.10).aspx)   
* [게시 기술과 active Directory 검색](https://technet.microsoft.com/library/cc775686(v=ws.10).aspx)   
* 그룹 정책 및 DNS와 상호 작용   
* [이해 스키마](https://technet.microsoft.com/library/cc759402(v=ws.10).aspx)   
  
자세한 목록은 Active Directory 개념을 참조 하세요. [이해 Active Directory](https://technet.microsoft.com/library/cc781408(v=ws.10).aspx)합니다.   

