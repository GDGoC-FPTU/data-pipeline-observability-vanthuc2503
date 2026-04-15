# Experiment Report: Data Quality Impact on AI Agent

**Student ID:** AI20K-0238
**Name:** Nguyen Van Thuc
**Date:** 14-04-2026

---

## 1. Ket qua thi nghiem

Chay `agent_simulation.py` voi 2 bo du lieu va ghi lai ket qua:

| Scenario | Agent Response | Accuracy (1-10) | Notes |
|----------|----------------|-----------------|-------|
| Clean Data (`processed_data.csv`) | "Based on my data, the best choice is Laptop at $1200." | 9/10 | Chọn sản phẩm electronics có giá hợp lý. Có dữ liệu đầy đủ và sạch. |
| Garbage Data (`garbage_data.csv`) | "Based on my data, the best choice is Nuclear Reactor at $999999." | 2/10 | Agent chọn sản phẩm có giá cao nhất (outlier) thay vì lựa chọn hợp lý. Dữ liệu chứa nhiều lỗi. |

---

## 2. Phan tich & nhan xet

### Tai sao Agent tra loi sai khi dung Garbage Data?

Agent trả lời sai vì dữ liệu "garbage" chứa nhiều lỗi chất lượng dữ liệu:

1. **Duplicate IDs**: ID "1" xuất hiện hai lần (Laptop và Banana) làm cho logic xử lý nhầm lẫn
2. **Wrong Data Types**: Giá của "Broken Chair" là "ten dollars" thay vì số, gây lỗi khi so sánh  
3. **Extreme Outliers**: "Nuclear Reactor" có giá $999,999 - vượt trội so với mọi sản phẩm khác. Thuật toán Agent chỉ tìm max(price) nên chọn nhầm
4. **Null Values**: Có dòng với missing ID và missing category, không thể xác định loại sản phẩm
5. **Inconsistent Formatting**: Category "electronics" (chữ thường) không match "Electronics" (hoa) trong clean data, dẫn tới lọc dữ liệu không chính xác

Những vấn đề này làm Agent không thể đưa ra quyết định chính xác hay có logic kinh doanh tốt.

---

## 3. Ket luan

**Quality Data > Quality Prompt?** **ĐỒNG Ý** 

Kết quả thực nghiệm cho thấy: **Chất lượng dữ liệu quan trọng hơn chất lượng prompt**. Dù Agent có logic đơn giản, nó vẫn hoạt động tốt với dữ liệu sạch (accuracy 9/10). Nhưng cùng Agent đó, với dữ liệu bẩn, accuracy rơi xuống 2/10 vì:
- Dữ liệu sạch giúp Agent xử lý chính xác theo logic được thiết kế
- Dữ liệu bẩn làm cho kết quả vô nghĩa: chọn Nuclear Reactor $999,999 thay vì Laptop

**Kết luận**: Không quan trọng model hay prompt tốt đến đâu, nếu dữ liệu đầu vào xấu thì output cũng xấu. Data Quality là nền tảng của AI/ML systems thành công.
