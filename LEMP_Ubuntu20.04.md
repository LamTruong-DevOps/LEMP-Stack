# Install Linux, Nginx, MySQL, PHP on Ubuntu 20.04
![LEMP](https://user-images.githubusercontent.com/97789851/154805186-c95aca00-a3f3-4d16-bd2a-7c19d7343a3b.png)
## Giới thiệu
**LEMP** là một nhóm các phần mềm có thể dùng để phục vụ các trang web động và các ứng dụng web được viết bằng PHP. Đây là từ viết tắt mô tả hệ điều hành **L**inux, với máy chủ web Nginx (phát âm như “ **E**ngine-X”). Dữ liệu backend được lưu trữ trong cơ sở dữ liệu **M**ySQL và xử lý bởi ngôn ngữ **P**HP.

***Lam Trường*** sẽ hướng dẫn các bạn cách cài đặt ngăn xếp **LEMP** trên máy chủ Ubuntu 20.04. Hệ điều hành Ubuntu hoàn thành yêu cầu đầu tiên vì nó được phát triển dựa trên **L**inux. Mình sẽ mô tả cách cài đặt và cấu hình các thành phần còn lại ngay phía dưới. 

**Cùng theo dõi nhé!! Chúc các bạn thành công :>**
## Thiết lập ban đầu
Người dùng **root** là người dùng quản trị trong môi trường Linux có các đặc quyền rất rộng. Do các đặc quyền cao của tài khoản root, bạn không nên sử dụng nó một cách thường xuyên. Tài khoản **root** có thể thực hiện các thay đổi rất nguy hiểm, thậm chí là do tình cờ.

**->** Bạn cần truy cập vào máy chủ Ubuntu 20.04 với tư cách là người dùng thông thường, không phải **root** và tường lửa **UFW** được bật trên máy chủ của bạn.

**Bước 1 - Đăng nhập với quyền root**

Để đăng nhập vào tài khoản **root** bạn sử dụng lệnh sau:
        
        sudo su
Sau khi đăng nhập bằng quyền **root**. Bước tiếp theo là thiết lập một tài khoản người dùng mới với các đặc quyền giảm bớt để sử dụng hàng ngày.

**Bước 2 - Tạo người dùng mới**

Ví dụ này tạo một người dùng mới có tên là **admin**, nhưng bạn nên thay thế người dùng đó bằng một tên người dùng mà bạn thích:

        adduser admin
Bạn sẽ được hỏi một số câu hỏi, bắt đầu với mật khẩu của tài khoản mới. 

Nhập một mật khẩu mạnh và điền vào bất kỳ trường thông tin bổ sung nào nếu bạn muốn. Điều này không bắt buộc và bạn có thể nhấn "ENTER" bỏ qua.

**Bước 3 - Cấp đặc quyền quản trị**

Bây giờ mình đã có một tài khoản người dùng mới với các đặc quyền tài khoản thông thường. Tuy nhiên, nhiều lúc mình có thể cần thực hiện các công việc nâng cao của quản trị. Để thiết lập siêu người dùng hoặc đặc quyền root cho tài khoản bình thường, điều này sẽ cho phép người dùng bình thường chạy các lệnh có đặc quyền quản trị bằng cách đặt từ trước lệnh **sudo**.

Để thêm các đặc quyền này cho người dùng mới, mình sẽ thêm người dùng đó vào nhóm **sudo**. Theo mặc định, trên Ubuntu 20.04, người dùng là thành viên của nhóm **sudo** được phép sử dụng lệnh **sudo**.

        usermod -aG sudo admin
**->** Giờ đây, khi đã đăng nhập với tư cách người dùng **admin**, bạn có thể nhập **sudo** trước các lệnh để chạy chúng với các đặc quyền của người dùng siêu cấp.

**Bước 4 - Thiết lập tường lửa cơ bản**

Máy chủ Ubuntu 20.04 có thể sử dụng tường lửa **UFW** để đảm bảo chỉ cho phép các kết nối đến một số dịch vụ nhất định. Mình có thể thiết lập tường lửa cơ bản bằng ứng dụng này.

Chúng ta cần đảm bảo rằng tường lửa cho phép các kết nối **SSH** để chúng ta có thể đăng nhập lại vào lần sau. Mình cho phép các kết nối này bằng lệnh sau:

        ufw allow OpenSSH
Sau đó, chúng ta kích hoạt tường lửa bằng cách gõ:

        ufw enable
Nhập "y" và nhấn "ENTER" để tiếp tục. Bạn có thể thấy rằng các kết nối **SSH** vẫn được phép bằng cách nhập lệnh sau để kiểm tra trạng thái của tường lửa:

        ufw status
Kết quả hiển thị:
        
        Status: active

        To                         Action      From
        --                         ------      ----
        OpenSSH                    ALLOW       Anywhere
        OpenSSH (v6)               ALLOW       Anywhere (v6)
**=> Như vậy chúng ta đã hoàn thành các thiết lập ban đầu của máy chủ.**

**Bây giờ, các bạn cần đăng xuất khỏi khoản root và đăng nhập vào tài khoản siêu cấp admin**

        logout
**Sử dụng tài khoản siêu cấp để đăng nhập, sau đây là kết quả hiển thị:**

        To run a command as administrator (user "root"), use "sudo <command>".
        See "man sudo_root" for details.
        admin@ubuntu:~$
## I. Cài đặt máy chủ Web Nginx