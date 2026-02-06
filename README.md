# SAFERUN PROGRAM - OPERATING SYSTEM PROJECT

## 1. Giới thiệu chung và chức năng:
- Mục tiêu: Xây dựng 1 chương trình để chặn 1 chương trình khác chạy một số system call nhất định.

- Các chức năng chính của `saferun`:
    + Tham số -d:[syscall_list](Deny list): Chặn các system call trong danh sách này.
    + Tham số -e:[syscall_list](Enable list): Chỉ cho phép các system call trong danh sách này.
    + Tham số --kill(Optional): Chấm dứt tiến trình ngay lập tức nếu phát hiện system call bị chặn. Nếu không thì báo lỗi, ví dụ:

        ```
        [WARN] Syscall #1 (write) đang bị chặn 
        [WARN 21:48:59] Policy block syscall #1 (write) - blocking (not killing) 
        ```
    
    + Tham số -h: Hiển thị định nghĩa các tham số và cách sử dụng chương trình.

- Đính kèm với reporitority này, chúng tôi có để 1 file `test.c` có khoảng 20 system call để cho mọi người test.
- Có thể make install để chạy với toàn hệ thống (không cần cd vào thư mục chứa code saferun) 
 
## 2. Đánh giá mức độ hoàn thiện:
- Việc sử dụng ptrace để kiểm soát syscall cho thấy dự án đã can thiệp kernel-level từ user-space.
- Hỗ trợ cả Deny List (-d) và Allow List (-e).
- Có tùy chọn Kill hoặc Stop/Block cho thấy sự cân nhắc về "User Experience": người dùng có thể muốn debug (Stop/Block) hoặc bảo mật tuyệt đối (Kil).
- Mục tiêu ban đầu của dự án là khả năng vận hành đa nền tảng. Tuy nhiên, hiện tại saferun mới chỉ hoạt động ổn định trên Ubuntu (x86_64 - chip AMD/Intel) và chưa tương thích với kiến trúc ARM.

## 3. Phân công nhiệm vụ:
- Dương Đức Tuấn (Nhóm trưởng): Viết configure.sh, Makefile, hoàn thiện final project.
- Nguyễn Hoài Thương: Viết log.c, log.h, monitor.h, monitor.c
- Nguyễn Hữu Tuyên: Viết file test.c, monitor.c
- Nguyễn Thanh Sơn: Viết file main.c
- Lê Nhất Vũ: Viết list_syscall.c, list_syscall.h

## 4. Hướng dẫn cài đặt, dịch và sử dụng:
- Bước 1: Clone this repository về máy và vào thư mục chứa code.
```bash
git clone https://github.com/DTuan2016/operating_system_prj

cd operating_system_prj/
```
- Bước 2: Make và install vào hệ thống. Không bắt buộc phải chạy lệnh `make install`
```bash
make

make install
```
- Bước 3: Test code với các lệnh sau đây.
```bash
./saferun -d:write,clone -kill -- ./test
```