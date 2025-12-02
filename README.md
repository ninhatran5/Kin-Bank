# hưỡng dẫn cấu trúc của trương trình, các yêu cầu để phát triển,các chức năng và giải thích 
# Bank-Account-Management-Sytem
Hệ thống quản lý tài khoản ngân hàng 
- xây dựng 1 chương trình quản lý tài khoản ngân hàng với nội dung yêu cầu như sau 

# yêu cầu 1 chương trình bao gồm như sau 
# 1 mục tiêu tổng quan:
Xây dựng hệ thống COBOL giúp ngân hàng quản lý tài khoản khách hàng:
+ Tạo tài khoản

+ Đăng nhập bằng tài khoản + mật khẩu

+ Gửi tiền

+ Rút tiền

+ Kiểm tra số dư

+ Xem lịch sử giao dịch

+ Lưu dữ liệu vào file tuần tự


# 2 yêu cầu chức năng chi tiết
*2.1 module đăng nhập 
-mục đích : Xác thực người dùng trước khi cho phép thực hiện các thao tác ngân hàng.

-luồng hoạt động

1.Nhập Account Number

2.Nhập Password

3.Chương trình tìm dữ liệu trong ACCOUNTS.DAT

4.Nếu trùng → đăng nhập thành công

5.Nếu sai quá 3 lần → khoá phiên, thoát chương trình

-yêu cầu về bảo mật

+ Mật khẩu lưu dạng plain-text (vì COBOL không hỗ trợ hash phức tạp trong bài tập), nhưng Hiển thị dạng ***** khi nhập

+ Password tối đa 20 ký tự

+ Có chức năng đổi mật khẩu

*2.2 tạo tài khoản
-dữ liệu cần nhập
+ Customer ID

+ Customer Name

+ Initial Balance

+ Password (nhập 2 lần để xác nhận)

-tính năng 

+ Tự sinh Account Number (10 chữ số)

+ Kiểm tra trùng Account Number

+ Lưu vào file ACCOUNTS.DAT

*2.3 gửi tiền

-yêu cầu 
+ Chỉ thực hiện sau khi đăng nhập

+ Nhập số tiền

+ Kiểm tra số tiền > 0

+ Cộng số dư và ghi lại vào file

+ Ghi giao dịch vào TRANSACTIONS.DAT

-giao dịch lưu dạng:

////////////////////

TYPE = "DEPOSIT"

////////////////////

*2.4 rút tiền 
-yêu cầu 

+ Chỉ thực hiện sau khi đăng nhập

+ Nhập số tiền

+ Kiểm tra số dư đủ

+ Trừ số dư

+ Ghi giao dịch vào file

-giao dịch lưu dạng:

////////////////////

TYPE = "WITHDRAW"

////////////////////

*2.5 kiểm tra số dư
-hiển thị:

+ Account Number

+ Customer Name

+ Current Balance

+ 3 giao dịch gần nhất

*2.6 Xem lịch sử giao dịch

-Yêu cầu:

+ Nhập số lượng giao dịch muốn xem

+ Đọc file TRANSACTIONS.DAT

+ Lọc theo Account Number

+ Hiển thị theo thứ tự mới nhất → cũ nhất

*2.7 Đổi mật khẩu

-Luồng:

+ Nhập mật khẩu hiện tại

+ Nhập mật khẩu mới

+ Nhập lại mật khẩu mới

+ Update vào file ACCOUNT

# 3. CẤU TRÚC FILE DỮ LIỆU
*3.1. File ACCOUNTS.DAT

01 ACCOUNT-RECORD.

   05 ACCOUNT-NO        PIC 9(10).
   
   05 CUSTOMER-ID       PIC X(10).
   
   05 CUSTOMER-NAME     PIC X(50).
   
   05 PASSWORD          PIC X(20).   
   
   05 BALANCE           PIC 9(12)V99.
   

*3.2. File TRANSACTIONS.DAT

01 TRANSACTION-RECORD.

   05 ACCOUNT-NO        PIC 9(10).
   
   05 DATE-TIME         PIC X(19).        *> YYYY-MM-DD HH:MM:SS
   
   05 TYPE              PIC X(10).        *> DEPOSIT / WITHDRAW
   
   05 AMOUNT            PIC 9(12)V99.
   
   05 BALANCE-AFTER     PIC 9(12)V99.
   

# 4. MENU CHƯƠNG TRÌNH
- Menu chính (sau đăng nhập)
1 - Gửi tiền
2 - Rút tiền
3 - Kiểm tra số dư
4 - Lịch sử giao dịch
5 - Đổi mật khẩu
6 - Thoát
Chọn: _

- Menu ngoài (chưa đăng nhập)
1 - Đăng nhập
2 - Tạo tài khoản
3 - Thoát
Chọn: _

# 5. YÊU CẦU KỸ THUẬT

- Ngôn ngữ: COBOL (GnuCOBOL)

- Sử dụng File Organization: LINE SEQUENTIAL hoặc VARIABLE RECORD

- Xử lý nhập password ẩn ký tự (echo off)

- Mỗi chức năng tách thành SECTION riêng:

+ LOGIN-SECTION

+ CREATE-ACCOUNT-SECTION

+ DEPOSIT-SECTION

+ WITHDRAW-SECTION

+ BALANCE-SECTION

+ HISTORY-SECTION

+ CHANGE-PASS-SECTION










