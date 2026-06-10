[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=24112856&assignment_repo_type=AssignmentRepo)
# Day 10 Lab: Data Pipeline & Data Observability

**Student Email:** gtcong12a03@gmail.com  
**Name:** Giang Thành Công  
**Student ID:** 2A202600544  

---

## Mo ta

Bài lab này tập trung vào việc xây dựng một đường ống xử lý dữ liệu tự động (automated ETL pipeline) bằng Python & Pandas và nghiên cứu tầm quan trọng của Data Observability đối với hoạt động của AI Agent:
1. **Extract:** Đọc dữ liệu JSON thô.
2. **Validate:** Kiểm tra và loại bỏ các dữ liệu rác, lỗi (giá trị âm, thiếu nhóm ngành hàng).
3. **Transform:** Chuẩn hóa thông tin ngành hàng thành định dạng Title Case, tính toán giá đã chiết khấu (discounted price) giảm 10%, và đóng dấu thời gian (processed timestamp).
4. **Load:** Lưu dữ liệu sạch xuống tệp CSV.
5. **Stress Test:** Thử nghiệm phản ứng của AI Agent khi đọc dữ liệu sạch (sau ETL) vs dữ liệu bẩn (chưa được làm sạch).

---

## Cach chay (How to Run)

### Prerequisites
Cài đặt các thư viện cần thiết trước khi bắt đầu:
```bash
pip install pandas pytest
```

### Chay ETL Pipeline
Để bắt đầu quá trình trích xuất và làm sạch dữ liệu:
```bash
python solution.py
```

### Chay Agent Simulation (Stress Test)
Để mô phỏng phản ứng của AI Agent đối với các loại dữ liệu khác nhau:
1. Tạo dữ liệu rác:
   ```bash
   python generate_garbage.py
   ```
2. Chạy giả lập phản hồi của AI Agent:
   ```bash
   python agent_simulation.py
   ```

---

## Cau truc thu muc

```
├── solution.py              # ETL Pipeline script
├── processed_data.csv       # Output cua pipeline sau khi lam sach
├── garbage_data.csv         # File du lieu gia lap bi loi chat luong
├── agent_simulation.py      # Script gia lap phan hoi cua AI Agent
├── generate_garbage.py      # Script tao du lieu rác tu dong
├── experiment_report.md     # Bao cao thi nghiem so sanh Clean vs Garbage Data
└── README.md                # File nay
```

---

## Ket qua

* **Tổng số bản ghi ban đầu:** 5
* **Số bản ghi hợp lệ lưu trữ:** 3
* **Số bản ghi bị loại bỏ:** 2
  * Bản ghi ID `3` (Mystery Box) bị loại do giá âm (`price = -10`).
  * Bản ghi ID `4` (Phone) bị loại do trống trường category (`category = ""`).
* **Hiệu suất AI Agent:**
  * **Với Clean Data:** Hoạt động chính xác, phản hồi đúng sản phẩm có giá trị tối ưu phù hợp với truy vấn.
  * **Với Garbage Data:** AI Agent bị lỗi logic do các bản ghi ngoại lệ cực đoan (outlier: Nuclear Reactor giá `$999,999`) và đưa ra câu trả lời phi thực tế.
