# ES6 & ReactJS -- Giải thích sâu và đầy đủ

## PHẦN 1 -- ECMASCRIPT 6 (ES6)

------------------------------------------------------------------------

## 4. Sự khác biệt sâu giữa var, let và const (Scope + Hoisting + TDZ)

### 1) **var -- function scope**

-   `var` chỉ bị giới hạn trong **hàm**.
-   Nếu khai báo trong `if`, `for`, `{ }` → vẫn truy cập được bên ngoài.

``` js
if (true) {
  var x = 10;
}
console.log(x); // 10
```

### 2) **let & const -- block scope**

-   Chỉ tồn tại trong **{}**.
-   An toàn, tránh ghi đè biến ngoài ý muốn.

``` js
if (true) {
  let y = 20;
}
console.log(y); // Error
```

### 3) **Hoisting khác nhau**

-   `var` được hoisting và khởi tạo = `undefined`
-   `let` và `const` được hoisting nhưng *không khởi tạo* → nằm trong
    **Temporal Dead Zone (TDZ)**

``` js
console.log(a); // undefined
var a = 5;

console.log(b); // Error (TDZ)
let b = 5;
```

### 4) **const**

-   Không gán lại biến\
-   Nhưng dữ liệu *bên trong object/array* vẫn thay đổi được

``` js
const user = { name: "Anh" };
user.name = "Dũng"; // OK
```

------------------------------------------------------------------------

## 6. Arrow function xử lý "this" khác function thường như thế nào?

### ✔ Function thường

-   `this` phụ thuộc vào **cách gọi hàm**
-   Một hàm có thể có nhiều giá trị `this` khác nhau

``` js
function demo() {
  console.log(this);
}
demo();        // this = window
obj.demo();    // this = obj
```

### ✔ Arrow function

-   **Không tạo this mới**
-   this = this của *ngữ cảnh bên ngoài nó* (lexical this)

Ví dụ kinh điển:

``` js
const obj = {
  name: "Anh",
  say() {
    setTimeout(() => {
      console.log(this.name);
    }, 1000);
  }
};
```

→ Arrow function lấy `this` từ `say()` → đúng ngữ cảnh.

### ✔ Arrow function:

-   Không làm constructor\
-   Không có prototype\
-   Không có `arguments` riêng

------------------------------------------------------------------------

## PHẦN 2 -- REACTJS

------------------------------------------------------------------------

## 3. Giải thích sâu hơn sự khác biệt giữa Props và State

### ✔ Props -- dữ liệu bên ngoài truyền vào

-   Truyền xuống từ component cha
-   Không được phép thay đổi trong component con
-   Giúp component **tái sử dụng** dễ dàng

Ví dụ:

``` jsx
<Hello name="Anh" />
```

``` jsx
function Hello(props) {
  return <p>Xin chào {props.name}</p>;
}
```

------------------------------------------------------------------------

### ✔ State -- dữ liệu nội bộ, có thể thay đổi

-   Được quản lý bởi component
-   Thay đổi bằng setState / setSomething
-   Khi state thay đổi → component tự render lại

``` jsx
const [count, setCount] = useState(0);
```

------------------------------------------------------------------------

## So sánh chuyên sâu

  Tiêu chí                   Props              State
  -------------------------- ------------------ ----------------------
  Nguồn gốc                  Cha truyền xuống   Nội bộ component
  Thay đổi được?             ❌ Không           ✔ Có
  Làm component re-render?   ❌ Không           ✔ Có
  Ai quản lý?                Component cha      Component sở hữu nó
  Giống gì?                  Tham số hàm        Biến trong component

------------------------------------------------------------------------
