# [네트워킹 설명서](index.yml)
## [Windows Server에서 지원하는 네트워킹 시나리오](windows-server-supported-networking-scenarios.md)

## [네트워킹의 새로운 기능](What-s-New-in-Networking.md)

## [Windows Server에 대한 핵심 네트워크 지침](core-network-guide/core-network-guide-windows-server.md)
### [핵심 네트워크 구성 요소](core-network-guide/Core-Network-Guide.md)
### [핵심 네트워크 부록 지침](core-network-guide/cncg/Core-Network-companion-Guides.md)
#### [802.1X 유선 및 무선 배포용 서버 인증서 배포](core-network-guide/cncg/server-certs/Deploy-Server-Certificates-for-802.1X-Wired-and-Wireless-Deployments.md)
##### [서버 인증서 배포 개요](core-network-guide/cncg/server-certs/Server-Certificate-Deployment-Overview.md)
##### [서버 인증서 배포 계획](core-network-guide/cncg/server-certs/Server-Certificate-Deployment-Planning.md)
##### [서버 인증서 배포](core-network-guide/cncg/server-certs/Server-Certificate-Deployment.md)
###### [웹 서버 WEB1 설치](core-network-guide/cncg/server-certs/Install-the-Web-Server-WEB1.md)
###### [DNS에 WEB1에 대한 별칭(CNAME) 레코드 만들기](core-network-guide/cncg/server-certs/create-an-Alias-CNAME-Record-in-DNS-for-WEB1.md)
###### [CRL(인증서 해지 목록)을 배포하도록 WEB1 구성](core-network-guide/cncg/server-certs/Configure-WEB1-to-Distribute-Certificate-Revocation-lists.md)
###### [CAPolicy.inf 파일 준비](core-network-guide/cncg/server-certs/Prepare-the-CAPolicy-inf-File.md)
###### [인증 기관 설치](core-network-guide/cncg/server-certs/Install-the-Certification-Authority.md)
###### [CA1에서 CDP 및 AIA 확장 구성](core-network-guide/cncg/server-certs/Configure-the-cdP-and-AIA-Extensions-on-CA1.md)
###### [가상 디렉터리에 CA 인증서 및 CRL 복사](core-network-guide/cncg/server-certs/copy-the-CA-Certificate-and-CRL-to-the-Virtual-directory.md)
###### [서버 인증서 템플릿 구성](core-network-guide/cncg/server-certs/Configure-the-Server-Certificate-Template.md)
###### [서버 인증서 자동 등록 구성](core-network-guide/cncg/server-certs/Configure-Server-Certificate-Autoenrollment.md)
###### [그룹 새로 고침 정책](core-network-guide/cncg/server-certs/Refresh-Group-Policy.md)
###### [서버 인증서의 서버 등록 확인](core-network-guide/cncg/server-certs/verify-Server-Enrollment-of-a-Server-Certificate.md)
#### [암호 기반 802.1X 인증 무선 액세스 배포](core-network-guide/cncg/wireless/a-deploy-8021X-wireless-access.md)
##### [무선 액세스 배포 개요](core-network-guide/cncg/wireless/b-wireless-access-deploy-overview.md)
##### [무선 액세스 배포 프로세스](core-network-guide/cncg/wireless/c-wireless-access-deploy-process.md)
##### [무선 액세스 배포 계획](core-network-guide/cncg/wireless/d-wireless-access-planning.md)
##### [무선 액세스 배포](core-network-guide/cncg/wireless/e-wireless-access-deployment.md)
#### [BranchCache 호스트 캐시 모드 배포](core-network-guide/cncg/bc-hcm/1-Deploy-Bc-Hcm.md)
##### [BranchCache 호스트 캐시 모드 배포 개요](core-network-guide/cncg/bc-hcm/2-Bc-Hcm-Deploy-Overview.md)
##### [BranchCache 호스트 캐시 모드 배포 계획](core-network-guide/cncg/bc-hcm/3-Bc-Hcm-Plan.md)
##### [BranchCache 호스트 캐시 모드 배포](core-network-guide/cncg/bc-hcm/4-Bc-Hcm-Deployment.md)
###### [서비스 연결 지점별 BranchCache 기능 설치 및 호스트 캐시 서버 구성](core-network-guide/cncg/bc-hcm/5-Bc-Feature-Scp.md)
###### [호스트 캐시 이동 및 크기 조정(선택 사항)](core-network-guide/cncg/bc-hcm/6-Bc-move-Resize-Cache.md)
###### [호스트 캐시 서버에서 콘텐츠 미리 해싱 및 미리 로드(선택 사항)](core-network-guide/cncg/bc-hcm/7-Bc-Prehash-Preload.md)
####### [웹 및 파일 콘텐츠용 콘텐츠 서버 데이터 패키지 만들기(선택 사항)](core-network-guide/cncg/bc-hcm/8-Bc-Data-Packages.md)
####### [호스트 캐시 서버의 데이터 패키지 가져오기(선택 사항)](core-network-guide/cncg/bc-hcm/9-Bc-import-Data.md)
###### [서비스 연결 지점별 클라이언트 자동 호스트 캐시 검색 구성](core-network-guide/cncg/bc-hcm/10-Bc-Client-By-Scp.md)
##### [추가 리소스](core-network-guide/cncg/bc-hcm/11-Bc-Hcm-additional-resources.md)

