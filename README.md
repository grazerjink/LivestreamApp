# LivestreamApp
Hướng dẫn sử dụng ứng dụng livestream dạy học trên MacOS.

Cài đặt Homebrew cho MacOS
------

Trước hết hãy kiểm tra máy đã được cài đặt Homebrew chưa, nếu chưa hãy tiến hành cài đặt nó. Đầu tiên ta hãy mở Terminal của máy và copy paste lệnh dưới vào terminal rồi nhấn Enter:

`/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`

Quá trình sẽ tự động tiến hành cài đặt kéo dài khoảng vài phút.

Cài đặt môi trường MQTT với thư viện emqttd.io
------

[Tải thư viện emqtt cho MacOS tại đây](http://emqtt.io/downloads)

Sau khi tải thành công, tiến hành giải nén ra ta sẽ có được thư mục có tên là emqttd. Di chuyển vào trong thư mục gõ những lệnh sau:

* Khởi chạy dịch vụ: `./bin/emqttd start`
* Tắt dịch vụ: `./bin/emqttd stop`

Cài đặt PostgreSQL
------

Ứng dụng sử dụng NoSQL database để lưu trữ dữ liệu, cụ thể là dùng PostgreSQL. Ta hãy cài ứng dụng này vào máy tính thông qua Homebrew. Hãy gõ lệnh sau để cài đặt tự động:

`/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`

Sau khi quá trình cài đặt hoàn tất. Ta gõ tiếp lệnh sau để khởi chạy service của PostgreSQL:

`brew services start postgresql`

Cài đặt Yarn
------

Để sử dụng đa dạng các thư viện mà không tốn nhiều công sức ở các giai đoạn cấu hình tích hợp vào dự án, ta sử dụng công cụ quản lí các phụ thuộc đó là Yarn. 

Hãy cài đặt Yarn thông qua brew. Gõ lệnh sau vào terminal:

`brew install yarn`

Quá trình này sẽ giúp ta cài đặt Nodejs gồm công cụ NPM và Yarn, gõ lệnh để kiểm tra sự tồn tại:

`npm --version`\
`yarn --version`

Cài đặt Ruby Version Management
------

Trước hết và chỉ riêng MacOS, ở một số máy Mac ta phải cài đặt phần mềm xác nhận các mã chứng thực và tài liệu mã nguồn bằng GPGTools [tại đây](https://gpgtools.org/) và quá trình này không bắt buộc nếu máy bạn không có yêu cầu.

Tiếp theo chúng ta mở terminal và gõ vào 2 lệnh sau để tiến hành cài đặt RVM:

`gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB`

`\curl -sSL https://get.rvm.io | bash -s stable`

Quá trình cài đặt RVM thành công, hệ thống máy tính bạn sẽ có 2 công cụ sau:
* Ruby - Ngôn ngữ lập trình Ruby.
* Gems - Gói quản lí các thư viện dùng trong lập trình Ruby.

Gõ lệnh sau vào terminal để kiểm tra sự tồn tại:

`ruby --version`\
`gem --version`

Cài đặt Rails Framework (v5.0)
------

Sau khi ta có được công cụ gem thông qua cài đặt RVM ở bước trên, ta tiếp tục gõ lệnh sau để cài đặt Rails Framework:

`gem install rails`

Gõ lệnh sau vào terminal để kiểm tra sự tồn tại:

`rails --version`

Cấu hình và khởi chạy ứng dụng livestream
------

Source code dự án cũng đã được nén và ghi vào chung CD, ta tiến hành giải nén và sau đó bật terminal cd vào bên trong thư mục của dự án.

`cd /path/to/LivestreamApp`

Chạy lệnh **bundle** để hệ thống hỗ trợ tải các thư viện cần thiết và build source giúp chúng ta.

`bundle`

Tiếp theo, chạy tiếp lệnh **db:migrate** để tạo cơ sở dữ liệu trong PostgreSQL với các thông tin như localhost, username, password đều để mặc định.

`rails db:migrate`

Sau đó, ta phải tải thư viện cho Reactjs bằng Yarn. Gõ lệnh:

`yarn install`

Hệ thống sẽ tiến hành tải và build source cho ta. Sau quá trình đó thì mọi chuyện coi như là hết, giờ ta chỉ việc chạy và demo ứng dụng Livestream này theo lệnh sau:

`rails s`

Thông tin liên hệ
------

Mọi thắc mắc hay gặp vấn đề gì trong quá trình cấu hình cài đặt xin vui lòng gửi email qua:\
`khaiquan9926@gmail.com`
hoặc có thể khởi tạo issue trong git project này.

Xin cảm ơn mọi người quan tâm theo dõi.
