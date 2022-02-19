# Install Linux, Nginx, MySQL, PHP on Ubuntu 20.04
![LEMP](https://user-images.githubusercontent.com/97789851/154805186-c95aca00-a3f3-4d16-bd2a-7c19d7343a3b.png)
## Giới thiệu
**LEMP** là một nhóm các phần mềm có thể dùng để phục vụ các trang web động và các ứng dụng web được viết bằng PHP. Đây là từ viết tắt mô tả hệ điều hành **L**inux, với máy chủ web Nginx (phát âm như “ **E**ngine-X”). Dữ liệu backend được lưu trữ trong cơ sở dữ liệu **M**ySQL và xử lý bởi ngôn ngữ **P**HP.

***Lam Trường*** sẽ hướng dẫn cách cài đặt ngăn xếp **LEMP** trên máy chủ Ubuntu 20.04. Hệ điều hành Ubuntu hoàn thành yêu cầu đầu tiên vì nó được phát triển dựa trên **L**inux. Mình sẽ mô tả cách cài đặt và cấu hình các thành phần còn lại ngay phía dưới. Các bạn cùng theo dõi nhé :>
## Thiết lập ban đầu
Người dùng **root** là người dùng quản trị trong môi trường Linux có các đặc quyền rất rộng. Do các đặc quyền cao của tài khoản root, bạn không nên sử dụng nó một cách thường xuyên. Điều này là do tài khoản root có thể thực hiện các thay đổi rất nguy hiểm, thậm chí là do tình cờ.

-> Bạn cần truy cập vào máy chủ Ubuntu 20.04 với tư cách là người dùng thông thường, không phải **root** và tường lửa **UFW** được bật trên máy chủ của bạn.

**Bước 1 - Đăng nhập với quyền root**

Để đăng nhập vào tài khoản **root** bạn sử dụng lệnh sau:
        
        $ sudo su