## [BranchCache](branchcache/BranchCache.md)
### [BranchCache netsh 및 Windows PowerShell 명령](branchcache/BranchCache-Network-Shell-and-Windows-powershell-Commands.md)
### [BranchCache 배포 지침](branchcache/deploy/BranchCache-Deployment-Guide.md)
#### [BranchCache 디자인 선택](branchcache/plan/Choosing-a-BranchCache-Design.md)
#### [BranchCache 배포](branchcache/deploy/Deploy-BranchCache.md)
##### [콘텐츠 서버 설치 및 구성](branchcache/deploy/Install-and-Configure-Content-Servers.md)
###### [BranchCache 기능을 사용하는 콘텐츠 서버 설치](branchcache/deploy/Install-Content-Servers-that-Use-the-BranchCache-Feature.md)
####### [BranchCache 기능 설치](branchcache/deploy/Install-the-BranchCache-Feature.md)
####### [WSUS(Windows Server Update Services) 콘텐츠 서버 구성](branchcache/deploy/configure-wsus-content-servers.md)
###### [파일 서비스 콘텐츠 서버 설치](branchcache/deploy/Install-File-Services-Content-Servers.md)
####### [파일 서비스 서버 역할 구성](branchcache/deploy/Configure-the-File-Services-server-role.md)
######## [콘텐츠 서버로 새 파일 서버 설치](branchcache/deploy/Install-a-New-File-Server-as-a-Content-Server.md)
######## [기존 파일 서버를 콘텐츠 서버로 구성](branchcache/deploy/Configure-an-Existing-File-Server-as-a-Content-Server.md)
####### [파일 서버에 해시 게시 사용](branchcache/deploy/Enable-Hash-Publication-for-File-Servers.md)
######## [비 도메인 구성원 파일 서버에 해시 게시 사용](branchcache/deploy/Enable-Hash-Publication-for-Non-Domain-Member-File-Servers.md)
######## [도메인 구성원 파일 서버에 해시 게시 사용](branchcache/deploy/Enable-Hash-Publication-for-Domain-Member-File-Servers.md)
######### [BranchCache 파일 서버 조직 구성 단위(OU) 만들기](branchcache/deploy/create-the-BranchCache-File-Servers-Organizational-Unit.md)
######### [BranchCache 파일 서버 OU로 파일 서버 이동](branchcache/deploy/move-File-Servers-to-the-BranchCache-File-Servers-Organizational-Unit.md)
######### [BranchCache 해시 게시 GPO(그룹 정책 개체) 만들기](branchcache/deploy/create-the-BranchCache-Hash-Publication-Group-Policy-Object.md)
######### [BranchCache 해시 게시 GPO 구성](branchcache/deploy/Configure-the-BranchCache-Hash-Publication-Group-Policy-Object.md)
####### [파일 공유에서 BranchCache 사용(선택 사항)](branchcache/deploy/enable-bc-on-file-share.md)
##### [호스트 캐시 서버 배포(선택 사항)](branchcache/deploy/deploy-hosted-cache-servers.md)
##### [호스트 캐시 서버에서 콘텐츠 미리 해싱 및 미리 로딩(선택 사항)](branchcache/deploy/prehashing-and-preloading.md)
##### [BranchCache 클라이언트 컴퓨터 구성](branchcache/deploy/Configure-BranchCache-Client-computers.md)
###### [그룹 정책을 사용하여 도메인 구성원 클라이언트 컴퓨터 구성](branchcache/deploy/Use-Group-Policy-to-Configure-Domain-Member-Client-computers.md)
###### [Windows PowerShell을 사용하여 비 도메인 구성원 클라이언트 컴퓨터 구성](branchcache/deploy/Use-Windows-powershell-to-Configure-Non-Domain-Member-Client-computers.md)
####### [비 도메인 구성원 BranchCache 트래픽을 허용하도록 방화벽 규칙 구성](branchcache/deploy/Configure-Firewall-Rules-for-Non-Domain-Members-to-Allow-BranchCache-Traffic.md)
###### [클라이언트 컴퓨터 설정 확인](branchcache/deploy/verify-Client-computer-Settings.md)

