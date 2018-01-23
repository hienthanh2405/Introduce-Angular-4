<h2> 1.Model và View: Two ways binding. </h2>
Two-way binding chính là cách thức tự động đồng bộ dữ liệu giữa Model và View tra ngoài View cho người dùng thấy được (chẳng hạn như là 1 ô textbox). Khi có bất kì thày đổi trên View này, chẳng hạn như trong ô textbox mình sẽ nhập là abc. Thì tự động dữ liệu abc này sẽ ngay lập tự được đồng bộ vào bên trong Model. Và tiếp theo bên trong Model nếu có bất kỳ sự thay đổi nào sẽ ngay lập tức được đồng bộ ngược lại ra View. Vì thế dữ liệu được trung chuyển từ Model sang View hay từ View sang Model là một thể thống nhất.
Chúng ta vẫn có thể áp dụng Two-way Binding bằng cách sử dụng directive ngModel trong Angular 2.Thẻ ngModel trong cặp dấu [()], nó sẽ thực hiện đồng bộ dữ liệu từ Component vs DOM và ngược lại.
Ví dụ :
         <h4> <input placeholder="Enter username" [(ngModel)]="name" > </h4>
<p>Để sử dụng Two ways binding trong angular thì chúng ta phải import thêm thư viện tại file app.module.ts</p>
</br><img src="https://i.imgur.com/mH1gMzr.png">
# 2. Tìm hiểu về Module, Component, Injectable, Pipe, Directive.

## 2.1. Angular Module
- Một TypeScript/ES6 module là một cách để đóng gói, nhóm, tái sử dụng, phân phối và nạp code trong JavaScript.
- Nói chung, một module sẽ chứa code, đóng gói một chức năng cụ thể. Module sẽ phân phối chức năng này tới phần còn lại của ứng dụng bằng cách định nghĩa một loạt exports, sau đó các phần khác của hệ thống có thể import.
- Module core của Angular 2 là 'angular2/core' và nó cung cấp cho bạn khả năng truy cập tới các chức năng core như Component.
- Angular Modules giúp tổ chúc application theo các tính năng chính của nó. Điều này giúp angular dễ mở rộng với những external libraries (ví dụ Material Design, Ionic.... cũng là các modules).
- Một Angular Module thực chất là một class được đánh dấu bới decorator @NgModule. Tất cả các thành phần trong ứng dụng angular đều được đánh dấu bởi một decorator riêng.
- Decorator sẽ nhận vào một meta data object để nói với Angular cách để compile và run module code này.
- Metadata trong một module gồm:
  + Định nghĩa các components, directives, pipes
  + Export các class cho external module.
  + Import các module cần thiết
  + Provide các service ở tầng ứng dụng để bất kỳ component nào cũng có thể dùng được.
