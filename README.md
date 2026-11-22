# CSC17104 – PROGRAMMING FOR DATA SCIENCE
#  FINAL PROJECT

## 1. Thông tin nhóm & Phân công công việc

| STT | Họ và tên | MSSV | GitHub Username | Vai trò & Phân công nhiệm vụ | Câu hỏi phụ trách chính |
| :---: | :---: | :---: | :---: | :--- | :--- |
| 1 | Lê Thanh Hải | 23127360 | JuzHarii | |  |
| 2 | Ngô Quang Thắng | 23127473 | Ganth1811 | |  |

- **Kế hoạch & Tiến độ nhóm (Trello / Google Sheets)**: [Link Trello / Google Sheets]

---

## 2. Giới thiệu bộ dữ liệu (Dataset Overview)
- **Tên bộ dữ liệu**: Board Games Dataset
- **Nguồn dữ liệu (Source & URL)**: [Kaggle - Board Games Dataset](https://www.kaggle.com/datasets/andrewmvd/board-games) (dữ liệu trích xuất từ [BoardGameGeek](https://boardgamegeek.com/))
- **Tác giả / Tổ chức phát hành**: Larisa Morozova (`@andrewmvd` trên Kaggle)
- **Giấy phép bản quyền (License)**: CC BY 4.0 (Creative Commons Attribution 4.0 International)
- **Mô tả ngắn**: Bộ dữ liệu chứa thông tin chi tiết về hơn 20.000 trò chơi board game đã được xếp hạng trên nền tảng BoardGameGeek (BGG) vào tháng 2/2021 (chỉ bao gồm các game có từ 30 lượt đánh giá trở lên). Dữ liệu gồm 14 thuộc tính: định danh (`ID`, `Name`), năm phát hành (`Year Published`), thông số người chơi (`Min Players`, `Max Players`, `Play Time`, `Min Age`), điểm số cộng đồng (`Users Rated`, `Rating Average`, `BGG Rank`, `Complexity Average`, `Owned Users`), cùng danh mục (`Domains`) và cơ chế chơi (`Mechanics`).
---

## 3. Danh sách câu hỏi nghiên cứu (Research Questions)


---

## 4. Các phát hiện chính (Key Findings)

---

## 5. Hướng dẫn cài đặt và chạy đồ án (How to Run the Project)

### Bước 1: Clone repository
```bash
git clone https://github.com/[your-repo]/[project-name].git
cd [project-name]
```

### Bước 2: Tạo và kích hoạt môi trường Conda
```bash
conda env create -f environment.yml
conda activate min_ds-env
```

### Bước 3: Tải dữ liệu
- Tải file `bgg_dataset.csv` từ [Kaggle Board Games Dataset](https://www.kaggle.com/datasets/andrewmvd/board-games) và đặt vào thư mục `data/raw/` (đường dẫn: `data/raw/bgg_dataset.csv`).
- *Lưu ý*: File sử dụng dấu chấm phẩy (`;`) làm ký tự phân cách các cột và dấu phẩy (`,`) cho các số thập phân.

### Bước 4: Chạy các Notebook theo thứ tự


---

## 6. Cấu trúc thư mục (Repository Structure)
```text
.
├── README.md                           # Thông tin dự án và hướng dẫn chạy
├── environment.yml                     # Cấu hình môi trường conda
├── LLM_USAGE.md                        # Nhật ký sử dụng các công cụ LLM
├── data/
│   ├── raw/                            # Dữ liệu gốc chưa xử lý
│   └── processed/                      # Dữ liệu đã qua tiền xử lý
├── src/                                # Các Python modules tái sử dụng
│   └── __init__.py
├── notebooks/
│   ├── 01_collection_exploration.ipynb # Thu thập và khám phá dữ liệu (EDA)
│   ├── 02_analysis.ipynb               # Phân tích các câu hỏi phi-ML
│   └── 03_ml_question.ipynb            # Huấn luyện và diễn giải bài toán ML
└── slides.pdf                          # Slide báo cáo thuyết trình
```
