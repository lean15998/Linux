# 1.Uptime

- Lệnh uptime dùng để tìm hiểu thời gian hệ thống hoạt động. Lệnh này sẽ hiển thị các giá trị liên quan đến thời gian hiện tại và lượng thời gian của hệ thống đang ở trạng thái chạy, số lượng người dùng hiện đang đăng nhập và thời gian tải trung bình.
- Cú pháp lệnh uptime: `uptime <options>`
- Có thể xem các tùy chọn bằng lệnh `uptime -help`
- Ví dụ:

<img src="">

- Theo thứ tự xuất hiện của kết quả trên chúng ta có:
<ul>
  <ul>
    <li> current time: Hiển thị thời gian hiện tại.
    <li> up: Hệ thống đang chạy và nó được hiển thị tổng thời gian mà hệ thống đã chạy.
    <li> user: Số lượng người dùng đã đăng nhập.
    <li> load average: Trung bình tải hệ thống.
  </ul>
</ul>

# 2. Lệnh w

<img src="">

- Lệnh sẽ hiển thị theo thứ tự:

<ul>
  <ul>
    <li> Thời gian hiện tại.
    <li> up: Hệ thống đã chạy được bao lâu.
    <li> user: Số lượng người dùng đã đăng nhập.
    <li> load average: Trung bình tải hệ thống.
  </ul>
</ul>

- Hàng thứ 2 thì các mục sau đây được hiển thị cho mỗi người dùng:

<ul>
  <ul>
    <li> USER: Tên đăng nhập.
    <li> TTY: Tên tty.
    <li> FORM: Máy chủ từ xa.
    <li> LOGIN@: Thời gian đăng nhập.
    <li> IDLE: Thời gian nhàn rỗi.
    <li> Thời gian JCPU: Là thời gian được sử dụng bởi tất cả các quy trình được đính kèm với tty. Nó không bao gồm các công việc nền trước đây nhưng bao gồm các công việc nền hiện đang chạy.
    <li> Thời gian của PCPU: Là thời gian được sử dụng bởi tiến trình hiện tại, được đặt tên trong WHAT.
  </ul>
</ul>