## [DirectAccess](../remote/remote-access/da-stub.md) 

## [DNS(Domain Name System)](dns/dns-top.md)
### [Windows Server DNS 클라이언트의 새로운 기능](dns/What-s-New-in-DNS-Client.md)
### [Windows Server DNS 서버의 새로운 기능](dns/What-s-New-in-DNS-Server.md)
### [DNS 정책 시나리오 지침](dns/deploy/DNS-Policy-Scenario-Guide.md)
#### [DNS 정책 개요](dns/deploy/DNS-Policies-Overview.md)
#### [주 서버를 사용한 지리적 위치 기반 트래픽 관리에 DNS 정책 사용](dns/deploy/primary-geo-location.md)
#### [주-보조 배포를 사용한 지리적 위치 기반 트래픽 관리에 DNS 정책 사용](dns/deploy/primary-secondary-geo-location.md)
#### [시간 기반 인텔리전트 DNS 응답에 DNS 정책 사용](dns/deploy/dns-tod-intelligent.md)
#### [Azure 클라우드 애플리케이션 서버를 사용하는 시간 기반 DNS 응답](dns/deploy/dns-tod-azure-cloud-app-server.md)
#### [스플릿 브레인 DNS 배포에 DNS 정책 사용](dns/deploy/split-brain-DNS-deployment.md)
#### [Active Directory에서 스플릿 브레인 DNS에 DNS 정책 사용](dns/deploy/dns-sb-with-ad.md)
#### [DNS 쿼리에 필터를 적용하는 데 DNS 정책 사용](dns/deploy/apply-filters-on-dns-queries.md)
#### [앱 부하 분산에 DNS 정책 사용](dns/deploy/app-lb.md)
#### [지리적 위치 인식을 통한 앱 부하 분산에 DNS 정책 사용](dns/deploy/app-lb-geo.md)
### [DNS 문제 해결](dns/troubleshoot/troubleshoot-dns-data-collection.md)
#### [DNS 클라이언트 문제 해결](dns/troubleshoot/troubleshoot-dns-client.md)
##### [DNS 클라이언트에서 DNS 클라이언트 쪽 캐싱 비활성화](dns/troubleshoot/disable-dns-client-side-caching.md)
#### [DNS 서버 문제 해결](dns/troubleshoot/troubleshoot-dns-server.md)

## [DHCP(Dynamic Host Configuration Protocol)](technologies/dhcp/dhcp-top.md)
### [DHCP의 새로운 기능](technologies/dhcp/What-s-New-in-DHCP.md)
#### [DHCP 서브넷 선택 옵션](technologies/dhcp/dhcp-subnet-options.md)
#### [DNS 레코드 등록에 대한 DHCP 로깅 이벤트](technologies/dhcp/dhcp-dns-events.md)
### [Windows PowerShell을 사용하여 DHCP 배포](technologies/dhcp/dhcp-deploy-wps.md)
### [DHCP 문제 해결](../troubleshoot/troubleshoot-dhcp-issue.md)
#### [DHCP(Dynamic Host Configuration Protocol) 기본 사항](../troubleshoot/dynamic-host-configuration-protocol-basics.md)
#### [DHCP 문제 해결을 위한 일반 지침](../troubleshoot/general-guidance-to-troubleshoot-dhcp.md)
##### [DHCP 서버 없이 자동 TCP/IP 주소 지정을 사용하는 방법](../troubleshoot/how-to-use-automatic-tcpip-addressing-without-a-dh.md)
#### [DHCP 클라이언트의 문제 해결](../troubleshoot/troubleshoot-problems-on-dhcp-client.md)
#### [DHCP 서버의 문제 해결](../troubleshoot/troubleshoot-problems-on-dhcp-server.md)

