# Tech

## Git:
+ git pull vs git merge
+ cherry pick

## JS:

### Các cách xử lý asynchronous
+ async await
+ Promise
+ Callback
+ Có thay thế hết promise = async await được ko, ko vì nhiều case dùng để gọi nhiều request cùng 1 lúc async ko giải quyết đc, phải dùng Promise

### Token thường lưu vào đâu, localStorage và sessionStorage khác nhau điểm nào
+ localStorage ko mất khi đóng tab hay browser, session thì mất.
+ localStorage có lưu lượng nhớ lớn hơn

### Dùng promise gọi 5 thằng 1 thằng dính lỗi thì ngừng luôn:
+ Promise.race

### Tạo 1 function counter:
+ Dùng closure, tạo 1 biến đc lưu vào bộ nhớ vs return về 1 hàm change value of biến đó

### Check array như nào:
+ Array.isArray
+ [] instanceof Array

## React:

### life cycle, có set đc state trong render vs cả componentdidupdate ko
+ Trong render ko set dc, componentdidupdate base on condional

### dùng đc component mà ko extends ko
+ React Component thiên về tính đa hình hơn là kế thừa

### Props vs state:
+ Cùng là object
+ Props immutable, state mutable
+ Props đc truyền từ thằng cha xuống, state đc khởi tạo trong component

### Virtual DOM
+ Clone từ DOM thật
+ Sử dụng thuật toán diffing để so sánh vs DOM thật rồi update lên DOM thật, giảm reflow vs repaint -> performent tốt
+ What makes React’s virtual DOM so fast?
React doesn’t really do anything new. It’s just a strategic move. What it does is It stores a replica of real DOM in memory. When you modify the DOM, it first applies these changes to the in-memory DOM. Then, using it’s diffing algorithm, figures out what has really changed.
Finally, it batches the changes and call applies them on real-dom in one go. Thus, minimizing the re-flow and re-paint.

### window.reloaded vs dom.reloaded khác j nhau
+ window là gọi khi cả html,js đc load xong còn dom là khi mới chỉ có html chưa có j

## Hook:

### useMemo
+ Memorization function, return về 1 variable vs save nó vào trong memory, nếu có case gọi lại vs những lần content đưa vào để xử lý giống nhau thì ko xử lý mà trả về luôn kết quả
+ Kiểm soát = cách truyền depedencies vào để xác định 
+ useMemo(() => {}, [depedencies])

### useCallback
+ Giống useMemo nhưng return về function

### useEffect
+ Được gọi sau render, vì nó là kiểu viết thay cho componentDidMount vs componentDidUpdate bên class
+ Chỉ gọi 1 lần thì để depedencies rỗng
+ Kiểm soát để không bị Infinite loops, truyền variable vào depedencies
+ Bài toán detect resize browser:
useEffect(() => {
  window.addListener('resize', function xử lý);

  // remove listener when unmount
  return () => window.removeListener('resize')
});
+ Nếu truyền 1, 2 vào depedencies thì bị ảnh hưởng j, ko, vẫn chỉ gọi 1 lần nhưng bị thừa depedencies
+ Nếu ko có depedencies thì dễ bị infinite loop

## Redux:
+ Luồng chạy của redux: Thông qua action vào reducer (sẽ có middleware ở giữa) update lên store rồi gen lên view 
+ redux tuân theo function programing để tránh side effect (xử lý ở middleware)
+ Immutable: tránh tham chiếu khi sử dụng array vs object

## Saga:
+ Effect takeEvery vs takeLatest
+ Debounce vs code thực tế: dùng setTimeOut vs clearSetTimeOut
+ Bài toán thực tế vào ô search text

## Css:
+ display: none  vs visibility: hidden, 1 thằng mất hẳn còn 1 thằng thì còn lưu lại vị trí
+ Inline: Có set đc width vs height ko: Ko, tự co dãn theo content bên trong vs có thể nằm trên cùng 1 line
+ Block: ko nằm trên cùng 1 dòng, có set đc width height
+ Inline-block: kết hợp 2 thằng trên
+ Reset css vs nomalize css ( chưa rõ )
+ box-sizing: tính cả padding vs border vào width vs height
+ position absolute vs fixed: Fixed gắn cứng lên page dù có scroll, absolute cần có relative để căn chỉnh
+ flex, order, justify-content, align-items, align-content
+ animation, transittion,
+ các lib có sẵn lợi gì hơn khi viết css thuần

## Scss
+ styled component có lợi j hơn scss: truyền đc props để custom
+ prop của styled component lúc load lúc ko do j, đã gặp case này bao h chưa: do render quá nhanh hoặc bị render thừa quá nhiều, ko kịp load
+ function dùng trong scss: (chưa rõ)

## Eventloop
+ eventloop hoạt động như thế nào, để làm j
+ ví dụ bài toán:
const a = function() {
  console.log('a');
  setTimeOut(() => {
    console.log('b');
  });
  console.log('c');
}

a();

