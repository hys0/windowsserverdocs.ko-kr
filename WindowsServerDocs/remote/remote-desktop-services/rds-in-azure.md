---
title: ARM 및 Azure Marketplace를 통해 원활하게 RDS 배포
description: ARM 템플릿 및 Azure Marketplace를 사용하여 Azure에서 소규모 RDS 배포를 만드는 방법을 알아봅니다.
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 9ada41e929c5e67cfcb1dcc5e7b4bc761c762d99
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71387451"
---
# <a name="seamlessly-deploy-rds-with-arm-and-azure-marketplace"></a>ARM 및 Azure Marketplace를 통해 원활하게 RDS 배포

>적용 대상: Windows Server(반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2

RDS(원격 데스크톱 서비스)는 Windows 데스크톱 및 애플리케이션을 비용 효과적으로 호스팅하기 위해 선택하는 플랫폼입니다. [Azure Marketplace 제품](#basic-rds-through-the-azure-marketplace) 또는 [빠른 시작 템플릿](#customized-rds-using-quickstart-templates)을 사용하여 Azure IaaS 배포에 대한 RDS를 빠르게 만들 수 있습니다. Azure Marketplace는 자동으로 테스트 도메인을 만들므로 쉽고 간단한 테스트 및 개념 증명 메커니즘입니다. 반면, 빠른 시작 템플릿은 기존 도메인을 사용할 수 있게 해주므로 프로덕션 환경을 빌드하는 데 유용한 도구입니다. 설정이 완료되면 Windows, Mac, iOS 및 Android용 Microsoft 원격 데스크톱 앱을 사용하여 다양한 플랫폼과 디바이스에서 게시된 데스크톱 및 애플리케이션에 연결할 수 있습니다.

## <a name="basic-rds-through-the-azure-marketplace"></a>Azure Marketplace를 통한 기본 RDS

가장 빠르게 실행하는 방법은 Azure Marketplace를 통해 배포를 만드는 것입니다. 모든 것이 완료되면 환경은 [기본 RDS 아키텍처](desktop-hosting-logical-architecture.md#basic-deployment)와 비슷하게 됩니다. 이 제품이 필요한 모든 RDS 구성 요소를 만들므로 사용자는 몇 가지 정보만 제공하면 됩니다. 

Marketplace 제품을 배포할 때는 다음 정보를 제공해야 합니다.
- 관리자 사용자 이름 및 암호. 배포를 관리할 새 사용자입니다.
- DNS 이름과 AD 도메인 이름. 생성된 새 리소스입니다. 의미 있는 이름이어야 합니다.
- VM 크기. RDSH 엔드포인트에 사용할 VM의 크기를 선택해야 합니다. 또한 초기 배포 후 크기를 수동으로 변경하여 워크로드 및 비용에 맞게 VM을 최적화할 수 있습니다.

Azure Marketplace에서 사용 공간이 적은 RDS 배포를 만들려면 다음 단계를 수행하세요. 

1. Azure Marketplace RDS 배포를 시작합니다.
   1. 로그인은 [Azure 포털](https://portal.azure.com)합니다.
   2. **새로 만들기**를 클릭하여 배포를 추가합니다.
   3. 검색 필드에 ‘RDS’를 입력하고 Enter 키를 누릅니다.
   4. **RDS(원격 데스크톱 서비스) - 기본 - 개발/테스트**를 클릭한 후 **만들기**를 클릭합니다.
   5. 포털의 단계를 따라 RDS를 만들고 배포합니다. 위에 나열된 정보와 같은 키 구성 세부 정보를 추가합니다. 
2. 배포에 연결합니다. 배포가 완료되면 출력 섹션에서 완료를 위한 마지막 단계를 확인하고 배포에 연결합니다.
   1. RDS 배포에 연결하는 데 필요한 인증서를 설치하려면 테스트 디바이스에서 [이 PowerShell 스크립트](https://gallery.technet.microsoft.com/Azure-Resource-Manager-4ea7e328)를 다운로드하고 실행합니다. 
   
      이 단계는 테스트 단계 중에만 필요합니다. 프로덕션 단계의 Azure에서 RDS를 배포하려면 웹 서버에서 공개적으로 신뢰하는 SSL 인증서 구매 및 사용과 같은 모범 사례를 따라야 합니다.

   2. 메시지가 표시되면 Azure 계정에 로그인합니다. Azure 구독, 리소스 그룹 및 이 새 배포를 위해 생성된 공개 IP 주소를 선택합니다.
   3. 스크립트가 완료되면 기본 브라우저에 RD 웹 페이지가 열립니다. 배포 중에 제공한 DNS 주소와 페이지의 URL을 비교하여 RD 웹 페이지를 다시 확인할 수 있습니다. 
   
      자동으로 게시된 기본 데스크톱을 보려면 배포 중에 만든 관리자 자격 증명으로 로그인합니다. 또한 사용자에게 데스크톱 및 애플리케이션을 테스트할 수 있는 RD 웹 사이트를 보낼 수 있습니다.

      > [!TIP]
      > 도메인 이름 또는 관리자 사용자를 잊으셨습니까? 포털의 새 리소스 그룹으로 다시 이동하고 **배포**를 클릭하면 입력한 매개 변수를 확인할 수 있습니다.

이제 RDS 배포가 완료되었으므로 [사용자를 추가하고 관리](rds-user-management.md)할 수 있습니다.

## <a name="customized-rds-using-quickstart-templates"></a>빠른 시작 템플릿을 사용하여 사용자 지정된 RDS

Azure Resource Manager 템플릿을 사용하여 Azure에서 RDS를 배포할 수 있습니다. 이는 기본 RDS 배포가 필요하지만 기존 구성 요소(예: AD)를 사용하려는 경우에 특히 유용합니다. Marketplace 제품과 달리 가상 네트워크에서 기존 AD 사용, RDSH VM에 사용자 지정 OS 이미지 사용 및 RDS 구성 요소에 고가용성 레이어링과 같은 추가 사용자 지정 작업을 수행할 수 있습니다. 각 구성 요소에 고가용성을 추가한 후 환경은 [가용성이 높은 RDS 아키텍처](desktop-hosting-logical-architecture.md#highly-available-deployment)와 유사해집니다.

Azure RDS 템플릿을 사용하여 사용 공간이 적은 RDS 배포를 만들려면 다음 단계를 수행하세요. 

1. Azure 빠른 시작 템플릿을 선택합니다.
   1. [RDS Azure 빠른 시작 템플릿](https://aka.ms/rdautomation) 사이트로 이동합니다.
   2. 수행하려는 작업과 일치하는 템플릿을 선택합니다. 특정 템플릿의 모든 사전 요구 사항을 충족해야 합니다. (예를 들어 VM에 사용자 지정 이미지를 사용하려는 경우 Azure Storage 계정에 해당 이미지를 이미 업로드했는지 확인하세요.)
   3. **Azure에 배포**를 클릭합니다.
   4. Azure Portal에서 몇 가지 세부 정보(예: 관리자 사용자 이름, AD 도메인 이름)를 제공해야 합니다. 이는 선택한 템플릿에 따라 다릅니다.
   5. **구매**를 클릭합니다.
2. 배포에 연결합니다. 
   1. RDS 배포에 연결하는 데 필요한 인증서를 설치하려면 테스트 디바이스에서 [이 PowerShell 스크립트](https://gallery.technet.microsoft.com/Azure-Resource-Manager-4ea7e328)를 다운로드하고 실행합니다. 
   
      이 단계는 테스트 단계 중에만 필요합니다. 프로덕션 단계의 Azure에서 RDS를 배포하려면 웹 서버에서 공개적으로 신뢰하는 SSL 인증서 구매 및 사용과 같은 모범 사례를 따라야 합니다.

   2. 메시지가 표시되면 Azure 계정에 로그인합니다. Azure 구독, 리소스 그룹 및 이 새 배포를 위해 생성된 공개 IP 주소를 선택합니다.
   3. 스크립트가 완료되면 기본 브라우저에 RD 웹 페이지가 열립니다. 배포 중에 제공한 DNS 주소와 페이지의 URL을 비교하여 RD 웹 페이지를 다시 확인할 수 있습니다. 
   
      자동으로 게시된 기본 데스크톱을 보려면 배포 중에 만든 관리자 자격 증명으로 로그인합니다. 또한 사용자에게 데스크톱 및 애플리케이션을 테스트할 수 있는 RD 웹 사이트를 보낼 수 있습니다.

      > [!TIP]
      > 도메인 이름 또는 관리자 사용자를 잊으셨습니까? 포털의 새 리소스 그룹으로 다시 이동하고 **배포**를 클릭하면 입력한 매개 변수를 확인할 수 있습니다.

이제 RDS 배포가 완료되었으므로 [사용자를 추가하고 관리](rds-user-management.md)할 수 있습니다.