- Module sẽ chứa những components, directives, services, pipes của riêng nó hay sẽ export để external module cũng có thể sử dụng được.
- Nói tóm lại, mỗi module sẽ tập trung vào tính năng, business riêng hoặc là một module chứa các utils.
- Ví dụ về NgModule. Đây là module đứng trên cùng của application.
```
   import { NgModule }      from '@angular/core';
   import { BrowserModule } from '@angular/platform-browser';
   import { AppComponent }  from './app.component';

   @NgModule({
     imports:      [ BrowserModule ],
     declarations: [ AppComponent ],
     bootstrap:    [ AppComponent ]
   })
   export class AppModule { }
```
  + Nhìn vào Module trên, các bạn có thể thấy nó được đánh dấu với decorator @NgModule. Một module BrowserModule, một module chứa các utils mà mọi browser app phải dùng.
  + BrowserModule đăng ký những service quan trọng, đồng thời cũng bao gồm các directives rất quen thuộc như NgIf, NgFor (tương ứng với ng-if và ng-repeat trong Ng1).
  + Thuộc tính declarations để định nghĩa component trong Module. Ở đây chỉ có một mình AppComponent, được coi là root component của app.
  + Bạn có thể tưởng tượng Module này như là một module cha cho những module sau này.
  ![app module](https://user-images.githubusercontent.com/35052781/35087864-3b7053b6-fc64-11e7-8def-0bfd78e82b49.png)
  + Còn AppComponent như là một base component để những component từ những Module khác dựa vào.
  ![ba4d06e1-d6ee-4a7c-8d20-e7829a09d882](https://user-images.githubusercontent.com/35052781/35087941-7711f8b6-fc64-11e7-90ea-3c271b1301c7.png)
- Giả sử có một ứng dụng quản lý sinh viên, giáo viên của một trường học với các tính năng chính là :
  + Đăng nhập, đăng ký, ..
  + Quản lý thông tin sinh viên, giáo viên
  + Cung cấp tính năng đăng ký học online.
  Nhìn vào các tính năng chính trên thì chúng ta có thể tách ứng dụng thành các module như sau: AuthenticationModule, StudentManagementModule, TeacherManagementModule, RegisterOnlineModule.
  
## 2.2. Component
### Component là gì?
- Component là các khối xây dựng lên ứng dụng Angular 2. Nó biểu diễn một phần có thể tái sử dụng của UI, thường là một một phần tử custom html.
- Một component thành lập bởi ít nhất một phần code html cái được biết là template, một class đóng gói dữ liệu và các tương tác với template, và selector (tên phần tử custom html).
- Ví dụ  Component App:
```
   import { Component } from '@angular/core';

   @Component({
     selector: 'my-app',
     template: '<h1>My First Angular  App</h1>'
   })
   export class AppComponent { }
```
  + Nó có một class AppComponent cái được decorated bởi một vài metadata. Decorator @Component liên kết class với template và selector my-app (phần tử <my-app> trong file index.html).
  + Metadata này nói với Angular 2 rằng bất cứ khi nào thấy phần tử html <my-app>, thì sẽ render template này trong bối cảnh của AppComponent class.
- Component điều chỉnh 1 phần trên màn hình (view), có thể chứa nhiều thẻ html, có thể chứa component khác, có thể nhận tham số và rất linh hoạt.
- Lợi ích của Component: dễ quản lý code và tái sử dụng code.

### Cách tạo 1 Component trong Angular 4
- Cách đặt tên component:" tên.component.ts"
- Các bước tạo 1 Component:
  + Bước 1: Trong src/app/People mình tạo file ra people.component.ts
```
   import { Component } from '@angular/core';

   @Component({
     selector: 'app-people',
     templateUrl: './people.component.html'
   })

   export class PeopleComponent {
     titlePeople = "Demo Component"
   }
```
  + Bước 2: Tiếp theo mình gọi Components mình mới tạo ra trong file app.module.ts để nó chạy được trong thư mục src/app/app.module.ts
```
   import { BrowserModule } from '@angular/platform-browser';
   import { NgModule } from '@angular/core';

   import { AppComponent } from './app.component';
   import { PeopleComponent } from './People/people.component';

   @NgModule({
     declarations: [
       AppComponent,
       PeopleComponent
     ],
     imports: [
       BrowserModule
     ],
     providers: [],
     bootstrap: [AppComponent]
   })
   export class AppModule { }
```
  + Bước 3:Mình cần import PeopleComponent vào trong app.module.ts để nó có thể chạy được
 ``` 
    import { PeopleComponent } from './People/people.component';
 ```
  + Bước 4: Bây giờ mình vào srec/app/app.component.html mình gọi ra là xong:
```
   <app-people></app-people>
```

  selecetor <app-people> nằm trong file  trong file people.component.ts
```
   @Component({
     selector: 'app-people',
     templateUrl: './people.component.html'
   })
```
  Đó chính là selector của nó. Bây giờ trong component ( people.component.ts ), bạn muốn hiển thị điều gì ra màn hình thì ghi vô titlePeople:
```
   export class PeopleComponent {
   titlePeople = "Demo Component"
}
```
   Đó chính là biến mình sẽ gọi ra trong file pepople.component.html
```
   <h2>{{ titlePeople }}</h2>
```
  Và khi run lên thì nó sẽ hiển thị trên trình duyệt là Demo Component
- Note: Ngoài ra, ta còn cách tạo nhanh 1 component bằng CLI: "ng g c tencomponent", nó sẽ tự động làm 4 bước trên giúp ta, ta chỉ cần vô các file đã được tạo ra và chỉnh sửa là ok.   

## 2.3. Pipe trong Angular
  Bạn có dữ liệu nhận được từ đâu đó(ví dụ như từ API trả về) cho kiểu Date là dãy số kiểu long, bây giờ bạn phải hiển thị dữ liệu đó thành dạng mà người dùng có thể hiểu được trong ứng dụng viết bằng Angular. Làm thế nào để thực hiện điều đó trong Angular? Sau đây mình sẽ giới thiệu cho các bạn về Pipe trong Angular – một thành phần cơ bản của Angular.
### Pipe là gì?
- Pipe được dùng để chuyển đổi dữ liệu mà bạn hiển thị lên template cho người dùng có thể hiểu được.
- Ví dụ: định dạng ngày tháng cho kiểu Date, viết hoa các chữ cái đầu tiên của tên riêng như tên người, tên thành phố, etc...
- Angular cung cấp cho chúng ta các Pipes sau đây (những Pipes là Stable): AsyncPipe, CurrencyPipe, DatePipe, DecimalPipe, JsonPipe, LowerCasePipe, PercentPipe, SlicePipe, TitleCasePipe, UpperCasePipe.
 ![pipe](https://user-images.githubusercontent.com/35052781/35133888-64d435be-fd05-11e7-9cd9-47359a4c8ed9.png)
  Trong đó có TitleCasePipe là pipe có từ phiên bản Angular 4.

### Pipe sử dụng như thế nào?
- Nếu bạn sử dụng Date và Currency pipes thì bạn cần phải có thêm polyfill để support trên các trình duyệt cũ, bằng việc thêm đoạn script sau vào file index.html
```
   <script src="https://cdn.polyfill.io/v2/polyfill.min.js?features=Intl.~locale.en"></script>
```
- Hoặc nếu bạn sử dụng Angular CLI thì chạy lệnh cài đặt npm install --save intl và uncomment dòng sau trong file polyfill.ts
```
   import 'core-js/es6/reflect';
   import 'core-js/es7/reflect';
   import 'zone.js/dist/zone';
```
- Chúng ta có thể sử dụng một pipe duy nhất, có thể bao gồm cả tham số, hoặc có thể sử dụng pipe theo tuần tự – với kết quả của pipe này là đầu vào của pipe tiếp theo.
- Ví dụ:
  + Sử dụng Pipe lowercase và uppercase: (sử dụng không có tham số)
```
   @Component({
     selector: 'lowerupper-pipe',
     template: `<div>
       <label>Name: </label><input #name (keyup)="change(name.value)" type="text">
       <p>In lowercase: {{value | lowercase}}</p>
       <p>In uppercase: {{value | uppercase}}</p>
     </div>`
   })
   export class LowerUpperPipeComponent {
     value: string;
     change(value: string) { 
       this.value = value; 
     }
   }
```
  + Sử dụng có tham số như Pipe date:
```
   @Component({
     selector: 'date-pipe',
     template: `<div>
       <p>Today is {{today | date}}</p>
       <p>Or if you prefer, {{today | date:'fullDate'}}</p>
       <p>The time is {{today | date:'jmZ'}}</p>
     </div>`
   })
   export class DatePipeComponent {
     today: number = Date.now();
   } 
```
  + Sử dụng nhiều tham số như Pipe slice:
```
   @Component({
     selector: 'slice-list-pipe',
     template: `<ul>
       <li *ngFor="let i of collection | slice:1:3">{{ i }}</li>
     </ul>`
   })
   export class SlicePipeListComponent {
     collection: string[] = ['a', 'b', 'c', 'd'];
   } 
```
  +Sử dụng nhiều Pipe tuần tự – Chaining Pipe:
```
   @Component({
     selector: 'date-pipe',
     template: `<div>
       <p>Today is {{today | date | lowercase}}</p>
       <p>Or if you prefer, {{today | date:'fullDate' | lowercase}}</p>
       <p>The time is {{today | date:'jmZ' | uppercase}}</p>
     </div>`
   })
   export class DatePipeComponent {
     today: number = Date.now();
   }
``` 
- Trong Angular chia làm hai loại Pipe là pure pipe và impure pipe:
  + Pure pipe: chỉ thực hiện thay đổi khi đầu vào thay đổi. (các immutable objects, primitive type: string, number, boolean, etc): lowercase, uppercase, date, etc...
  + Impure pipe: thực hiện thay đổi mỗi chu kỳ của Change detection (chu kỳ kiểm tra xem các state trong ứng dụng có thay đổi không để update lên view): async, json, etc...

### Cách tạo một Custom Pipe trong Angular như thế nào?
- Đầu tiên, chúng ta tạo một class và decorate nó với decorator @Pipe, decorator này cần tối thiểu một object có property name, chính là tên của pipe.
- Ví dụ, chúng ta có thể tạo một pipe để convert nhiệt độ giữa độ C và độ F với tên tempConverter như sau:
```
  import { Pipe } from '@angular/core';

  @Pipe({
     name: 'tempConverter'
   })
   export class TempConverterPipe {
   }
```
 + Mặc định khi tạo là pure pipe.
 + Tiếp theo, chúng ta cần implement một interface là PipeTransform, và implement hàm transform của interface đó:
```
   import { Pipe, PipeTransform } from '@angular/core';

   @Pipe({
    name: 'tempConverter'
   })
   export class TempConverterPipe implements PipeTransform {
     transform(value: any, ...args: any[]): any {
     }
   }
``` 
  + Trong hàm transform, chúng ta sẽ thực hiện các công việc để biến đổi đầu vào ra kết quả mong muốn ở đầu ra.
  + Sau khi hoàn thành implement class Pipe ở trên, chúng ta cần khai báo vào NgModule mà nó thuộc về để có thể sử dụng nó trong toàn module đó:
```
   import { TempConverterPipe } from './pipes/temp-converter.pipe';

   @NgModule({
     declarations: [
      // các Component, Directive, Pipe khác
       TempConverterPipe
     ],
     imports: [...],
     providers: [...],
     //...
   })
   export class AppModule { }
```
  + Sử dụng pipe ở trong Component như sau:
```
   Temperature {{ temp | tempConverter:true:'F' }}
```

## 2.4. Tổng quan về Directives
- Directives là một thành phần mở rộng HTML, hay nói cách khác là các thuộc tính (properties) của các thẻ HTML mà Angular nó định nghĩa thêm, vì nó là riêng của Angular nên phải tuân thủ theo nguyên tắc của nó là chữ bắt đầu luôn luôn là ký tự "ng-prefix", trong đó tiền tố prefix là tên của derective mà chúng ta sử dụng. 
  Như ở các ví dụ trước, để khai báo là một Directive Controller thì chúng ta khai báo "ng-controller"
- Có 3 loại directive trong Angular:
  + Components(Một Component là một directive với một template. Đây là directive phổ biến nhất trong ba directive và chúng ta thường dùng chúng nhiều khi xây dựng ứng dụng.)
  + Structure directives(Structural directive có thể thay đổi cấu trúc DOM bằng cách thêm hay bớt phần tử DOM. NgFor và NgIf là hai ví dụ quen thuộc.)
  + Attribute directives(Một Attribute directive có thể thay đổi giao diện hay hành vi của một phần tử. NgStyle là một ví dụ, có thể thay đổi nhiều style cho phần tử cùng lúc.)
- Các directive thường dùng:
### NgIf
- Sử dụng khi muốn thêm hoặc xóa bỏ một phần tử khi render. Ví dụ: hiển thị thông báo lỗi khi người dùng nhập form chưa đúng.
- Cú pháp: ```<h2 *ngIf="printable">{{ message }}</h2>```
- Lưu ý: đừng quên dấu * phía trước ngIf directive

### NgFor
- Sử dụng khi muốn render một list các phần tử. Ví dụ: render list các bài học trong một series chẳng hạn.
- Cú pháp:
```
   <div *ngFor="let contact of contacts">
     <h3>{{ contact.name }}</h3>
     <div>
       <img *ngIf="contact.avatar?.url" [src]="contact.avatar?.url" alt="Avatar of {{ contact.name }}">
     </div>
   </div>
```
- Lưu ý: đừng quên dấu * phía trước ngFor directive và sử dụng cấu trúc "let tenbien of tenmang"

### NgSwitchCase
- Sử dụng thay thế việc if nhiều lần, tương tự như switch-case trong Javascript.
- Cú pháp: 
```
   <div [ngSwitch]="conditionExpression">
     <template [ngSwitchCase]="case1Exp">...</template>
     <template ngSwitchCase="case2LiteralString">...</template>
     <template ngSwitchDefault>...</template>
   </div>
```
Hoặc:
```
   <div [ngSwitch]="tabIndex">
     <div *ngSwitchCase="1">
       <div>
         Tab content 1
       </div>
       <p>
         Lorem ipsum dolor sit amet, consectetur adipisicing elit. Labore, rerum.
       </p>
     </div>
     <div *ngSwitchCase="2">
       <div>
         Tab content 2
       </div>
       <p>
         Raw denim you probably haven't heard of them jean shorts Austin. Nesciunt tofu stumptown aliqua, retro synth master cleanse.
       </p>
     </div>
     <div *ngSwitchCase="3">
       <div>
         Tab content 3
       </div>
       <p>
         Lorem ipsum dolor sit amet, consectetur adipisicing elit. Ducimus a sequi cupiditate accusantium vitae impedit eum illo voluptatem neque, nisi.
       </p>
     </div>
   </div>
```
- Lưu ý: Không có dấu *ở phía trước ngSwitch directive. Thay vào đó, sử dụng property binding.
         Đặt dấu * ở phía trước ngSwitchCasevà ngSwitchDefault. Trường hợp sử dụng với thẻ template như ở ví dụ đầu tiên của ngSwitch thì không.

### ngStyle
- Dùng để thay đổi nhiều style của phần từ.
- Cú pháp:
```
   <some-element [ngStyle]="{'font-style': styleExp}">...</some-element>
   <some-element [ngStyle]="{'max-width.px': widthExp}">...</some-element>
   <some-element [ngStyle]="objExp">...</some-element>
```
- Ví dụ:
```
   <div [ngStyle]="{
       // CSS property names
       'font-style': canSave ? 'italic' : 'normal',        // italic
       'font-weight': !isUnchanged ? 'bold' : 'normal',    // normal
       'font-size.px': isSpecial ? 24 : 8,                 // with unit
     }">
     This div is cool.
   </div>
```
Hoặc:
```
   <div [ngStyle]="objStyle">
     This div is cool.
   </div>
   objStyle = {
     // CSS property names
     'font-style': this.canSave ? 'italic' : 'normal',        // italic
     'font-weight': !this.isUnchanged ? 'bold' : 'normal',    // normal
     'font-size.px': this.isSpecial ? 24 : 8,                 // with unit
   };
```

### ngClass
- Cú pháp:
```
   <some-element ngClass="first second">...</some-element>     // bind string
   <some-element [ngClass]="'first second'">...</some-element> // bind string value
   <some-element [ngClass]="['first', 'second']">...</some-element> // bind array
   <some-element [ngClass]="{    // bind object
       'first': true,
       'second': true,
       'third': false
       }">
       ...
   </some-element>
   <some-element [ngClass]="stringExp|arrayExp|objExp">    // variable
       ...
   </some-element>
```
  + string: là một list các CSS class, cách nhau bởi dấu cách.
  + array: là array string CSS class.
  + object: key -> value, nếu value = true thì add, ngược lại thì remove.
- Ví dụ: 
```
   <button class="btn" [ngClass]="'active btn-primary'">
       String binding
   </button>
   // or
   <button class="btn" ngClass="active btn-primary">
      String binding
   </button>
   // or
   <button class="btn" [ngClass]="['active', 'btn-primary']">
       Array binding
   </button>
   // or
   <button class="btn" [ngClass]="{active: tabIndex == 1}">
      Object binding
   </button>
```
<br>
<h2>3. Lập Trình Hướng Đối Tượng Với Typescript</h2>
<p>
TypeScript là một ngôn ngữ mã nguồn mở miễn phí của Microsoft. 
Nó là superset của JavaScript. Có 4 tính chất của một ngôn ngữ lập trình hướng đối tượng 
là tính bao đóng (encapsulation), tính kế thừa(inheritance), tính đa hình(polymorphism), tính trừu tượng(Abstraction)
</p>
<h3>3.1	Tính kế thừa (Inheritance)</h3>
<p>Đặc tính này cho phép một đối tượng có thể có sẵn các đặc tính mà đối tượng khác đã có. Điều này cho phép các đối tượng chia sẻ hay mở rộng các đặc tính sẵn có mà không phải tiến hành định nghĩa lại. 
Sử dụng chúng thông qua từ khóa extends và cho phép các class và interface thừa kế các resource.</p>
<h3>3.2	Tính trừu tượng (Abstraction)</h3>
<p>Lớp trừu tượng là lớp mà từ đó các lớp khác có thể kế thừa được. Lớp trừu tượng có thể chứa các thuộc tính cũng như các hàm thực thi(các phương thức abstract thì chỉ khai báo chứ không thực thi). </p>
<img src="https://i.imgur.com/zuHYypU.png">
<img src="https://i.imgur.com/At0J9iD.png">
<i>Tính trừu tượng cho phép tạo ra các thông tin không được hiển thị rõ ràng và tính đóng gói cho phép một người lập trình thể hiện tính trừu tượng ở mức độ mong muốn.</i>
<h3>3.3	Tính đa hình (Polymorphism)</h3>
<p>Tính đa hình trong lập trình hướng đối tượng là sự thay đổi hành vi của phương thức ở mỗi đối tượng khác nhau thể hiện thông qua việc gửi các thông điệp (việc gọi các hàm bên trong của một đối tượng.).</p>
<p>Ví dụ: khi định nghĩa hai đối tượng “Square” và “Cicle” thì có một phương thức chung là “Perimeter”. Khi gọi phương thức này thì nếu đối tượng là “Square” nó sẽ tính theo công thức khác với khi đối tượng là “Cicle”.</p>
<img src="https://i.imgur.com/X7NypmN.png">
<img src="https://i.imgur.com/lUIioq2.png">
<p>Đa hình: Thể hiện rõ nhất trong override và overload của superclass và subclass.</p>
<p>Override: là hai phương thức cùng tên, cùng tham số, cùng kiểu trả về nhưng thằng con viết lại và dùng theo cách của nó, và xuất hiện ở lớp cha và tiếp tục xuất hiện ở lớp con. Khi dùng nó sẽ ưu tiên gọi thằng cha.. sau đó thằng cha mà không có thì sẽ gọi thằng con.</p>
<p>Overload: hai phương thức cùng tên nhưng phải khác tham số hoặc kiểu trả về (áp trong cùng một class).</p>
<p>Ví dụ: Hàm khởi tạo luôn có tên giống với class. Một class có thể có nhiều hàm khởi tạo(Override). Một hàm khởi tạo có thể có  hoặc không có tham số, hàm không có tham số được gọi là hàm khởi tạo mặc định(Overload).</p>
<h3>3.4	Tính bao đóng (Encapsulation):</h3>
<p>Tính chất này không cho phép người dùng hay đối tượng thay đổi dự liệu thành viên của đối tượng nội nhằm đảm bảo sự toàn vẹn của đối tượng. 
Không cho phép bên ngoài biết được bên trong đối tượng có những gì hay logic xử lí như thế nào, 
nếu muốn thay đổi bên trong đối tượng thi phải được sự chấp nhận của đối tượng đó thông qua các mức độ truy cập(access modifier) private, default (hay là pravite package) , protected, public.</p>
<img src="https://i.imgur.com/r7Undr9.png">
<br>
<h2> 4. Các directive cơ bản trong Angular: ngFor, ngIf, ngModel </h2><br>
Angular directive được sử dụng để kế thừa HTML. Có những thuộc tính đặc biệt bắt đầu với tiền tố ng-. Chúng ta sẽ thảo luận những directive:<br>
  <h3> 4.1 Tìm hiểu về ngIf </h3><br>
Chúng ta dùng chỉ thị *ngIf để thực hiện biểu thức điều kiện.Theo sau *ngIf là một câu lệnh so sánh hay bất cứ một biểu thức là mà có trả về giá trị true hoặc false.<br>
Ví dụ: hiển thị ẩn hoặc hiện hình ảnh<br>
Ban đầu ta tạo một component tên demo_ngIF. Khi tạo xong thì nó sẽ có những file sau:<br>
         <img src="https://i.imgur.com/QVLAdgj.png"><br>
Trong file demo-ng-if.component.html ta viết:<br>
        <img src="https://i.imgur.com/TD2QjG8.png"><br>
File demo-ng-if.component.ts ta tạo thêm một biến isShowImg = true và một link ảnh bất kì. <br>
        <img src="https://i.imgur.com/plW499Q.png"><br>
Sau khi hoàn tất ta cho chạy chương trình thì kết quả sẽ hiện ra 1 form có hình ảnh và một button.<br>
        <img src="https://i.imgur.com/orucZW4.png"><br>
Nhờ vào thẻ ngIf nên khi ta bấm vào button Show Image thì hình ảnh trong form sẽ ẩn hoặc hiện.<br>
        <img src="https://i.imgur.com/bwnRwTh.png"><br>
Lưu ý: đừng quên dấu * phía trước ngIf<br>
<h3> 4.2 Tìm hiểu về ngFor </h3><br>
Chúng ta dùng thẻ *ngFor để thực hiện việc duyệt các kiểu dữ liệu danh sách (như mảng)<br>
<ul>

<li> NgFor cung cấp các biến cục bộ, có thể tạo một alias cho các biến đó như:</li>

<li> index xác định chỉ số hiện tại của vòng lặp tương ứng.</li>
<li> first xác định vòng lặp hiện tại có phải là vòng lặp đầu tiên không -> true : false.</li>
<li> last xác định vòng lặp hiện tại có phải là vòng lặp cuối cùng không -> true : false.</li>

<li> even xác định vòng lặp hiện tại có phải là vòng lặp có chỉ số chẵn không -> true : false.</li>

<li> odd xác định vòng lặp hiện tại có phải là vòng lặp có chỉ số lẻ không -> true : false.</li>

</ul>
Giá trị của ngFor là một câu lệnh có cú pháp như sau:<br>
   <h4> let <biến lặp> of <danh sách> </h4><br>
Biến lặp là do chúng ta tự đặt, bạn muốn đặt là gì cũng được, ngFor sẽ lặp qua danh sách và mỗi lần lặp thì chúng ta dùng biến lặp để lấy dữ liệu của phần tử hiện tại trong danh sách.
<br>
Ví dụ: render list các students trong một class chẳng hạn.<br>
Như ví dụ trên thì ta cũng tạo ra một component tên demo_ngFor. Trong đó sẽ có file:<br>
         <img src="https://i.imgur.com/ZDBT42N.png">
<br>
File demo-ng-for.component.ts ta tạo ra một mảng giá trị lưu tất cả thông tin của students.
<br>
         <img src="https://i.imgur.com/ZXJAXb4.png"><br>
File demo-ng-for.component.html ta tạo ra một đoạn html thể hiện danh sách students.Như trong hình ta thấy ở thẻ div có cú pháp <h4> <div *ngFor ="let list of arrStudent ;let i=index"> </h4>. Chúng ta dùng thuộc tính *ngFor="let list of arrStudent ;let i=index " để duyệt danh sách students trong mảng arrStudent . trong đó ta khởi tạo biến i=index để xác định chỉ số hiện tại.<br>
         img src="https://i.imgur.com/GaqV3xK.png"><br>
Sau khi hoàn thành những bước trên,chạy chương trình vừa viết thì ta được một list danh sách students trong mảng arrStudent ra màn hình.<br>
        <img src="https://i.imgur.com/8ilTogT.png"><br>
Lưu ý: đừng quên dấu * phía trước ngFor
<br>
<h3> 4.3 Tìm hiểu về ngModel </h3><br>
ngModel là một Directive dùng để liên kết dữ liệu với client, nghĩa là nó thường được dùng để cho người dùng nhập liệu nên ta hay sử dụng trong form html.<br>
Một yêu cầu cần có của thẻ ngModel là bạn phải import lớp FormsModule vào file app.module.ts thì mới có thể sử dụng:
<br>
        <img src="https://i.imgur.com/mH1gMzr.png"><br>
File user-form.component.ts ta tạo ra biến name.<br>
Sau đó chúng ta có thể sử dụng ngModel cho từng input như sau trong file user-form.component.html : <br>
       <img src="https://i.imgur.com/3HTTgK7.png"> <br>
Chúng ta sẽ thêm 2 thuộc tính có tên là [(ngModel)] và name. Đây là cách sử dụng của directive ngModel , với dấu [ biểu thị cho việc Input, và dấu ( biểu thị cho việc Ouput, tức là directive ngModel khi được dùng cho element input thì có thể nhận dữ liệu - vì có khai báo [], và có thể xuất dữ liệu - vì có khai báo (), có nghĩa là bằng việc set giá trị ở thuộc tính [(ngModel)], ở đây là username, chúng ta có thể thông qua biến name ở trong file user-form.component.ts để set/get giá trị cho input name của form.<br>
Hoàn tất các bước trên, chạy chương trình ta được kết quả sau: <br>
       <img src="https://i.imgur.com/TCLil2k.png">

