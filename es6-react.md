# Tổng hợp ES6 và ReactJS

## Phần 1: ECMAScript 6

### 1. Promise.all(), Promise.race(), Promise.allSettled(), Promise.any()

-   **Promise.all()**: Chờ tất cả thành công; 1 lỗi → lỗi chung.
-   **Promise.race()**: Promise hoàn thành đầu tiên (thành công hoặc
    lỗi).
-   **Promise.allSettled()**: Chờ tất cả xong; trả về trạng thái từng
    cái.
-   **Promise.any()**: Thành công đầu tiên; tất cả lỗi → mới lỗi.

### 2. Destructuring assignment

**Object:**

``` js
const user = { name: "Anh", age: 20 };
const { name, age } = user;
```

**Array:**

``` js
const colors = ["red", "green"];
const [first, second] = colors;
```

### 3. Spread vs Rest

-   **Spread (...):** Trải phần tử\

``` js
const arr2 = [...arr1];
```

-   **Rest (...):** Thu phần tử\

``` js
function sum(...nums) {}
```

### 4. let/const vs var (scope)

-   **var:** function scope\
-   **let/const:** block scope `{}`\
-   **const:** không gán lại

### 5. Template literals

-   Dùng `` ` `` và `${}` để chèn biến\

``` js
console.log(`Hello ${name}`);
```

### 6. Arrow function và this

-   Không có `this` riêng → lấy từ scope ngoài.
-   Function thường: `this` thay đổi theo cách gọi.

### 7. Default parameters

``` js
function greet(name = "Guest") {}
```

------------------------------------------------------------------------

## Phần 2: ReactJS

### 1. Controlled vs Uncontrolled components

-   **Controlled:** Giá trị input lưu trong state.
-   **Uncontrolled:** Input tự quản lý, dùng `ref` để lấy giá trị.

### 2. React keys

-   Giúp React nhận diện phần tử trong list → render tối ưu và tránh
    lỗi.

### 3. Props vs State

-   **Props:** Từ cha truyền xuống; không tự thay đổi.
-   **State:** Tự quản lý trong component; thay đổi bằng `setState`.
