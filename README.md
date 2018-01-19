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
