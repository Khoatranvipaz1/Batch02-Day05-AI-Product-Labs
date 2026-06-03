# Workshop - Mổ App AI Thật

**Họ tên:** Nghiêm Tuấn Linh  
**Mã học viên:** 2A202600897  
**Sản phẩm được chọn:** MoMo - Moni  
**Track:** D - Personal Finance  
**Flow dùng thử:** Hỏi Moni xem tháng trước tiêu linh tinh hơi nhiều và nên cắt bớt khoản nào.

---

## 1. Chọn một sản phẩm để dùng thử

| Sản phẩm | AI feature | Cách truy cập |
|---|---|---|
| MoMo - Moni | Trợ thủ tài chính, phân tích chi tiêu, chatbot | App MoMo |

**Task dùng thử:**  
Người dùng hỏi Moni:

```text
moni ơi tháng trước mình tiêu linh tinh hơi nhiều, giúp mình xem khoản nào cắt bớt với
```

Và tiếp tục hỏi:

```text
tháng trước khoản naod tôi tiêu nhiều nhất
cho tôi xem tổng gd ăn uống
thế bạn cho tôi biết khoản nhóm nào tôi chi nhiều nhấzt
```

---

## 2. Dùng thử: promise vs reality

- **Product hứa gì?**  
  Moni được đặt như một trợ thủ AI tài chính trong MoMo. Product tạo kỳ vọng rằng người dùng có thể hỏi bằng ngôn ngữ tự nhiên về chi tiêu cá nhân, sau đó nhận được phân tích để hiểu tiền của mình đi đâu và nên cắt bớt khoản nào.

- **User nào được hứa sẽ được giúp?**  
  User là người dùng MoMo hằng ngày, có nhiều giao dịch nhỏ trong tháng và không muốn tự mở từng giao dịch để cộng tay. User muốn AI đọc dữ liệu, gom nhóm chi tiêu, chỉ ra nhóm nào lớn nhất và đề xuất hành động tiếp theo.

- **Kỳ vọng AI làm được task nào?**  
  Với câu hỏi "tháng trước mình tiêu linh tinh hơi nhiều, giúp mình xem khoản nào cắt bớt", Moni nên:

  - đọc dữ liệu giao dịch tháng trước;
  - gom giao dịch theo nhóm chi tiêu;
  - tính tổng tiền từng nhóm;
  - xếp hạng nhóm chi tiêu từ cao xuống thấp;
  - chỉ ra nhóm nào nên cắt bớt trước;
  - nếu thiếu dữ liệu phân loại, nói rõ phần nào chưa chắc;
  - đưa action để xem chi tiết hoặc sửa phân loại.

- **Khi dùng thật, điểm gãy xuất hiện ở đâu?**  
  Điểm gãy nằm ở bước **chuyển dữ liệu thành insight hành động**. Moni lấy được tổng chi tiêu tháng 05/2026 là **1.202.222đ**, có **23 giao dịch**, trung bình **38.781đ/ngày**. Tuy nhiên, khi user hỏi khoản nào tiêu nhiều nhất hoặc khoản nào nên cắt bớt, Moni không trả lời trực tiếp nhóm chi tiêu cao nhất. Moni yêu cầu user chọn từng nhóm hoặc xem từng giao dịch lớn nhất.

### Evidence từ ảnh chụp màn hình

| Ảnh | Prompt / input | Hành vi quan sát được |
|---|---|---|
| `d43183cb-038a-4089-afc4-05eac6197151.jpg` | "moni ơi tháng trước mình tiêu linh tinh hơi nhiều, giúp mình xem khoản nào cắt bớt với" | Moni trả tổng chi tiêu tháng 05/2026 là **1.202.222đ**, **23 giao dịch**, trung bình **38.781đ/ngày**, nhưng chỉ nói user nên tập trung vào nhóm không cần thiết hoặc tỷ trọng lớn. Moni chưa liệt kê nhóm nào lớn nhất. |
| `0b87a6db-84ad-4459-a76f-5304211016a1.jpg` | "tháng trước khoản naod tôi tiêu nhiều nhất" | Moni tiếp tục trả tổng chi tiêu **1.202.222đ** và hỏi user muốn xem theo từng nhóm chi tiêu hay liệt kê giao dịch lớn nhất. |
| `0b87a6db-84ad-4459-a76f-5304211016a1.jpg` | "cho tôi xem tổng gd ăn uống" | Khi user chỉ định rõ nhóm, Moni trả được nhóm **Ăn uống: 154.000đ**, **2 giao dịch**, trung bình **4.967đ/ngày**. |
| `8f59ed48-a224-4661-a29c-ed1209d1abda.jpg` | "thế bạn cho tôi biết khoản nhóm nào tôi chi nhiều nhấzt" | Moni lại trả tổng chi tiêu **1.202.222đ** và nói hiện tại chưa thấy dữ liệu chi tiết theo từng nhóm chi tiêu. |

