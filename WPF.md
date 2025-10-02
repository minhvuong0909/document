# Giải ngố WPF - làm app GUI trên desktop - chỉ chạy trên windows, dùng desktop runtime

- 1 màn hình đc gọi là 1 window và 1 app đc có nhiều màn hình
- các màn hình này (kèm code phía sau) tụ họp lại trong 1 project thuộc nhóm `/STYLE WPF PROJECT -> App GUI`

- 1 màn hình - 1 window - xem tương đương như 1 trang web

```javascript
<window>    Class Window        <HTML>              Cây DOM
    <Grid>  Class Button             <Body>
        ô nhập, nút nhấn                ô nhập input
    </Grid>                         </Body>
</window>                       </HTML>
```

bên lập trình FE, Javascript, có nghe DOM - Document Object Model

- mỗi object khi tải về trình duyệt đc xem là object bự trong ram
- object bụ html chứa bên trong object nhỏ hơn: Head, Body
- body chứa object nhỏ hơn, div, h1, input, br, ...
