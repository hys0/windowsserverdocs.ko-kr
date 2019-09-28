---
title: DNS 정책 시나리오 가이드
description: 이 항목은 Windows Server 2016에 대 한 DNS 정책 시나리오 가이드의 일부입니다.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-dns
ms.topic: article
ms.assetid: 50fdb08a-bbd8-4107-954a-6699672110ff
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 8fab127fcd524526a515752871c1a3db92047c46
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71406231"
---
# <a name="dns-policy-scenario-guide"></a>DNS 정책 시나리오 가이드

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 가이드는 DNS, 네트워크 및 시스템 관리자 사용에 대 한 것입니다.  
  
Windows Server에서 DNS에 대 한 새로운 기능이 DNS 정책&reg; 2016 합니다. DNS 정책을 사용 하 여 DNS 서버 정책에서 정의 하는 다른 매개 변수를 기반으로 하는 이름 확인 쿼리를 처리 하는 방법을 제어 하는 방법에 알아보려면이 가이드를 사용할 수 있습니다.   
  
이 가이드에는 기본 및 보조 DNS 서버, 응용 프로그램 고가용성, 스플릿 브레인 DNS 등에 대 한 지리적 위치 기반 트래픽 관리를 포함 하 여 목표를 달성 하려면 DNS 서버 동작을 구성 하는 방법에 대 한 지침을 제공 하는 특정 DNS 정책 시나리오 뿐만 아니라 DNS 정책 개요 정보를 포함 합니다.  
  
이 가이드에는 다음 섹션이 수록되어 있습니다.  
  
- [DNS 정책 개요](DNS-Policies-Overview.md)  
- [주 서버와 지리적 위치 기반 트래픽 관리에 DNS 정책 사용](primary-geo-location.md)  
- [주-보조 배포를 사용 하 여 지리적 위치 기반 트래픽 관리에 DNS 정책 사용](primary-secondary-geo-location.md)  
- [하루 중 시간을 기준으로 지능형 DNS 응답에 DNS 정책 사용](dns-tod-intelligent.md)
- [Azure Cloud App Server를 사용 하는 시간을 기준으로 하는 DNS 응답](dns-tod-azure-cloud-app-server.md)
- [분할을 위한 dns 배포에 DNS 정책 사용](split-brain-DNS-deployment.md)
- [Active Directory에서 분할 하는 DNS에 대 한 DNS 정책 사용](dns-sb-with-ad.md)
- [Dns 쿼리에서 필터를 적용 하는 데 DNS 정책 사용](apply-filters-on-dns-queries.md)
- [응용 프로그램 부하 분산에 DNS 정책 사용](app-lb.md)
- [지리적 위치 인식을 사용 하 여 응용 프로그램 부하 분산에 DNS 정책 사용](app-lb-geo.md)

