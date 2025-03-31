# Demo Hugo với Blowfish

Đây là dự án mẫu sử dụng **Hugo**, một trình tạo trang web tĩnh mạnh mẽ, kết hợp với **Blowfish**, một giao diện đẹp mắt và linh hoạt cho Hugo.

## Giới thiệu

Hugo là một trình tạo trang web tĩnh nhanh chóng và linh hoạt, giúp bạn xây dựng các trang web hiện đại một cách hiệu quả. Blowfish là một giao diện được thiết kế đặc biệt cho Hugo, cung cấp nhiều tính năng và tùy chỉnh để tạo ra một trang web chuyên nghiệp.

## Yêu cầu hệ thống

- **Hugo**: Phiên bản mới nhất. Bạn có thể tải xuống từ [trang chủ của Hugo](https://gohugo.io/getting-started/installing/).
- **Git**: Để quản lý mã nguồn và tải xuống các theme.

## Cài đặt

### 1. Cài đặt Hugo

Nếu bạn chưa cài đặt Hugo, hãy làm theo các bước sau:

- **Trên macOS**:

  ```bash
  brew install hugo
Trên Windows:

Tải xuống tệp cài đặt từ trang chủ của Hugo và làm theo hướng dẫn.

Trên Linux:

bash
Sao chép
Chỉnh sửa
sudo apt-get install hugo
2. Tạo một trang web mới với Hugo
bash
Sao chép
Chỉnh sửa
hugo new site my-hugo-site
cd my-hugo-site
3. Thêm giao diện Blowfish vào dự án
Có nhiều cách để thêm Blowfish vào dự án Hugo của bạn. Dưới đây là hai phương pháp phổ biến:

a. Sử dụng Git Submodule (Khuyến nghị)
bash
Sao chép
Chỉnh sửa
git init
git submodule add -b main https://github.com/nunocoracao/blowfish.git themes/blowfish
b. Sử dụng Hugo Module
Đảm bảo rằng bạn đã cài đặt Go trên hệ thống của mình. Sau đó, trong thư mục dự án Hugo của bạn, chạy:

bash
Sao chép
Chỉnh sửa
hugo mod init github.com/yourusername/your-repo
hugo mod get github.com/nunocoracao/blowfish
4. Cấu hình giao diện Blowfish
Trong tệp config.toml của dự án, thêm hoặc chỉnh sửa các dòng sau:

toml
Sao chép
Chỉnh sửa
theme = "blowfish"

[params]
  # Các cấu hình khác cho Blowfish
Để biết thêm chi tiết về cấu hình, vui lòng tham khảo tài liệu chính thức của Blowfish tại đây.

5. Thêm nội dung vào trang web
Tạo một bài viết mới bằng lệnh:

bash
Sao chép
Chỉnh sửa
hugo new posts/my-first-post.md
Sau đó, chỉnh sửa tệp content/posts/my-first-post.md và thêm nội dung của bạn.

6. Chạy trang web cục bộ
Để xem trang web của bạn trên máy tính cục bộ, chạy lệnh:

bash
Sao chép
Chỉnh sửa
hugo server
Mở trình duyệt và truy cập http://localhost:1313 để xem trang web của bạn.

Triển khai lên môi trường sản xuất
Sau khi hoàn tất phát triển, bạn có thể triển khai trang web của mình lên các dịch vụ lưu trữ như Netlify, Vercel hoặc GitHub Pages. Vui lòng tham khảo tài liệu của các dịch vụ này để biết thêm chi tiết.
