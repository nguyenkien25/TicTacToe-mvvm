# TicTacToe - MVVM

MVVM với [Data Binding](https://developer.android.com/topic/libraries/data-binding/) trên Android có lợi ích của việc kiểm tra dễ dàng hơn và mô đun, trong khi cũng làm giảm số lượng mã glue mà chúng ta phải viết để kết nối các view + model.

## Model

Mô hình bao gồm Data + State + Business logic.

## View

View bind tới các biến observable và hành động tiếp xúc bởi các ViewModel một cách linh hoạt.

## ViewModel

ViewModel là chịu trách nhiệm cho model và chuẩn bị dữ liệu observable cần thiết cho View.
Nó cũng cung cấp móc cho view để pass các event tới model. Tuy nhiên ViewModel không gắn với view.

View ([tictactoe.xml](https://github.com/nguyenkien25/TicTacToe-mvvm/blob/master/app/src/main/res/layout/tictactoe.xml) [menu_tictactoe.xml](https://github.com/nguyenkien25/TicTacToe-mvvm/blob/master/app/src/main/res/menu/menu_tictactoe.xml) [TicTacToeActivity](https://github.com/nguyenkien25/TicTacToe-mvvm/blob/master/app/src/main/java/com/acme/tictactoe/view/TicTacToeActivity.java))
---Invoke Action , Bind to Data --> ViewModel ([ViewModel <Interface>](https://github.com/nguyenkien25/TicTacToe-mvvm/blob/master/app/src/main/java/com/acme/tictactoe/viewmodel/ViewModel.java) [TicTacToeViewModel](https://github.com/nguyenkien25/TicTacToe-mvvm/blob/master/app/src/main/java/com/acme/tictactoe/viewmodel/TicTacToeViewModel.java))
---Interact with--> Model ([Board](https://github.com/nguyenkien25/TicTacToe-mvvm/blob/master/app/src/main/java/com/acme/tictactoe/model/Board.java) [Cell](https://github.com/nguyenkien25/TicTacToe-mvvm/blob/master/app/src/main/java/com/acme/tictactoe/model/Cell.java) [Player](https://github.com/nguyenkien25/TicTacToe-mvvm/blob/master/app/src/main/java/com/acme/tictactoe/model/Player.java))

Chúng ta hãy xem xét kỹ hơn một số bộ phận chuyển động ở đây, bắt đầu với ViewModel. [TicTacToeViewModel](https://github.com/nguyenkien25/TicTacToe-mvvm/blob/master/app/src/main/java/com/acme/tictactoe/viewmodel/TicTacToeViewModel.java)

Một vài trích đoạn từ chế độ [view tictactoe.xml](https://github.com/nguyenkien25/TicTacToe-mvvm/blob/master/app/src/main/res/layout/tictactoe.xml) để xem làm thế nào các biến này và những hành động bị ràng buộc.

## Evaluation

Unit test càng dễ dàng hơn, bởi vì không còn sự phụ thuộc vào view. Khi thử nghiệm, bạn chỉ cần xác minh rằng các biến observable được đặt phù hợp khi thay đổi model.

## MVVM  Concerns

- *Maintenance* - Từ view có thể liên kết với cả hai biến và biểu thức, logic trình bày không liên quan có thể creep theo thời gian, thêm hiệu quả code XML của chúng ta.
Để tránh điều này, luôn luôn có được giá trị trực tiếp từ các ViewModel hơn là cố gắng để tính toán hoặc lấy nó trong các view ràng buộc.
Bằng cách này, việc tính toán có thể được unit test một cách thích hợp.
