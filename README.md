# LLAMMA---threory
## LLAMMA **(Lending Liquidating Automated Market Maker Algorithm)** 
- Là một cơ chế lending giúp người vay có thể chọn khoảng giá của tài sản thế chấp để giảm thiểu rủi ro thanh lý khi giá của collateral giảm xuống.
- Người vay khi vay một lượng token sẽ được phép chọn một khoảng giá `[A; B]` nào đó
- Cũng giống style UniswapV3 thì LLAMMA cũng có khái niệm ticks và bands giống vậy, user cũng được phép chọn số lượng band
- Trong LLAMMA, các bands đã được xác định trước theo một lưới giá cố định, nhưng người dùng vẫn có thể chọn số lượng bands khi mở khoản vay. Điều này khác với Uniswap V3, nơi tick spacing cố định nhưng LPs có thể chọn bất kỳ khoảng nào để cung cấp thanh khoản.
- He thong se chon n bands gan gia thi truong cua collateral (n do nguoi dung chon)
- Khi giá của collateral giảm dần đến ngưỡng < B LLAMMA sẽ lần lượt thanh lý số collateral ở từng band bằng cách bán chúng đổi lấy BORROW_COIN => Giảm thiểu rủi ro cho người vay, khi giá xuống còn < A thì bất kỳ ai cũng có thể thanh lý khoàn vay của user
- Nếu giá hiện tại là X':
  - Nếu X' > B && HF < 1: Bất kỳ ai cũng có thể thanh lý, nhưng LLAMMA sẽ không thanh lý cho đến khi giá <= B.
  - Nếu X' < A && HF > 1: Hiển nhiễn đã thanh lý hoàn toàn
- Khi giá của collateral tăng trở lại qua ngưỡng > A thì LLAMMA sẽ lại bán lại số token để mua lại collateral cho user
- Xét trên khoảng `[Li, Ri]`,
  - Nếu `Pcur > Ri` thì toàn bộ band này vẫn an toàn còn nguyên collateral
  - Nếu `Li < Pcur < Ri` thì một phần collateral bị bán theo tỉ lệ
  - Nếu `Pcur < Li` thì toàn bộ collateral đã bị bán

## Swap trong LLAMMA
- Swap từ `stablecoin` sang `collateral`: lấy collateral từ band cao nhất trước(trong các band của các người vay) theo giá trong band
- Swap từ `collateral` sang `stablecoin`: lấy stablecoin từ band thấp nhất trước(trong các band của các người vay) theo giá trong band
- Nếu các band giao nhau thì phân chia theo tỉ lệ sở hữu

## Vay thêm

 
## Công thức


## Note
- `active_band`: band giá hiện tại mà giá hiện tại thuộc vào.
  - xác định bằng cách lấy band giá nhơ hơn gần nhất mà  <= giá hiện tại trong AMM, nếu không có band nào thấp hơn thì chọn band cao hơn gần nhất (theo đầu L)