### Quote từ app

```text
Hiện tại, Moni chưa thấy dữ liệu chi tiết theo từng nhóm chi tiêu. Bạn có muốn xem lại các giao dịch lớn nhất hoặc chi tiết từng khoản để Moni giúp bạn xác định nhóm chi tiêu nhiều nhất không?
```

### Nhận xét quan sát

Vấn đề không phải Moni hoàn toàn không có dữ liệu. Moni có thể lấy tổng chi tiêu tháng và trả dữ liệu một nhóm cụ thể khi user hỏi "ăn uống". Vấn đề là Moni chưa tự gom nhóm và xếp hạng để trả lời đúng intent "khoản nào cắt bớt" / "nhóm nào chi nhiều nhất". User phải hỏi từng nhóm riêng lẻ, sau đó tự suy luận.

---

## 3. Vẽ 4 paths

| Path | Quan sát trong Moni | Đánh giá |
|---|---|---|
| Happy | Khi user hỏi cụ thể "cho tôi xem tổng gd ăn uống", Moni trả được **Ăn uống: 154.000đ**, **2 giao dịch**, trung bình **4.967đ/ngày**. | Moni có khả năng trả dữ liệu theo category nếu user chỉ định category rõ ràng. |
| Low-confidence | Khi không có ranking theo nhóm, Moni hỏi user muốn xem từng nhóm hay liệt kê giao dịch lớn nhất. | Có hỏi lại, nhưng hỏi lại chưa giảm việc cho user. User cần câu trả lời "nhóm nào nhiều nhất", không phải tự chọn nhóm để kiểm tra. |
| Failure | Moni trả tổng chi tiêu và số giao dịch, nhưng không chỉ ra nhóm chi tiêu cao nhất hoặc khoản nên cắt bớt trước. | Đây là path yếu nhất: **spending category ranking failure**. |
| Correction | Chưa thấy có cơ chế để user sửa category giao dịch, xác nhận ranking, hoặc lưu correction để lần sau phân loại tốt hơn. | Product thiếu recovery path khi AI không biết nhóm nào cao nhất hoặc khi phân loại giao dịch chưa rõ. |

### Path yếu nhất

**Spending category ranking failure** - Moni có tổng dữ liệu chi tiêu nhưng không tự xếp hạng nhóm chi tiêu để trả lời câu hỏi cần cắt bớt khoản nào.

```text
User hỏi: "tháng trước mình tiêu linh tinh hơi nhiều, giúp mình xem khoản nào cắt bớt"
-> Moni trả tổng chi tiêu tháng 05/2026: 1.202.222đ
-> Moni trả 23 giao dịch và trung bình 38.781đ/ngày
-> Moni không nói nhóm nào lớn nhất
-> Moni hỏi user có muốn liệt kê nhóm chi tiêu lớn nhất không
-> User hỏi tiếp "khoản nào tôi tiêu nhiều nhất"
-> Moni vẫn không trả ranking, yêu cầu user chọn từng nhóm hoặc xem giao dịch lớn
-> User hỏi riêng nhóm ăn uống
-> Moni trả Ăn uống = 154.000đ
-> User tiếp tục hỏi nhóm nào chi nhiều nhất
-> Moni nói chưa thấy dữ liệu chi tiết theo từng nhóm
-> User vẫn chưa biết nên cắt bớt khoản nào trước
```

---

## 4. Viết finding thành quyết định

Không viết:

```text
Moni trả lời chung chung và không hữu ích.
```

Viết:

