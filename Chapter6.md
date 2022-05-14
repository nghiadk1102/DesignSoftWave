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

Dễ dàng nhận ra một thiết kế class có mục đích chung rõ ràng hơn là tạo một thiết kế. Dưới đây là một số câu hỏi bạn có thể tự hỏi, điều này sẽ giúp bạn tìm được sự cân bằng phù hợp giữa mục đích chung và mục đích đặc biệt cho một giao diện. 
Giao diện đơn giản nhất sẽ đáp ứng mọi nhu cầu hiện tại của tôi là gì?

Nếu bạn giảm số lượng phương thức trong một API mà không làm giảm khả năng tổng thể của nó, thì có thể bạn đang tạo nhiều phương thức có mục đích chung hơn. API văn bản dành cho mục đích đặc biệt có ít nhất ba phương pháp để xóa văn bản: backspace, delete và deleteSelection. API có mục đích chung hơn chỉ có một phương pháp để xóa văn bản, phục vụ cả ba mục đích. Giảm số lượng phương thức chỉ có ý nghĩa miễn là API cho từng phương thức riêng lẻ vẫn đơn giản; nếu bạn phải đưa ra nhiều đối số bổ sung để giảm số lượng phương pháp, thì bạn có thể không thực sự đơn giản hóa mọi thứ.

Method này sẽ được sử dụng trong bao nhiêu trường hợp? 

Nếu một phương thức được thiết kế cho một mục đích sử dụng cụ thể, chẳng hạn như phương thức xóa lùi, thì đó là một dấu hiệu báo trước rằng nó có thể là mục đích quá đặc biệt.

Xem liệu bạn có thể thay thế một số phương pháp có mục đích đặc biệt bằng một phương pháp có mục đích chung duy nhất hay không. API này có dễ sử dụng cho nhu cầu hiện tại của tôi không?

Câu hỏi này có thể giúp bạn xác định khi nào bạn đã đi quá xa trong việc tạo ra một API đơn giản và có mục đích chung. Nếu bạn phải viết nhiều mã bổ sung để sử dụng một lớp cho mục đích hiện tại của mình, đó là dấu hiệu đỏ cho thấy giao diện không cung cấp chức năng phù hợp. Ví dụ, một cách tiếp cận cho lớp văn bản sẽ là thiết kế nó xung quanh các hoạt động với một ký tự: chèn chèn một ký tự và xóa sẽ xóa một ký tự. API này vừa đơn giản vừa có mục đích chung. Tuy nhiên, nó sẽ không đặc biệt dễ sử dụng đối với trình soạn thảo văn bản: mã cấp cao hơn sẽ chứa rất nhiều vòng lặp để chèn hoặc xóa phạm vi ký tự. Cách tiếp cận một ký tự cũng sẽ không hiệu quả đối với các hoạt động lớn. Vì vậy, tốt hơn là lớp văn bản có hỗ trợ tích hợp cho các hoạt động trên phạm vi ký tự.

6.6 Đẩy bộ phận chuyên biệt lên đầu (hoặc dưới cùng) 

Hầu hết các hệ thống phần mềm chắc chắn phải có một số mã chuyên biệt. Ví dụ, các ứng dụng cung cấp các tính năng cụ thể cho người dùng của họ; những thứ này thường được chuyên môn hóa cao. Vì vậy, thường không thể loại bỏ chuyên môn hóa hoàn toàn. Tuy nhiên, mã chuyên dụng nên được tách biệt rõ ràng khỏi mã mục đích chung. Điều này có thể được thực hiện bằng cách đẩy mã chuyên dụng lên hoặc xuống trong ngăn xếp phần mềm. Một cách để tách mã chuyên dụng là đẩy nó lên trên. Các lớp cấp cao nhất của một ứng dụng, cung cấp các tính năng cụ thể, nhất thiết sẽ chuyên biệt cho các tính năng đó. Nhưng chuyên môn hóa này không cần phải thấm sâu vào các lớp cấp thấp hơn được sử dụng để triển khai các tính năng. Chúng ta đã thấy điều này trong ví dụ về trình soạn thảo trước đó trong chương này. Việc triển khai dành cho sinh viên ban đầu đã làm rò rỉ các chi tiết về giao diện người dùng chuyên biệt, chẳng hạn như hoạt động của phím xóa lùi đối với việc triển khai lớp văn bản. API văn bản được cải tiến đã đẩy tất cả chuyên môn lên trên vào mã giao diện người dùng, chỉ để lại mã mục đích chung trong lớp văn bản.


