# Hướng dẫn làm việc nhóm với Git và Jupyter Notebook

Tài liệu này ghi lại một số quy ước để nhóm làm việc chung trên repository mà không bị đụng code hay làm hỏng file notebook.

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

## 3. Phân chia việc để tránh đụng file

Cách tốt nhất để không bị xung đột code là không cùng sửa một file notebook vào cùng một thời điểm:
- Mỗi thành viên làm câu hỏi của mình theo phân công trong `README.md`.
- Nếu cả hai cần phân tích cùng lúc, có thể tạo notebook nháp trên branch riêng (chẳng hạn `02_analysis_hai.ipynb` và `02_analysis_thang.ipynb`), khi xong xuôi thì gom lại vào file chính sau.
- Với các hàm dùng lại nhiều lần (xử lý dữ liệu, định dạng biểu đồ), nên viết ra file Python trong thư mục `src/` (ví dụ `src/utils.py`) rồi import vào notebook. File `.py` là text thuần nên Git merge rất nhàn và an toàn.

## 4. Quy trình Git hàng ngày

Trước khi ngồi vào làm, kéo code mới nhất từ nhánh chính về:

```bash
git pull origin main
```

Nên tạo branch riêng cho từng phần việc thay vì commit thẳng lên `main`:

```bash
git checkout -b feature/eda
# Code, clear output, commit...
git push origin feature/eda
```

File dữ liệu thô tải từ Kaggle về đặt trong `data/raw/`. Thư mục này đã có `.gitignore` chặn nên đừng dùng cờ `-f` để ép Git theo dõi các file CSV lớn.

## 5. Xử lý khi dính merge conflict

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
