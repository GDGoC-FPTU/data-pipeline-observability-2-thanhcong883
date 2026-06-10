# Experiment Report: Data Quality Impact on AI Agent

**Student ID:** 2A202600544
**Name:** Giang Thành Công
**Date:** 10/06/2026

---

## 1. Ket qua thi nghiem

Chay `agent_simulation.py` voi 2 bo du lieu va ghi lai ket qua:

| Scenario | Agent Response | Accuracy (1-10) | Notes |
|----------|----------------|-----------------|-------|
| Clean Data (`processed_data.csv`) | Agent: Based on my data, the best choice is Laptop at $1200. | 10 | Dữ liệu đã qua tiền xử lý, loại bỏ giá trị âm, trống category và tính đúng giá chiết khấu. |
| Garbage Data (`garbage_data.csv`) | Agent: Based on my data, the best choice is Nuclear Reactor at $999999. | 1 | Dữ liệu bị lỗi ngoại lệ cực đoan (outlier), trùng lặp ID, sai kiểu dữ liệu và giá trị rỗng (null/None) khiến Agent đưa ra quyết định sai lầm. |

---

## 2. Phan tich & nhan xet

### Tai sao Agent tra loi sai khi dung Garbage Data?

Agent trả lời sai khi sử dụng Garbage Data vì dữ liệu này chứa nhiều vấn đề nghiêm trọng về chất lượng dữ liệu:
1. **Duplicate IDs (Trùng lặp ID):** ID số 1 xuất hiện cả ở 'Laptop' và 'Banana', khiến việc định danh dữ liệu bị lỗi và mất tính nhất quán.
2. **Wrong Data Types (Sai kiểu dữ liệu):** Giá trị giá của 'Broken Chair' là dạng text 'ten dollars' thay vì dạng số, điều này dễ gây ra lỗi tính toán (TypeError/ValueError) khi Agent xử lý số liệu hoặc so sánh giá trị.
3. **Extreme Outliers (Ngoại lệ cực đoan):** Sản phẩm 'Nuclear Reactor' có giá trị lên tới $999,999, vượt xa các sản phẩm thông thường. Vì Agent chọn sản phẩm tốt nhất dựa trên giá cao nhất (`idxmax()`), outlier này đã đánh lừa Agent khiến nó đưa ra đề xuất phi thực tế.
4. **Null Values (Giá trị rỗng):** 'Ghost Item' có ID là None và Category là None, gây thiếu hụt thông tin định danh và phân loại, dễ làm phát sinh lỗi null pointer trong logic nghiệp vụ.

Tất cả các yếu tố này làm nhiễu dữ liệu đầu vào của Agent, phá vỡ logic phân tích và dẫn tới kết quả sai lệch hoàn toàn.

---

## 3. Ket luan

**Quality Data > Quality Prompt?** (Dong y hay khong? Giai thich ngan gon.)

Tôi hoàn toàn đồng ý với nhận định "Quality Data > Quality Prompt". Dù prompt của chúng ta có được thiết kế tối ưu và thông minh đến đâu, nếu dữ liệu đầu vào bị nhiễm độc (outliers, null, sai kiểu dữ liệu), Agent vẫn sẽ truy xuất thông tin sai lệch và đưa ra câu trả lời không chính xác (Garbage In, Garbage Out). Chất lượng dữ liệu chính là nền móng cốt lõi để đảm bảo sự ổn định và chính xác của các mô hình AI Agent. Do đó, việc xây dựng một pipeline ETL mạnh mẽ để làm sạch và giám sát dữ liệu (Data Observability) là bắt buộc.