```text
Khi user hỏi "tháng trước mình tiêu linh tinh hơi nhiều, giúp mình xem khoản nào cắt bớt", Moni lấy được tổng chi tiêu tháng 05/2026 là 1.202.222đ và có thể trả dữ liệu của một nhóm cụ thể như Ăn uống = 154.000đ. Tuy nhiên, Moni không tự gom nhóm, xếp hạng và chỉ ra nhóm chi tiêu cao nhất hoặc nhóm nên cắt bớt trước. Hậu quả là user phải hỏi từng nhóm riêng lẻ và tự suy luận, trong khi đây chính là việc user mong AI làm giúp.
```

### Product decision

Moni cần ưu tiên sửa flow **category ranking for cut-back advice** cho các câu hỏi dạng:

- "khoản nào tôi tiêu nhiều nhất";
- "tôi nên cắt bớt khoản nào";
- "tháng trước tiêu linh tinh nhiều quá";
- "nhóm nào chi nhiều nhất".

Với trợ thủ tài chính cá nhân, câu trả lời không nên dừng ở tổng chi tiêu. Moni cần chuyển dữ liệu giao dịch thành insight có thể hành động:

```text
Giao dịch tháng trước
-> phân loại / gom nhóm
-> tính tổng từng nhóm
-> xếp hạng
-> nếu chưa chắc thì show phần chưa phân loại
-> đề xuất nhóm nên cắt bớt trước
-> đưa action xem/sửa giao dịch
```

### Requirement đề xuất

- Nếu user hỏi về "tiêu nhiều nhất", "cắt bớt", "nhóm nào chi nhiều", hệ thống phải kích hoạt intent **spending category ranking**.
- Trả lời trực tiếp top category hoặc nói rõ "chưa đủ dữ liệu để kết luận" kèm lý do.
- Hiển thị tổng chi tiêu, top 3 nhóm, số tiền từng nhóm và tỷ lệ phần trăm.
- Tách riêng nhóm **Khác / chưa phân loại** để tránh kết luận sai.
- Đề xuất nhóm nên cắt bớt dựa trên tổng tiền và độ cần thiết của category.
- Có action button:
  - Xem giao dịch nhóm này;
  - So sánh với tháng trước;
  - Đặt hạn mức cho nhóm này;
  - Sửa phân loại giao dịch.

### Câu trả lời to-be mong muốn

```text
Tháng 05/2026, bạn đã chi tổng cộng 1.202.222đ với 23 giao dịch.

Mình chưa nên kết luận ngay nếu còn giao dịch chưa phân loại, nhưng trong các nhóm hiện có, mình thấy:

1. [Nhóm cao nhất]: ...đ, chiếm ...%
2. Ăn uống: 154.000đ, chiếm khoảng 12,8%
3. Khác / chưa phân loại: ...đ

Nếu mục tiêu là cắt bớt chi tiêu linh tinh, bạn nên xem trước nhóm có tỷ trọng lớn nhất và các giao dịch trong nhóm Khác / chưa phân loại. Bạn muốn mình mở danh sách giao dịch của nhóm này hay đặt hạn mức cho tháng sau?
```

---

## 5. Sketch as-is / to-be

| As-is: flow hiện tại | To-be: flow đề xuất |
|---|---|
| User mở MoMo và vào Trợ thủ AI - Moni. | User mở MoMo và vào Trợ thủ AI - Moni. |
| User hỏi: "tháng trước mình tiêu linh tinh hơi nhiều, giúp mình xem khoản nào cắt bớt". | User hỏi: "tháng trước mình tiêu linh tinh hơi nhiều, giúp mình xem khoản nào cắt bớt". |
| Moni lấy tổng chi tiêu tháng 05/2026. | Moni nhận diện intent: **spending category ranking / cut-back advice**. |
| Moni trả tổng tiền 1.202.222đ, 23 giao dịch, trung bình 38.781đ/ngày. | Moni lấy dữ liệu giao dịch tháng 05/2026. |
| **Điểm gãy:** Moni không chỉ ra khoản nào nên cắt bớt hoặc nhóm nào tiêu nhiều nhất. | Moni gom giao dịch theo category. |
| Moni hỏi user muốn xem từng nhóm hay giao dịch lớn nhất. | Moni tính tổng tiền từng category. |
| User phải hỏi tiếp từng nhóm, ví dụ "ăn uống". | Moni xếp hạng category từ cao xuống thấp. |
| Moni trả dữ liệu riêng của nhóm ăn uống: 154.000đ. | Moni trả top category, top 3 nhóm và phần chưa phân loại. |
| User hỏi lại nhóm nào chi nhiều nhất. | Moni đề xuất nhóm nên cắt bớt trước và giải thích lý do. |
| Moni nói chưa thấy dữ liệu chi tiết theo từng nhóm. | Moni đưa action để xem giao dịch, sửa phân loại, đặt hạn mức. |

