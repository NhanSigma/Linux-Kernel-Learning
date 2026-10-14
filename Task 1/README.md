# 1. Cài QEMU

## 1. QEMU là gì

QEMU là phần mềm mô phỏng phần cứng, cho phép chạy một hệ điều hành trong máy ảo với CPU, RAM và các thiết bị được mô phỏng.

## 2. Tại sao không dùng thẳng Ubuntu mà phải thông qua QEMU

Khi giải Linux Kernel Pwn, mục tiêu thường là một kernel cụ thể do ban tổ chức cung cấp. Nếu chạy trực tiếp trên Ubuntu/WSL, ta sẽ sử dụng kernel hiện tại của môi trường đó, có thể khác phiên bản hoặc cấu hình bảo vệ so với challenge.

QEMU cho phép chạy riêng kernel và root filesystem của challenge, hỗ trợ debug và giúp giảm nguy cơ làm ảnh hưởng hệ điều hành chính khi kernel guest bị crash. Ubuntu vẫn được dùng để phân tích file, viết exploit và biên dịch chương trình.

## 3. Các file thường gặp trong challenge Linux Kernel

Không phải challenge nào cũng cung cấp đầy đủ các file sau.

| File | Tác dụng |
|---|---|
| `bzImage` | Ảnh kernel Linux đã biên dịch; QEMU có thể boot trực tiếp file này làm kernel mục tiêu. |
| `rootfs.cpio.gz` | Root filesystem dạng initramfs đã nén, chứa chương trình, thư viện và môi trường chạy trong máy ảo. Tên file có thể khác, ví dụ `initramfs.cpio.gz`. |
| `run.sh` | Script khởi động QEMU, thường đặt các tham số như RAM, CPU, kernel, root filesystem và console. Đọc script trước khi chạy. |
| `vuln.ko` | Module kernel có lỗ hổng, nếu challenge sử dụng module riêng. Có thể được nạp vào kernel guest để tương tác với lỗi. |
| `vmlinux` | File kernel dạng ELF, thường hữu ích cho phân tích và debug; có thể chứa symbol giúp xác định hàm và địa chỉ. |
| `exploit.c` hoặc `solve.py` | Mã exploit mẫu nếu ban tổ chức cung cấp; nếu không, người giải sẽ tự viết. Đây không phải file bắt buộc. |

