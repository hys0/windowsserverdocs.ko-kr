---
title: ARM 및 Azure Marketplace를 통해 원활하게 RDS 배포
description: ARM 템플릿 및 Azure Marketplace를 사용 하 여 Azure에서 소규모 RDS 배포를 만드는 방법에 알아봅니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5f72ceb6-6f90-48f6-bfc3-bdad63984ce7
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 02/10/2017
ms.openlocfilehash: e4de3d4ac14a0dbc5500fd7ab8bd8f1568f3da53
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59823084"
---
# <a name="seamlessly-deploy-rds-with-arm-and-azure-marketplace"></a>ARM 및 Azure Marketplace를 통해 원활하게 RDS 배포

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2

원격 데스크톱 서비스 (RDS)는 비용 효율적으로 Windows 데스크톱 및 응용 프로그램을 호스트 하는 선택한 플랫폼입니다. 사용할 수는 [Azure Marketplace 제품은](#basic-rds-through-the-azure-marketplace) 또는 [빠른 시작 템플릿](#Customized-RDS-using-Quickstart-templates) Azure IaaS 배포에는 RDS를 신속 하 게 만들려고 합니다. Azure marketplace는 쉽고 간단한 메커니즘을 테스트 및 개념의 하므로 사용자에 대 한 테스트 도메인을 만듭니다. 빠른 시작 템플릿을 사용 하면 기존 도메인에 있도록 프로덕션 환경을 구축할 수 있는 유용한 도구를 사용 하 여 다른 한편으로 합니다. 한 번 설정 하면 연결할 수 있습니다 게시 된 데스크톱 및 응용 프로그램에 다양 한 플랫폼 및 장치에서 Windows, Mac, iOS 및 Android 용 Microsoft 원격 데스크톱 앱을 사용 하 여.

## <a name="basic-rds-through-the-azure-marketplace"></a>Azure Marketplace 통해 기본 RDS

Azure Marketplace를 통해 배포를 만들기 시작 하는 가장 빠른 방법은 및 실행 합니다. 환경의 모양은 모두 완료 되 면 합니다 [기본 RDS 아키텍처](desktop-hosting-logical-architecture.md#basic-deployment)합니다. 제품 해야-몇 가지 정보를 제공 하기만 하면 되는 모든 RDS 구성 요소를 만듭니다. 

Marketplace 제품을 배포 하는 경우 다음 정보를 제공 해야 합니다.
- 관리자 사용자 이름 및 암호를 제공 합니다. 배포를 관리 하는 새 사용자입니다.
- DNS 이름과 AD 도메인 이름입니다. 이들은 만들어진 새 리소스입니다. 의미 있는 이름이 되는지 확인 합니다.
- VM 크기입니다. RDSH 끝점에 대해 사용 하도록 Vm의 크기를 선택 하 고 얻게 됩니다. 비용 및 워크 로드에 대 한 Vm을 활용할 수 있도록 초기 배포 후 크기를 수동으로 변경할 수 있습니다.

Azure Marketplace에서 사용량이 적은 RDS 배포를 만들려면 다음이 단계를 사용 합니다. 

1. Azure Marketplace RDS 배포를 시작 합니다.
   1. [Azure 포털](https://portal.azure.com)할 수 있습니다.
   2. 클릭 **새로 만들기** 배포를 추가 합니다.
   3. 검색 필드에 "RDS"를 입력 하 고 Enter 키를 누릅니다.
   4. 클릭 **원격 데스크톱 서비스 (RDS)-기본-개발/테스트**를 클릭 하 고 **만들기**합니다.
   5. 포털을 만들고 rds. 배포의 단계에 따라 위에 나열 된 정보와 같은 키 구성 세부 정보를 추가 합니다. 
2. 배포에 연결 합니다. 배포가 완료 되 면 완료 하 고 배포에 연결 하는 마지막 단계에 대 한 출력 섹션을 확인 합니다.
   1. 다운로드 및 실행 [이 PowerShell 스크립트](https://gallery.technet.microsoft.com/Azure-Resource-Manager-4ea7e328) RDS 배포에 연결 하는 데 필요한 모든 인증서를 설치 하기 위해 테스트 장치에 있습니다. 
   
      이 단계는 테스트 단계 동안만 필요 합니다. 프로덕션에 Azure에서 RDS를 배포할 때 구매 및 웹 서버에서 공개적으로 신뢰할 수 있는 SSL 인증서를 사용 하 여 같은 모범 사례를 수행 해야 합니다.

   2. 메시지가 표시 되 면 Azure 계정에 로그인 합니다. Azure 구독, 리소스 그룹 및이 새 배포를 위해 생성 하는 공용 IP 주소를 선택 합니다.
   3. 스크립트가 완료 되 면 기본 브라우저에서 RD 웹 페이지를 시작 합니다. 배포 중에 제공한 DNS 주소를 페이지의 URL을 비교 하 여 RD 웹 페이지를 다시 확인 수 있습니다. 
   
      배포 게시 기본 바탕 화면을 참조 하는 동안 만든 관리자 자격 증명으로 로그인 합니다. 또한 데스크톱 및 응용 프로그램을 테스트 하려면 RD 웹 사이트 사용자를 보낼 수 있습니다.

      > [!TIP]
      > 도메인 이름 또는 관리 사용자를 잊으셨습니까? 이동할 수 있습니다는 포털에서 새 리소스 그룹을 다시 클릭 **배포**를 입력 한 매개 변수를 확인 합니다.

RDS 배포를 설정 했으므로 있습니다 [사용자 추가 및 관리](rds-user-management.md)합니다.

## <a name="customized-rds-using-quickstart-templates"></a>빠른 시작 템플릿을 사용 하 여 사용자 지정된 RDS

Azure에서 RDS를 배포 하려면 Azure Resource Manager 템플릿을 사용할 수 있습니다. 기본 RDS 배포를 기존 구성 요소를 (예: AD)를 사용 하려는 경우 특히 유용 합니다. 제품 Marketplace와 달리 가상 네트워크에 기존 AD를 사용 하는 등의 추가 사용자 지정 RDSH Vm 및 RDS 구성 요소에 대 한 고가용성에는 계층에 대 한 사용자 지정 운영 체제 이미지를 사용 하 여 만들 수 있습니다. 고가용성에 각 구성 요소를 추가한 후 환경의 모양은 합니다 [항상 사용 가능한 RDS 아키텍처](desktop-hosting-logical-architecture.md#highly-available-deployment)합니다.

RDS Azure 템플릿을 사용 하 여 사용량이 적은 RDS 배포를 만들려면 다음이 단계를 사용 합니다. 

1. Azure 빠른 시작 템플릿을 선택 합니다.
   1. 로 이동 합니다 [RDS Azure 빠른 시작 템플릿](https://aka.ms/rdautomation) 사이트입니다.
   2. 수행 하려는 일치 하는 템플릿을 선택 합니다. 해당 특정 템플릿에 대 한 모든 필수 구성 요소를 충족 하는지 확인 합니다. (예를 들어, Vm에 대 한 사용자 지정 이미지를 사용 하도록 하려는 경우 해야 이미이 Azure storage 계정에 해당 이미지를 업로드 합니다.)
   3. 클릭 **Azure에 배포**합니다.
   4. Azure portal에서 몇 가지 세부 정보 (예: 관리자 사용자 이름, AD 도메인 이름)를 제공 해야 합니다. 이 선택 하는 템플릿에 따라 다릅니다.
   5. 클릭 **구매**합니다.
2. 배포에 연결 합니다. 
   1. 다운로드 및 실행 [이 PowerShell 스크립트](https://gallery.technet.microsoft.com/Azure-Resource-Manager-4ea7e328) RDS 배포에 연결 하는 데 필요한 모든 인증서를 설치 하기 위해 테스트 장치에 있습니다. 
   
      이 단계는 테스트 단계 동안만 필요 합니다. 프로덕션에 Azure에서 RDS를 배포할 때 구매 및 웹 서버에서 공개적으로 신뢰할 수 있는 SSL 인증서를 사용 하 여 같은 모범 사례를 수행 해야 합니다.

   2. 메시지가 표시 되 면 Azure 계정에 로그인 합니다. Azure 구독, 리소스 그룹 및이 새 배포를 위해 생성 하는 공용 IP 주소를 선택 합니다.
   3. 스크립트가 완료 되 면 기본 브라우저에서 RD 웹 페이지를 시작 합니다. 배포 중에 제공한 DNS 주소를 페이지의 URL을 비교 하 여 RD 웹 페이지를 다시 확인 수 있습니다. 
   
      배포 게시 기본 바탕 화면을 참조 하는 동안 만든 관리자 자격 증명으로 로그인 합니다. 또한 데스크톱 및 응용 프로그램을 테스트 하려면 RD 웹 사이트 사용자를 보낼 수 있습니다.

      > [!TIP]
      > 도메인 이름 또는 관리 사용자를 잊으셨습니까? 이동할 수 있습니다는 포털에서 새 리소스 그룹을 다시 클릭 **배포**를 입력 한 매개 변수를 확인 합니다.

RDS 배포를 설정 했으므로 있습니다 [사용자 추가 및 관리](rds-user-management.md)합니다.