## [HPN(고성능 네트워킹)](technologies/hpn/hpn-top.md)
### [네트워크 오프로드 및 최적화 기술](technologies/hpn/network-offload-and-optimization.md)
#### [SO(소프트웨어 전용) 기능 및 기술](technologies/hpn/hpn-software-only-features.md)
#### [SH(소프트웨어 및 하드웨어) 통합 기능 및 기술](technologies/hpn/hpn-software-hardware-features.md)
#### [HO(하드웨어 전용) 기능 및 기술](technologies/hpn/hpn-hardware-only-features.md)
#### [NIC 고급 속성](technologies/hpn/hpn-nic-advanced-properties.md)

### [Insider Preview](technologies/hpn/hpn-insider-preview.md)
### [vSwitch의 RSC(수신 세그먼트 통합)](technologies/hpn/rsc-in-the-vswitch.md)

### [수렴형 NIC 구성 지침](technologies/conv-nic/cnic-top.md)
#### [단일 네트워크 어댑터 구성](technologies/conv-nic/cnic-single.md)
#### [데이터 센터 네트워크 어댑터 구성](technologies/conv-nic/cnic-datacenter.md)
#### [실제 스위치 구성](technologies/conv-nic/cnic-app-switch-config.md)
#### [수렴형 NIC 문제 해결](technologies/conv-nic/cnic-app-troubleshoot.md)

### [\(DCB\)(데이터 센터 브리징)](technologies/dcb/dcb-top.md)
#### [DCB 설치](technologies/dcb/dcb-install.md)
#### [DCB 관리](technologies/dcb/dcb-manage.md)

### [vRSS(가상 수신측 배율)](technologies/vrss/vrss-top.md)
#### [vRSS 사용 계획](technologies/vrss/vrss-plan.md)
#### [가상 네트워크 어댑터에서 vRSS 사용](technologies/vrss/vrss-enable.md)
#### [vRSS 관리](technologies/vrss/vrss-manage.md)
#### [vRSS FAQ](technologies/vrss/vrss-faq.md)
#### [RSS 및 vRSS에 대한 Windows PowerShell 명령](technologies/vrss/vrss-wps.md)
#### [vRSS 이슈 해결](technologies/vrss/vrss-resolve-issues.md)

## [HCN(호스트 컴퓨팅 네트워크) 서비스 API](technologies/hcn/hcn-top.md)   
### [일반 HCN 시나리오](technologies/hcn/hcn-scenarios.md)
### [HCN에 대한 RPC 컨텍스트 핸들](technologies/hcn/hcn-declaration-handles.md)
### [HCN JSON 문서 스키마](technologies/hcn/hcn-json-document-schemas.md)
### [생성된 C# 코드의 예](technologies/hcn/example-c-sharp.md)
### [생성된 Go 코드의 예](technologies/hcn/example-go.md)

## [Hyper-V 가상 스위치](technologies/vswitch-stub.md)

