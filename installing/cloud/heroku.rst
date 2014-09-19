Heroku
======

**Chú ý**: Cài đặt lên Heroku yêu cầu máy ở local phải chạy 1 phiên bản unix, NodeBB không chạy trên Windows.

1. Tải và cài đặt `Heroku Toolbelt <https://toolbelt.heroku.com/>`_ cho hệ điều hành của bạn
2. Đăng nhập vào tài khoản Heroku: ``heroku login``
3. Xác nhận tài khoản Heroku bằng cách thêm thẻ credit (tại http://heroku.com/verify)
4. Tạo bản sao repository: ``git clone -b v0.5.x https://github.com/NodeBB/NodeBB.git /path/to/repo/clone``
5. ``cd /path/to/repo/clone``
6. Cài đặt dependencies ``npm install``
7. Tạo heroku app: ``heroku create``
8. Bật WebSocket (beta): ``heroku labs:enable websockets -a {APP_NAME}``, ``{APP_NAME}`` được cung cấp bởi Heroku, và giống như sau ``adjective-noun-wxyz.herokuapp.com`` (Chú ý: `Đọc tài liệu sau <https://discussion.heroku.com/t/application-error/160>`_): bỏ `.herokuapp.com` khi nhập ``{APP_NAME}`` phía trên.
9. Bật `Redis To Go <https://addons.heroku.com/redistogo>`_ cho tài khoản heroku của bạn: ``heroku addons:add redistogo:nano``
10. Chạy mã cài đặt NodeBB: ``node app --setup`` (thông tin về Heroku server và Redis to Go instance có thể tìm thấy ở trang tài khoản của bạn)

    * Tên server của bạn nằm trong trang cài đặt Heroku app và giống như sau ``adjective-noun-wxyz.herokuapp.com``
    * Sử dụng bất cứ cổng nào, nó sẽ bị bỏ qua.
    * Redis server có thể tìm trong redis url. Ví dụ với url là: ``redis://redistogo:h28h3wgh37fns7@crestfish.redistogo.com:12345/``
    * Server là ``fishyfish.redistogo.com``
    * Cổng là ``12345``
    * Mật khẩu là ``h28h3wgh37fns7``

12. Thêm 3 gói sau vào phần ``dependencies`` trong file ``package.json``:

.. code:: json

        "dependencies": {
            ...
            "nodebb-plugin-dbsearch": "0.0.10",
            "redis": "~0.10.1",
            "connect-redis": "~2.0.0"
        },
        "devDependencies": {

13. Tạo 1 Procfile cho Heroku: ``echo "web: node loader.js" > Procfile``
14. Commit Procfile:

.. code:: bash

	git add -f Procfile config.json package.json && git commit -am "adding Procfile and configs for Heroku"

15. Push lên heroku: ``git push heroku master``
    * Hãy chắc chắn rằng khóa SSH đúng đã được thêm vào tài khoản của bạn, nếu không thì push sẽ không thành công!
16. Khởi tạo 1 dyno: ``heroku ps:scale web=1``
17. Truy cập vào ứng dụng!

Nếu hướng dẫn trên không rõ ràng hoặc bạn gặp rắc rối, hãy cho chúng tôi biết bằng cách `tạo báo cáo <https://github.com/NodeBB/NodeBB/issues>`_.

Luôn cập nhật
---------------------

Nếu bạn muốn pull những thay đổi mới nhất từ git repository vào ứng dụng Heroku của bạn:

1. Chuyển hướng repository tới ``/path/to/nodebb``
2. ``git pull``
3. ``npm install``
4. ``node app --upgrade``
5. ``git commit -am "upgrading to latest nodebb"``
6. ``git push heroku master``