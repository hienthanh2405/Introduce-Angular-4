<h2> 4. Các directive cơ bản trong Angular: ngFor, ngIf, ngModel </h2>
AngularJS directive được sử dụng để kế thừa HTML. Có những thuộc tính đặc biệt bắt đầu với tiền tố ng-. Chúng ta sẽ thảo luận những directive:

<h3> 4.1 Tìm hiểu về ngIf </h3>
ngIf được sử dụng khi muốn thêm hoặc xóa bỏ một phần tử khi render. 
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
Sử dụng khi muốn render một list các phần tử. 
+ NgFor cung cấp các biến cục bộ, có thể tạo một alias cho các biến đó như:
 - index xác định chỉ số hiện tại của vòng lặp tương ứng.
 - first xác định vòng lặp hiện tại có phải là vòng lặp đầu tiên không -> true : false.
 - last xác định vòng lặp hiện tại có phải là vòng lặp cuối cùng không -> true : false.
 - even xác định vòng lặp hiện tại có phải là vòng lặp có chỉ số chẵn không -> true : false.
 - odd xác định vòng lặp hiện tại có phải là vòng lặp có chỉ số lẻ không -> true : false.

Ví dụ: render list các students trong một class chẳng hạn.
Như ví dụ trên thì ta cũng tạo ra một component tên demo_ngFor. Trong đó sẽ có file:
    <img src="https://i.imgur.com/ZDBT42N.png">
File demo-ng-for.component.ts ta tạo ra một mảng giá trị lưu tất cả thông tin của students.
    <img src="https://i.imgur.com/ZXJAXb4.png">
File demo-ng-for.component.html ta tạo ra một đoạn html thể hiện danh sách students.Như trong hình ta thấy ở thẻ div có cú pháp <h4> <div *ngFor ="let list of arrStudent ;let i=index"> </h4>. Ta sử dụng thẻ *ngFor để duyệt danh sách students trong mảng arrStudent . trong đó ta khởi tạo biến i=index để xác định chỉ số hiện tại.
    <img src="https://i.imgur.com/GaqV3xK.png">
Sau khi hoàn thành những bước trên,chạy chương trình vừa viết thì ta được một list danh sách students trong mảng arrStudent ra màn hình.
   <img src="https://i.imgur.com/8ilTogT.png">
Lưu ý: đừng quên dấu * phía trước ngFor

<h3> 4.3 Tìm hiểu về ngModel </h3>
ngModel là một Directive dùng để liên kết dữ liệu với client, nghĩa là nó thường được dùng để cho người dùng nhập liệu nên ta hay sử dụng trong form html.
Để sử dụng ngModel trong angular 4 thì chúng ta phải import thêm thư viện tại file app.module.ts
    <img src="https://i.imgur.com/mH1gMzr.png">
File user-form.component.ts ta tạo ra biến name.
Sau đó chúng ta có thể sử dụng ngModel cho từng input như sau trong file user-form.component.html :
   <img src="https://i.imgur.com/3HTTgK7.png">
Chúng ta sẽ thêm 2 thuộc tính có tên là [(ngModel)] và name. Đây là cách sử dụng của directive ngModel , với dấu [ biểu thị cho việc Input, và dấu ( biểu thị cho việc Ouput, tức là directive ngModel khi được dùng cho element input thì có thể nhận dữ liệu - vì có khai báo [], và có thể xuất dữ liệu - vì có khai báo (), có nghĩa là bằng việc set giá trị ở thuộc tính [(ngModel)], ở đây là username, chúng ta có thể thông qua biến name ở trong file user-form.component.ts để set/get giá trị cho input name của form.
Hoàn tất các bước trên, chạy chương trình ta được kết quả sau:
  <img src="https://i.imgur.com/TCLil2k.png">




