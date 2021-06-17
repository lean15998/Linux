# 1.DNS là gì?

- **DNS(Domain Name System)** là một hệ thống dùng để phân giải tên miền. Nó dùng để thiết lập mối quan hệ giữa tên tên miền và địa chỉ IP. DNS giúp chúng ta có thể chuyển đổi tên miền (tenmien.com) sang một địa chỉ IP (xxx.xxx.xxx.xxx).
- DNS Server là một loại máy chủ dùng để quản lý và xử lý các tên miền thực hiện các bản ghi liên quan của chúng. DNS Server là thành phần chính thực hiện giao thức DNS và cung cấp các dịch vụ phân giải tên miền cho máy chủ và máy khách web trên mạng dựa trên IP. DNS Server dùng để định vị và phân phối các trang web cho người dùng cuối qua Internet, máy chủ DNS được phát triển trên phần cứng thông thường nhưng chạy phần mềm DNS chuyên dụng. Nó luôn được kết nối với Internet.
- DNS Server dùng để chứa cơ sở dữ liệu bao gồm các địa chỉ IP ứng với tên miền nhất định được gọi là bản ghi DNS. Nó thực hiện chức năng cơ bản nhất là phân giải tên miền thành địa chỉ IP tương ứng. Trong quá trình phân giải tên miền thì kết quả tìm kiếm nếu có trong các bản ghi DNS thì tên miền được trả về ứng với địa chỉ IP của nó. Nếu tên miền không được đăng ký hoặc thêm vào máy chủ DNS đó, truy vấn sẽ được chuyển đến các máy chủ DNS khác cho đến khi tìm thấy bản ghi tên miền.

# 2.Các loại  DNS Server

- Tất cả các máy chủ DNS thuộc một trong 4 loại DNS Server sau:
<ul>
  <ul>
    <li> Recursive resolver
    <li> Root nameserver
    <li> TLD nameserver
    <li> Authoritative nameserver
  </ul>
</ul>
- Khi chúng ta thực hiện tra cứu DNS thì các máy chủ này sẽ phối hợp với nhau để hoàn thành nhiệm vụ cung cấp IP cho tên miền mà chúng ta tìm kiếm.

### Recursive resolver

- Một recursive resolver là điểm dừng đầu tiên trong quá trình truy vấn DNS. Nó hoạt động như một cầu nối trung gian giữa máy client và DNS nameserver.
- Sau khi nhận được truy vấn DNS từ một client web thì recursive resolver sẽ phản hồi với dữ liệu được lưu trong bộ nhớ cache hoặc gửi yêu cầu đến root nameservers tiếp theo là đến TLD nameservers và cuối cùng đến authoritative nameserver.
- Sau khi nhận được phản hồi từ authoritative nameserver chứa địa chỉ IP được yêu cầu, recursive resolver sẽ gửi phản hồi cho Client.
- Trong quá trình này, recursive resolver sẽ lưu trữ thông tin nhận được từ authoritative nameserver. Khi một Client yêu cầu địa chỉ IP của một tên miền giống với client trước yêu cầu thì recursive resolver sẽ cung cấp các bản ghi được yêu cầu từ bộ nhớ cache của nó. Bỏ qua quá trình hỏi root nameservers.

### Root nameserver

- Trên thế giới hiện tại có 13 Root nameservers DNS. Các Root nameservers DNS này sẽ chứa các bản ghi gồm toàn bộ các thông tin về tên miền cùng với địa chỉ IP ứng với tên miền đó. Đây cũng chính là điểm dừng đầu tiên trong quá trình phân giải DNS.
- Root nameservers chấp nhận truy vấn của recursive resolver gồm một tên miền và thực hiện trả lời bằng cách hướng recursive resolver đến TLD nameservers dựa trên phần mở rộng của tên miền đó (.com, .vn, .net, .org,...). Các Root nameservers này được giảm sác và theo dõi bỡi Internet Corporation for Assigned Names and Numbers (ICANN).
<br>
<img src="https://github.com/lean15998/Linux/blob/main/images/24.01.PNG">
<br>

### TLD nameservers

