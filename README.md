[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=23572323&assignment_repo_type=AssignmentRepo)
# Day 10 Lab: Data Pipeline & Data Observability

**Student ID:** AI20K-0238
**Student Email:** thucpkbn@gmail.com
**Name:** Nguyen Van Thuc

---

## Mo ta

Bài lab này tập trung vào **Data Pipeline and Data Observability**. Mục tiêu chính:

1. **Xây dựng ETL Pipeline tự động**:
   - Extract dữ liệu từ JSON file
   - Validate và loại bỏ records không hợp lệ (price <= 0, category rỗng)
   - Transform: chuẩn hóa category, tính discounted_price (giảm 10%), thêm timestamp
   - Load vào CSV file

2. **Thực hiện Stress Test (Data Quality Impact)**:
   - Chạy Agent với dữ liệu sạch (processed_data.csv) → Chính xác
   - Chạy Agent với dữ liệu bẩn (garbage_data.csv) → Sai lệch
   - Kết luận: Data Quality > Good Prompt

---

## Cach chay (How to Run)

### Prerequisites
```bash
pip install pandas
```

### Chay ETL Pipeline
```bash
python solution.py
```
Output: Tạo file `processed_data.csv` với dữ liệu đã được validate & transform

### Chay Agent Simulation (Stress Test)
```bash
# Test Agent với dữ liệu sạch và dữ liệu bẩn
python agent_simulation.py
```
Kiểm tra xem Agent trả lời như thế nào với mỗi loại dữ liệu

---

## Cau truc thu muc

```
├── solution.py              # ETL Pipeline script
├── processed_data.csv       # Output cua pipeline
├── experiment_report.md     # Bao cao thi nghiem
└── README.md                # File nay
```

---

## Ket qua

### ETL Pipeline Results

| Metric | Count |
|--------|-------|
| Total Records (raw_data.json) | 5 |
| Valid Records (passed validation) | 3 |
| Invalid Records (dropped) | 2 |
| Success Rate | 60% |

**Chi tiết records bị loại (`Errors: 2`):**
- **Record 3**: "Mystery Box" - Price = -10 (âm, bị loại)
- **Record 4**: "Phone" - Category rỗng (bị loại)

**Records đã xử lý thành công:**
- Laptop: $1200 → Discounted: $1080
- Chair: $45 → Discounted: $40.50  
- Monitor: $300 → Discounted: $270

### Agent Simulation Results

| Scenario | Result | Accuracy |
|----------|--------|----------|
| Clean Data | "Best choice is Laptop at $1200" | 9/10 |
| Garbage Data | "Best choice is Nuclear Reactor at $999999" | 2/10 |

**Kết luận**: Dữ liệu sạch là yếu tố quyết định hiệu suất AI system, quan trọng hơn cả prompting.
