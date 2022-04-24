Chapter 6

Khái quát-Mục đích

Modules sâu hơn

Trong quy trình giảng dạy khóa học thiết kế phần mềm, tôi không ngừng cố gắng xác định nguyên nhân của sự phức tạp trong code của sinh viên, điều đó đã thay đổi suy nghĩ của tôi về thiết kế phần mềm theo một số cách khác nhau. Điều quan trọng nhất là liên quan đến tính tổng quát và chuyên môn hóa. Tôi đã nhiều lần nhận thấy rằng sự chuyên môn hóa dẫn đến sự phức tạp. Bây giờ tôi nghĩ rằng chuyên môn hóa quá mức có thể là nguyên nhân lớn nhất gây ra sự phức tạp trong phần mềm. Ngược lại, code có mục đích chung sẽ đơn giản hơn, rõ ràng hơn và dễ hiểu hơn.

Nguyên tắc này được áp dụng ở nhiều level khác nhau trong thiết kế phần mềm. Khi thiết kế các modules như class hoặc method, một trong những cách tốt nhất để tạo ra một deep API là làm cho nó có mục đích khái quát (các API có mục đích mục đích khái quát dẫn đến nhiều thông tin ẩn hơn). Khi viết code cụ thể, một trong những cách hiệu quả nhất để đơn giản hóa mã là loại bỏ các trường hợp đặc biệt, để mã trường hợp chung cũng xử lý các trường hợp ngoại lệ. Loại bỏ các trường hợp đặc biệt cũng có thể làm cho mã hiệu quả hơn, như chúng ta sẽ thấy trong Chương 20. Chương này thảo luận về các vấn đề do chuyên môn hóa gây ra và lợi ích của tính tổng quát. Không thể loại bỏ hoàn toàn chuyên môn hóa, vì vậy chương này cũng đưa ra các hướng dẫn về cách tách mã mục đích đặc biệt khỏi mã mục đích chung.

6.1 Tạo ra các class có mục đích chung-khái quát

Một trong những quyết định phổ biến nhất mà bạn sẽ phải đối mặt khi thiết kế một class mới là liệu có nên triển khai nó theo kiểu mục đích chung hay mục đích đặc biệt. Một số người có thể cho rằng bạn nên thực hiện cách tiếp cận có mục đích chung, trong đó bạn thực hiện một cơ chế có thể được sử dụng để giải quyết nhiều vấn đề, không chỉ những vấn đề quan trọng hiện tại. Trong trường hợp này, cơ chế mới có thể tìm thấy những cách sử dụng không lường trước được trong tương lai, do đó tiết kiệm thời gian. Cách tiếp cận có mục đích chung có vẻ phù hợp với tư duy đầu tư được thảo luận trong Chương 3, nơi bạn dành nhiều thời gian hơn trước để tiết kiệm thời gian sau này. Mặt khác, chúng tôi biết rằng thật khó để dự đoán nhu cầu trong tương lai của một hệ thống phần mềm, vì vậy, một giải pháp có mục đích chung có thể bao gồm các cơ sở vật chất không bao giờ thực sự cần thiết. Hơn nữa, nếu bạn triển khai một thứ gì đó quá chung chung, nó có thể không thực hiện tốt việc giải quyết vấn đề cụ thể mà bạn gặp phải ngày hôm nay.

