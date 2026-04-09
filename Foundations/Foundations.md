# Chương 2: Getting Started

## 2.1 Sắp xếp chèn (Insertion Sort)

Thuật toán sắp xếp chèn hoạt động tương tự như cách bạn sắp xếp các quân bài trên tay. Bạn lấy một quân bài mới và chèn nó vào đúng vị trí trong tập hợp các quân bài đã được sắp xếp trước đó.



---

## Bài tập thực hành (Exercises)

### Bài 2.1-1: Minh họa Insertion Sort
**Yêu cầu:** Minh họa các bước của thuật toán trên mảng $A = \{31, 41, 59, 26, 41, 58\}$.

* **Mảng ban đầu:** $\{31, 41, 59, 26, 41, 58\}$
* **Bước 1 ($i=1$):** Chèn $41$. Mảng không đổi: $\{31, 41, 59, 26, 41, 58\}$
* **Bước 2 ($i=2$):** Chèn $59$. Mảng không đổi: $\{31, 41, 59, 26, 41, 58\}$
* **Bước 3 ($i=3$):** Chèn $26$. Đưa $26$ về đầu: $\{26, 31, 41, 59, 41, 58\}$
* **Bước 4 ($i=4$):** Chèn $41$. Đưa $41$ vào sau giá trị $41$ cũ: $\{26, 31, 41, 41, 59, 58\}$
* **Bước 5 ($i=5$):** Chèn $58$. Đưa $58$ vào giữa $41$ và $59$: **$\{26, 31, 41, 41, 58, 59\}$**

---

### Bài 2.1-2: Insertion Sort theo thứ tự giảm dần
**Yêu cầu:** Viết lại mã giả/code cho thuật toán sắp xếp giảm dần.

```python
def insertion_sort_decreasing(arr):
    for i in range(1, len(arr)):
        key = arr[i]
        j = i - 1
        # Thay đổi điều kiện từ arr[j] > key thành arr[j] < key
        while j >= 0 and arr[j] < key:
            arr[j + 1] = arr[j]
            j -= 1
        arr[j + 1] = key
    return arr
```

---

### Bài 2.1-3: Tìm kiếm tuyến tính (Linear Search)
**Yêu cầu:** Tìm giá trị $v$ trong mảng $A$.

**Mã giả:**
```text
LINEAR-SEARCH(A, v)
    for i = 0 to A.length - 1
        if A[i] == v
            return i
    return NIL
```

**Chứng minh bất biến vòng lặp (Loop Invariant):**
* **Khởi tạo (Initialization):** Trước vòng lặp đầu tiên ($i=0$), tập hợp các phần tử đã kiểm tra là rỗng. Do đó, việc không tìm thấy $v$ là hiển nhiên đúng.
* **Duy trì (Maintenance):** Nếu tại bước $i$, $A[i] \neq v$, vòng lặp tiếp tục sang $i+1$. Điều này đảm bảo rằng nếu thuật toán chưa kết thúc, thì $v$ không xuất hiện trong đoạn $A[0 \dots i]$.
* **Kết thúc (Termination):** Vòng lặp kết thúc khi $i = A.length$. Lúc này, ta đã kiểm tra toàn bộ mảng và không thấy $v$, vì vậy trả về `NIL` là chính xác.

---

### Bài 2.1-4: Cộng hai số nguyên nhị phân $n$-bit
**Bài toán:**
* **Đầu vào:** Hai mảng $A$ và $B$ có $n$ phần tử biểu diễn hai số nhị phân.
* **Đầu ra:** Mảng $C$ có $(n+1)$ phần tử biểu diễn tổng $A + B$.

**Mã giả tối ưu:**
```text
ADD-BINARY-INTEGERS(A, B):
    n = A.length
    C = new array[n + 1]
    carry = 0  // Biến nhớ

    for i = n - 1 down to 0:
        sum = A[i] + B[i] + carry
        C[i + 1] = sum % 2    // Lấy phần dư (0 hoặc 1)
        carry = sum // 2      // Lấy phần nguyên (nhớ 1 nếu sum >= 2)
    
    C[0] = carry
    return C
```

**Ví dụ minh họa:**
> Với $A = \{0, 1, 0, 0\}$ (số 4) và $B = \{0, 1, 0, 1\}$ (số 5)
>
> 1. $i=3: 0+1+0 = 1 \rightarrow C[4]=1, carry=0$
> 2. $i=2: 0+0+0 = 0 \rightarrow C[3]=0, carry=0$
> 3. $i=1: 1+1+0 = 2 \rightarrow C[2]=0, carry=1$
> 4. $i=0: 0+0+1 = 1 \rightarrow C[1]=1, carry=0$
> 5. Kết thúc: $C[0]=0$. 
> **Kết quả:** $C = \{0, 1, 0, 0, 1\}$ (số 9). Chính xác!