### As-is flow

```text
User mở Moni
-> Hỏi: "tháng trước mình tiêu linh tinh hơi nhiều, giúp mình xem khoản nào cắt bớt"
-> Moni trả tổng chi tiêu 1.202.222đ
-> Moni trả 23 giao dịch, trung bình 38.781đ/ngày
-> Moni không chỉ ra nhóm nào lớn nhất
-> Moni hỏi user có muốn xem từng nhóm/giao dịch lớn không
-> User hỏi "khoản nào tôi tiêu nhiều nhất"
-> Moni vẫn không trả ranking
-> User hỏi riêng "ăn uống"
-> Moni trả Ăn uống = 154.000đ
-> User hỏi lại "nhóm nào tôi chi nhiều nhất"
-> Moni nói chưa thấy dữ liệu chi tiết theo từng nhóm
```

### To-be flow

```text
User hỏi: "tháng trước mình tiêu linh tinh hơi nhiều, giúp mình xem khoản nào cắt bớt"
-> Moni nhận diện intent: spending category ranking / cut-back advice
-> Moni lấy dữ liệu giao dịch tháng 05/2026
-> Moni gom nhóm giao dịch theo category
-> Moni tính tổng tiền từng nhóm
-> Moni xếp hạng category từ cao xuống thấp
-> Moni trả nhóm chi tiêu cao nhất và top 3 nhóm
-> Moni nói rõ phần nào chưa được phân loại
-> Moni đề xuất nhóm nên cắt bớt trước
-> User chọn xem giao dịch, sửa phân loại hoặc đặt hạn mức
```

### Lúc AI không chắc thì sao?

Nếu Moni chưa có đủ dữ liệu chi tiết theo từng nhóm, không nên chỉ trả lời chung chung "chưa thấy dữ liệu". Moni nên nói rõ mức độ chắc chắn và đưa path tiếp theo:

```text
Mình lấy được tổng chi tiêu tháng 05/2026 là 1.202.222đ, nhưng hiện có một số giao dịch chưa được gán nhóm rõ ràng. Vì vậy ranking có thể chưa chính xác.

Mình có thể làm 2 việc:
1. Liệt kê 5 giao dịch lớn nhất để bạn gán nhóm nhanh.
2. Tạm tính ranking theo các nhóm đã biết, kèm nhóm Khác / chưa phân loại.
```

### Lúc AI sai user recover thế nào?

Cần có correction path:

```text
User chọn "Sửa phân loại giao dịch"
-> Moni hiện các giao dịch chưa rõ nhóm
-> User chọn một giao dịch
-> User gán lại category
-> Moni cập nhật ranking ngay
-> Moni lưu correction để lần sau gợi ý phân loại tốt hơn
```

---

## 6. Tự kiểm trước khi nộp

- [x] Có ít nhất 1 screenshot hoặc observation cụ thể.
- [x] Có đủ 4 paths hoặc nói rõ path nào chưa có trong product.
- [x] Finding được viết thành product decision, không chỉ là nhận xét.
- [x] Sketch có as-is và to-be.
- [x] Có một câu nói rõ finding này sẽ đổi gì trong SPEC.

### Câu nói rõ finding này sẽ đổi gì trong SPEC

Finding này sẽ đổi SPEC của Moni bằng cách thêm requirement:

```text
Mọi câu hỏi dạng "tôi nên cắt bớt khoản nào", "nhóm nào tôi chi nhiều nhất", "khoản nào tiêu nhiều nhất" phải kích hoạt spending category ranking flow. Moni phải trả top category hoặc nếu chưa đủ dữ liệu thì phải nói rõ lý do, hiển thị top nhóm đã biết, phần Khác / chưa phân loại và action để user xem hoặc sửa giao dịch.
```
