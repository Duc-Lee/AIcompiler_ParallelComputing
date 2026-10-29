## Lession 1: Numpy in Python

- Sang phần mới là phần về Phân tích dữ liệu bằng Python (Data analysis with Python)
  - Mô đun này sẽ tập trung vào các thư viện cốt lõi:
    - **Numpy, Pandas**: Dùng để xử lí, thao tác và phân tích dữ liệu
    - **Matplotlib, Seaborn**: Dùng để trực quan hóa dữ liệu (Data visualization)
- Trong số đó, Numpy đóng vai trò nền tảng tối quan trọng. Kể cả sau này khi làm việc với các mô đun Deep-Learning (Học sâu), bạn vẫn sẽ dùng Numpy theo nhiều cách khác nhau. Numpy cho phép chúng ta tạo mảng, thao tác với ma trận và thực thi các phép toán số học cực kì nhanh chóng.

### 1. Định nghĩa và cách cài đặt Numpy

- Numpy là thư viện cơ bản phục vụ tính toán khoa học trong Python. Nó cung cấp mảng đa chiều, ma trận cùng hệ thống các hàm toán học tối ưu để thao tác trực tiếp trên các cấu trúc dữ liệu này thông qua các phép toán vector hoá (vectorized operations).
- Khi khởi tạo một môi trường ảo (virtual environment) mới, Numpy không được tích hợp sẵn. Có 2 cách cài đặt:
  - **Cách 1: Qua file requirements.txt**
    - Thêm numpy vào file `requirements.txt`, sau đó mở terminal chạy lệnh:
```bash
pip install -r requirements.txt
```
  - **Cách 2: Chạy trực tiếp trong terminal**
```bash
pip install numpy
```
- Để sử dụng thư viện numpy, đặt bí danh (alias) là `np`:
```python
import numpy as np
```
- Việc khởi tạo đặt bí danh alias là `np` giúp không cần gõ lại toàn bộ nguyên vẹn chữ numpy.

### 2. Khởi tạo mảng và tìm hiểu về chiều

#### a. Mảng 1 chiều (1D - Array)
- Sử dụng hàm `np.array()` và truyền một danh sách (list) hoặc tuple.

```python
import numpy as np

# Tao mang 1 chieu
arr = np.array([1, 2, 3, 4, 5])

print(arr)
# Output: [1 2 3 4 5]

# Kiem tra du lieu cua doi tuong
print(type(arr))
# Output: <class 'numpy.ndarray'>

# Kiem tra kich thuoc va hinh dang
print(arr.shape)
# Output: (5,)
```
> Lưu ý quan trọng về mảng 1D: Kết quả shape hiển thị `(5,)` với một khoảng trống sau dấu phẩy nghĩa là mảng này chỉ có đúng 1 chiều gồm 5 phần tử. Đây không phải là 1 hàng 5 cột; mảng 1 chiều thuần túy không phân định hàng hay cột.

#### b. Chuyển đổi hình dạng (Reshape)
- Muốn chuyển dữ liệu thành dạng hàng và cột cụ thể (mảng 2 chiều) ta dùng phương thức `.reshape()`.
- Cú pháp:

```python
import numpy as np

arr = np.array([1, 2, 3, 4, 5])

# Chuyen doi hinh dang sang 2 chieu
arr_2D = arr.reshape(1, 5)

# Chuyen 1 hang thanh 5 cot
print(arr_2D)
# Output: [[1 2 3 4 5]]
```

- **Quy tắc bảo toàn phần tử**: Tổng số phần tử phải tương thích. 5 phần tử chỉ có thể reshape thành (1, 5) hoặc (5, 1). Nếu cố reshape thành (1, 4) sẽ báo lỗi vì $1 \times 4 = 4 \neq 5$.
- **Nhận biết số chiều qua ngoặc vuông `[]`**:
  - Mảng 1 chiều: `[1, 2, 3, 4, 5]`
  - Mảng 2 chiều: `[[1, 2, 3, 4, 5]]`
  - Mảng 3 chiều: `[[[1, 2, 3, 4, 5]]]`

#### c. Khởi tạo mảng 2 chiều trực tiếp (Nested List)
- Ta có thể truyền trực tiếp một list lồng nhau vào `np.array()`:

```python
import numpy as np

# Mang 2 chieu 2 hang, 5 cot
arr2 = np.array([
    [1, 2, 3, 4, 5],
    [2, 3, 4, 5, 6]
])

print(arr2)
# Output:
# [[1 2 3 4 5]
#  [2 3 4 5 6]]

print(arr2.shape)
# Output: (2, 5) -> 2 hang va 5 cot
```

### 3. Các hàm khởi tạo mảng tích hợp (Built-in Functions)
- Thay vì phải tự gõ từng list thủ công, Numpy cung cấp các hàm dựng sẵn:

#### a. np.arange()
- Tạo mảng tuần tự theo độ dài giá trị `(start, stop, step)`:

```python
import numpy as np

# Tao mang 0 den 9, nhay 2
arr = np.arange(0, 10, 2)
print(arr)
# Output: [0 2 4 6 8]

# Reshape thanh 5 hang 1 cot
arr2 = arr.reshape(5, 1)
print(arr2)
# Output:
# [[0]
#  [2]
#  [4]
#  [6]
#  [8]]
```

