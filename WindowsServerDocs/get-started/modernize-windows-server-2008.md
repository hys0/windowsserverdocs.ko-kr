---
title: Windows Server 2008 및 Windows Server 2008 R2 업그레이드
description: Windows Server 2008 및 2008 R2 서비스가 종료될 예정입니다. 온-프레미스 업그레이드 또는 Azure에 다시 호스팅하는 방법을 알아봅니다.
ms.prod: windows-server-threshold
ms.mktglfcycl: manage
ms.sitesec: library
author: mikeblodge
ms.author: mikeblodge
ms.date: 07/12/2018
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.localizationpriority: high
ms.openlocfilehash: 4127eab613abb429a200f513a11b944e05da0f76
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59851344"
---
# <a name="upgrade-windows-server-2008-and-windows-server-2008-r2"></a>Windows Server 2008 및 Windows Server 2008 R2 업그레이드

Windows Server 2008 및 Windows Server 2008 R2에 대한 연장 지원이 2020년 1월 14일에 종료됩니다. 두 가지 방법이 현대화 사용할 수 있습니다. 온-프레미스 업그레이드 또는 Azure에서 rehost를 통한 마이그레이션. **Azure에서 다시 호스팅하는 경우에 무료로 기존 서버 이미지를 마이그레이션할 수 있습니다.**

![Windows Server 2008에서 업그레이드하는 경로를 설명하는 순서도](media/WS08_upgrade_paths.png)


## <a name="on-premises-upgrade"></a>온-프레미스 업그레이드
서버를 온-프레미스로 유지하려고 하고 Windows Server 2008 또는 Windows Server 2008 R2를 실행하는 경우 [Windows Server 2016으로 업그레이드](installation-and-upgrade.md#upgrading-to-windows-server-2016)하기 전에 [Windows Server 2012/2012 R2로 업그레이드](installation-and-upgrade.md#upgrading-to-windows-server-2012-r2)해야 합니다. 업그레이드하는 경우 여전히 다시 호스팅하여 Azure로 마이그레이션할 수 있습니다.

온-프레미스 업그레이드 옵션에 대한 자세한 내용은 [Windows Server 2008 R2 또는 Windows Server 2008에서 업그레이드](installation-and-upgrade.md#upgrading-from-windows-server-2008-r2-or-windows-server-2008)를 참조하십시오.

Windows Server 2003을 실행하는 경우 [Windows Server 2008로 업그레이드](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff972408(v%3dws.10))해야 합니다. 온-프레미스 업그레이드 옵션에 대한 자세한 내용은 [Windows Server 2008로 업그레이드하는 경로](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd979563(v=ws.10))를 참조하십시오.


## <a name="migrate-to-azure"></a>Azure로 마이그레이션
온-프레미스 Windows Server 2008 및 Windows Server 2008 R2 서버를 Azure로 마이그레이션하여 가상 컴퓨터에서 계속 실행할 수 있습니다. Azure에서 규정을 더 잘 준수하고, 보안을 강화하고, 작업에 클라우드 혁신을 추가할 수 있습니다. Azure로 마이그레이션하는 장점은 다음과 같습니다.

- Azure의 보안 업데이트.
- 추가 비용 없이 추가 3년 동안 Windows Server 2008 R2 또는 2008의 중요 보안 업데이트를 받을 수 있습니다. 
- Azure의 무료 업그레이드.
- 준비가 되었을 때 더 많은 클라우드 서비스를 채택할 수 있습니다.
- SQL Server를 Azure 관리 인스턴스 또는 VM으로 마이그레이션하여 추가 비용 없이 추가 3년 동안 Windows Server 2008 R2 또는 2008 중요 보안 업데이트를 받을 수 있습니다. 
- 기존 SQL Server 및 Windows Server 라이선스를 활용하여 Azure에 고유하게 클라우드를 절감할 수 있습니다.

<a href="uploading-specialized-WS08-image-to-azure.md"><img src="media/WS08-image-banner-small.png"></a>

마이그레이션을 시작하려면 [Azure에 Windows Server 2008/2008 R2 특수 이미지 업로드](uploading-specialized-WS08-image-to-azure.md)를 참조하십시오.

기존 IT 리소스를 분석하고 현재 보유한 것을 평가하는 방법과 특정 서비스 및 응용 프로그램을 클라우드로 이동하거나 워크로드를 온-프레미스로 유지하고 Windows Server의 최신 버전으로 업그레이드하는 것의 이점을 파악하려면 [Windows Server 마이그레이션 가이드](https://go.microsoft.com/fwlink/?linkid=872689)를 참조하십시오.


## <a name="upgrade-sql-server-20082008-r2-in-parallel-with-your-windows-servers"></a>Windows Server와 동시에 SQL Server 2008/2008 R2 업그레이드

![SQL Server 로고](media/sqlr2.jpg)

SQL Server 2008/2008 R2를 실행하는 경우 SQL Server [2016](https://docs.microsoft.com/sql/sql-server/sql-server-technical-documentation?view=sql-server-2016) 또는 [2017](https://docs.microsoft.com/sql/sql-server/sql-server-technical-documentation?view=sql-server-2017)로 업그레이드할 수 있습니다.


## <a name="additional-resources"></a>추가 자료
[Microsoft Azure](https://docs.microsoft.com/azure/#pivot=products)