Do đó, một số người có thể tranh luận rằng: tốt hơn là nên tập trung vào nhu cầu của thời điểm hiện tại, chỉ xây dựng những gì bạn biết mình cần và chuyên biệt hóa nó theo cách bạn định sử dụng hiện tại. Nếu bạn thực hiện phương pháp tiếp cận mục đích đặc biệt và khám phá các công dụng bổ sung sau đó, bạn luôn có thể cấu trúc lại nó để biến nó thành mục đích chung. Cách tiếp cận mục đích đặc biệt có vẻ phù hợp với cách tiếp cận gia tăng để phát triển phần mềm. Khi lần đầu tiên tôi bắt đầu giảng dạy khóa học thiết kế phần mềm của mình, tôi đã hướng đến cách tiếp cận thứ hai (bắt đầu với mục đích đặc biệt), nhưng sau khi dạy khóa học một vài lần, tôi đã thay đổi quyết định. Khi xem xét các dự án của sinh viên, tôi nhận thấy rằng các class có mục đích chung hầu như luôn tốt hơn các class thay thế dành cho mục đích đặc biệt. Điều đặc biệt làm tôi ngạc nhiên là các giao diện có mục đích chung đơn giản và sâu sắc hơn các giao diện dành cho mục đích đặc biệt, và chúng dẫn đến việc triển khai ít mã hơn. Hóa ra là ngay cả khi bạn sử dụng một class theo mục đích đặc biệt, thì việc xây dựng nó theo cách có mục đích chung sẽ ít hơn. Và phương pháp tiếp cận mục đích chung có thể giúp bạn tiết kiệm nhiều thời gian hơn trong tương lai, nếu bạn sử dụng lại class cho các mục đích khác. Nhưng mục đích chung vẫn tốt hơn ngay cả khi bạn không sử dụng tái sử dụng class. Theo kinh nghiệm của tôi, điểm thú vị là triển khai các mô-đun mới theo cách có mục đích chung. Cụm từ “có mục đích chung chung” có nghĩa là chức năng của mô-đun phải phản ánh nhu cầu hiện tại của bạn, nhưng giao diện của nó thì không. Thay vào đó, giao diện phải đủ chung để hỗ trợ nhiều mục đích sử dụng. Giao diện phải dễ sử dụng cho các nhu cầu ngày nay mà không bị ràng buộc cụ thể với chúng. Từ “phần nào” rất quan trọng: đừng mang theo và xây dựng thứ gì đó có mục đích chung chung đến mức khó sử dụng cho nhu cầu hiện tại của bạn.


6.2 Ví dụ: lưu trữ text cho editor

Hãy xem xét một ví dụ từ một lớp học thiết kế phần mềm, trong đó sinh viên được yêu cầu xây dựng một trình soạn thảo văn bản GUI đơn giản. Trình chỉnh sửa phải hiển thị một file và cho phép người dùng trỏ, click và nhập để chỉnh sửa file. Nó cũng phải hỗ trợ nhiều chế độ xem đồng thời của cùng một tệp trong các cửa sổ khác nhau và nó phải hỗ trợ hoàn tác và làm lại nhiều cấp độ đối với các sửa đổi đối với tệp. Mỗi dự án của sinh viên bao gồm một class quản lý văn bản cơ bản của tệp. Các class văn bản thường cung cấp các phương thức để tải tệp vào bộ nhớ, đọc và sửa đổi văn bản của tệp cũng như ghi văn bản đã sửa đổi trở lại tệp. Nhiều nhóm sinh viên đã triển khai các API có mục đích đặc biệt cho class văn bản.

Họ biết rằng lớp sẽ được sử dụng trong một trình soạn thảo tương tác, vì vậy họ nghĩ về các tính năng mà trình soạn thảo phải cung cấp và điều chỉnh API của lớp văn bản cho phù hợp với các tính năng cụ thể đó. Ví dụ: nếu người dùng trình chỉnh sửa gõ phím xóa lùi, trình chỉnh sửa sẽ xóa ngay ký tự bên trái con trỏ; nếu người dùng gõ phím xóa, trình chỉnh sửa sẽ xóa ngay ký tự ở bên phải con trỏ. Biết được điều này, một số nhóm đã tạo một phương thức trong lớp văn bản để hỗ trợ từng tính năng cụ thể sau:

void backspace(Cursor cursor);
void delete(Cursor cursor);

Mỗi phương thức này lấy vị trí con trỏ làm đối số của nó; một loại Con trỏ đặc biệt đại diện cho vị trí này. Trình chỉnh sửa cũng phải hỗ trợ một lựa chọn có thể được sao chép hoặc xóa. Các sinh viên đã xử lý điều này bằng cách xác định một class Selection và pass một object của class này vào class văn bản trong quá trình xóa:

void deleteSelection(Selection selection)

Các sinh viên có thể nghĩ rằng sẽ dễ dàng triển khai giao diện người dùng hơn nếu các phương thức của class văn bản tương ứng với các tính năng hiển thị cho người dùng. Tuy nhiên, trên thực tế, chuyên môn hóa này mang lại ít lợi ích cho code giao diện người dùng và nó tạo ra sự phức tạp về nhận thực cho các nhà phát triển làm việc trên giao diện người dùng hoặc lớp văn bản. Class văn bản kết thúc với một số lượng lớn các phương thức nông, mỗi phương thức chỉ thích hợp cho một thao tác giao diện người dùng. Nhiều phương thức, chẳng hạn như xóa, chỉ được gọi ở một nơi duy nhất. Do đó, một nhà phát triển làm việc trên giao diện người dùng đã phải tìm hiểu về một số lượng lớn các phương thức cho lớp văn bản.