#### b. np.ones()
- Tạo một mảng toàn số 1, thường dùng khởi tạo số ban đầu Deep Learning:

```python
import numpy as np

# Khoi tao mang 2 chieu 3 hang, 4 cot toan so 1
arr = np.ones((3, 4))
print(arr)
# Output:
# [[1. 1. 1. 1.]
#  [1. 1. 1. 1.]
#  [1. 1. 1. 1.]]
```

- Tương tự ta có hàm `np.zeros()` để khởi tạo mảng toàn số 0.

#### c. np.eye()
- Tạo ma trận đơn vị (Identity matrix) - các phần tử trên đường chéo chính bằng 1, các phần tử còn lại bằng 0:

```python
import numpy as np

# Ma tran don vi 3x2
arr = np.eye(3, 2)
print(arr)
# Output:
# [[1. 0.]
#  [0. 1.]
#  [0. 0.]]
```

### 4. Các thuộc tính cơ bản của mảng Numpy

```python
import numpy as np

arr = np.array([[1, 2, 3], [4, 5, 6]])

# Kich thuoc cac chieu
print(arr.shape)
# Output: (2, 3)

# So chieu
print(arr.ndim)
# Output: 2

# So phan tu trong mang
print(arr.size)
# Output: 6

# Kieu du lieu cua phan tu
print(arr.dtype)
# Output: int32
```

### 5. Các phép toán vector hoá (Vectorized operations)
- Numpy cho phép tính toán theo từng phần tử (element-wise) trên các mảng có cùng kích thước dựa vào vị trí index tương ứng mà không cần viết vòng lặp:

```python
import numpy as np

arr1 = np.array([1, 2, 3, 4, 5])
arr2 = np.array([10, 20, 30, 40, 50])

# Phep cong phan tu
print("Cong: ", arr1 + arr2)

# Phep tru phan tu
print("Tru: ", arr1 - arr2)

# Phep nhan phan tu
print("Nhan: ", arr1 * arr2)

# Phep chia phan tu
print("Chia: ", arr1 / arr2)
# Output: [0.1 0.1 0.1 0.1 0.1]
```

- Kết quả trả về của mọi phép toán này luôn luôn là một mảng Numpy mới.

### 6. Các hàm toán học phổ biến
- Các hàm toán học này được áp dụng đồng loạt lên toàn bộ các phần tử trong mảng:

```python
import numpy as np

arr = np.array([1, 2, 3, 4, 5, 6])

# Can bac 2
print(np.sqrt(arr))

# Ham mu e^x
print(np.exp(arr))

# Ham luong giac
print(np.sin(arr))
print(np.cos(arr))
print(np.tan(arr))

# Ham logarit tu nhien
print(np.log(arr))
```

- Ngoài ra còn cung cấp các hàm lượng giác ngược như `arcsin()`, `arccos()`, `arctan()` và hàm hyperbolic như `sinh()`, `cosh()`, `tanh()`, `arcsinh()`, `arccosh()`, `arctanh()`.

### 7. Slicing & Index
- Index (chỉ mục) trong Numpy luôn tính từ 0.
- Cú pháp truy cập mảng 2 chiều là `array[hang, cot]`.
- Hoặc slicing cho mảng 2 chiều: `array[start_row:stop_row, start_col:stop_col]`.

- Khởi tạo mảng 2 chiều gồm 3 hàng, 4 cột:

```python
import numpy as np

arr = np.array([
    [1, 2, 3, 4],
    [5, 6, 7, 8],
    [9, 10, 11, 12]
])
```

- **Truy cập 1 phần tử đơn lẻ**:

```python
# Lay phan tu o hang 0, cot 0
print(arr[0, 0])
# Output: 1
```

- **Cắt các dữ liệu con (Sub-arrays)**:
  - **Lấy cụm `[[7, 8], [11, 12]]`**:
    - Nằm ở hàng 1 và hàng 2 $\rightarrow$ slice hàng `1:`
    - Nằm ở cột 2 và 3 $\rightarrow$ slice cột `2:`

```python
# Lay cum [7, 8] va [11, 12]
# [7, 8] hang 1 -> slice hang 1
# [11, 12] hang 2 -> slice hang 2
# Cot tu index 2 ve sau
print(arr[1:, 2:])
# Output:
# [[ 7,  8],
#  [11, 12]]
```

  - **Lấy cụm `[[3, 4], [7, 8]]`**:
    - Nằm ở hàng 0 và hàng 1 $\rightarrow$ slice hàng `0:2`
    - Nằm ở cột 2 và 3 $\rightarrow$ slice cột `2:`

```python
print(arr[:2, 2:])
# Output:
# [[3, 4],
#  [7, 8]]
```

  - **Lấy cụm `[[6, 7], [10, 11]]`**:
    - Nằm ở hàng 1 và hàng 2 $\rightarrow$ slice hàng `1:`
    - Nằm ở cột 1 và cột 2 $\rightarrow$ slice cột `1:3`

