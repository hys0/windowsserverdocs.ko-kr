---
title: "3 단계 도메인 이름 추가"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e5b4a362-1881-4024-ae4e-cc3b05e50103
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 64bf24e45155fdd981e2061b3de7ebce1c53b36c
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="add-third-level-domain-names"></a>3 단계 도메인 이름 추가

>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다.

사용자가 설정 도메인 이름 마법사의 세 수준 도메인 이름 요청 하는 기능을 추가할 수 있습니다. 만들고 도메인 관리자에서 운영 체제의 사용 되는 코드 조립 설치 하 여이 작업을 수행 합니다.  
  
## <a name="create-a-provider-of-third-level-domain-names"></a>3 단계 도메인 이름 공급자 만들기  
 만들고 도메인 이름 마법사를 제공 하는 코드 조립 설치 하 여 3 단계 도메인 이름을 사용할 수 있습니다. 이렇게 하려면 다음 작업을 수행 합니다.  
  
-   [IDomainSignupProvider 인터페이스 구현을 조립에 추가](Add-Third-Level-Domain-Names.md#BKMK_DomainSignup)  
  
-   [IDomainMaintenanceProvider 인터페이스 구현을 조립에 추가](Add-Third-Level-Domain-Names.md#BKMK_DomainMaintenance)  
  
-   [조립 Authenticode 서명으로 서명](Add-Third-Level-Domain-Names.md#BKMK_SignAssembly)  
  
-   [조립 참조 컴퓨터에 설치](Add-Third-Level-Domain-Names.md#BKMK_InstallAssembly)  
  
-   [Windows Server 도메인 이름 관리 서비스를 다시 시작](Add-Third-Level-Domain-Names.md#BKMK_RestartService)  
  
###  <a name="BKMK_DomainSignup"></a>IDomainSignupProvider 인터페이스 구현을 조립에 추가  
 IDomainSignupProvider 인터페이스 도메인 제품 마법사에 추가 하는 데 사용 됩니다.  
  
##### <a name="to-add-the-idomainsignupprovider-code-to-the-assembly"></a>IDomainSignupProvider 코드는 조립을 추가 하려면  
  
1.  프로그램에서 마우스 오른쪽 단추로 클릭 하 여 Visual Studio 2008 관리자 권한으로 엽니다는 **시작** 메뉴를 선택 하 고 **관리자 권한으로 실행**합니다.  
  
2.  클릭 **파일**, 클릭 **새로**을 차례로 클릭 하 고 **프로젝트**합니다.  
  
3.  에 **새 프로젝트** 대화 상자를 클릭 **C#**, 클릭 **클래스 라이브러리**솔루션을 이름을 입력 하 고 클릭 한 다음 **확인**합니다.  
  
4.  Class1.cs 파일을 이름을 바꿉니다. 예를 들어 MyDomainNameProvider.cs  
  
5.  Wssg.Web.DomainManagerObjectModel.dll, CertManaged.dll, WssgCertMgmt.dll WssgCommon.dll 파일에 대 한 언급을 추가 합니다.  
  
6.  다음 추가 사용 하 여 문의 합니다.  
  
    ```c#  
  
    using System.Collections.ObjectModel;  
    using System.Net;  
    using System.Net.Sockets;  
    using Microsoft.WindowsServerSolutions.Certificates;  
    using Microsoft.WindowsServerSolutions.CertificateManagement;  
    using Microsoft.WindowsServerSolutions.Common;  
    using Microsoft.Win32;  
    ```  
  
7.  네임 및 이때에 맞게 클래스 헤더 변경 합니다.  
  
    ```c#  
    namespace Microsoft.WindowsServerSolutions.RemoteAccess.Domains  
    {  
        public class MyDomainNameProvider : IDomainSignupProvider  
        {  
        }  
    }  
    ```  
  
8.  필요한 변수와 초기화 방법을 제공 하는 제품 마법사에서 정의 된에 추가 합니다.  
  
    > [!NOTE]
    >  초기화 방법을 고유 해야 하는 도메인 공급자에 대 한 식별자를 정의 합니다. 일반적으로를 식별자로 GUID 정의 됩니다. GUID 만들기에 대 한 자세한 내용은 참조 [Guid 만들기 (guidgen.exe)](https://go.microsoft.com/fwlink/?LinkId=116098)합니다.  
  
     예제는 초기화 방법을 보여 줍니다.  
  
    ```c#  
  
    static readonly Guid MyID = new Guid("8C999DF5-696A-47af-822D-94F1673D3397");  
    public Guid ID { get { return MyID; } }  
    public string Name { get { return "My Provider"; } }  
    List<Offering> offerings = new List<Offering>();  
  
    public void Initialize(DomainProviderSettings config)  
    {  
       var offer1 = new Offering()  
       {  
          Description = "My Domain Provider",  
          Name = "Offering 1",  
          ProviderID = ID,  
          MoreInfoUrl = new Uri("http://www.contoso.com"),  
          MembershipServiceName = "My Membership",  
          EulaUrl = new Uri("http://www.contoso.com"),  
       };  
  
       this.offerings.Add(offer1);  
       RegistryKey key =   
          Registry.LocalMachine.CreateSubKey(@"Software\Microsoft\Windows Server\Domain Manager\Settings");  
       key.Close();  
    }  
    ```  
  
9. 이전 단계에서 초기화 하는 서비스가 목록이 반환 GetOfferings 방법에 추가 합니다. 예제는 GetOfferings 방법을 보여 줍니다.  
  
    ```c#  
  
    public ReadOnlyCollection<Offering> GetOfferings()  
    {  
       return this.offerings.AsReadOnly();  
    }  
    ```  
  
10. 목록에서 제공 하 여 반환 FindOfferingForDomain 방법에 추가 합니다. 예제는 FindOfferingForDomain 방법을 보여 줍니다.  
  
    ```  
  
    public Offering FindOfferingForDomain(string domain)  
    {  
       // Return the offering that has the domain name.  
       return offerings[0];  
    }  
  
    ```  
  
11. 자격 증명은 제품에 액세스 하는 데 필요한 정의 SetCredentials 방법에 추가 합니다. 예제는 SetCredentials 방법을 보여 줍니다.  
  
    ```c#  
  
    private string currentUser { get; set; }  
    private string currentPassword { get; set; }  
  
    public bool SetCredentials(DomainNameRequest request,   
       DomainProviderCredentials credentials, bool validate)  
    {  
       currentUser = credentials.UserName;  
       currentPassword = credentials.Password;  
       if (validate)  
       {  
          return ValidateCredentials();  
       }  
  
       return true;  
    }  
    ```  
  
12. 추가 ValidateCredentials 방법에 정의 된 대로만 SetCredentials 자격 증명을 확인 합니다. 예제는 ValidateCredentials 방법을 보여 줍니다.  
  
    ```c#  
  
    public static readonly string offerUser = "user1@contoso.com";  
    public static readonly string offerPassword = "password1";  
  
    public bool ValidateCredentials()  
    {  
       if (IsUser())  
          return string.Equals(currentPassword, offerPassword);  
       else  
          return false;  
    }   
  
    private bool IsUser()  
    {  
       return string.Equals(currentUser, offerUser, StringComparison.OrdinalIgnoreCase);  
    }  
    ```  
  
13. 반환 요청에 지정 된 제공에서 지원 되는 루트 도메인 이름 목록을 GetAvailableDomainRoots 방법에 추가 합니다. 이 목록은 루트 도메인 이름 빈 수 없습니다. 예제는 GetAvailableDomainRoots 방법을 보여 줍니다.  
  
    ```c#  
  
    public ReadOnlyCollection<string> GetAvailableDomainRoots(DomainNameRequest request)  
    {  
       List<string> list = new List<string>();  
       list.Add("domain1.com");  
       list.Add("domain1.org");  
  
       return list.AsReadOnly();  
    }  
    ```  
  
14. 현재 사용자 이미 소유 하 고, 현재 제공에 상대적 도메인 이름 목록이 반환 GetUserDomainNames 방법에 추가 합니다. 이 목록이 빈 수 있습니다. 예제는 GetUserDomainNames 방법을 보여 줍니다.  
  
    ```c#  
  
    public static readonly string AvailableDomain1 = "available.domain1.com",  
       AvailableDomain2 = "available.domain2.com";  
    public static readonly string OccupiedDomain1 = "occupied.domain1.com",  
       OccupiedDomain2 = "occupied.domain2.com";  
  
    public ReadOnlyCollection<string> GetUserDomainNames(DomainNameRequest request)  
    {  
       var userDomains = new List<string>();  
       userDomains.Add(OccupiedDomain1);  
       userDomains.Add(AvailableDomain1);  
  
       return userDomains.AsReadOnly();  
    }  
    ```  
  
15. 지정 된 제공 수 있게 하는 도메인의 최대 수를 반환 GetUserDomainQuota 방법에 추가 합니다. 최대 적용할 수 없는 경우이 방법을 0을 반환 해야 합니다. GetUserDomainQuota 방법에는 다음과 같습니다.  
  
    ```c#  
  
    public int GetUserDomainQuota(DomainNameRequest request)  
    {  
       return 0;  
    }  
    ```  
  
16. 요청한 도메인 이름의 사용 가능 여부를 검사 CheckDomainAvailability 방법에 추가 하 고 제안 사항 목록이 반환할 수 있습니다. 예제는 CheckDomainAvailability 방법을 보여 줍니다.  
  
    ```c#  
  
    public bool CheckDomainAvailability(DomainNameRequest request,   
       out ReadOnlyCollection<string> suggestions)  
    {  
       suggestions = null;  
  
       return true;  
    }  
    ```  
  
17. 요청한 도메인 이름 커밋합니다 CommitDomain 방법에 추가 합니다. 이 방법 성공적으로 완료 사용자 계정에 연결 된 도메인 이름, 유지 관리 공급자 상태 작동이, 불완전 하 고 활성화 되는 공급자와 제공 인증서를 검색할 수 즉시 호출는 의미입니다. 예제는 CommitDomain 방법을 보여 줍니다.  
  
    ```c#  
  
    public DomainStatus CommitDomain(DomainNameRequest request)  
    {              
       ReadOnlyCollection<string> suggestions;  
       if (!CheckDomainAvailability(request, out suggestions))  
       {  
          throw new DomainException(FailureReason.InvalidDomainName, null, null);  
       }  
  
       return DomainStatus.Ready;  
    }  
    ```  
  
18. 사용자 도메인 이름을 해제 하려는 공급자에 게 알립니다 ReleaseDomain 방법에 추가 합니다. 예제는 ReleaseDomain 방법을 보여 줍니다.  
  
    ```c#  
  
    public bool ReleaseDomain(DomainNameRequest request)  
    {  
       return true;  
    }  
    ```  
  
19. 도메인 등록 워크플로에서 페이지를 방문 페이지의 URL을 반환 GetProviderLandingUrl 방법에 추가 합니다. 예제는 GetProviderLandingUrl 방법을 보여 줍니다.  
  
    ```c#  
  
    public Url GetProviderLandingUrl(DomainNameRequest request)  
    {  
       return new Url("www.contoso.com");  
    }  
    ```  
  
20. 도메인 유지 관리 작업에 사용 되는 IDomainMaintenanceProvider 인스턴스를 반환 GetDomainMaintenanceProvider 방법에 추가 합니다. 이 방법은 CommitDomain 방법에 성공적으로 후을 도메인 관리자가 시작 될 때 이라고 합니다. 예제는 GetDomainMaintenanceProvider 방법을 보여 줍니다.  
  
    ```c#  
  
    public IDomainMaintenanceProvider GetDomainMaintenanceProvider()  
    {  
       return new MyDomainMaintenanceProvider();  
    }  
    ```  
  
21. 프로젝트를 저장 하 고 절차에 추가 하기 때문에 닫습니다 하지 마십시오. 다음 절차 완료 될 때까지 프로젝트를 만들 수 없습니다.  
  
###  <a name="BKMK_DomainMaintenance"></a>IDomainMaintenanceProvider 인터페이스 구현을 조립에 추가  
 IDomainMaintenanceProvider 생성 된 후 도메인을 유지 하는 데 사용 됩니다.  
  
##### <a name="to-add-the-idomainmaintenanceprovider-code-to-the-assembly"></a>IDomainMaintenanceProvider 코드는 조립을 추가 하려면  
  
1.  도메인 유지 관리 공급자에 대 한 클래스 헤더를 추가 합니다. 공급자의 정의 이름 이전에 정의 GetDomainMaintenanceProvider 방법에서 이름과 일치 하는지 확인 합니다.  
  
    ```c#  
  
    public class MyDomainMaintenanceProvider : IDomainMaintenanceProvider  
    {  
    }  
    ```  
  
2.  활성 공급자 설정 정품 인증 방법에 추가 합니다. 예제 정품 인증 방법에 보여 줍니다.  
  
    ```c#  
  
    string DomainName { get; set; }  
    protected DomainProviderSettings Settings { get; set; }  
  
    public void Activate(DomainProviderSettings settings,   
       DomainNameConfiguration config, DomainProviderCredentials credentials)  
    {  
       Settings = settings;  
       SetCredentials(credentials);  
       DomainName = config.AutoConfiguredAnywhereAccessFullName.Punycode;  
    }  
    ```  
  
3.  모든 작업을 비활성화 하는 데 사용 되는 비활성화 메서드를 추가 합니다. 예제는 비활성화 방법을 보여 줍니다.  
  
    ```  
  
    public void Deactivate()  
    {  
       //Deactivate all actions  
    }  
  
    ```  
  
4.  업데이트를 사용자 자격 증명 SetCredentials 방법에 추가 합니다. 예를 들어, 더 이상 사용할 수 있는 자격 증명을 업데이트이 방법을 호출할 수 없습니다. 예제는 SetCredentials 방법을 보여 줍니다.  
  
    ```c#  
  
    protected DomainProviderCredentials Credentials { get; set; }  
  
    public bool SetCredentials(DomainProviderCredentials credentials)  
    {  
       this.Credentials = credentials;  
  
       return true;  
    }  
    ```  
  
5.  지정된 된 자격 증명을의 유효성을 검사 ValidateCredentials 방법에 추가 합니다. 예제는 ValidateCredentials 방법을 보여 줍니다.  
  
    ```c#  
  
    public static readonly string offerUser = "user1@contoso.com";  
    public static readonly string offerPassword = "password1";  
  
    public bool ValidateCredentials()  
    {  
       if (string.Equals(this.Credentials.UserName,   
          offerUser,   
          StringComparison.OrdinalIgnoreCase) &&   
             string.Equals(this.Credentials.Password, offerPassword))  
          return true;  
  
       return false;  
    }  
    ```  
  
6.  서버 외부 IP 주소를 반환 GetPublicAddress 방법에 추가 합니다. 예제는 GetPublicAddress 방법을 보여 줍니다.  
  
    ```c#  
  
    public IPAddress GetPublicIPAddress()  
    {  
       string PublicIP = "0.0.0.0";  
       using (RegistryKey key = ProductInfo.RegKey.OpenSubKey("Domain Manager\\Settings", true))  
       {  
          PublicIP = (key == null) ? "0.0.0.0" : key.GetValue("PublicIP", "0.0.0.0").ToString();  
       }  
       IPAddress ip = IPAddress.Parse(PublicIP);  
  
       if (PublicIP == "0.0.0.0")  
       {  
          string strHostName = Dns.GetHostName();  
          IPHostEntry ipEntry = Dns.GetHostEntry(strHostName);  
  
          IPAddress[] addr = ipEntry.AddressList;  
          foreach (IPAddress add in addr)  
          {  
             if (add.AddressFamily == AddressFamily.InterNetwork)  
             {  
                return add;  
             }  
          }  
       }  
       else  
       {  
          return IPAddress.Parse(PublicIP);  
       }  
  
       return null;    
    }  
    ```  
  
7.  현재 구성 되어 있는 도메인 이름에 대 한 인증서 요청을 제출 SubmitCertificateRequest 방법에 추가 합니다.  
  
    ```c#  
  
    string cert=null;  
  
    public void SubmitCertificateRequest(string certificateRequest)  
    {  
       cert = CertManaged.SubmitRequest(certificateRequest, CertCommon.CAServerFQDN + "\\" +      
          CertCommon.CAName,   
          Microsoft.WindowsServerSolutions.CertificateManagement.CRFlags.Base64Header,   
          CertCommon.CATemplate,   
          EncodingFlags.Base64);  
    }  
    ```  
  
8.  도메인 상태가 작동이 불완전 인증서 응답을 반환 GetCertificateResponse 방법에 추가 합니다. 이 방법은 인증서 갱신 요청 및 새로운 인증서 요청 둘 다에 대 한 이라고 합니다. 예제는 GetCertificateResponse 방법을 보여 줍니다.  
  
    ```c#  
  
    public string GetCertificateResponse(bool renew)  
    {  
       return cert;  
    }  
    ```  
  
9. 인증서 갱신 처리 SubmitRenewCertificateRequest 방법에 추가 합니다. 예제는 SubmitRenewCertificateRequest 방법을 보여 줍니다.  
  
    ```c#  
  
    public void SubmitRenewCertificateRequest()  
    {  
       // Add certificate renewal code   
    }  
    ```  
  
10. 업데이트 하는 공급자가 저장 되어 DNS 레코드 UpdateDNSRecords 방법에 추가 합니다. 예제는 UpdateDNS 방법을 보여 줍니다.  
  
    ```c#  
  
    public bool UpdateDnsRecords(IList<DnsRecord> records)  
    {  
       string UpdateDNS = "true";  
       using (RegistryKey key = ProductInfo.RegKey.OpenSubKey("Domain Manager\\Settings", true))  
       {  
          UpdateDNS = (key == null) ? "true" : key.GetValue("UpdateDNS", "true").ToString();  
       }  
  
       return UpdateDNS == "true";  
    }  
  
    ```  
  
11. 백 엔드 서비스의 연결을 설정 하려고 TestConnection 방법에 추가 합니다. 이 방법을 인증이 필요한 적절 한 예외 해야 수 하면 됩니다. 예제는 TestConnection 방법을 보여 줍니다.  
  
    ```c#  
  
    public bool TestConnection()  
    {  
       // Add code to test connection  
  
       return true;  
    }  
    ```  
  
12. 현재 상태는 도메인의 반환 GetDomainState 방법에 추가 합니다. 예제는 GetDomainState 방법을 보여 줍니다.  
  
    ```c#  
  
    public DomainState GetDomainState()  
    {  
       string domainstatus = "FullyOperational";  
       long expirationDate = 365;  
       using (RegistryKey key = ProductInfo.RegKey.OpenSubKey("Domain Manager\\Settings", true))  
       {  
          domainstatus = (key == null) ? "Ready" : key.GetValue("DomainStatus", "Ready").ToString();  
          expirationDate = Int64.Parse(key.GetValue("ExpirationDate", "365").ToString());  
       }  
  
       switch (domainstatus)  
       {  
          case "Failed":  
             return new DomainState(DomainStatus.Failed,   
                null,   
                DateTime.Now.AddDays(expirationDate));  
          case "Ready":  
             return new DomainState(DomainStatus.Ready,   
                null,   
                DateTime.Now.AddDays(expirationDate));  
          case "InRenewal":  
             return new DomainState(DomainStatus.InRenewal,   
                null,   
                DateTime.Now.AddDays(expirationDate));  
          case "InRenewalCustomerInterventionRequired":  
             return new DomainState(DomainStatus.InRenewalCustomerInterventionRequired,   
                null,   
                DateTime.Now.AddDays(expirationDate));  
          case "Pending":  
             return new DomainState(DomainStatus.Pending,   
                null,   
                DateTime.Now.AddDays(expirationDate));  
          case "PendingCustomerInterventionRequired":  
             return new DomainState(DomainStatus.PendingCustomerInterventionRequired,   
                null,   
                DateTime.Now.AddDays(expirationDate));  
          case "RenewalFailed":  
             return new DomainState(DomainStatus.RenewalFailed,   
                null,   
                DateTime.Now.AddDays(expirationDate));  
          default:  
             return new DomainState(DomainStatus.Unknown,   
                null,   
                DateTime.Now.AddDays(expirationDate));                   
          }  
    }  
    ```  
  
13. 현재 상태 인증서를 반환 GetCertificateState 방법에 추가 합니다. 예제는 GetCertificateState 방법을 보여 줍니다.  
  
    ```c#  
  
    public CertificateState GetCertificateState(bool renew)  
    {  
       return new CertificateState(CertificateStatus.Ready, string.Empty);  
    }  
    ```  
  
14. 저장 한 솔루션을 작성 합니다.  
  
###  <a name="BKMK_SignAssembly"></a>조립 Authenticode 서명으로 서명  
 운영 체제에 사용할 수 있도록는 조립 Authenticode 로그인을 해야 합니다. 로그인 하 여 조립에 대 한 자세한 내용은 참조 [Authenticode로 코드를 확인 하 고 서명](https://msdn.microsoft.com/library/ms537364\(VS.85\).aspx#SignCode)합니다.  
  
###  <a name="BKMK_InstallAssembly"></a>조립 참조 컴퓨터에 설치  
 참조 컴퓨터에서 폴더에 있는 조립을 놓습니다. 다음 단계에서를 레지스트리 입력 하는 때문에 폴더 경로 메모를 작성 합니다.  
  
### <a name="add-a-key-to-the-registry"></a>레지스트리 키 추가  
 특성 및는 조립의 위치를 정의 레지스트리 항목을 추가 합니다.  
  
##### <a name="to-add-a-key-to-the-registry"></a>레지스트리 키를 추가 하려면  
  
1.  참조 컴퓨터에서 클릭 **시작**, 입력 **regedit**를 누른 다음 **Enter**합니다.  
  
2.  왼쪽된 창에서 확장 **HKEY_LOCAL_MACHINE**, 확장 **소프트웨어**, 확장 **Microsoft**, 확장 **Windows Server**, 확장 **도메인 관리자**를 확장 한 다음 **공급자**합니다.  
  
3.  마우스 오른쪽 단추로 클릭 **공급자**를 가리킨 **새로**을 차례로 클릭 하 고 **키**합니다.  
  
4.  키 이름으로 공급자에 대 한 식별자를 입력 합니다. 식별자가 공급자의 8 단계에서에 대해 정의 된 GUID [IDomainSignupProvider 인터페이스 구현을 조립에 추가](Add-Third-Level-Domain-Names.md#BKMK_DomainSignup)합니다.  
  
5.  키 방금 만든 마우스 단추로 클릭 한 다음 **문자열 값**합니다.  
  
6.  입력 **조립** 문자열을 차례로 누르기 이름을 **Enter**합니다.  
  
7.  새을 마우스 오른쪽 단추로 클릭 **조립** 오른쪽 창에는 문자열와 클릭 한 다음 **수정**합니다.  
  
8.  전체 경로 조립 파일을 이전에 만든와 클릭 한 다음 입력 **확인**합니다.  
  
9. 다시 키를 마우스 오른쪽 단추로 클릭 한 다음 한 **문자열 값**합니다.  
  
10. 입력 **사용** 문자열을 차례로 누르기 이름을 **Enter**합니다.  
  
11. 새을 마우스 오른쪽 단추로 클릭 **사용** 오른쪽 창에는 문자열와 클릭 한 다음 **수정**합니다.  
  
12. 입력 **진정한**을 차례로 클릭 하 고 **확인**합니다.  
  
13. 다시 키를 마우스 오른쪽 단추로 클릭 한 다음 한 **문자열 값**합니다.  
  
14. 입력 **종류** 문자열을 차례로 누르기 이름을 **Enter**합니다.  
  
15. 새을 마우스 오른쪽 단추로 클릭 **종류** 오른쪽 창에는 문자열와 클릭 한 다음 **수정**합니다.  
  
16. 공급자는 조립에 정의 된의 클래스 전체 이름을 입력 하 고 클릭 한 다음 **확인**합니다.  
  
###  <a name="BKMK_RestartService"></a>Windows Server 도메인 이름 관리 서비스를 다시 시작  
 Windows Server 도메인 관리 서비스 공급자는 운영 체제에 사용할 수 있게 하려면 다시 시작 해야 합니다.  
  
##### <a name="restart-the-service"></a>서비스를 다시 시작  
  
1.  클릭 **시작**, 입력 **mmc**를 누른 다음 **Enter**합니다.  
  
2.  서비스 스냅인 나열 되지 않은 콘솔에서을 하는 경우 다음 단계를 완료 하 여 추가 합니다.  
  
    1.  클릭 **파일**을 차례로 클릭 하 고 **스냅인 추가/제거**합니다.  
  
    2.  **사용 가능한 스냅인** 목록에서 클릭 **서비스**, 차례로 클릭 하 고 **추가**합니다.  
  
    3.  에 **서비스** 대화 상자에 있는 **로컬 컴퓨터** 을 선택한 다음 클릭 **완료**합니다.  
  
    4.  클릭 **확인** 닫을 수 있는 **스냅인 추가/제거** 대화 상자가 합니다.  
  
3.  두 번 클릭 **서비스**, 아래로 스크롤하고 **Windows Server 도메인 관리**을 차례로 클릭 하 고 **서비스를 다시 시작**합니다.  
  
## <a name="see-also"></a>참조 하십시오  
 [만들기 및 이미지를 사용자 지정](Creating-and-Customizing-the-Image.md)   
 [추가로 사용자 지정](Additional-Customizations.md)   
 [배포에 대 한 이미지를 준비 중](Preparing-the-Image-for-Deployment.md)   
 [고객 만족도 테스트합니다.](Testing-the-Customer-Experience.md)