Cách tiếp cận này đã tạo ra rò rỉ thông tin giữa giao diện người dùng và lớp văn bản. Các trừu tượng liên quan đến giao diện người dùng, chẳng hạn như lựa chọn hoặc phím xóa lùi, được phản ánh trong lớp văn bản; điều này làm tăng độ khó nhận thức cho các nhà phát triển làm việc trên lớp văn bản. Mỗi hoạt động giao diện người dùng mới yêu cầu một phương thức được định nghĩa trong class văn bản, vì vậy một nhà phát triển làm việc trên giao diện người dùng cũng có khả năng làm việc trên lớp văn bản. Một trong những mục tiêu trong thiết kế class là cho phép mỗi class được phát triển độc lập, nhưng cách tiếp cận chuyên biệt đã gắn giao diện người dùng và các class văn bản lại với nhau.


6.3 API mục đích khái quát

Một cách tiếp cận tốt hơn là làm cho lớp văn bản chung chung hơn. API của nó chỉ nên được định nghĩa về các tính năng văn bản cơ bản, mà không phản ánh các hoạt động cấp cao hơn sẽ được triển khai với nó. Ví dụ: chỉ cần hai phương pháp để sửa đổi văn bản:

void insert(Postition position, String newText)
void delete(Position start, Position end)

Phương thức đầu tiên chèn một chuỗi tùy ý tại một vị trí tùy ý trong văn bản và phương thức thứ hai xóa tất cả các ký tự ở các vị trí lớn hơn hoặc bằng bắt đầu nhưng nhỏ hơn kết thúc.
API này cũng sử dụng một type chung chung hơn là Position thay vì Cursor, phản ánh một interface cụ thể. Class văn bản cũng phải cung cấp các phương tiện có mục đích chung để thao tác các vị trí trong văn bản, chẳng hạn như sau:

Position changePosition(Position position, int numChars)

Method này trả về một position mới là một số ký tự nhất định từ một vị trí nhất định. Nếu đối số numChars là dương, vị trí mới nằm trong file sau vị trí; nếu numChars là số âm, vị trí mới nằm trước vị trí. Phương thức tự động chuyển sang dòng tiếp theo hoặc dòng trước đó khi cần thiết. Với các phương pháp này, phím xóa có thể được thực hiện với đoạn mã sau (giả sử biến con trỏ giữ vị trí con trỏ hiện tại):

text.delete(cursor, text.changePosition(cursor, 1))

Tương tự, backspace cũng có thể được implemented như sau:

text.delete(text.changePosition(cursor, -1), cursor)

Với API văn bản có mục đích chung, mã để triển khai các chức năng của interface như delete và backspace dài hơn một chút so với cách tiếp cận ban đầu sử dụng API văn bản chuyên biệt. Tuy nhiên, mã mới rõ ràng hơn mã cũ. Một nhà phát triển làm việc trong mô-đun interface có thể quan tâm đến việc những ký tự nào bị xóa bởi phím xóa lùi. Với mã mới, điều này là hiển nhiên. Với mã cũ, nhà phát triển phải vào lớp văn bản và đọc tài liệu và / hoặc mã của phương thức xóa lùi để xác minh hành vi. Hơn nữa, cách tiếp cận mục đích chung có ít mã tổng thể hơn so với cách tiếp cận chuyên biệt, vì nó thay thế một số lượng lớn các phương thức có mục đích đặc biệt trong lớp văn bản bằng một số lượng nhỏ hơn các phương thức có mục đích chung.

Một class văn bản được triển khai với giao diện có mục đích chung có thể được sử dụng cho các mục đích khác ngoài một trình soạn thảo tương tác. Như một ví dụ, giả sử bạn đang xây dựng một ứng dụng sửa đổi một tệp được chỉ định bằng cách thay thế tất cả các lần xuất hiện của một chuỗi cụ thể bằng một chuỗi khác. Các phương thức từ lớp văn bản chuyên biệt, chẳng hạn như xóa lùi và xóa, sẽ có ít giá trị cho ứng dụng này. Tuy nhiên, lớp văn bản có mục đích chung sẽ có hầu hết các chức năng cần thiết cho ứng dụng mới. Tất cả những gì còn thiếu là một phương pháp để tìm kiếm sự xuất hiện tiếp theo của một chuỗi đã cho, chẳng hạn như sau:

Position findNext(Position start, String string)

Tất nhiên, một trình soạn thảo văn bản tương tác có thể có một cơ chế để tìm kiếm và thay thế, trong trường hợp đó, lớp văn bản sẽ bao gồm phương thức này.

6.4 Tính tổng quát dẫn đến việc che dấu thông tin tốt hơn