## [IPAM(IP 주소 관리)](technologies/ipam/ipam-top.md)
### [IPAM의 새로운 기능](technologies/ipam/What-s-New-in-IPAM.md)
### [IPAM 관리](technologies/ipam/Manage-IPAM.md)
#### [DNS 리소스 레코드 관리](technologies/ipam/DNS-Resource-Record-Management.md)
##### [DNS 리소스 레코드 추가](technologies/ipam/add-a-DNS-Resource-Record.md)
##### [DNS 리소스 레코드 삭제](technologies/ipam/delete-DNS-Resource-Records.md)
##### [DNS 리소스 레코드의 보기 필터링](technologies/ipam/Filter-the-View-of-DNS-Resource-Records.md)
##### [특정 IP 주소의 DNS 리소스 레코드 보기](technologies/ipam/View-DNS-Resource-Records-for-a-Specific-IP-address.md)
#### [DNS 영역 관리](technologies/ipam/DNS-Zone-Management.md)
##### [DNS 영역 만들기](technologies/ipam/create-a-DNS-Zone.md)
##### [DNS 영역 편집](technologies/ipam/edit-a-DNS-Zone.md)
##### [DNS 영역의 DNS 리소스 레코드 보기](technologies/ipam/View-DNS-Resource-Records-for-a-DNS-Zone.md)
##### [DNS 영역 보기](technologies/ipam/View-DNS-Zones.md)
#### [여러 Active Directory 포리스트의 리소스 관리](technologies/ipam/Manage-Resources-in-Multiple-active-directory-forests.md)
#### [사용률 데이터 제거](technologies/ipam/Purge-Utilization-Data.md)
#### [역할 기반 액세스 제어](technologies/ipam/Role-based-Access-Control.md)
##### [서버 관리자를 사용하여 역할 기반 액세스 제어 관리](technologies/ipam/Manage-Role-Based-Access-Control-with-server-manager.md)
###### [액세스 제어를 위한 사용자 역할 만들기](technologies/ipam/create-a-User-Role-for-Access-Control.md)
###### [액세스 정책 만들기](technologies/ipam/create-an-Access-Policy.md)
###### [DNS 영역의 액세스 범위 설정](technologies/ipam/Set-Access-Scope-for-a-DNS-Zone.md)
###### [DNS 리소스 레코드의 액세스 범위 설정](technologies/ipam/Set-Access-Scope-for-DNS-Resource-Records.md)
###### [역할 및 역할 권한 보기](technologies/ipam/View-Roles-and-Role-Permissions.md)
##### [Windows PowerShell을 사용하여 역할 기반 액세스 제어 관리](technologies/ipam/Manage-Role-Based-Access-Control-with-Windows-powershell.md)

## [네트워크 부하 분산](technologies/Network-Load-Balancing.md)



## [NPS(네트워크 정책 서버)](technologies/nps/nps-top.md)
### [NPS 모범 사례](technologies/nps/nps-best-practices.md)
### [NPS 시작](technologies/nps/nps-getstart-top.md)
#### [연결 요청 처리](technologies/nps/nps-crp-top.md)
##### [연결 요청 정책](technologies/nps/nps-crp-crpolicies.md)
##### [영역 이름](technologies/nps/nps-crp-realm-names.md)
##### [원격 RADIUS 서버 그룹](technologies/nps/nps-crp-rrsg.md)
#### [네트워크 정책](technologies/nps/nps-np-overview.md)
##### [액세스 권한](technologies/nps/nps-np-access.md)
#### [NPS 템플릿](technologies/nps/nps-templates.md)
#### [RADIUS 클라이언트](technologies/nps/nps-radius-clients.md)
### [NPS 계획](technologies/nps/nps-plan-top.md)
#### [RADIUS 서버로 작동하는 NPS 계획](technologies/nps/nps-plan-server.md)
#### [RADIUS 프록시로 작동하는 NPS 계획](technologies/nps/nps-plan-proxy.md)
### [NPS 배포](technologies/nps/nps-deploy.md)
### [NPS 관리](technologies/nps/nps-manage-top.md)
#### [관리 도구를 사용하여 네트워크 정책 서버 관리](technologies/nps/nps-admintools.md)
#### [연결 요청 정책 구성](technologies/nps/nps-crp-configure.md)
#### [RADIUS 트래픽에 대한 방화벽 구성](technologies/nps/nps-firewalls-configure.md)
#### [네트워크 정책 구성](technologies/nps/nps-np-configure.md)
#### [NPS 계정 구성](technologies/nps/nps-accounting-configure.md)
#### [RADIUS 클라이언트 구성](technologies/nps/nps-radius-clients-configure.md)
#### [원격 RADIUS 서버 그룹 구성](technologies/nps/nps-crp-rrsg-configure.md)
#### [NPS와 함께 사용되는 인증서 관리](technologies/nps/nps-manage-certificates.md)
##### [PEAP 및 EAP 요구 사항에 대한 인증서 템플릿 구성](technologies/nps/nps-manage-cert-requirements.md)
#### [NPS 관리](technologies/nps/nps-manage-servers.md)
##### [멀티홈 컴퓨터에서 NPS 구성](technologies/nps/nps-multihomed-configure.md)
##### [NPS UDP 포트 정보 구성](technologies/nps/nps-udp-ports-configure.md)
##### [NAS 알림 전달 사용 안 함](technologies/nps/nps-disable-nas-notifications.md)
##### [다른 서버에서 가져올 수 있도록 NPS 구성 내보내기](technologies/nps/nps-manage-export.md)
##### [NPS로 처리되는 동시 인증 늘리기](technologies/nps/nps-concurrent-auth.md)
##### [NPS 설치](technologies/nps/nps-manage-install.md)
##### [NPS 프록시 서버 부하 분산](technologies/nps/nps-manage-proxy-lb.md)
##### [Active Directory 도메인에서 NPS 등록](technologies/nps/nps-manage-register.md)
##### [Active Directory 도메인에서 NPS 등록 해제](technologies/nps/nps-manage-unregister.md)
##### [NPS에서 정규식 사용](technologies/nps/nps-crp-reg-expressions.md)
##### [NPS 변경 후 구성 확인](technologies/nps/nps-manage-verify.md)
##### [NPS 데이터 수집](technologies/nps/nps-data-collection.md)
#### [NPS 템플릿 관리](technologies/nps/nps-manage-templates.md)