```python
print(arr[1:, 1:3])
# Output:
# [[ 6,  7],
#  [10, 11]]
```

- **Sửa đổi giá trị phần tử qua index**:

```python
# Gan lai cho arr[0][0] truc tiep = 100
arr[0][0] = 100
print(arr)
# Output:
# [[100, 2, 3],
#  [4, 5, 6],
#  [7, 8, 9]]

# Gan gia tri 50 cho toan bo ptu hang 1 den het con lai
arr[1:, :] = 50
print(arr)
# Output:
# [[100,  2,  3],
#  [ 50, 50, 50],
#  [ 50, 50, 50]]
```

### 8. Các ứng dụng thực tế và thống kê cơ bản

#### a. Chuẩn hoá dữ liệu (Standardization / Z-score Normalization)
- Trong Machine Learning, ta thường đưa dữ liệu về phân phối chuẩn hoá có giá trị trung bình $E(X) = \mu = 0$, độ lệch chuẩn $\sigma = 1$:

$$data_{normalized} = \frac{data - \mu}{\sigma}$$

$$\Rightarrow data_{normalized} = \frac{data - 0}{1} = data$$

```python
import numpy as np

# Khoi tao data
data = np.array([1, 2, 3, 4, 5, 6, 7, 8, 9, 10])

# Tinh E(X) va do lech chuan
mean = np.mean(data)
std = np.std(data)

print(mean)
print(std)

# Ap dung chuan hoa
normalized_data = (data - mean) / std
print("Du lieu sau chuan hoa:\n", normalized_data)
```

#### b. Các phép toán thống kê

```python
import numpy as np

data = np.array([1, 2, 3, 4, 5, 6, 7, 8, 9, 10])

# Tinh gia tri trung binh E(X)
print(np.mean(data))

# Tinh gia tri trung vi Med(X)
print(np.median(data))

# Tinh do lech chuan
print(np.std(data))

# Tinh phuong sai Variance(X)
print(np.var(data))
```

- **Giải thích từng bước**:
  - **Tính giá trị trung bình $E(X)$**:
    $$E(X) = \mu = \frac{1}{N} \sum_{i=1}^{N} x_i$$
    $$\Rightarrow \mu = \frac{1 + 2 + 3 + 4 + 5 + 6 + 7 + 8 + 9 + 10}{10} = 5.5$$

  - **Tính giá trị trung vị $\text{Med}(X)$**:
    - Mảng đã được sắp xếp.
    - $N$ mảng chẵn $\Rightarrow \text{Med}(X)$ là trung bình cộng của vị trí $\frac{N}{2}$ và $\frac{N}{2} + 1$.
    - $N$ mảng lẻ $\Rightarrow \text{Med}(X)$ là ở giữa $\frac{N}{2} + 1$.
    - $\Rightarrow N = 10$ (chẵn) nên 2 vị trí chính giữa là $x_5$ và $x_6$, với $x_5 = 5$, $x_6 = 6$:
      $$\Rightarrow \text{Med}(X) = \text{median} = \frac{5 + 6}{2} = 5.5$$

  - **Phương sai $\sigma^2$**:
    $$\text{Var}(X) = \sigma^2 = \frac{1}{N} \sum_{i=1}^{N} (x_i - \mu)^2$$
    Ta có:
    $$\text{Var}(X) = \frac{\sum_{i=1}^{10} (x_i - 5.5)^2}{10} = \frac{82.5}{10} = 8.25$$

  - **Độ lệch chuẩn $\sigma$**:
    $$\sigma = \sqrt{\sigma^2}$$
    $$\Rightarrow \sigma = \sqrt{8.25} \approx 2.8722813232690143$$

### 9. Các phép toán Logic và Lọc dữ liệu (Boolean Masking)
- Thao tác này là tiền đề tối quan trọng khi làm việc tới thư viện Pandas và bảng dữ liệu DataFrame.

#### a. Điều kiện đơn

```python
import numpy as np

data = np.array([1, 2, 3, 4, 5, 6, 7, 8, 9, 10])

# So sanh mang voi mot gia tri
# Tra ve mang Boolean
print(data > 5)

# Output:
# [False False False False False  True  True  True  True  True]

# Loc phan tu thoa man dieu kien
filtered_data = data[data > 5]
print(filtered_data)
# Output:
# [ 6  7  8  9 10]
```

#### b. Kết hợp nhiều điều kiện logic
- Kết hợp nhiều điều kiện logic trên mảng Numpy, từ khoá `and` của Python sẽ gây ra lỗi vì nó không đánh giá theo dạng mảng vector. Thay vào đó:
  - Dùng toán tử Bitwise `&` (thay cho `and`) và `|` (thay cho `or`).
  - Bắt buộc phải bọc biểu thức trong dấu ngoặc đơn `()` để tránh lẫn độ ưu tiên toán tử.

```python
import numpy as np

data = np.array([1, 2, 3, 4, 5, 6, 7, 8, 9, 10])

# Loc cac phan tu nam trong khoang [5, 8]
result = data[(data >= 5) & (data <= 8)]
print(result)

# Output:
# [5 6 7 8]
```