- TLD nameservers dùng để duy trì thông tin cho tất cả các tên miền có chung một phần mở rộng như chúng ta đã nói bên trên (.com, .vn, .net, .org,...).
- Ví dụ: Trên trình duyệt web chúng ta thực hiện gõ vào thanh tìm kiếm google.com khi nhận được phản hồi từ Root nameservers thì recursive resolver sẽ gửi truy vấn đến TLD nameservers. Tại đây chúng ta nhận được câu trả lời chỉ cách chúng ta đến máy chủ tên có thẩm quyền cho tên miền có phần mở rộng là `.com` .
- Việc quản lý các máy TLD nameservers bởi Internet Assigned Numbers Authority (IANA), một chi nhánh của ICANN. IANA chia các máy chủ TLD thành hai nhóm chính:
<ul>
  <ul>
    <li> Các tên miền cấp cao chung: Đây là các tên miền không cụ thể theo quốc gia, một số TLD chung được biết đến nhiều nhất bao gồm .com, .org, .net, .edu và .gov.
    <li> Tên miền cấp cao nhất của mã quốc gia: Chúng bao gồm bất kỳ tên miền nào dành riêng cho một quốc gia hoặc tiểu bang. Ví dụ bao gồm .vn, .uk, .us, .ru và .jp.
  </ul>
</ul>
  
### Authoritative nameserver

- Khi recursive resolver nhận được phản hồi từ TLD nameservers, phản hồi đó sẽ hướng recursive resolver đến authoritative nameserver. Đây chính là bước cuối cùng mà recursive resolver sẽ tìm được tìm địa chỉ IP cần tìm kiếm.
- Authoritative nameserves là nơi chứa thông tin cụ thể của các tên miền như là: `google.com` và nó có thể cung cấp cho recursive resolver địa chỉ IP của máy chủ đó được tìm thấy trong bản ghi DNS. Nếu như tên miền có bản ghi CNAME (alias) nó sẽ cung cấp cho recursive resolver với một miền alias mà tại đây recursive resolver sẽ phải thực hiện tra cứu DNS hoàn toàn mới để tạo một bản ghi từ authoritative nameserver khác.

# 3.Cấu hình DNS Server
<br>
<img src="https://github.com/lean15998/Linux/blob/main/images/24.02.PNG">
<br>

### Tại DNS Server

- Cài đặt các gói `bind9` và `bind9utils`
- Mở file `/etc/bind/named.conf.local` và thêm 1 zone phân giải thuận từ tên miền sang địa chỉ IP và 1 zone phân giải nghịch từ địa chỉ IP sang tên miền.
<br>
<img src="https://github.com/lean15998/Linux/blob/main/images/24.03.PNG">
<br>

- Tạo 2 file cấu hình cho 2 zone trên và tiến hành cấu hình.

<br>
<img src="https://github.com/lean15998/Linux/blob/main/images/24.04.PNG">
<br>
<img src="https://github.com/lean15998/Linux/blob/main/images/24.05.PNG">
<br>
Trong đó:
<ul>
  <ul>
    <li> SOA: Chỉ ra rằng máy chủ Name Server là nơi cung cấp thông tin tin cậy từ dữ liệu có trong zone.
    <li> NS: Mỗi name server cho zone sẽ có một NS record.
    <li> A: Record A (Address) ánh xạ tên máy (hostname) vào địa chỉ IP.
    <li> CNAME: Record CNAME (canonical name) tạo tên bí danh alias trỏ vào một tên canonical.
    <li> PTR: Record PTR (pointer) dùng để ánh xạ địa chỉ IP thành hostname.
  </ul>
</ul>
- Khởi động lại dịch vụ bind9
<br>

### Tại Client

- Cài đặt địa chỉ DNS
<br>
<img src="https://github.com/lean15998/Linux/blob/main/images/24.06.PNG">
<br>

- Kiểm tra

<br>
<img src="https://github.com/lean15998/Linux/blob/main/images/24.07.PNG">
<br>
<img src="https://github.com/lean15998/Linux/blob/main/images/24.08.PNG">




