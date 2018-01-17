<h2> 4. Các directive cơ bản trong Angular: ngFor, ngIf, ngModel </h2>

AngularJS directive được sử dụng để kế thừa HTML. Có những thuộc tính đặc biệt bắt đầu với tiền tố ng-. Chúng ta sẽ thảo luận những directive:

<h3> 4.1 Tìm hiểu về ngIf </h3>
Chúng ta dùng chỉ thị *ngIf để thực hiện biểu thức điều kiện.Theo sau *ngIf là một câu lệnh so sánh hay bất cứ một biểu thức là mà có trả về giá trị true hoặc false.

Ví dụ: hiển thị ẩn hoặc hiện hình ảnh
Ban đầu ta tạo một component tên demo_ngIF. Khi tạo xong thì nó sẽ có những file sau:

    <img src="https://i.imgur.com/QVLAdgj.png">

Trong file demo-ng-if.component.html ta viết:

    <img src="https://i.imgur.com/TD2QjG8.png">

File demo-ng-if.component.ts ta tạo thêm một biến isShowImg = true và một link ảnh bất kì. .

    <img src="https://i.imgur.com/plW499Q.png">

Sau khi hoàn tất ta cho chạy chương trình thì kết quả sẽ hiện ra 1 form có hình ảnh và một button.

<img src="https://i.imgur.com/orucZW4.png">

Nhờ vào thẻ ngIf nên khi ta bấm vào button Show Image thì hình ảnh trong form sẽ ẩn hoặc hiện.

    <img src="https://i.imgur.com/bwnRwTh.png">

Lưu ý: đừng quên dấu * phía trước ngIf 


<h3> 4.2 Tìm hiểu về ngFor </h3>

Chúng ta dùng thẻ *ngFor để thực hiện việc duyệt các kiểu dữ liệu danh sách (như mảng)

<ul>
<li> NgFor cung cấp các biến cục bộ, có thể tạo một alias cho các biến đó như:</li>
<li> index xác định chỉ số hiện tại của vòng lặp tương ứng.</li>
<li> first xác định vòng lặp hiện tại có phải là vòng lặp đầu tiên không -> true : false.</li>
<li> last xác định vòng lặp hiện tại có phải là vòng lặp cuối cùng không -> true : false.</li>
<li> even xác định vòng lặp hiện tại có phải là vòng lặp có chỉ số chẵn không -> true : false.</li>
<li> odd xác định vòng lặp hiện tại có phải là vòng lặp có chỉ số lẻ không -> true : false.</li>
</ul>

Giá trị của ngFor là một câu lệnh có cú pháp như sau:
 <h4> let <biến lặp> of <danh sách> </h4>

Biến lặp là do chúng ta tự đặt, bạn muốn đặt là gì cũng được, ngFor sẽ lặp qua danh sách và mỗi lần lặp thì chúng ta dùng biến lặp để lấy dữ liệu của phần tử hiện tại trong danh sách.

Ví dụ: render list các students trong một class chẳng hạn.

Như ví dụ trên thì ta cũng tạo ra một component tên demo_ngFor. Trong đó sẽ có file:

    <img src="https://i.imgur.com/ZDBT42N.png">

File demo-ng-for.component.ts ta tạo ra một mảng giá trị lưu tất cả thông tin của students.

    <img src="https://i.imgur.com/ZXJAXb4.png">

File demo-ng-for.component.html ta tạo ra một đoạn html thể hiện danh sách students.Như trong hình ta thấy ở thẻ div có cú pháp <h4> <div *ngFor ="let list of arrStudent ;let i=index"> </h4>. Chúng ta dùng thuộc tính *ngFor="let list of arrStudent ;let i=index " để duyệt danh sách students trong mảng arrStudent . trong đó ta khởi tạo biến i=index để xác định chỉ số hiện tại.

    <img src="https://i.imgur.com/GaqV3xK.png">

Sau khi hoàn thành những bước trên,chạy chương trình vừa viết thì ta được một list danh sách students trong mảng arrStudent ra màn hình.

   <img src="https://i.imgur.com/8ilTogT.png">

Lưu ý: đừng quên dấu * phía trước ngFor

<h3> 4.3 Tìm hiểu về ngModel </h3>

ngModel là một Directive dùng để liên kết dữ liệu với client, nghĩa là nó thường được dùng để cho người dùng nhập liệu nên ta hay sử dụng trong form html.

Một yêu cầu cần có của thẻ ngModel là bạn phải import lớp FormsModule vào file app.module.ts thì mới có thể sử dụng:

     <img src="https://i.imgur.com/mH1gMzr.png">

File user-form.component.ts ta tạo ra biến name.

Sau đó chúng ta có thể sử dụng ngModel cho từng input như sau trong file user-form.component.html :

   <img src="https://i.imgur.com/3HTTgK7.png">

Chúng ta sẽ thêm 2 thuộc tính có tên là [(ngModel)] và name. Đây là cách sử dụng của directive ngModel , với dấu [ biểu thị cho việc Input, và dấu ( biểu thị cho việc Ouput, tức là directive ngModel khi được dùng cho element input thì có thể nhận dữ liệu - vì có khai báo [], và có thể xuất dữ liệu - vì có khai báo (), có nghĩa là bằng việc set giá trị ở thuộc tính [(ngModel)], ở đây là username, chúng ta có thể thông qua biến name ở trong file user-form.component.ts để set/get giá trị cho input name của form.
Hoàn tất các bước trên, chạy chương trình ta được kết quả sau:

  <img src="https://i.imgur.com/TCLil2k.png">

<h2> 1.Model và View: Two ways binding. </h2>

Two-way binding chính là cách thức tự động đồng bộ dữ liệu giữa Model và View tra ngoài View cho người dùng thấy được (chẳng hạn như là 1 ô textbox). Khi có bất kì thày đổi trên View này, chẳng hạn như trong ô textbox mình sẽ nhập là abc. Thì tự động dữ liệu abc này sẽ ngay lập tự được đồng bộ vào bên trong Model. Và tiếp theo bên trong Model nếu có bất kỳ sự thay đổi nào sẽ ngay lập tức được đồng bộ ngược lại ra View. Vì thế dữ liệu được trung chuyển từ Model sang View hay từ View sang Model là một thể thống nhất.
Chúng ta vẫn có thể áp dụng Two-way Binding bằng cách sử dụng directive ngModel trong Angular 2.Thẻ ngModel trong cặp dấu [()], nó sẽ thực hiện đồng bộ dữ liệu từ Component vs DOM và ngược lại.
 Ví dụ :
      <h4> <input placeholder="Enter username" [(ngModel)]="name" > </h4>
Để sử dụng Two ways binding trong angular thì chúng ta phải import thêm thư viện tại file app.module.ts

    <img src="https://i.imgur.com/mH1gMzr.png">