## [Netsh(네트워크 셸)](technologies/netsh/netsh.md)
### [Netsh 명령 구문, 컨텍스트 및 서식 지정](technologies/netsh/netsh-contexts.md)
### [Netsh(네트워크 셸) 예제 배치 파일](technologies/netsh/netsh-wins.md)
### [Netsh http 명령](technologies/netsh/netsh-http.md)
### [Netsh 인터페이스 portproxy 명령](technologies/netsh/netsh-interface-portproxy.md)
### [Netsh mbn 명령](technologies/netsh/netsh-mbn.md)

## [네트워크 하위 시스템 성능 튜닝](technologies/network-subsystem/net-sub-performance-top.md)
### [네트워크 어댑터 선택](technologies/network-subsystem/net-sub-choose-nic.md)
### [네트워크 인터페이스의 순서 구성](technologies/network-subsystem/net-sub-interface-metric.md)
### [네트워크 어댑터 성능 튜닝](technologies/network-subsystem/net-sub-performance-tuning-nics.md)
### [네트워크 관련 성능 카운터](technologies/network-subsystem/net-sub-performance-counters.md)
### [네트워크 워크로드용 성능 도구](technologies/network-subsystem/net-sub-performance-tools.md)

## [NIC 팀](technologies/nic-teaming/NIC-Teaming.md)
### [NIC 팀 MAC 주소 사용 및 관리](technologies/nic-teaming/NIC-Teaming-MAC-address-Use-and-Management.md)
### [호스트 컴퓨터 또는 VM에 새 NIC 팀 만들기](technologies/nic-teaming/create-a-New-NIC-Team-on-a-Host-computer-or-VM.md)
### [NIC 팀 문제 해결](technologies/nic-teaming/Troubleshooting-NIC-Teaming.md)

## [QoS(서비스 품질) 정책](technologies/qos/qos-policy-top.md)
### [QoS 정책 시작](technologies/qos/qos-policy-get-started.md)
#### [QoS 정책의 작동 방식](technologies/qos/qos-policy-works.md)
#### [QoS 정책 아키텍처](technologies/qos/qos-policy-architecture.md)
#### [QoS 정책 시나리오](technologies/qos/qos-policy-scenarios.md)
###[QoS 정책 관리](technologies/qos/qos-policy-manage.md)
#### [QoS 정책 이벤트 및 오류](technologies/qos/qos-policy-errors.md)
### [QoS 정책 FAQ](technologies/qos/qos-policy-faq.md)

## [SDN(소프트웨어 정의 네트워킹)](sdn/index.yml)

### [Windows Server의 SDN 개요](sdn/software-defined-networking.md)

