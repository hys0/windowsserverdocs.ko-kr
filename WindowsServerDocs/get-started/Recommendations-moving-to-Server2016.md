---
title: Windows Server 2016으로 이동하기 위한 권장 사항
description: Windows Server 2016으로 이동하기 위한 권장 사항입니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.date: 10/18/2016
ms.technology: server-general
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 74aa1da3-7076-4a1f-ad5b-9e17bd46dba2
author: jaimeo
ms.author: jaimeo
manager: dongill
ms.localizationpriority: medium
ms.openlocfilehash: 08a92188446d018edd36a638abb30745721bd601
ms.sourcegitcommit: 1533d994a6ddea54ac189ceb316b7d3c074307db
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/01/2018
ms.locfileid: "1672464"
---
# <a name="recommendations-for-moving-to-windows-server-2016"></a>Windows Server 2016으로 이동하기 위한 권장 사항

>적용 대상: Windows Server 2016


|실행 중인 버전|Windows Server 2012 R2 또는 Windows Server 2012|Windows Server2008 R2 또는 Windows Server 2008|  
|-------------------|----------|--------------|--------------|---------------------------------------|  
|**Windows Server 역할 인프라**|[특정 역할 지침](https://technet.microsoft.com/windowsserver/jj554790)에 따라 업그레이드 또는 마이그레이션을 선택합니다.|- Windows Server 2016의 새 기능을 활용하려면 기존 호스트에 가상 컴퓨터에서 새 하드웨어를 배포하거나 Windows Server 2016을 설치합니다. 일부 새 기능은 Hyper-V를 실행하는 Windows Server 2016 물리적 호스트에서 가장 잘 작동합니다. <br>- [특정 역할 지침](https://technet.microsoft.com/windowsserver/jj554790)을 따릅니다.|
|**Microsoft 서버 관리 및 응용 프로그램 작업**|- 응용 프로그램 업그레이드에는 Windows Server 2016으로의 *마이그레이션*이 포함되어야 합니다. [호환성 목록](Server-Application-Compatibility.md)을 참조하세요. <br>- Windows Server 2016으로의 업그레이드만(즉, 응용 프로그램은 업그레이드하지 않음) 응용 프로그램 관련 지침을 사용해야 합니다.|- Windows Server 2016의 새 기능을 활용하려면 기존 호스트에 가상 컴퓨터에서 새 하드웨어를 배포하거나 Windows Server 2016을 설치합니다. 일부 새 기능은 Hyper-V를 실행하는 Windows Server 2016 물리적 호스트에서 가장 잘 작동합니다. 가능한 경우 마이그레이션 가이드를 따르세요. <br>- 또는 현재 OS를 그대로 유지하고 Windows Server 2016 호스트 또는 Microsoft Azure에서 실행되는 가상 컴퓨터에서 실행합니다. [Software Assurance](https://www.microsoft.com/en-us/Licensing/licensing-programs/software-assurance-default.aspx)를 통한 확장 지원 옵션에 대해 알아보려면 EA 대리점, TAM 또는 Microsoft에 문의하세요.|
|**ISV 응용 프로그램 작업**|- Windows Server 2016으로의 업그레이드에는 응용 프로그램 관련 지침을 사용해야 합니다. <br>- 타사 응용 프로그램과 Windows Server 호환성에 대한 자세한 내용을 보려면 [Windows Server 로고 인증 포털](https://msdn.microsoft.com/enterprisecloudcertified)을 방문하세요.|- Windows Server 2016의 새 기능을 활용하려면 기존 호스트에 가상 컴퓨터에서 새 하드웨어를 배포하거나 Windows Server 2016을 설치합니다. 일부 새 기능은 Hyper-V를 실행하는 Windows Server 2016 물리적 호스트에서 가장 잘 작동합니다. 가능한 경우 마이그레이션 가이드를 따르세요. <br>- 또는 현재 OS를 그대로 유지하고 Windows Server 2016 호스트 또는 Microsoft Azure에서 실행되는 가상 컴퓨터에서 실행합니다. [Software Assurance](https://www.microsoft.com/en-us/Licensing/licensing-programs/software-assurance-default.aspx)를 통한 확장 지원 옵션에 대해 알아보려면 EA 대리점, TAM 또는 Microsoft에 문의하세요.|
|**사용자 지정 응용 프로그램 작업**|- Windows Server 2016의 호환성 및 업그레이드 지침에 대해서는 응용 프로그램 개발자에게 문의하세요. <br>- 전환하기 전에 Microsoft Azure를 활용하여 Windows Server 2016에서 응용 프로그램을 테스트하세요. <br>- 다음 섹션의 전체 옵션을 참조하세요.|- Windows Server 2016의 호환성 및 업그레이드 지침에 대해서는 응용 프로그램 개발자에게 문의하세요. <br>- 전환하기 전에 Microsoft Azure를 활용하여 Windows Server 2016에서 응용 프로그램을 테스트하세요. <br>- Windows Server 2016의 새 기능을 활용하려면 기존 호스트에 가상 컴퓨터에서 새 하드웨어를 배포하거나 Windows Server 2016을 설치합니다. 일부 새 기능은 Hyper-V를 실행하는 Windows Server 2016 물리적 호스트에서 가장 잘 작동합니다. <br>- 다음 섹션의 전체 옵션을 참조하세요.|

## <a name="complete-options-for-moving-servers-running-custom-or-in-house-applications-on-older-versions-of-windows-server-to-windows-server-2016"></a>이전 버전의 Windows Server에서 사용자 지정 또는 “내부” 응용 프로그램을 실행하는 서버를 Windows Server 2016으로 전환하기 위한 전체 옵션

현재 서비스 및 작업에 미치는 영향을 최소화하면서 사용자 및 고객이 Windows Server 2016의 기능을 활용하는 데 도움이 되는 옵션이 이전보다 다양하게 제공됩니다.

- 온-프레미스 상의 테스트를 위해 [Windows Server](https://www.microsoft.com/evalcenter/evaluate-windows-server-2016) 평가판을 다운로드하여 응용 프로그램에서 최신 운영 체제를 사용해 보세요. 테스트가 완료되고 품질이 확인되면 정품 라이선스 키로 간단한 라이선스 변환을 수행할 수 있습니다(시스템 다시 시작 필요).

- [Microsoft Azure](https://azure.microsoft.com)를 테스트 기반으로 사용하여 사용자 지정 응용 프로그램이 최신 서버 운영 체제에서 작동되는지 확인할 수도 있습니다. 테스트가 완료되고 품질이 확인되면 온-프레미스에서 [최신 Windows Server 버전으로 마이그레이션](https://docs.microsoft.com/windows-server/get-started/installation-and-upgrade#upgrade)하세요. 

- 또는 테스트가 완료되고 품질이 확인된 후에 [Microsoft Azure](https://azure.microsoft.com)를 사용자 지정 응용 프로그램 또는 서비스에 대한 영구 위치로 사용할 수 있습니다. 이 경우 Azure의 새 서버로 전환할 준비가 될 때까지 이전 서버를 계속 사용할 수 있습니다.

    - Windows Server용 Software Assurance가 이미 있는 경우 [Azure 하이브리드 사용 혜택](https://azure.microsoft.com/pricing/hybrid-use-benefit/)을 통해 배포하면 비용을 절감할 수 있습니다. 

- 대부분의 경우 [Microsoft Azure](https://azure.microsoft.com)를 사용하여 현재 실행 중인 이전 버전의 Windows Server에 동일한 응용 프로그램을 호스트할 수 있습니다. [Azure Marketplace](https://azure.microsoft.com/marketplace/) 이미지를 사용하여 선택한 운영 체제의 가상 컴퓨터에 응용 프로그램 및 작업을 마이그레이션합니다.

    - Windows Server용 Software Assurance가 이미 있는 경우 [Azure 하이브리드 사용 혜택](https://azure.microsoft.com/pricing/hybrid-use-benefit/)을 통해 배포하면 비용을 절감할 수 있습니다. 

- Windows Server용 [Software Assurance](https://www.microsoft.com/en-us/Licensing/licensing-programs/software-assurance-default.aspx) 프로그램은 새로운 버전 권한 혜택을 제공합니다. 기타 혜택 목록 외에도, Software Assurance가 있는 서버는 시기가 적절한 경우 새 라이선스를 구입하지 않고도 최신 버전의 Window Server로 업그레이드할 수 있습니다. 

## <a name="additional-resources"></a>추가 리소스

- [Windows Server 2016에서 제거되었거나 사용되지 않는 기능](deprecated-features.md)
- 일반 서버 업그레이드 및 마이그레이션 옵션에 대해서는 [Windows Server 2016용 업그레이드 및 변환 옵션](Supported-Upgrade-Paths.md)을 참조하세요.
- 제품 수명 주기 및 지원 수준에 대한 자세한 내용은 [지원 기간 정책 FAQ](https://support.microsoft.com/help/17140/support-lifecycle-policy-faq)를 참조하세요.

