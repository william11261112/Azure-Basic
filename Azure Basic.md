# Chapter 1 - Azure Concepts
### **Module 1.硬體基礎架構**
![](https://i.imgur.com/h5QKpqo.png)
#### 1. Region
- 全球大約60幾個region，內部皆包含多個data center，data center間距離不會太遠。
#### 2. Region pair
- 為了在維護期間不間斷，兩region要300英里以上
#### 3. Geography
- 在不同地區快速選擇region
#### 4. Availability zone
- data center再次區分，有獨立的供電、冷卻系統。並非所有region都有。有zone就一定有三個以上。(增加可用性)
#### 5. Availability set
- 想要有zone但是沒辦法 ->機櫃分組
- Fault Domain(物理分組)
避免單點故障，最多3個fault domain
- Update Domain(邏輯分組)
避免server同時進行維護，最多設定20個
![](https://i.imgur.com/n9sAR8Q.png)
### **Module 2.Azure管理架構**
![](https://i.imgur.com/zlRmxrg.png)
###### *tenant(租用帳號)是一個總公司的概念
#### 1. Subsciption
- 帳單分離、功能分離
- ![](https://i.imgur.com/khi32xI.png)
#### 2. Resource Groups
- 同生命週期的放一起
#### 3. Management Groups
- 管理眾多Subscription




# Chapter 2 - Management Tools on Azure
### **Module 1. Azure Advisor**
- 根據使用者狀況給予建議
- 自動建議降低花費
- 自動分析網路架構、架構安全性、可用性
- 會提供詳細操作步驟
![](https://i.imgur.com/8Wtvnnv.png)
### **Module 2. Azure Resource Manager(ARM)**
#### 1. 什麼是ARM
- 針對resource group進行部屬跟管理
- 做建立資源、調整參數、權限控制、刪除資源
- 可自動生成格式(JSON檔)叫ARM template(ARM定義文件)
- 替雲端資源做組織化(同生命週期)
- 控制resource、跟resource group權限(只有相對應的使用者能訪問)
![](https://i.imgur.com/pwG5Oen.png)
#### 2. ARM流程
![](https://i.imgur.com/IUq9OiL.png)






# Chapter 3 - Azure Core Services
### **Module 1. Azure 運算服務**
#### 1. Virtual Machine
- 可建立自己的image(針對硬碟備份的快照，記錄安裝完作業系統硬碟狀態)
- 下圖右邊三個是需要Azure VM的時候
![](https://i.imgur.com/NYxAMlo.png)
#### 1-1. Virtual Machine Scale Sets
- 部屬VM跟控制數量
- 幫忙負擔vm，需要大量運算資源可自動擴編，反之可自動縮減。
![](https://i.imgur.com/rDjAv0A.png)
#### 2. Azure Container Service
- 不需要作業系統的虛擬環境，部屬跟啟動特別快，只會使用一個應用程式 container是PaaS
![](https://i.imgur.com/sC6OmqW.png)
![](https://i.imgur.com/RyZyorB.png)
#### 2-1. ACR(Azure Container Registy)
- Container需要image才能用，ACR就是用來存放image跟管理的服務還有版本控管
- 支援跨區域的部屬
- 安全性(透過azure的身分管理系統管理訪問權限)
- 結合其他container的服務，Azure DevOP可直接選取ACR直接更新image跟image的版本控管
![](https://i.imgur.com/SwLsOop.png)
#### 2-2. ACI(Azure Container Instance)
- 託管Container，託管底層運算資源、作業系統、container運作引擎
- PaaS服務，底層作業系統為WINDOWS、LINUX
- 將應用程式獨立
- 自己選擇調整資源
- ![](https://i.imgur.com/qB4FSL2.png)
#### 2-3. AKS(Azure Kubernetes Service/K8S)
- 幫助處理container跟底層機器跟擴展需求
- Kubrenetes cluster底層機器兩種功能
> Master Node:接收指令，指揮流量
> Worker Node:負責完成Master Node指派的工作
- 自動選擇負載低的機器做container的部屬
- 建立負載平衡器
- 監控各層級負載
- ![](https://i.imgur.com/RfDNOVK.png)
#### 3. Azure Serverless Service
- 無伺服器運算架構
#### 3-1. Azure App Service
- 網站伺服器託管服務(PaaS)
- 上傳網頁原始碼就能架設網站
- 支援多程式語言
- 支援託管Container架構的網站應用程式(windows/linux的conatiner都可)
- 串接CI(Continuous integration)/CD(Continuous Deployment)的流程
- 高可用性，會自動處理故障轉移
![](https://i.imgur.com/dDYDypc.png)
#### 3-2. Azure Function
- 上傳程式碼，替我們跑程式碼邏輯(專注在程式碼部分就好)
- 透過時間排程、URL、或者是Azure其他服務進行觸發，因為內建URL也可變為後端API
- 自行調整規模來達到需求
![](https://i.imgur.com/5SJi7Fv.png)
#### 3-3. Azure Logic Apps
- 建立自動化工作流程
- 簡化的視覺化設計
- 提供連接器(為流程提供觸發的手段，讓Logic APP連接到不同的系統、應用程式等等)
- 也可透過連接外部API或Azure Function達到想要的動作
![](https://i.imgur.com/H3s7nOF.png)
#### 3-4. Azure Event Grid
- 事件處理器
- 透過訂閱事件，取得Azure資源做操作
- 可在Azure Portal頁面做設定，將Event內容傳送到不同端點
- 串接Azure服務或應用程式達到自動化效果
- 自動選擇最大可用性做部屬
![](https://i.imgur.com/s4mGe5S.png)
![](https://i.imgur.com/Qlv1LtK.png)
- 從左邊Azure有支援Event Gird服務中開啟訂閱事件，透過Event Grid 路由設定送到目標端點(Logic App或Azure Function等等)
### **Module 2. Azure 網路服務**
#### 1. Azure Virtual Network
- Azure VNet是SDN(Software-Defined Network)，可隨時做動態設定調整跟監控流量
- 隔離不同使用者的網路環境
- 同一個虛擬網路又能繼續切割成subnet
- 設定安全性的規則，用Network Security Group
- ![](https://i.imgur.com/VV4JxR9.png)
- VNet的使用規則(上述範例有256*256個IP能用)
![](https://i.imgur.com/WDHwRWy.png)
- Public IP Address(為浮動，固定要申請)
- Azure上申請Public IP的服務就是Public IP Addresses，將其套用在雲端資源的網路介面卡上
- VM的網路介面卡可同時擁有Public/Private IP，VM有可同時有多張網路介面卡
![](https://i.imgur.com/O0YuxQS.png)
- Subnets為VNet IP分段(可能同虛擬網路的機器有不同用途)
#### 1-1. Network Security Group
- 過濾流量進出
- 預設外部流量會被擋(所以要設定流量規則)
- 可以針對IP跟Port Number做限制
![](https://i.imgur.com/rFCj0yo.png)
![](https://i.imgur.com/KntAAcH.png)
#### 1-2. VNet Peering 
- 兩虛擬網路可直接溝通
- 用Azure backbone網路就不用設定Public IP
- 不同Region的VM也能達到內部網路互通的效果
![](https://i.imgur.com/0FnKdjp.png)
![](https://i.imgur.com/c23RUqc.png)
- 用Private IP識別身分就好，降低風險
#### 1-3. Virtual Network Gateway
- 建立加密連線通道
- Azure會自動建立兩個以上Gateway，只要切割subnet給VNG就會自動託管多個Gateway的底層架構
- 會要求選SKU(底層資源等級)
- 可應用在圖右下那幾個層面上
![](https://i.imgur.com/KnDU6A3.png)
- VPN
>Site to Site VPN(較適合固定地端網路環境/固定IP):
1.要先切出Gateway Subnet
2.建立Local Network Gateway，對應地端router
3.地端router做加密設定，Azure虛擬網路設定路由
4.注意Private IP不能重疊
![](https://i.imgur.com/ZnBXrbD.png)
>Point to Site VPN(不固定IP):
1.要先切出Gateway Subnet
2.建立加密憑證上傳到Virtual Network Gateway，用戶端電腦也要安裝憑證
3.設定用戶端IP範圍
4.Virtual Network Gateway會分派Private IP到電腦
![](https://i.imgur.com/AhZEmK8.png)
#### 1-4. ExpressRoute
- 用專線連接Azure虛擬網路
- 用實體網路線路連接到Microsoft邊緣站點(可很快連到機房網路)
- 預設會有兩條線路，連到邊緣站點跟不同的路由器，確保可用性
- 可支援跨區域連線
- 支援多種頻寬選擇(可修改頻寬，不停機)
![](https://i.imgur.com/N9GJMwg.png)
![](https://i.imgur.com/xTj63WM.png)
#### 2. Azure Load Balancing Service
- Load Balancing
![](https://i.imgur.com/Z24QMdz.png)
- OSI Model
![](https://i.imgur.com/msf9tlH.png)
#### 2-1. Azure Load Balancer
- 應用在傳輸層，導流TCP/UDP流量
- 沒分析封包，所以超快
![](https://i.imgur.com/o7en4iF.png)
#### 2-2. Application Gateway
- 在應用層，完整的封包解密
- 為網站設計的負載平衡器
- Azure WAF可擋sql injection、crosssite script
- SSL憑證可上傳到Application Gateway
- Sticky Session發送cookie，紀錄客戶端資訊
- 是PaaS服務
#### Azure Load Balancer/Application Gateway
![](https://i.imgur.com/WpM7Hz5.png)
#### 3. What is DNS?
- Domain Name System
- 先找Host Table(Host Table會記錄Domain Name解析結果)
- 先搜頂級域名(.com)再來是次級域名(.google)
- 用UDP找，所以超快
![](https://i.imgur.com/R134U7J.png)
#### 3-1. App Service Domain
- Azure上註冊網域的服務
- 幫你向Godaddy註冊
- 支援多頂級網域
- 可自動續約網域
- 幫你在WHOIS保護個資
![](https://i.imgur.com/P1mqZD4.png)
#### 3-2. Azure DNS
- 域名託管服務
- 紀錄DNS Record(A type是IPv4格式)
- Azure在全球有不同Name Server，提供高解析速度
- 支援託管Private域名，只能在VNet用
- 有權限控管，Resource Lock可鎖Azure DNS的資源，減少操作失誤跟惡意攻擊
![](https://i.imgur.com/Yvhz7m9.png)
### **Module 3. Azure 儲存類型服務**
#### 1. Storage Type
- Block Storage
>將記憶體切成同樣大小，把檔案隨機放入Block內，記住Block ID，檔案要用的時候將Block ID 串起來。常見連接形式有硬碟、fiber、iSCSI。為實體跟虛擬機器的儲存空間，裝載作業系統跟應用程式。
- File Storage 
>要找檔案就必須先找檔案目錄，常見連接方式NFS、SMB透過網路連接檔案系統，可共享檔案內容。

- Object Storage
>物件導向儲存體，會針對檔案整體進行儲存，每份檔案都有Metadata來紀錄檔案各種資料。儲存體跟檔案名稱必須獨一無二，因為要產生URL，之後就透過HTTP或API的方式取得檔案。極高的可用性和無限的拓展性。

![](https://i.imgur.com/JmsCX4D.png)
#### 2. Storage Account
![](https://i.imgur.com/3WyHTT0.png)
- 針對儲存空間服務的管理單位
- 儲存資料的時候還要選Replication Option，Azure會根據這個選項自動備份到不同的Region存放，增加耐久跟可用性
- 支援資料保護機制
- 支援靜態加密
- Replication Options
>LRS:再建Storage Account的Region的資料中心進行3次備份，成本最低。
>ZRS:在同Region中的不同Avalibility Zone，額外備份3份，有更高可用性。
>GRS:跨Region的LRS，所以會有6份備份，第二個Region是備用，所以沒辦法直接取用檔案，原Region掛掉才能用
>GZRS:GRS+ZRS會有6份備份，第二個Region是備用，所以沒辦法直接取用檔案，原Region掛掉才能用
>RA-GRS:以GRS為基底，但提供第二個讀取連結，可選近Region一點的來讀取檔案
>RA-GZRS:以GZRS為基底，但提供第二個讀取連結，可選近Region一點的來讀取檔案

![](https://i.imgur.com/YrMJcBH.png)
- SAS(Shared Access Signature)
數位憑證，像加密金鑰
>1. 使用者先設定好可存取的服務，勾選可允需操作行為
>2. 可為數位憑證作有效期限
>3. 可設定傳輸協議
>4. 設定好後產出SAS

![](https://i.imgur.com/VXOsxXn.png)

#### 3. Disk
- 提供虛擬硬碟
- 在Replication Options中預設用LRS
- HDD/SSD
- 支援snapshot，快速備份跟還原
- 靜態加密
#### 4. Blob Storage
- Object類型儲存服務，有container(這裡指存放檔案容器)
- 享有replication option
- 產生URL
- 可架設靜態網站
- 圖右下為container權限，blob是有url才能存取
![](https://i.imgur.com/H0se3HH.png)
- Access Tier(訪問等級)
>HOT:頻繁存取檔案，立刻讀取檔案
>COLD:不頻繁存取檔案，立刻讀取檔案
>ARCHIVE:幾乎不用檔案，用磁帶存取檔案，所以超慢

![](https://i.imgur.com/ZG6cXDo.png)
- Lifecycle Management
預先設定好檔案生命週期，依時間調整Access Tier
![](https://i.imgur.com/7YX7cjQ.png)
#### 5. Files Share
- 透過網路共享協定，在我們的電腦中儲存檔案
- 支援的協定:SMB/NFS
- 支援多台裝置掛載同一儲存空間
- 效能等級
>1. Premium(SSD)
>2. Transaction optimized
>3. Hot
>4. Cold
- Azure File Snyc
可安裝代理應用程式，將windows server做快取使用，減少流量成本跟網路延遲
![](https://i.imgur.com/k06YXRR.png)
#### 6. Azure Storage Tools
- Azure Storage Explorer
>1. 管理不同的儲存服務，跨region跟subscirbtion也可以
>2. 可操作新的功能
>3. 圖形化介面
>4. 用Azure AD控制訪問權限
- AZcopy
>1. Command Line介面(windows/linux/macos)
>2. 提供兩種身分驗證(Azure AD/SAS Token)
>3. 只支援Blob Storage跟Files Share
>4. 指令會記錄工作狀態(Error File/Plan File負責復原)

![](https://i.imgur.com/NL0TKLn.png)




# Chapter 4 - Security and Identity
### **Module 1. Azure 虛擬網路安全性**
- Perimeter layer(外圍層)
網路環境外部保護，流量進雲端之前就做檢查
- Networking layer(網路層)
網路環境內部保護，進入雲端後過濾不合理流量
#### 1. Azure Bastion
- 做為跳板，架設在Virtual Network中，可使用Azure Bastion連到VM
- PaaS服務，基於TLS安全傳輸協議，支援SSH/RDP傳輸協議
- 用瀏覽器操作
- 不用Public IP，不會被外部攻擊
![](https://i.imgur.com/wb0mYj1.png)
#### 2. Azure Firewall
- 屬託管服務
- 可設定過濾域名規則，網路溝通做IP轉換，管理多Public IP
- Azure Monitor分析Log(所有進出網路流量)，可設定威脅警報
![](https://i.imgur.com/P6tPPtK.png)
![](https://i.imgur.com/VD4yCod.png)
#### 3. Azure WAF(Web Application Firewall)
- 替網站伺服器做防火牆，可直接在Load Balance上使用
- 支援服務
>1. Application Gateway
>2. Front Door
>3. Azure CDN(全球化部屬站點)
- 可建立客製化防護範圍
![](https://i.imgur.com/RXcaYx6.png)
![](https://i.imgur.com/2asVNfG.png)
#### 4. Azure DDoS Protection
- 有分服務等級，Standard Tier提供專業客服，還有cost protection(防自動擴編花太多錢)
![](https://i.imgur.com/IdP8XMW.png)
![](https://i.imgur.com/UJwucPB.png)
### **Module 2. Azure 身分認證機制**
- MFA(Multi-Factor Authentication兩步驟驗證)
- Azure AD管理組織內群組，設定使用者權限
- Azure RBAC是權限管理機制，主要授權Azure AD User使用雲端資源
![](https://i.imgur.com/xyhOwz8.png)
#### 1. Azure Active Directory(Azure AD)
- 建立身分給使用者，讓使用者透過金鑰或密碼使用服務
- 用Azure AD註冊的裝置或應用程式，透過Azure AD賦予權限
- 用Azure AD Connect連接地端帳號，達到混合雲。只要一組帳密就能連接雲端跟地端
- 帳號管理者(Azure AD Role)賦予使用者權限
![](https://i.imgur.com/uG0HNiZ.png)
- Azure AD Role
>1. Global Administrater:屬最高管理者
>2. User Administrater:管理Azure AD中的使用者
>3. Billing Administrater:查看帳單，管理subscription
>4. Application Developer:管理應用程式
>5. Custom Role:可自行定義

![](https://i.imgur.com/MLnhLTk.png)
- Azure AD Feature 
>1. 支援MFA
>2. 多種裝置可註冊到Azure AD，讓設備有存取平台服務的功能
>3. Application Management:用程式碼的方式註冊，讓應用程式存取雲端資源
>4. Single Sign ON(SSO):用同一組帳號登入不同的系統
>5. B2B:讓其他Azure AD 的使用者進來做共同作業
>6. B2C:支援外部帳號驗證系統
### **Module 3. Azure 資源管理辦法**
#### 1. Azure RBAC
- 設定Azure RBAC要三元素
>1. Scope(資源跟管理單位)，會產生繼承效果(上層有權限，下面的都能用)
>2. Role Type:
    - Owner -> 擁有Scope所有操作權限
    - Contributer -> Scope所有操作權限，但不能管理Scope權限相關的控制
    - Reader -> 只能瀏覽資源設定跟資源權限
    - 一樣有Custom Role
>3. Object:權限賦予對象
    - User
    - Application
    - Managed Identity:賦予其他雲端資源角色，例如VM要跟DataBase溝通

![](https://i.imgur.com/K4yIQsF.png)
#### 2. Resource Lock
- 資源安全鎖，防止資源被竄改
- Delete Lock:不論權限，只能更新資源，無法刪除
- ReadOnly Lock:不論權限，無法更新資源，無法刪除
- Lock Scope:套用範圍跟RBAC很像，產生繼承效果(上層有作用，下面一併用同規則)
![](https://i.imgur.com/VbdIvFj.png)
#### 3. Azure Policy
- 管理標準、定義授權、檢查合規性
- 提供Dashboard，圖形化介面
- 內建合規性項目、一些標準檢查
- 可將多個Policy組合(Initiative Definition)包含各種合規性檢查，讓使用者套用
![](https://i.imgur.com/QTOpDWd.png)
- Policy and Initiative Assignment
套用範圍如下圖，不能針對單一雲端資源做套用，一樣有繼承關係
![](https://i.imgur.com/VL1yQGq.png)





# Chapter 5 - Monitoring
### **Module 1. Azure Monitor監控服務**
- 全方面的監控
- 可使用代理程式來收集Log上傳分析
- 圖表視覺化呈現
- 可輸出Monitor收集的資料
![](https://i.imgur.com/bogyTOV.png)
- 運作流程如下
![](https://i.imgur.com/Gyzjr2w.png)
#### 1. Metrics Explorer
- 監控數據，做出圖表
- 圖表設定欄位
- 提供多圖表類型
- 添加圖表到DashBoard
#### 2. Log Analytics
- Log Analytics Workspace
1. 建立Log Analytics Workspace，系統或代理程式收集到的Log丟進去
2. 分析Log檔案產生對應的Tables
3. 用KQL(類SQL)語法做查詢
![](https://i.imgur.com/LfmPebq.png)
- Log Analytics
1. 是Azure上分析Log的工具，可在瀏覽器執行操作
2. 靠KQL語法進行操作
3. 將查詢出的Log做成圖表
4. 支援輸出查詢結果
![](https://i.imgur.com/W0dOeGy.png)
#### 3. Application Insights
- 即時監控應用程式
- 主要用內嵌程式碼(SDK)收集/傳送資料
- 監控項目多
- 數據呈現功能很多
![](https://i.imgur.com/GiigI7I.png)
- 運作流程
![](https://i.imgur.com/xzCnzeX.png)
#### 4. Alerts and Actions
- Alerts Rule
1. 設定監控目標以及警報的標準
2. 可針對單一資源，或整個資源單位做監控
3. 設定警報觸發條件
4. 設定相對應執行行為(Action Group)
![](https://i.imgur.com/NQxAILZ.png)

![](https://i.imgur.com/d0lo9Pa.png)
### **Module 2. Azure 雲端狀態監控服務(Service Health)**
![](https://i.imgur.com/7UqYfgm.png)
### **Module 3. Azure Virtual Network監控工具(Network Watcher)**
- 自動監控跟呈現網路拓樸關係圖，可以監控VM還有其他服務連接狀況
- 提供診斷工具
- 提供Network Security Group的Log，可以監測Virtual Network所有流量進出
![](https://i.imgur.com/g3w0Kyj.png)





# Chapter 6 - Backup and Recovery
### **Module 1. DR Concept 災難備援**
- Disaster Recovery
1. Backup & Recovery
定期備份，可是要另外找地方存放資料。如果存放位置根伺服器一起，伺服器爆掉備份檔也不能用。
2. Remote Redundancy
異地備援，將備份檔案存在不同地方，屬高可用性(HA)
3. Active & Active
架構面DR解決方案，將運算資源放在不同地方，屬高可用性(HA)

上述方法都是為了達成BC(Business Continuity業務不中斷)
- RTO & RPO(為了客觀考慮成本)
RTO(Recovery Time Objective)
復原架構或資料的預期時間，會有停機時間問題
RPO(Recovery Point Objective)
故障到上個還原點的時間，會有Data Loss的問題

![](https://i.imgur.com/AybwpMZ.png)
### **Module 2. Azure Backup & Recovery Service**
- Azure Backup
排程備份資料庫
- Azure Site Recovery
異地備援
- Recovery Service Vault
1. 存放Azure Backup跟Azure Site Recovery備份出來的快照
2. 預設會有加密處理(有平台加密金鑰或自己設金鑰也可以)
3. 跨區域存放資料，soft delete 14天可還原資料，不會隨便被刪除
4. 很好管理
5. supports Azure Virtual Machines, SQL in Azure VM, AzureFiles, SAP HANA in Azure VM, Azure Backup Server, Azure Backup Agent, and DPM

![](https://i.imgur.com/NpkQsjM.png)
### **Module 3. Azure Backup**
- 支援VM/Blob/Azure File Share
- 無限擴展儲存空間
- 傳輸加密靜態加密
- 中央化集中管理平台， 支援地端跟雲端資料備份
- 支援備份時間排程跟備份要保留多久(Backup Policy)
- 用快照還原

![](https://i.imgur.com/4EwKQvg.png)
- 運作方式
![](https://i.imgur.com/qNQJLEG.png)
- 資料復原過程
![](https://i.imgur.com/X0kJiFN.png)
### **Module 4. Azure Site Recovery**
- 替VM做異地備援
- 支援Hypervisor備份
- 災難演習
- 故障轉移(Failover)，將原本VM停機，移到新VM進行工作
![](https://i.imgur.com/N5wgGeL.png)
- 運作過程
![](https://i.imgur.com/4jMwB4H.png)




# 講師上課DAY 1. 儲存服務、運算服務
### Azure Storage Service
![](https://i.imgur.com/BKHostK.png)
- Queue Storage:
此儲存服務主要是確保雙方在傳遞訊息時都能確實收到訊息,假設有一方的收訊不好,傳遞的訊息會先儲存在queue中，等到對方收訊好的時候再次傳送，QueueStorage也很適合用來暫存訊息(因為有DeadLetter Queue)
*DeadLetter:無效信件佇列的目的，是保留無法傳遞至任何收件者的訊息，或是無法加以處理的訊息。 隨後可以從 DLQ 移除訊息並加以檢查。 透過運算子的協助，應用程式可能會更正問題並重新提交訊息、記錄發生錯誤及採取更正動作。
### Azure Disk Storage
![](https://i.imgur.com/ivpSMhz.png)
- Block
實體，光纖，iSCSI
- File
連接方式NFS、SMB透過網路連接檔案系統，可共享檔案內容。
- Object
Metadata來紀錄檔案各種資料。儲存體跟檔案名稱必須獨一無二，因為要產生URL，之後就透過HTTP或API的方式取得檔案。
*ex.Dog/Dog.jpg與Dog1/Dog.jpg,對物件的儲存體來說,他其實是沒有重複到的,因為它會像式Dog/Dog.jpg這樣整個的形式去做儲存,所以也符合每個檔案都是獨一無二這個情形

- Azure Disk Storage(Block)
>- 因底層架構不同,所以Disk並不屬於StorageAccount的管理範圍
>- 通常為LRS
>- 選擇硬碟時，會考慮IOPS、Throughput
>IOPS(Input/Output per Secend):讀寫資料時的最大量
>Throughput:傳輸資料最大量
>- SnapShot:快照備份，將當下的狀態備份
>- 支援靜態加密
### Azure Storage Account
- 是一個管理單位
- Blob Storage、Files Share、Table、Queue、Data Lake
- Storage Account種類
![](https://i.imgur.com/KX1gDgt.png)
- SecureStorage
![](https://i.imgur.com/qN9IiLO.png)
1. Authentication with AzureAD&AzureRBAC
2. SharedAccessSignatures(SAS)
3. SharedKey:共用金鑰
4. Azure Key Vault:儲存敏感性資料，要輸密碼不需要明文輸入，可呼叫key vault直接套進去(secret)
5. Client-side Encryption:還未上傳時做加密
6. CORS(跨原始來源資源共享):當A網站需要用到B網站的資料時,B網站就需要開CORS,讓A網站透過http協議的傳輸方式(GET.POST等等)來進行資料存取
![](https://i.imgur.com/2xAzBZ4.png)
*Max age的時間是以秒為單位
### Azure Blob Storage
- 當我們用blob storage去架設網站的時候,azure會幫我們生成兩個container,分別是web和log,幫我們生成一個靜態網站網址,我們就可以在$web的container裡放html檔案,透過網址的方式去存取到我們的靜態網頁
### Azure Files and File sync
#### 1. Files share Portocols(SMB/NFS)
- 同屬第七層(Application Layer)
![](https://i.imgur.com/cwljAnb.png)
#### 2. Share Snapshot
![](https://i.imgur.com/h6JPRLS.png)
- READ-Only
- 最多200張快照，要用新的snapshot要先刪除舊的
### Azure Storage Tools
#### 1. Azure Storage Explorer
#### 2. AZcopy
### Azure Data transfer Service
#### 1. Azure Data Box
- 他可以把TB等級的巨量資料migrate到雲端上
ex.假設你需要這個服務,微軟就會把這個機器寄到你家,你把需要存取的資料放入寄回給微軟,他就會幫你把這些資料上到cloud裡面,而且都會有AES加密以確保資料安全
![](https://i.imgur.com/xaw4Yyl.png)
#### 2. Azure Import Service
- 幫你把硬碟運送到Azure的DataCenter,也可以幫你把資料從blob之類的儲存體轉換到你的硬碟儲存,直接運輸到你內部部屬的網站
![](https://i.imgur.com/DqkD6KC.png)




# 講師上課DAY 2. 資料庫服務
### What is Data?
- structured data
所有的資料有固定格式，先定義好結構(MS SQL / MySQL)
- semi-structured data
做資料存放不用事先定義，事後可用特定語法找資料(COSMO DB/MONGO DB)NO SQL的DATABASE
- unstructured data
檔案格式存放不受任何限制(BLOB Storage)
![](https://i.imgur.com/hkiMrD2.png)
### DataBase Introduction
![](https://i.imgur.com/YF05ItG.png)
- Relational Database(關聯式資料庫)
- No-SQL Database
![](https://i.imgur.com/oqMZXDx.png)
### RDP vs No-SQL
![](https://i.imgur.com/Zmu7LGt.png)
- scalability
>vertical:是指想要擴展的話必須買更大機器
>horizontal:需求不足會叫更多機器
### Database Decision
![](https://i.imgur.com/Yn6r9ou.png)

![](https://i.imgur.com/MGjv5A0.png)
### Introduction to SQL
![](https://i.imgur.com/9rlmrrG.png)
### SQL Statement types
- 特性與結構
![](https://i.imgur.com/3nfhEdK.png)
### Database solution
- On-premise
- Host
- Managed
![](https://i.imgur.com/RerIKjC.png)
### Database service provide by Azure
![](https://i.imgur.com/StuL8CN.png)
- SQL Database、SQL Database for MySQL、SQL Database for PostgreSQL(結構化資料庫，但資料庫引擎不一樣)
- Cosmos DB：NoSQL的database，可以和多種市面上的DB做整合使用
### SQL Editer
- 最常用的是SSMS，只能對微軟的電腦做使用
![](https://i.imgur.com/4A7yU1V.png)
### Azure SQL Family
- PaaS服務不受版本限制
- 有高可用性(會建立自動化備份、異地備援、資料保留)
![](https://i.imgur.com/5q3QIQU.png)
### Azure SQL Database
- 屬於全託管服務(自動化備份、point-in-time某個時間點的資料庫重新建置、跨區域複寫、failover)
- 計價方式(vCore based、DTU Based根據capacity unit做計費)
- TDE靜態加密
- Service tier 
>General purpose - 專門為一般工作負載做設計
>Business Critical - 專門給業務，需要高交易率、低延遲
>Hyperscale - 超大規模資料庫，可調整運算能力

![](https://i.imgur.com/TET6JwH.png)
### Database Resource Type
- Single Database
可以在Database建一個資料庫，建資料庫時是獨立的，以DTU、vCore為基礎模型，兩者都可以選擇。
- Elastic Pools
可以管理及調整價格性能，彈性較高
- Database Server
可設定防火牆、auto-failover規則、管理登入、設定威脅偵測
![](https://i.imgur.com/yBVovP0.png)
### Key Difference 
- Serverless：可以自動化的擴展，沒辦法預期使用量、在測試期間、使用量低就使用
- Provisioned：可以預先分配，依照原本設定的條件做限制擴展，預測使用量、需要高計算使用量就適合用Provisioned，以小時計價，可以快速調整運算能力
- 只有single database才有serverless
![](https://i.imgur.com/c5XlI1X.png)

![](https://i.imgur.com/JpcjYFr.png)
### Azure CosmosDB
- Consistency(支援5種一致性)，右下部分
根據需求來選擇database，能夠容許多少的資料延遲想要資料是最新狀態稱為強一致性： strong consistency
有可能會讀到舊的資料，因為更新速度太慢稱為最終一致性：eventual consistency
- 只有Cosmos DB支援五種一致性，其它最多只有兩種。
![](https://i.imgur.com/07t1HXX.png)
### Azure Cosmos DB Entities
- 往右對照
![](https://i.imgur.com/R3fjfHh.png)




# 講師上課DAY 3. 網路服務
### Azure virtual network
- 提供邏輯空間
- CIDR是vnet的範圍，切出的範圍(/2、/29)
- Vnet必須在同region
- 切subnet時azure會保留前四個(10.0.0.0到10.0.0.3)跟最後一個ip位置(10.0.0.255)
### Route table
![](https://i.imgur.com/5xG0hvu.png)
- Route name (規則名)
- Address prefix (位置)
- Next hop type (怎麼去)
- Azure default table
![](https://i.imgur.com/A28XcJU.png)
### NAT Gateway
- 機器無聯網能力但想安裝套件(想聯網)
- 要新增規則到route table
![](https://i.imgur.com/j0t39VQ.png)
- SNAT
![](https://i.imgur.com/XiLhP6H.png)
- DNAT
![](https://i.imgur.com/KFQf3iT.png)
### Bastion host
- 機器無聯網能力，透過bastion去連機器(RDP/SSH)
![](https://i.imgur.com/QMMM2Yv.png)
### Public IP Address
- 派發在網卡和load balancer內，獨立於VM的個體
### Network Interface
- 有私人、共用ip
- 實體位置(mac address)
![](https://i.imgur.com/azePDQL.png)
### Network Security Group
- subnet和網路介面的防火牆
![](https://i.imgur.com/eNERj2M.png)
### NSG Flow Log
- 紀錄nsg的流量進出
![](https://i.imgur.com/xS5E33c.png)
### Virtual Network Gateway
![](https://i.imgur.com/dMU53mI.png)
- 地端也需要local network Gateway
- S2S/P2S
### Azure Express Route
- 地端與電信商合作牽專線
![](https://i.imgur.com/7lR0gQg.png)
### Vnet Peering 
- Vnet對Vnet直接溝通
- CIDR range不能重複
- 只能是一對一
![](https://i.imgur.com/F6HTGom.png)

![](https://i.imgur.com/VS7U9ik.png)
- Vnet最多建立125個peering
![](https://i.imgur.com/sm1qR6s.png)
### Azure Service Endpoint
- 走內部網路要求服務
![](https://i.imgur.com/yjc9Lcx.png)




# 講師上課DAY 4. 負載平衡、DNS、快取 CDN
### Azure load balance service
- Azure load balancer
- Traffic Manager
- Application Gateway
- Front door 
![](https://i.imgur.com/EaYfPpG.png)
### Azure Load Balancer 
- 屬第四層
- 導流tcp/udp
- PaaS服務、兼具高可用、高擴展
- 具備health track(機器無法回應停止導流到他身上，突然活過來的話會繼續導流到他身上)
- 不可跨vnet
![](https://i.imgur.com/V2hRcXi.png)
- SKU分為Basic/Standard
![](https://i.imgur.com/eu9SV7k.png)

![](https://i.imgur.com/5TjMnbb.png)
### Application Gateway
- 屬第七層
- 流量走http/https
![](https://i.imgur.com/4gT11mv.png)(要背)

![](https://i.imgur.com/ZkjgSom.png)

![](https://i.imgur.com/SBJYzzX.png)
### Azure Web Application Firewall
- 可放在application gateway、front door、Azure CDN
- 可自訂規則
![](https://i.imgur.com/IT3L8xx.png)

![](https://i.imgur.com/q3R6PLt.png)

![](https://i.imgur.com/T4AHDqE.png)
### Comparison
![](https://i.imgur.com/Lb6sZ4h.png)
### Traffic Manager
- 屬第七層
- 
### Cache
- 加速讀取速度
- 大幅降低原始資料庫負載
- 有分client side / server side
![](https://i.imgur.com/jKI52KM.png)
### Data Journey
![](https://i.imgur.com/UQ1VYJ5.png)
### CDN
![](https://i.imgur.com/dqQmM9t.png)

![](https://i.imgur.com/38Rzhpl.png)
### Cache rule
- 物件存留、壓縮(compression)、允許/拒絕region流量(geo-filtering)
![](https://i.imgur.com/d2DkJhI.png)
### Database Catching
- 建redis cache(常見在電商)
- 資料讀取分散，分擔database壓力
![](https://i.imgur.com/xkP3Yzr.png)
- Primary node : 寫入、刪除
- Replica node : 讀取
- 非同步所以會有延遲(小)
![](https://i.imgur.com/0qmbJTX.png)
### Scaling on Azure
### High Avalibility(HA)
- 高可用性因素
>Recoverbility : 出錯後回復能力(備援)
>Fault Tolerance : 容錯能力(防單點故障)
>Scalability : 擴展能力
- 停機時間(downtime)
>預期性
>非預期
![](https://i.imgur.com/3QdbVDc.png)
- RTO & RPO(為了客觀考慮成本)
RTO(Recovery Time Objective)
復原架構或資料的預期時間，會有停機時間問題
RPO(Recovery Point Objective)
故障到上個還原點的時間，會有Data Loss的問題
![](https://i.imgur.com/ICCPJpE.png)
### Auto Scaling on Azure 
![](https://i.imgur.com/LVSiXr8.png)
### VMSS(Virtual Machine Scal Set)
![](https://i.imgur.com/1DrZqk8.png)
![](https://i.imgur.com/KwnrC2V.png)
![](https://i.imgur.com/5jGe2Ce.png)
- 擴展規則(關機器關哪台)
![](https://i.imgur.com/p20t8V5.png)
### Setup VMSS - Management
- Automatic
立即更新機器、但順序隨機
- Manual
開起來的vm需要手動更新
- Rolling
有按鈕可以一次做更新

# 講師上課DAY 5. 監控服務、防火牆 
### Monitor
- 可分析訪問習慣
- 知道需求多寡
![](https://i.imgur.com/0025YBN.png)
- monitor優點
![](https://i.imgur.com/2icQWZK.png)
- 成本好調整
![](https://i.imgur.com/yT8gj5z.png)
- 可以把log送到blob storage去分析
![](https://i.imgur.com/XgB75az.png)
- 可以監控是否符合預期狀況
![](https://i.imgur.com/x5KO874.png)
- 從log去找到攻擊手法，再去防禦
s3就等同於blob storage
![](https://i.imgur.com/m5hy3zm.png)




# 講師上課DAY 6. 雲端容器託管、無伺服器服務 
### Container
- 只需定義application跟dependency就好、不用管os、開啟速度更快(輕量化)
![](https://i.imgur.com/pgRuQBv.png)

![](https://i.imgur.com/4nzIhGM.png)

### Docker
- container只是概念、docker是解決辦法
- 不分os
![](https://i.imgur.com/BfusOfH.png)

![](https://i.imgur.com/cOi3tVy.png)
- Dockerfile
定義image要有什麼東西
![](https://i.imgur.com/rBK02Q1.png)

![](https://i.imgur.com/eR7kFwv.png)
- Docker Image
1. image是模具、container是餡料
2. Base image是基底
![](https://i.imgur.com/X33clkf.png)
### Docker Container
### Docker Registry
存docker image的地方、大家上傳自己docker image的地方。用Docker push上傳、Docker pull下載、Docker run執行、Docker commit看版本
![](https://i.imgur.com/31pocrJ.png)
### Azure ACI
![](https://i.imgur.com/ahhd58t.png)

![](https://i.imgur.com/ZUG28Dl.png)
- 1. 先定義Container image
![](https://i.imgur.com/FtuZQ9H.png)
  2. 設os
![](https://i.imgur.com/RvrmDVq.png)
  3. 設定網路(private狀態不能用windows、只想開container就不用開網路)
![](https://i.imgur.com/ueCAe9c.png)

### ACR
- 用DOCKER CLI push 上去
![](https://i.imgur.com/IX5jzKZ.png)

### K8S
- 部署container管理的方式
- opensource
- 自動部屬、管理container
- 支援大型容器負載
- cluster是正在執行的vm的集合
![](https://i.imgur.com/qOwsO4k.png)

### Kubernetes node
- 執行最小單位
![](https://i.imgur.com/YNNTXab.png)
- kubelet
負責node狀態以及跟master溝通
- kube-proxy
負責node排班狀態
- container runtime
真正執行程式的容器

### Kubernetes Control Plane
- 建商概念
- 透過他去管理其他node
- 有4個組件
- Kube-api-server
下指令跟node的溝通橋樑、身分認證跟授權的角色
![](https://i.imgur.com/PZR20zq.png)
- etcd
還原kubenetes狀態(災難備援)
![](https://i.imgur.com/LStEExm.png)
- kube-controller-manager
會看到cluster狀態，monitor的角色
>node controller
>replication controller
>endpoint controller
>service account&tokencontroller

![](https://i.imgur.com/7T6Etsh.png)
- cloud-controller-manager
雲端平台負責的事
- kube-scheduler
根據條件找最適合的node
![](https://i.imgur.com/EeHsbvS.png)

### AKS
![](https://i.imgur.com/N77rhiA.png)

![](https://i.imgur.com/VuJx7GA.png)

![](https://i.imgur.com/Qe35VtN.png)

### Azure Serverless Solutions
- 不用管基礎架構
- 主要用在event trigger
![](https://i.imgur.com/xxPYLUz.png)

![](https://i.imgur.com/qd8HCYs.png)
### Azure Function
- 只要管程式碼
- 各種方式做觸發
- 常用在後端API
- 有可能有COLD start(有延遲)
![](https://i.imgur.com/7fdLYXk.png)
### Azure function Binding
- 是azure function的trigger
![](https://i.imgur.com/KT5qn8B.png)
- Azure Function方案
- linux base要編輯只能地端編輯
![](https://i.imgur.com/KJKYt1n.png)
- Premium方案才能走內網
![](https://i.imgur.com/E9Eu0bQ.png)





# 講師上課DAY 7. Windows Server 介紹及基本設定、AD 系統實作
### Server
- Server:提供運算資源做運算服務
>computing resource:硬體提供的資源
>service:軟體提供的資源

![](https://i.imgur.com/UofcvZy.png)
- Client Server Model(端對端模型)
![](https://i.imgur.com/xiy8fFS.png)
- Server類型
![](https://i.imgur.com/VKrvpxQ.png)

![](https://i.imgur.com/R2XxX2E.png)
loadbalancer是proxy server的概念

- File Server
負責集中檔案管理，可設定權限，透過internet/Local-network做存取
![](https://i.imgur.com/jOFtPiN.png)

- RAID
虛擬化的儲存空間 
![](https://i.imgur.com/r3RcQ6z.png)

![](https://i.imgur.com/pT3EP8k.png)
Block就是Block Storage
- schema不一樣
![](https://i.imgur.com/2D8cnfy.png)

![](https://i.imgur.com/fsLsZhB.png)

![](https://i.imgur.com/YiJWdhQ.png)
- 地端storage
![](https://i.imgur.com/Z5ko0qT.png)
- DAS(BLOCK)/NAS(FILE)/SAN(OBJECT)
![](https://i.imgur.com/7Nmjt9r.png)
VM是用NAS




### Overview of Windows File Systems
### FAT
- File allocation Table
當檔案刪除後寫入新資料，FAT不會將檔案整理成完整片段再寫入，長期使用後會使檔案資料變得逐漸分散，而減慢了讀寫速度
![](https://i.imgur.com/JYUpRXz.png)

![](https://i.imgur.com/RkMLKBM.png)

![](https://i.imgur.com/XPf8olQ.png)
### NTFS 
- NTFS
![](https://i.imgur.com/qv6uoTa.png)

![](https://i.imgur.com/d49IpQm.png)
### ReFS
- 針對12年windows server做使用，但後面都能用
![](https://i.imgur.com/yJFBw3O.png)

![](https://i.imgur.com/DxwBzDi.png)

### Comparison
![](https://i.imgur.com/ZdbYFY5.png)

### Overview of iSCSI
![](https://i.imgur.com/mUdWEUD.png)
### SCSI
- 實體連接線路
![](https://i.imgur.com/EmJueC1.png)
### iSCSI
- 前面i是internet
![](https://i.imgur.com/bnL1Pzo.png)

### Overview of sharing portocal
### SMB
- 提供檔案跟電腦透過網路溝通
![](https://i.imgur.com/nZ8Obcp.png)
### NFS
![](https://i.imgur.com/MAFORUQ.png)
### Comparison
![](https://i.imgur.com/am1Qmk4.png)
![](https://i.imgur.com/oLfnacr.png)

### Web Server on Windows Server

![](https://i.imgur.com/yQTAR32.png)
### IIS
- HTTP web server 走tcp協定。request跟responce為無狀態姓
![](https://i.imgur.com/Tz0x4F3.png)

![](https://i.imgur.com/8R31dCZ.png)

![](https://i.imgur.com/iaIEKmu.png)




# 講師上課Last DAY. 身分驗證與權限控管
### Basic Knowledge with Powershell
![](https://i.imgur.com/ouGUhfx.png)
- 看command (Windows powershell ISE)
![](https://i.imgur.com/2xBnyWc.png)
- modules是command的集合體
![](https://i.imgur.com/rgzxF5S.png)
- Cmdlet原生指令