### [SDN 기술](sdn/technologies/Software-Defined-Networking-Technologies.md)
#### [Hyper-V 네트워크 가상화](sdn/technologies/hyper-v-network-virtualization/Hyper-V-Network-Virtualization.md)
##### [Hyper-V 네트워크 가상화 개요](sdn/technologies/hyper-v-network-virtualization/hyperv-network-virtualization-overview-windows-server.md)
##### [Hyper-V 네트워크 가상화 기술 세부 정보](sdn/technologies/hyper-v-network-virtualization/hyperv-network-virtualization-technical-details-windows-server.md)
##### [Hyper-V 네트워크 가상화의 새로운 기능](sdn/technologies/hyper-v-network-virtualization/whats-new-hyperv-network-virtualization-windows-server.md)
#### [SDN용 iDNS(내부 DNS 서비스)](sdn/technologies/Idns-for-Sdn.md)
#### [네트워크 컨트롤러](sdn/technologies/network-controller/Network-Controller.md)
##### [네트워크 컨트롤러 고가용성](sdn/technologies/network-controller/network-controller-high-availability.md)
##### [서버 관리자를 사용하여 네트워크 컨트롤러 서버 역할 설치](sdn/technologies/network-controller/Install-the-Network-Controller-server-role-using-server-manager.md)
##### [네트워크 컨트롤러의 배포 후 단계](sdn/technologies/network-controller/post-deploy-steps-nc.md)
#### [네트워크 기능 가상화](sdn/technologies/network-function-virtualization/Network-Function-Virtualization.md)
##### [데이터 센터 방화벽 개요](sdn/technologies/network-function-virtualization/Datacenter-Firewall-Overview.md)
##### [SDN용 RAS 게이트웨이](sdn/technologies/network-function-virtualization/RAS-Gateway-for-SDN.md)
###### [RAS 게이트웨이의 새로운 기능](sdn/technologies/network-function-virtualization/What-s-New-in-RAS-Gateway.md)
###### [RAS 게이트웨이 배포 아키텍처](sdn/technologies/network-function-virtualization/RAS-Gateway-Deployment-Architecture.md)
###### [RAS 게이트웨이 고가용성](sdn/technologies/network-function-virtualization/RAS-Gateway-High-Availability.md)
##### [SDN에 대한 SLB(소프트웨어 부하 분산)](sdn/technologies/network-function-virtualization/software-load-balancing-for-sdn.md)
#### [SDN에 대한 SET(스위치 포함 팀)](sdn/technologies/Set-for-Sdn.md)
#### [컨테이너 네트워킹](sdn/technologies/Containers/Container-networking-overview.md)

### [SDN 계획](sdn/plan/Plan-a-Software-Defined-Network-Infrastructure.md)
#### [네트워크 컨트롤러를 배포하기 위한 설치 및 준비 요구 사항](sdn/plan/Installation-and-Preparation-Requirements-for-Deploying-Network-Controller.md)

### SDN 배포
#### [SDN 인프라 배포](sdn/deploy/Deploy-a-Software-Defined-Network-Infrastructure.md)
##### [스크립트를 사용하여 SDN 인프라 배포](sdn/deploy/Deploy-a-Software-Defined-Network-infrastructure-using-scripts.md)
#### [Windows PowerShell을 사용하여 SDN 기술 배포](sdn/deploy/Deploy-Software-Defined-Network-Technologies-using-Windows-powershell.md)
##### [Windows PowerShell을 사용하여 네트워크 컨트롤러 배포](sdn/deploy/Deploy-Network-Controller-using-Windows-powershell.md)

### [SDN 관리](sdn/manage/manage-sdn.md)
#### [테넌트 가상 네트워크 관리](sdn/manage/Manage-Tenant-Virtual-Networks.md)
##### [가상 네트워크 및 VLAN 사용 방법의 이해](sdn/manage/Understanding-Usage-of-Virtual-Networks-and-VLANs.md)
##### [ACL(액세스 제어 목록)을 사용하여 데이터 센터 네트워크 트래픽 흐름 관리](sdn/manage/use-acls-for-traffic-flow.md)
##### [테넌트 가상 네트워크 만들기, 삭제 또는 업데이트](sdn/manage/create,-delete,-or-Update-Tenant-Virtual-Networks.md)
##### [테넌트 가상 네트워크에 가상 게이트웨이 추가](sdn/manage/add-a-Virtual-Gateway-to-a-Tenant-Virtual-Network.md)
##### [테넌트 가상 네트워크에 컨테이너 엔드포인트 연결](sdn/manage/Connect-container-endpoints-to-a-Tenant-Virtual-Network.md)
##### [가상 서브넷의 암호화 구성](sdn/vnet-encryption/sdn-config-vnet-encryption.md)
##### [가상 네트워크의 송신 계량](sdn/manage/sdn-egress.md)

