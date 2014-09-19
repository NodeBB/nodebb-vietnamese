Koding
======

**Chú ý**: Việc cài đặt trên Koding cần có tài khoản miễn phí trên Koding.com.

1. Tạo tài khoản hoặc đăng nhập vào `Koding.com <http://koding.com>`
2. Nhấn vào nút màu xanh lá trông như sau ``>_``
3. Bạn sẽ nhìn thấy VM của bạn với chữ Off ở bên phải màu đỏ, hãy nhấn vào đó để bật VM
4. Nhấn tiếp vào nó khi có thông báo Ready.
5. Bây giờ bạn đang ở trong cửa sổ terminal. Việc cài đặt gần giống với Ubuntu, nhưng hơi khác một chút vì một số gói đã được cài đặt sẵn.
6. Đầu tiên, ta phải chắc chắn rằng mọi thứ đã được cập nhật - ``sudo apt-get update && sudo apt-get upgrade``
7. Nhập vào mật khẩu mà bạn đã đăng ký, nếu bạn đăng ký bằng Github hoặc qua 1 bên thứ ba nào khác, bạn phải cài đặt 1 cái trong trang cài đặt tài khoản. Sau đó quay trở lại.
8. Bây giờ chạy lệnh sau ``sudo apt-get install python-software-properties python g++ make``
9. Cài đặt gói hỗ trợ - ``sudo apt-get install redis-server imagemagick``
10. Tiếp, tạo bản sao NodeBB vào trong NodeBB folder - ``git clone -b v0.5.x https://github.com/NodeBB/NodeBB.git nodebb`` (Tùy chọn: Thay thế nodebb ở cuối nếu bạn muốn có tên folder khác)
11. Truy cập vào NodeBB folder - ``cd nodebb`` (trừ khi bạn đã đặt tên folder khác ở bước trước và nếu bạn dã quên tên folder, chay ``ls`` để nhìn thấy tên của folder)
12. Bây giờ chúng ta cài đặt các trình phụ thuộc của NodeBB - ``npm install`` (có thể mất 1 đến 2 phút)
13. Cài đặt nodebb bằng dòng lệnh - ``./nodebb setup``
14. Câu hỏi đầu tiên sẽ hỏi tên miền của bạn, đừng để nó là localhost. Tên miền của bạn sẽ như sau ``http://{yourkodingusername}.kd.io`` - Username của bạn có thể nhìn thấy ở góc trên cùng bên phải.
15. Hoàn tất việc cài đặt (giá trị mặc định sau khi cài đặt tên miền đều có thể chấp nhận, hãy ấn enter cho đến khi có yêu cầu "Create an Admin"
16. Tạo username và mật khẩu admin, sau đó nó sẽ tạo các categories và một vài thứ khác mà làm NodeBB tuyệt vời.
17. Giờ chúng ta có thể chạy NodeBB - ``./nodebb start``
18. Mở tab khác trên trình duyệt và truy cập vào địa chỉ ``http://{yourkodingusername}.kd.io:4567`` (nếu như bạn không thay đổi cổng mặc định trong phần cài đặt)
19. Bạn sẽ nhìn thấy 1 màn hình để tiếp tục truy cập vào trang của bạn, nhấn vào link ở nửa bên dưới để tiếp tục truy cập trang.

Chúc mừng, bạn đã cài đặt thành công NodeBB trên Koding.com

Nếu hướng dẫn trên không rõ ràng hoặc bạn gặp rắc rối, hãy cho chúng tôi biết bằng cách `tạo báo cáo <https://github.com/NodeBB/NodeBB/issues>`_. (Hãy tag @a5mith trong issue của bạn, vì tôi đã viết hướng dẫn này)

Một vài vấn đề khi chạy trên Koding
---------------------

Vì Koding là miễn phí, nên nó sẽ có 1 vài sắc thái của host cloud:

1. VM sẽ tự động tắt sau 15 phút không có hoạt động. Điều này không may là không ám chỉ trang web, mà là cửa sổ Terminal (Bạn có thể khắc phục điều này bằng cách luôn mở terminal và chạy lệnh ``ls`` mỗi 10 phút để làm mới lại bộ đếm)
2. Thỉnh thoảng bạn sẽ nhận được thông báo rằng "Your VM is unavailable, try again later", bạn có thể thử đăng xuất và đăng nhập lại, tải lại trang, hoặc báo cáo lỗi với đội hỗ trợ của họ.
3. Koding.com sử dụng ubuntu để host VM, vì vậy hiểu biết căn bản về Unbuntu sẽ có ích.