Đôi khi, cách tiếp cận tốt nhất là đẩy sự chuyên môn hóa xuống. Một ví dụ về điều này là trình điều khiển thiết bị. Một hệ điều hành thường phải hỗ trợ hàng trăm hoặc hàng nghìn loại thiết bị khác nhau của thiết bị, chẳng hạn như các loại thiết bị lưu trữ thứ cấp khác nhau. Mỗi loại thiết bị này có bộ lệnh chuyên biệt riêng. Để ngăn các đặc tính của thiết bị chuyên dụng bị rò rỉ vào mã hệ điều hành chính, hệ điều hành xác định một giao diện với các hoạt động có mục đích chung mà bất kỳ thiết bị lưu trữ thứ cấp nào cũng phải thực hiện, chẳng hạn như “đọc khối” và “ghi khối”. Đối với mỗi thiết bị khác nhau, một mô-đun trình điều khiển thiết bị triển khai giao diện có mục đích chung bằng cách sử dụng các tính năng chuyên biệt của thiết bị cụ thể đó. Cách tiếp cận này đẩy chuyên môn hóa xuống các trình điều khiển thiết bị, do đó cốt lõi của hệ điều hành có thể được viết mà không cần bất kỳ kiến ​​thức nào về các đặc tính cụ thể của thiết bị. Cách tiếp cận này cũng giúp dễ dàng thêm các thiết bị mới: nếu một thiết bị có đủ tính năng để triển khai giao diện trình điều khiển thiết bị, nó có thể được thêm vào hệ thống mà không cần thay đổi hệ điều hành chính.

6.7 Ví dụ: cơ chế hoàn tác của trình soạn thảo

Trong dự án trình soạn thảo GUI, một trong những yêu cầu là hỗ trợ hoàn tác / làm lại nhiều cấp, không chỉ đối với các thay đổi đối với chính văn bản mà còn đối với các thay đổi trong lựa chọn, con trỏ chèn và chế độ xem. Ví dụ: nếu người dùng chọn một số văn bản, xóa văn bản đó, cuộn đến một vị trí khác trong tệp, sau đó gọi hoàn tác, trình chỉnh sửa phải khôi phục trạng thái của văn bản đó về trạng thái ngay trước khi xóa. Điều này bao gồm khôi phục văn bản đã xóa, chọn lại văn bản đó và cũng làm cho văn bản đã chọn hiển thị trong cửa sổ. Một số dự án của sinh viên đã thực hiện toàn bộ cơ chế hoàn tác như một phần của lớp văn bản. Lớp văn bản duy trì một danh sách tất cả các thay đổi có thể hoàn tác. Nó tự động thêm các mục vào danh sách này bất cứ khi nào văn bản được thay đổi. Đối với các thay đổi đối với lựa chọn, con trỏ chèn và chế độ xem, mã giao diện người dùng gọi các phương thức bổ sung trong lớp văn bản, sau đó thêm các mục nhập cho những thay đổi đó vào danh sách hoàn tác. Khi người dùng yêu cầu hoàn tác hoặc làm lại, mã giao diện người dùng gọi một phương thức trong lớp văn bản, sau đó xử lý các mục nhập trong danh sách hoàn tác. Đối với các mục nhập liên quan đến văn bản, nó đã cập nhật phần bên trong của lớp văn bản; đối với các mục nhập liên quan đến những thứ khác, chẳng hạn như lựa chọn, lớp văn bản được gọi trở lại mã giao diện người dùng để thực hiện hoàn tác hoặc làm lại.

Cách tiếp cận này dẫn đến một tập hợp các tính năng khó xử lý trong lớp văn bản. Cốt lõi của hoàn tác / làm lại bao gồm một cơ chế có mục đích chung để quản lý danh sách các hành động đã được thực hiện và chuyển qua chúng trong các hoạt động hoàn tác và làm lại. Phần lõi nằm trong lớp văn bản cùng với các trình xử lý có mục đích đặc biệt thực hiện hoàn tác và làm lại cho những thứ cụ thể như văn bản và lựa chọn. Các trình xử lý hoàn tác có mục đích đặc biệt cho vùng chọn và con trỏ không liên quan gì đến bất kỳ thứ gì khác trong lớp văn bản; chúng dẫn đến rò rỉ thông tin giữa lớp văn bản và giao diện người dùng, cũng như các phương thức bổ sung trong mỗi mô-đun để chuyển thông tin hoàn tác qua lại. Nếu một loại thực thể hoàn tác mới được thêm vào hệ thống trong tương lai, nó sẽ yêu cầu các thay đổi đối với lớp văn bản, bao gồm các phương thức mới dành riêng cho thực thể đó. Ngoài ra, cốt lõi hoàn tác có mục đích chung ít liên quan đến các cơ sở văn bản có mục đích chung trong lớp.