#### [테넌트 워크로드 관리](sdn/manage/Manage-Tenant-Workloads.md)
##### [VM을 만들어서 테넌트 가상 네트워크 또는 VLAN에 연결](sdn/manage/create-a-Tenant-VM.md)
##### [테넌트 VM 네트워크 어댑터에 대한 QoS 구성](sdn/manage/Configure-QoS-for-Tenant-VM-Network-Adapter.md)
##### [데이터 센터 방화벽 ACL 구성](sdn/manage/Configure-Datacenter-Firewall-Acls.md)
##### [부하 분산 및 NAT(Network Address Translation)에 대한 소프트웨어 부하 분산 장치 구성](sdn/manage/Configure-SLB-and-Nat.md)
##### [가상 네트워크에서 네트워크 가상 어플라이언스 사용](sdn/manage/Use-Network-Virtual-Appliances-on-a-VN.md)
##### [가상 네트워크의 게스트 클러스터링](sdn/manage/guest-clustering.md)
#### [SDN 인프라 업데이트, 백업 및 복원](sdn/manage/Update-Backup-Restore.md)

### [SDN 보안](sdn/security/sdn-security-top.md)
#### [네트워크 컨트롤러 보안](sdn/security/nc-security.md)
#### [SDN 인증서 관리](sdn/security/sdn-manage-certs.md)
#### [SPN(서비스 사용자 이름)을 사용하는 Kerberos](sdn/security/kerberos-with-spn.md)
#### [SDN 방화벽 감사](sdn/security/sdn-firewall-auditing.md)

### [가상 네트워크 피어링](sdn/vnet-peering/sdn-vnet-peering.md)
#### [가상 네트워크 피어링 구성](sdn/vnet-peering/sdn-configure-vnet-peering.md)

### [Windows Server 2019 게이트웨이 성능](sdn/gateway-performance.md)
### [게이트웨이 대역폭 할당](sdn/gateway-allocation.md)

### [SDN 문제 해결](sdn/troubleshoot/Troubleshoot-Software-Defined-Networking.md)
#### [Windows Server 소프트웨어 정의 네트워킹 스택 문제 해결](sdn/troubleshoot/troubleshoot-windows-server-software-defined-networking-stack.md)

### [SDN용 System Center 기술](sdn/Sc-Tech-for-Sdn.md)
### [Microsoft Azure 및 SDN](sdn/Azure_and_Sdn.md)
### [데이터 센터 및 클라우드 네트워킹 팀에 문의](sdn/contact-sdn-team.md)

## [VPN(가상 사설망)](technologies/vpn-stub.md)

## [WINS(Windows Internet Name Service)](technologies/wins/wins-top.md)

## [Windows 시간 서비스](windows-time-service/windows-time-service-top.md)
### [Insider Preview - Windows Server 2019의 Windows 시간 서비스](windows-time-service/insider-preview.md)
### [Windows Server 2016의 정확한 시간](windows-time-service/accurate-time.md)
### [정확한 시간을 위한 경계 지원](windows-time-service/support-boundary.md)
### [높은 정확성을 위한 시스템 구성](windows-time-service/configuring-systems-for-high-accuracy.md)
### [추적 가능성을 위한 Windows 시간](windows-time-service/windows-time-for-traceability.md)
### [Windows 시간 서비스 기술 참조](windows-time-service/windows-time-service-tech-ref.md)
#### [Windows 시간 서비스의 작동 방식](windows-time-service/How-the-Windows-Time-Service-Works.md)
#### [Windows 시간 서비스 도구 및 설정](windows-time-service/Windows-Time-Service-Tools-and-Settings.md)

