---
title: Windows server의 핵심 네트워크 가이드
description: 이 항목에서는 계획 하 고 배포 완벽 하 게 작동 네트워크와 Windows Server 2016와 새 숲 속의 새로운 Active Directory 도메인에 필요한 핵심 구성 요소 수 있는 Core 네트워크 가이드 소개
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.date: ''
ms.assetid: 9b3ef3eb-4246-4e0e-8bf1-53224ca5f2f9
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 63e4cf8c5bf56ef5131e835163a5fcb5dfd98b55
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="core-network-guide-for-windows-server"></a>Windows server의 핵심 네트워크 가이드

>적용 대상: Windows Server, Windows Server 2016

이 항목에서는 Windows Server에 대 한 핵심 네트워크 가이드 간략하게&reg; 2016을 다음 섹션에 포함 되어 있습니다.  
  
-   [Windows Server의 핵심 네트워크 소개](#bkmk_intro)  
  
-   [Windows server의 핵심 네트워크 가이드](#bkmk_core)  
  
## <a name="bkmk_intro"></a>Windows Server의 핵심 네트워크 소개

핵심 네트워크의 네트워크 하드웨어, 디바이스, 컬렉션 이며 조직의 IT 정보 기술 ()에 대 한 기본 서비스를 제공 하는 소프트웨어 필요 합니다.

Windows Server의 핵심 네트워크는 다음을 포함 한 여러 가지 이점을 제공 합니다.

- 컴퓨터와 다른 TCP/IP (TCP/IP) 호환 디바이스 간에 네트워크 연결에 대 한 핵심 프로토콜 합니다. TCP/IP는 컴퓨터를 연결 하 고 네트워크 빌드에 대 한 프로토콜 표준 제품군입니다. TCP/IP는 Microsoft와 함께 제공 되는 네트워크 프로토콜 소프트웨어&reg; Windows&reg; TCP/IP 지원 및 구현 하는 운영 체제 프로토콜 제품군입니다.

- DHCP(Dynamic Host Configuration Protocol) (DHCP) 서버 자동 IP 주소 지정 합니다. 네트워크의 모든 컴퓨터의 IP 주소를 수동으로 구성 시간이 및 덜 동적으로 IP 주소 임대 DHCP 서버에서 된 컴퓨터 및 기타 장치를 제공 하는 보다 효율적입니다.

- 시스템 DNS (도메인 이름) 해상도 서비스의 이름을 지정 합니다. DNS는 사용자가, 컴퓨터, 응용 프로그램 및 서비스 네트워크에서 완벽 하 게 된 도메인의 이름을 컴퓨터나 디바이스를 사용 하 여 컴퓨터와 디바이스의 IP 주소를 찾을 수 있습니다.

- 숲-동일한 클래스 및 특성 정의 (스키마), (구성) 하는 사이트 및 복제 정보 및 숲 검색 기능 (드)를 공유 하는 하나 이상의 Active Directory 도메인은 합니다.

- 새 숲 속의 첫 번째 도메인 숲 루트 도메인에 만들었습니다. 숲 속 전체 관리 그룹 인는 엔터프라이즈 관리자 및 스키마 관리자 그룹 숲 루트 도메인에 있습니다. 또한 이렇게, 다른 도메인와 마찬가지로 모음입니다 컴퓨터, 사용자 및 그룹 개체 Active Directory Domain Services (AD DS)에서 관리자 권한으로 정의 됩니다. 이러한 물체 일반적인 디렉터리 데이터베이스 및 보안 정책이 공유합니다. 또한 증가 하는 조직 도메인을 추가 하는 경우 보안 관계 다른 도메인 공유할 수 있습니다. 디렉터리 서비스는 또한 디렉터리 데이터를 저장 하 고 권한이 부여 된 컴퓨터, 응용 프로그램 및 사용자 데이터에 액세스할 수 있게 합니다.

- 컴퓨터와 사용자 계정 데이터베이스 합니다. 디렉터리 서비스는 사람 및 리소스 응용 프로그램, 데이터베이스, 공유 파일 및 폴더, 프린터 등 네트워크와 액세스 네트워크에 연결 하려면 실시 권 자는 컴퓨터에 대 한 사용자와 컴퓨터 계정을 만들 수 있게 해 주는 중앙된 사용자 계정 데이터베이스를 제공 합니다.

핵심 네트워크 조직 성장 하 고 IT 요구 사항을 변경 때이 네트워크에 맞게 수도 있습니다. 예를 들어, core 네트워크 도메인, IP 서브넷, 원격 액세스 서비스, 무선 서비스 및 기타 기능 및 Windows Server 2016에서 제공 하는 서버 역할을 추가할 수 있습니다.

## <a name="bkmk_core"></a>Windows server의 핵심 네트워크 가이드

Windows Server 2016 Core 네트워크 가이드 계획 하 고 새 Active Directory를 완벽 하 게 작동 네트워크에 필요한 핵심 구성 요소를 배포 하는 방법에 대해 설명&reg; 새 숲 속의 도메인. 이 가이드를 사용 하 여, 다음과 같은 Windows 서버 구성 요소를 구성 된 컴퓨터 배포할 수 있습니다.

- Active Directory Domain Services (AD DS) 서버 역할

- 시스템 DNS (도메인 이름) 서버 역할

- DHCP(Dynamic Host Configuration Protocol) (DHCP) 서버 역할

- 액세스 서비스 및 네트워크 정책 서버 역할의 네트워크 NPS 정책 서버 () 역할 서비스

- 웹 IIS () 서버 역할

- TCP/IP 버전 4 (TCP/IP) 개별 서버에 연결

이 가이드는 다음 위치에서 사용할 수 있습니다.

- [네트워크 가이드 핵심](../core-network-guide/Core-Network-Guide.md) Windows Server 2016 찾아볼 수 있습니다.
  