Những vấn đề này có thể được giải quyết bằng cách trích xuất lõi có mục đích chung của cơ chế hoàn tác / làm lại và đặt nó vào một lớp riêng biệt

public class History {
	public interface Action {
		public void redo();
		public void undo();
	}

	History() {...}

	void addAction(Action action) {...}
	void addFence() {...}
	void undo() {...}
	void redo() {...}
} 

Trong này thiết kế, class History quản lý một tập hợp các đối tượng implemented interface History.Action.
Mỗi History.Action mô tả một thao tác đơn lẻ, chẳng hạn như chèn văn bản hoặc thay đổi vị trí con trỏ và nó cung cấp các phương thức có thể hoàn tác hoặc làm lại thao tác.
History class không biết gì về thông tin được lưu trữ trong các hành động hoặc cách chúng thực hiện các phương thức hoàn tác và làm lại của chúng

History duy trì một danh sách lịch sử mô tả tất cả các hành động được thực hiện trong suốt thời gian tồn tại của ứng dụng, đồng thời nó cung cấp các phương thức hoàn tác và làm lại đi ngược và chuyển tiếp qua danh sách để phản hồi lại các thao tác hoàn tác và làm lại do người dùng yêu cầu, gọi các phương thức hoàn tác và làm lại trong History. History.Actions là các đối tượng có mục đích đặc biệt: mỗi đối tượng hiểu một loại hoạt động hoàn tác cụ thể. Chúng được triển khai bên ngoài lớp History, trong các mô-đun hiểu các loại hành động hoàn tác cụ thể. Lớp văn bản có thể triển khai các đối tượng UndoableInsert và UndoableDelete để mô tả các thao tác chèn và xóa văn bản. Bất cứ khi nào nó chèn văn bản, Text class sẽ tạo một đối tượng UndoableInsert mới mô tả việc chèn và gọi History.addAction để thêm nó vào danh sách history. Interface của trình chỉnh sửa có thể tạo các đối tượng UndoableSelection và UndoableCursor mô tả các thay đổi đối với con trỏ chọn và chèn.

History class cũng cho phép các action có thể dc nhóm lại, ví dụ: một yêu cầu hoàn tác duy nhất từ người dùng có thể khôi phục văn bản đã xóa, chọn lại văn bản đã xóa và định vị lại con trỏ chèn. Để thực hiện điều đó, ta sử dụng "hàng rào", là các điểm đánh dấu được đặt trong danh sách lịch sử để phân tách các nhóm hành động có liên quan. Mỗi cuộc gọi đến History.redo sẽ đi ngược lại qua danh sách lịch sử, hoàn tác các hành động cho đến khi nó đến hàng rào tiếp theo. Vị trí của hàng rào được xác định bởi mã cấp cao hơn bằng cách gọi History.addFence. Cách tiếp cận này chia chức năng của hoàn tác thành ba loại, mỗi loại được thực hiện ở một nơi khác nhau:
- Một cơ chế có mục đích chung để quản lý và nhóm các hành động và gọi các hoạt động hoàn tác / làm lại (được thực hiện bởi class History). Chi tiết cụ thể của các hành động cụ thể (được thực hiện bởi nhiều lớp, mỗi lớp hiểu một số lượng nhỏ các kiểu hành động). Chính sách nhóm các hành động (được thực hiện bằng mã giao diện người dùng cấp cao để cung cấp hành vi ứng dụng tổng thể phù hợp). Mỗi danh mục này có thể được thực hiện mà không cần hiểu biết gì về các danh mục khác. Các lớp Lịch sử không biết những loại hành động đang được hoàn tác; nó có thể được sử dụng trong nhiều ứng dụng. Mỗi lớp hành động chỉ hiểu một loại hành động duy nhất và cả lớp Lịch sử cũng như các lớp hành động đều cần phải biết chính sách về nhóm hành động.

