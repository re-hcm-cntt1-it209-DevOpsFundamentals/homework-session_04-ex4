# Bài 4: Quản lý tệp tin bỏ qua (.gitignore) và Sửa lịch sử (Amend)

## 1. Mục tiêu

- Cấu hình tệp `.gitignore` để bỏ qua các file chứa thông tin nhạy cảm.
- Gỡ file đã được Git theo dõi khỏi Git Index nhưng vẫn giữ file trên máy tính.
- Sử dụng `git commit --amend` để chỉnh sửa commit gần nhất.
- Kiểm tra trạng thái repository và lịch sử commit sau khi xử lý.

## 2. Khởi tạo Repository

Khởi tạo Git repository:

```bash
git init

Cấu hình thông tin người dùng cho repository:

git config --local user.name "Nguyen Dai Phat"
git config --local user.email "n24dtcn062@student.ptithcm.edu.vn"

Đổi branch mặc định thành main:

git branch -M main
3. Tạo Commit Ban Đầu

Tạo file README.md:

touch README.md

Thêm nội dung giới thiệu bài thực hành vào README.md, sau đó đưa file vào staging:

git add README.md

Tạo commit đầu tiên:

git commit -m "Initial commit"

Kiểm tra lịch sử:

git log --oneline
4. Mô phỏng Commit Nhầm File Credentials

Tạo file chứa thông tin giả lập:

touch credentials.txt

Ví dụ nội dung:

DB_USERNAME=admin
DB_PASSWORD=123456
API_KEY=example-secret-key

Các thông tin trên chỉ được sử dụng để mô phỏng dữ liệu nhạy cảm trong bài thực hành.

Kiểm tra trạng thái:

git status

Sau đó cố tình đưa file vào staging:

git add credentials.txt

Tạo commit:

git commit -m "Add credentials"

Kiểm tra các file đang được Git theo dõi:

git ls-files

Kết quả ban đầu:

README.md
credentials.txt

Điều này cho thấy credentials.txt đã được Git theo dõi và đã nằm trong commit.

5. Cấu hình .gitignore

Tạo file .gitignore:

touch .gitignore

Thêm credentials.txt vào .gitignore:

credentials.txt

Kiểm tra nội dung:

cat .gitignore

.gitignore giúp Git bỏ qua credentials.txt trong các lần theo dõi sau.

Tuy nhiên, vì credentials.txt đã được Git track từ trước nên chỉ thêm vào .gitignore là chưa đủ.

6. Gỡ credentials.txt khỏi Git Index

Sử dụng lệnh:

git rm --cached credentials.txt

Tùy chọn --cached chỉ gỡ file khỏi Git Index, không xóa file vật lý khỏi máy tính.

Sau khi thực hiện:

Git Repository
    |
    └── credentials.txt không còn được track

Working Directory
    |
    └── credentials.txt vẫn còn trên máy

Kiểm tra trạng thái:

git status

Kiểm tra danh sách file được Git theo dõi:

git ls-files

Kết quả không còn credentials.txt:

README.md

Trong khi file credentials.txt vẫn tồn tại trong thư mục làm việc.

7. Commit và Sửa Commit Gần Nhất bằng Amend

Đưa .gitignore vào staging:

git add .gitignore

Sử dụng git commit --amend để thay thế commit gần nhất:

git commit --amend -m "Configure gitignore and remove credentials"

Lệnh --amend cho phép chỉnh sửa commit gần nhất thay vì tạo thêm một commit mới.

Commit trước đó:

Add credentials

được thay thế bằng:

Configure gitignore and remove credentials
8. Kiểm tra Lịch sử Commit

Kiểm tra commit gần nhất:

git log -n 1

Kết quả hiển thị commit mới với thông điệp:

Configure gitignore and remove credentials

Kiểm tra trạng thái repository:

git status

Kết quả mong đợi:

On branch main
nothing to commit, working tree clean

Kiểm tra các file đang được Git theo dõi:

git ls-files

Kết quả:

.gitignore
README.md

Kiểm tra file thực tế trong thư mục:

ls

credentials.txt vẫn tồn tại trên máy nhưng không còn được Git theo dõi.

9. Kết quả

Đã hoàn thành các yêu cầu:

 Khởi tạo Git repository.
 Tạo và cấu hình .gitignore.
 Mô phỏng tình huống commit nhầm credentials.txt.
 Sử dụng git rm --cached credentials.txt.
 Giữ lại credentials.txt trên máy tính.
 Không còn credentials.txt trong danh sách file được Git theo dõi.
 Sử dụng git commit --amend.
 Thay đổi thông điệp của commit gần nhất.
 Kiểm tra thành công bằng git status.
 Kiểm tra lịch sử bằng git log -n 1.
10. Các lệnh kiểm tra chính
Kiểm tra trạng thái
git status

Kết quả mong đợi:

On branch main
nothing to commit, working tree clean
Kiểm tra commit gần nhất
git log -n 1

Commit gần nhất có thông điệp:

Configure gitignore and remove credentials
Kiểm tra file được Git theo dõi
git ls-files

credentials.txt không còn xuất hiện trong danh sách.

11. Lưu ý về dữ liệu nhạy cảm

Trong dự án thực tế, các file chứa credentials, API key, password hoặc thông tin bí mật cần được thêm vào .gitignore trước khi commit.

Ví dụ:

credentials.txt
.env
*.pem
application-local.properties

Nếu một credential thật đã được push lên remote repository, chỉ sử dụng git rm --cached và git commit --amend là chưa đủ. Credential đã bị lộ cần được thu hồi hoặc thay đổi ngay, đồng thời có thể cần xử lý lịch sử Git nếu muốn loại bỏ dữ liệu khỏi các commit cũ.


### Cấu trúc cuối cùng của `bai4`

```text
bai4/
├── .gitignore
└── README.md

Bài 4 không bắt buộc phải có thư mục images/ theo yêu cầu bạn đưa. Đề chỉ yêu cầu README giải thích quá trình và kết quả git log -n 1, nên không cần tự tạo ảnh cho đủ bộ.

Sau khi tạo README, nhớ:

git add README.md
git commit --amend --no-edit

Lệnh này quan trọng: vì commit gần nhất đã được amend trước đó, nếu bạn tạo README sau đó thì dùng --amend --no-edit để README cũng nằm trong chính commit cuối cùng, thay vì sinh thêm một commit mới.

Cuối cùng:

git log -n 1
git status