Cách tiếp cận có mục đích chung cung cấp sự tách biệt rõ ràng hơn giữa các class văn bản và interface, dẫn đến việc che dấu thông tin tốt hơn. Class văn bản không cần biết về các chi tiết cụ thể của interface, chẳng hạn như cách xử lý phím backspace; những chi tiết này bây giờ được gói gọn trong interface class. Các tính interface có thể được thêm vào mà không cần tạo các chức năng hỗ trợ mới trong class văn bản. Giao diện mục đích chung cũng giảm độ phức tạp nhận thức: một nhà phát triển làm việc trên interface chỉ cần học một vài phương pháp đơn giản, có thể được sử dụng lại cho nhiều mục đích khác nhau.

Phương thức backspace trong phiên bản gốc của lớp văn bản là một phương thức trừu tượng sai. Nó nhằm mục đích ẩn thông tin về những ký tự nào bị xóa, nhưng mô-đun giao diện người dùng thực sự cần biết điều này; các nhà phát triển giao diện người dùng có khả năng đọc mã của phương thức xóa lùi để xác nhận hành vi chính xác của nó. Đặt phương thức trong lớp văn bản chỉ khiến các nhà phát triển giao diện người dùng khó lấy thông tin họ cần hơn. "Một trong những yếu tố quan trọng nhất của thiết kế phần mềm là xác định ai cần biết những gì và khi nào". Khi các chi tiết là quan trọng, tốt hơn nên làm cho chúng rõ ràng và rõ ràng nhất có thể, chẳng hạn như việc triển khai sửa đổi hoạt động backspace. Ẩn thông tin này đằng sau một giao diện chỉ tạo ra sự mờ mịt.

6.5 Các câu hỏi để tự hỏi bản thân

Dễ dàng nhận ra một thiết kế lớp có mục đích chung rõ ràng hơn là tạo một thiết kế. Dưới đây là một số câu hỏi bạn có thể tự hỏi, điều này sẽ giúp bạn tìm được sự cân bằng phù hợp giữa mục đích chung và mục đích đặc biệt cho một giao diện. Giao diện đơn giản nhất sẽ đáp ứng mọi nhu cầu hiện tại của tôi là gì? Nếu bạn giảm số lượng phương thức trong một API mà không làm giảm khả năng tổng thể của nó, thì có thể bạn đang tạo nhiều phương thức có mục đích chung hơn. API văn bản dành cho mục đích đặc biệt có ít nhất ba phương pháp để xóa văn bản: backspace, delete và deleteSelection. API có mục đích chung hơn chỉ có một phương pháp để xóa văn bản, phục vụ cả ba mục đích. Giảm số lượng phương thức chỉ có ý nghĩa miễn là API cho từng phương thức riêng lẻ vẫn đơn giản; nếu bạn phải đưa ra nhiều đối số bổ sung để giảm số lượng phương pháp, thì bạn có thể không thực sự đơn giản hóa mọi thứ.

Phương pháp này sẽ được sử dụng trong bao nhiêu trường hợp? Nếu một phương thức được thiết kế cho một mục đích sử dụng cụ thể, chẳng hạn như phương thức xóa lùi, thì đó là một dấu hiệu báo trước rằng nó có thể là mục đích quá đặc biệt. Xem liệu bạn có thể thay thế một số phương pháp có mục đích đặc biệt bằng một phương pháp có mục đích chung duy nhất hay không. API này có dễ sử dụng cho nhu cầu hiện tại của tôi không? Câu hỏi này có thể giúp bạn xác định khi nào bạn đã đi quá xa trong việc tạo ra một API đơn giản và có mục đích chung. Nếu bạn phải viết nhiều mã bổ sung để sử dụng một lớp cho mục đích hiện tại của mình, đó là dấu hiệu đỏ cho thấy giao diện không cung cấp chức năng phù hợp. Ví dụ, một cách tiếp cận cho lớp văn bản sẽ là thiết kế nó xung quanh các hoạt động với một ký tự: chèn chèn một ký tự và xóa sẽ xóa một ký tự. API này vừa đơn giản vừa có mục đích chung. Tuy nhiên, nó sẽ không đặc biệt dễ sử dụng đối với trình soạn thảo văn bản: mã cấp cao hơn sẽ chứa rất nhiều vòng lặp để chèn hoặc xóa phạm vi ký tự. Cách tiếp cận một ký tự cũng sẽ không hiệu quả đối với các hoạt động lớn. Vì vậy, tốt hơn là lớp văn bản có hỗ trợ tích hợp cho các hoạt động trên phạm vi ký tự.



