Quyết định thiết kế quan trọng là quyết định tách phần mục đích chung của cơ chế hoàn tác khỏi các phần mục đích đặc biệt, tạo ra một lớp riêng biệt cho phần mục đích chung và đẩy các phần có mục đích đặc biệt xuống thành các lớp con của Lịch sử. Sau khi hoàn thành, phần còn lại của thiết kế sẽ rơi ra ngoài một cách tự nhiên. Lưu ý: đề xuất tách mã mục đích chung khỏi mã mục đích đặc biệt đề cập đến mã liên quan đến một cơ chế cụ thể. Ví dụ: mã hoàn tác có mục đích đặc biệt (chẳng hạn như mã để hoàn tác chèn văn bản) nên được tách biệt với mã hoàn tác có mục đích chung (chẳng hạn như mã để quản lý danh sách lịch sử). Tuy nhiên, có thể hợp lý khi kết hợp mã mục đích đặc biệt cho một cơ chế với mã mục đích chung cho một cơ chế khác. Lớp văn bản là một ví dụ về điều này: nó thực hiện một cơ chế có mục đích chung để quản lý văn bản, nhưng nó bao gồm mã mục đích đặc biệt liên quan đến việc hoàn tác. Mã hoàn tác có mục đích đặc biệt vì nó chỉ xử lý các hoạt động hoàn tác để sửa đổi văn bản. Việc kết hợp mã này với cơ sở hạ tầng hoàn tác có mục đích chung trong lớp Lịch sử là không hợp lý, nhưng sẽ hợp lý nếu đặt nó vào lớp văn bản, vì nó có liên quan chặt chẽ với các chức năng văn bản khác.

6.8 Loại bỏ các trường hợp đặc biệt trong mã

Cho đến thời điểm này, tôi đã thảo luận về chuyên môn hóa trong bối cảnh thiết kế lớp và phương thức. Một dạng chuyên môn hóa khác xảy ra trong mã cho thân phương thức, dưới dạng các trường hợp đặc biệt. Các trường hợp đặc biệt có thể dẫn đến mã bị đánh đố với các câu lệnh if, điều này làm cho mã khó hiểu và dễ bị lỗi. Vì vậy, các trường hợp đặc biệt nên được loại bỏ bất cứ khi nào có thể. Cách tốt nhất để làm điều này là thiết kế trường hợp bình thường theo cách tự động xử lý các điều kiện cạnh mà không cần bất kỳ mã bổ sung nào. Trong dự án soạn thảo văn bản, học sinh phải thực hiện cơ chế lựa chọn văn bản và sao chép hoặc xóa lựa chọn. Hầu hết các sinh viên đã giới thiệu một biến trạng thái trong quá trình thực hiện lựa chọn của họ để cho biết lựa chọn có tồn tại hay không. Có lẽ họ đã chọn cách tiếp cận này vì đôi khi không có lựa chọn nào được hiển thị trên màn hình, vì vậy việc thể hiện khái niệm này trong quá trình thực hiện có vẻ tự nhiên. Tuy nhiên, cách tiếp cận này dẫn đến nhiều lần kiểm tra để phát hiện điều kiện “không có lựa chọn” và xử lý nó một cách đặc biệt. Mã xử lý lựa chọn có thể được đơn giản hóa bằng cách loại bỏ trường hợp đặc biệt "không có lựa chọn", để lựa chọn luôn tồn tại. Khi không có vùng chọn nào hiển thị trên màn hình, nó có thể được biểu diễn bên trong bằng một vùng chọn trống, có vị trí bắt đầu và kết thúc giống nhau. Với cách tiếp cận này, mã quản lý lựa chọn có thể được viết mà không có bất kỳ kiểm tra nào cho “không có lựa chọn”. Khi sao chép vùng chọn, nếu vùng chọn trống thì 0 byte sẽ được chèn vào vị trí mới; nếu được triển khai chính xác, sẽ không cần kiểm tra 0 byte như một trường hợp đặc biệt. Tương tự, có thể thiết kế mã xóa vùng chọn để trường hợp trống được triển khai chính xác, sẽ không cần kiểm tra 0 byte như trường hợp đặc biệt. Tương tự, có thể thiết kế mã xóa vùng chọn để xử lý trường hợp trống mà không cần kiểm tra trường hợp đặc biệt nào. Xem xét một lựa chọn tất cả trên một dòng. Để xóa vùng chọn, hãy trích xuất phần dòng trước vùng chọn và nối nó với phần dòng sau vùng chọn để tạo thành dòng mới. Nếu vùng chọn trống, cách tiếp cận này sẽ tạo lại dòng ban đầu. Chương 10 sẽ thảo luận về các trường hợp ngoại lệ, tạo ra nhiều trường hợp đặc biệt hơn, và làm thế nào để giảm số lượng nơi phải xử lý chúng.

6.9 Kết luận
Sự chuyên môn hóa không cần thiết, cho dù ở dạng các lớp và phương thức có mục đích đặc biệt hay các trường hợp đặc biệt trong mã, là một yếu tố góp phần đáng kể vào sự phức tạp của phần mềm. Không thể loại bỏ hoàn toàn chuyên môn hóa, nhưng với thiết kế tốt, bạn sẽ có thể giảm đáng kể nó và tách mã chuyên dụng khỏi mã mục đích chung. Điều này sẽ dẫn đến các lớp sâu hơn, ẩn thông tin tốt hơn và mã đơn giản và rõ ràng hơn.











