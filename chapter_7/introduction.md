Chương 7 Different Layer, Different Abstraction

Hệ thống phần mềm tổ chức theo các layer, trong đó các layer cao hơn sử dụng các tiện ích do các layer thấp hơn cung cấp. Trong một hệ thống được thiết kế tốt, mỗi layer cung cấp một sự trừu tượng khác với các layer bên trên và bên dưới nó; nếu bạn làm theo một thao tác đơn lẻ khi nó di chuyển lên và xuống qua các layer bằng cách gọi các phương thức, thì các phần trừu tượng sẽ thay đổi theo mỗi lần gọi phương thức.

Ví dụ: Trong hệ thống tệp, layer trên cùng thực hiện trừu tượng hóa tệp. Một tệp bao gồm một mảng byte có độ dài thay đổi, có thể được cập nhật bằng cách đọc và ghi các dải byte có độ dài thay đổi. layer thấp hơn tiếp theo trong hệ thống tệp thực hiện một bộ đệm trong bộ nhớ của các khối đĩa có kích thước cố định; người gọi có thể cho rằng các khối được sử dụng thường xuyên sẽ ở trong bộ nhớ nơi chúng có thể được truy cập nhanh chóng. layer thấp nhất bao gồm các trình điều khiển thiết bị, các trình điều khiển này di chuyển các khối giữa các thiết bị lưu trữ thứ cấp và bộ nhớ. Trong một giao thức truyền tải mạng như TCP, phần trừu tượng được cung cấp bởi layer trên cùng là một dòng byte được phân phối đáng tin cậy từ máy này sang máy khác. Mức này được xây dựng trên mức thấp hơn để truyền các gói có kích thước giới hạn giữa các máy trên cơ sở nỗ lực tối đa: hầu hết các gói sẽ được gửi thành công, nhưng một số gói có thể bị mất hoặc phân phối không theo thứ tự.

Nếu một hệ thống chứa các lớp liền kề với những nội dung trừu tượng tương tự, thì đây là một dấu hiệu cho thấy có vấn đề với việc phân hủy lớp. Chương này thảo luận về các tình huống mà điều này xảy ra, các vấn đề dẫn đến và cách cấu trúc lại để loại bỏ các vấn đề.