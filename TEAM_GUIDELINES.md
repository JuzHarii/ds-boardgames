# Hướng dẫn làm việc nhóm với Git và Jupyter Notebook

Tài liệu này tổng hợp các quy ước làm việc nhóm, quy trình Git và các mốc thời gian của đồ án theo đúng yêu cầu từ môn học.

## 1. Thiết lập môi trường và công cụ

Nhóm dùng chung môi trường Conda đã khai báo trong `environment.yml`. Trước khi bắt đầu làm việc trên terminal, kích hoạt môi trường:

```bash
conda activate min_ds-env
```

Sau khi clone repo về máy lần đầu, chạy thêm lệnh sau để cài trình xử lý diff và merge của nbdime cho Git:

```bash
nbdime config-git --enable
```

Lệnh này giúp Git hiểu cấu trúc từng cell của notebook khi chạy `git diff` hoặc `git merge`, thay vì so sánh như text JSON thô. Ngoài ra, hạn chế tự cài thêm thư viện ngoài file `environment.yml`. Nếu cần gói mới thì trao đổi trước để cập nhật file cấu hình chung.

## 2. Xóa output trước khi commit

Notebook của Jupyter thực chất là file JSON lưu cả code lẫn output (bảng biểu và chuỗi ảnh base64 rất dài). Nếu để nguyên output rồi commit, lịch sử thay đổi sẽ bị tràn hàng nghìn dòng rác và rất dễ dính merge conflict.

Thói quen cần nhớ trước khi chạy `git add`:
1. Vào JupyterLab hoặc VS Code, chọn menu **Kernel -> Restart Kernel and Clear All Outputs**.
2. Bấm Ctrl+S để lưu lại file sạch.
3. Sau đó mới add và commit.

Đến đợt nộp bài cuối cùng, khi đã chốt kết quả phân tích thì nhóm mới chạy lại toàn bộ để lưu biểu đồ hoàn chỉnh.

## 3. Quy trình làm việc trên Git theo từng giai đoạn

Để đảm bảo khối lượng công việc cân bằng giữa các thành viên và thể hiện rõ ràng trên lịch sử commit GitHub, nhóm áp dụng quy trình 3 bước cho từng giai đoạn:

1. **Chuẩn bị khung sườn (Skeleton)**: Một bạn tạo file notebook khung sườn ban đầu (đầy đủ các đầu mục Markdown theo yêu cầu của đồ án) rồi push lên nhánh `main`.
2. **Làm việc độc lập trên branch riêng**: Mỗi người checkout nhánh riêng mang tên mình (ví dụ `feature/eda-hai`, `feature/eda-thang`) và tự thực hiện phần việc đó một cách độc lập. Lịch sử commit trên GitHub của mỗi bạn cần thể hiện rõ sự đóng góp cân bằng.
3. **Họp nhóm và chốt bản chung (Group Version)**: Sau khi xong việc ở nhánh riêng, nhóm họp lại để cùng đọc hiểu notebook của nhau, chọn ra phương án xử lý tốt nhất để ghép thành bản chung của nhóm, sau đó mới merge các branch cá nhân vào `main`.

Với các câu hỏi phân tích và machine learning, mỗi người phụ trách các câu hỏi riêng theo phân công, nhưng cả hai đều phải hiểu trọn vẹn nội dung của nhau.

Nếu có các hàm tính toán hay định dạng biểu đồ dùng lại nhiều lần, hãy đưa ra file Python thuần trong thư mục `src/` (ví dụ `src/utils.py`) rồi import vào notebook. File `.py` là text thuần nên Git merge rất nhàn và không lo lỗi format.

## 4. Xử lý khi dính merge conflict

Nếu lỡ dính conflict khi pull hoặc merge một file `.ipynb`, đừng mở file đó bằng text editor để tự xóa các dòng `<<<<<<< HEAD`. Làm vậy rất dễ lệch dấu ngoặc JSON khiến Jupyter không mở được file nữa.

Tùy tình huống mà xử lý:
- Nếu bản local trên máy bạn là bản chuẩn, đè bản local lên:
  ```bash
  git checkout --ours notebooks/<ten_file>.ipynb
  git add notebooks/<ten_file>.ipynb
  git commit -m "fix: giu ban notebook local"
  ```
- Nếu muốn xem từng cell bị lệch để chọn giữ cell nào, dùng giao diện trực quan của nbdime:
  ```bash
  nbmerge-web <base.ipynb> <local.ipynb> <remote.ipynb> -o <merged.ipynb>
  ```

## 5. Trách nhiệm nhóm và cách tính điểm

Thầy chấm điểm đồ án dựa trên nguyên tắc điểm chung của nhóm xấp xỉ bằng trung bình cộng điểm cá nhân của từng thành viên:
- Nếu một bạn làm sơ sài hoặc vào buổi báo cáo không nắm được notebook chung, điểm của cả nhóm sẽ bị kéo tụt xuống.
- Bạn nào nắm chắc kiến thức hơn cần chủ động hỗ trợ bạn còn lại. Tuy nhiên, hỗ trợ ở đây là giải thích và hướng dẫn để bạn tự làm, tuyệt đối không làm hộ.
- Khi thuyết trình, thầy sẽ chỉ định ngẫu nhiên ai trình bày phần nào. Vì vậy, cả hai thành viên bắt buộc phải hiểu tường tận từng bước tiền xử lý, từng câu hỏi phân tích và mô hình trong đồ án.

## 6. Kế hoạch từng giai đoạn và công cụ theo dõi

Trước khi bắt tay vào mỗi giai đoạn của đồ án, nhóm cần họp ngắn để vạch ra danh sách việc cần làm, thời gian dự kiến cho từng việc và ai là người phụ trách chính.

Nhóm sử dụng Trello (hoặc Google Sheets) để theo dõi tiến độ công việc và đính kèm đường link này vào file `README.md` theo đúng yêu cầu môn học.

## 7. Các mốc thời gian quan trọng và phản biện chéo

Gọi ngày thuyết trình là ngày x:
- **Ngày x - 2 (trước 9:00 sáng)**: Nhóm phải hoàn thành và đẩy toàn bộ sản phẩm lên GitHub. Sau đó mở một GitHub Issue trên repository để thông báo đồ án đã hoàn tất và mời các nhóm khác vào review.
- **Ngày x - 2 (sau 9:00 sáng)**: Mỗi thành viên của nhóm phải chủ động sang repository của nhóm khác để đọc bài và viết review thông qua GitHub Issue của nhóm bạn (đây là tiêu chí tính điểm cá nhân).
- **Ngày x - 1**: Nhóm đọc các nhận xét phản biện từ nhóm bạn, tiếp thu chỉnh sửa lại đồ án, sau đó nộp bản hoàn chỉnh lên cả GitHub và Moodle.
- **Ngày x (Thuyết trình online)**: Mỗi nhóm có khoảng 15 phút trình bày và 5 phút hỏi đáp (Q&A). Nhóm có thể chiếu và báo cáo trực tiếp trên file Jupyter Notebook, không cần tốn thời gian làm thêm slide. Khi trình bày, tập trung vào ý tưởng và kết quả chính, tránh đọc lướt từng dòng code.

