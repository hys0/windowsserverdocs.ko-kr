---
title: Windows Server에 대한 핵심 네트워크 지침
description: 이 항목에서는 계획 하 고는 완벽 하 게 작동 하는 네트워크와 Windows Server 2016 새 포리스트의 새 Active Directory 도메인에 필요한 핵심 구성 요소를 배포할 수 있는 핵심 네트워크 가이드의 개요
manager: brianlic
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.date: ''
ms.assetid: 9b3ef3eb-4246-4e0e-8bf1-53224ca5f2f9
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 52f8b9e1446b5b3f3b1e7060cc737204771d1eae
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71356070"
---
# <a name="core-network-guidance-for-windows-server"></a>Windows Server에 대한 핵심 네트워크 지침

>적용 대상: Windows Server, Windows Server 2016

이 항목에서는 Windows Server @ no__t-0 2016에 대 한 핵심 네트워크 지침의 개요를 제공 하며 다음 섹션을 포함 합니다.  
  
-   [Windows Server Core 네트워크 소개](#bkmk_intro)  
  
-   [Windows Server에 대 한 핵심 네트워크 가이드](#bkmk_core)  
  
## <a name="bkmk_intro"></a>Windows Server Core 네트워크 소개

핵심 네트워크는 조직의 IT(정보 기술) 요구 사항에 맞는 기반 서비스를 제공하는 네트워크 하드웨어, 장치 및 소프트웨어의 모음입니다.

Windows Server 핵심 네트워크는 다음을 포함한 다양한 이점을 제공합니다.

- 컴퓨터와 다른 TCP/IP 호환 장치 사이의 네트워크 연결을 위한 핵심 프로토콜. TCP/IP는 컴퓨터를 연결하고 네트워크를 구성하기 위한 표준 프로토콜 집합입니다. TCP/IP는 Microsoft와 함께 제공 되는 네트워크 프로토콜 소프트웨어&reg; Windows&reg; 프로토콜을 구현 하 고 TCP/IP를 지 원하는 운영 체제 제품군입니다.

- DHCP(Dynamic Host Configuration Protocol) 서버 자동 IP 주소. 네트워크에 있는 모든 컴퓨터의 IP 주소를 수동으로 구성하는 작업은 DHCP 서버에서 컴퓨터 및 기타 장치에 IP 주소를 동적으로 임대하는 것보다 시간이 많이 걸리고 유연성도 낮습니다.

- DNS(Domain Name System) 이름 확인 서비스. DNS를 통해 사용자, 컴퓨터, 응용 프로그램 및 서비스는 컴퓨터나 장치의 정규화된 도메인 이름을 사용하여 네트워크에 있는 컴퓨터와 장치의 IP 주소를 찾을 수 있습니다.

- 동일한 클래스와 특성 정의(스키마), 사이트와 복제 정보(구성) 및 포리스트 전체 검색 기능(글로벌 카탈로그)을 공유하는 하나 이상의 Active Directory 도메인인 포리스트

- 새 포리스트에서 처음으로 만든 도메인인 포리스트 루트 도메인. 포리스트 전체 관리 그룹인 Enterprise Admins 및 Schema Admins 그룹은 포리스트 루트 도메인에 위치합니다. 또한 포리스트 루트 도메인은 다른 도메인과 마찬가지로 AD DS(Active Directory 도메인 서비스)에서 관리자가 정의한 컴퓨터, 사용자 및 그룹 개체의 모음입니다. 이러한 개체는 공통의 디렉터리 데이터베이스 및 보안 정책을 공유합니다. 또한 조직의 규모가 커짐에 따라 도메인을 추가하는 경우 다른 도메인과의 보안 관계도 공유할 수 있습니다. 또한 디렉터리 서비스는 디렉터리 데이터를 저장하고, 권한 있는 컴퓨터, 응용 프로그램 및 사용자는 이 서비스를 통해 데이터에 액세스할 수 있습니다.

- 사용자 및 컴퓨터 계정 데이터베이스. 디렉터리 서비스는 네트워크에 연결할 수 있도록 권한이 부여된 사람 및 컴퓨터를 위한 사용자 및 컴퓨터 계정을 만들고 응용 프로그램, 데이터베이스, 공유된 파일과 폴더, 프린터 등의 네트워크 리소스에 액세스할 수 있는 중앙 집중식 사용자 계정 데이터베이스를 제공합니다.

또한 핵심 네트워크를 사용하면 조직의 규모가 커지고 IT 요구 사항이 변함에 따라 네트워크를 조정할 수 있습니다. 예를 들어 핵심 네트워크와 도메인, IP 서브넷, 원격 액세스 서비스, 무선 서비스 및 기타 기능 및 Windows Server 2016에서 제공 하는 서버 역할을 추가할 수 있습니다.

## <a name="bkmk_core"></a>Windows Server에 대 한 핵심 네트워크 가이드

계획 하 고는 완벽 하 게 작동 하는 네트워크와 새로운 Active Directory에 필요한 핵심 구성 요소를 배포 하는 방법에 지침을 제공 하는 Windows Server 2016 핵심 네트워크 가이드&reg; 새 포리스트에 있는 도메인입니다. 이 가이드를 사용하여 다음 Windows Server 구성 요소로 구성된 컴퓨터를 배포할 수 있습니다.

- AD DS(Active Directory Domain Services) 서버 역할

- DNS(Domain Name System) 서버 역할

- DHCP(Dynamic Host Configuration Protocol) 서버 역할

- 네트워크 정책 및 액세스 서비스 서버 역할의 NPS(네트워크 정책 서버) 역할 서비스

- 웹 서버(IIS) 서버 역할

- 개별 서버에 대한 TCP/IP(전송 컨트롤 프로토콜/인터넷 프로토콜) 버전 4 연결

이 가이드는 다음 위치에서 사용할 수 있습니다.

- [핵심 네트워크 가이드](../core-network-guide/Core-Network-Guide.md) Windows Server 2016 기술 라이브러리에서입니다.
  


