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
```import { NgModule }      from '@angular/core';
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
```import { Component } from '@angular/core';

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
```import { Component } from '@angular/core';

   @Component({
     selector: 'app-people',
     templateUrl: './people.component.html'
   })

   export class PeopleComponent {
     titlePeople = "Demo Component"
   }
```
  + Bước 2: Tiếp theo mình gọi Components mình mới tạo ra trong file app.module.ts để nó chạy được trong thư mục src/app/app.module.ts
```import { BrowserModule } from '@angular/platform-browser';
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
 ``` import { PeopleComponent } from './People/people.component';```
  + Bước 4: Bây giờ mình vào srec/app/app.component.html mình gọi ra là xong:
```<app-people></app-people>```

  selecetor <app-people> nằm trong file  trong file people.component.ts
```@Component({
     selector: 'app-people',
     templateUrl: './people.component.html'
   })
```
  Đó chính là selector của nó. Bây giờ trong component ( people.component.ts ), bạn muốn hiển thị điều gì ra màn hình thì ghi vô titlePeople:
```export class PeopleComponent {
   titlePeople = "Demo Component"
}
```
   Đó chính là biến mình sẽ gọi ra trong file pepople.component.html
```<h2>{{ titlePeople }}</h2>```
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
```<script src="https://cdn.polyfill.io/v2/polyfill.min.js?features=Intl.~locale.en"></script>```
- Hoặc nếu bạn sử dụng Angular CLI thì chạy lệnh cài đặt npm install --save intl và uncomment dòng sau trong file polyfill.ts
```import 'core-js/es6/reflect';
   import 'core-js/es7/reflect';
   import 'zone.js/dist/zone';
```
- Chúng ta có thể sử dụng một pipe duy nhất, có thể bao gồm cả tham số, hoặc có thể sử dụng pipe theo tuần tự – với kết quả của pipe này là đầu vào của pipe tiếp theo.
- Ví dụ:
  + Sử dụng Pipe lowercase và uppercase: (sử dụng không có tham số)
```@Component({
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
```@Component({
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
```@Component({
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
```@Component({
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
```import { Pipe } from '@angular/core';

  @Pipe({
     name: 'tempConverter'
   })
   export class TempConverterPipe {
   }
```
 + Mặc định khi tạo là pure pipe.
 + Tiếp theo, chúng ta cần implement một interface là PipeTransform, và implement hàm transform của interface đó:
```import { Pipe, PipeTransform } from '@angular/core';

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
```import { TempConverterPipe } from './pipes/temp-converter.pipe';

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
```Temperature {{ temp | tempConverter:true:'F' }}```
