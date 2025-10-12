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

## Các syntax, method đặc biệt khi làm GUI

```javascript
-MessageBox.Show("Nhận vào question", "Label", "Nút chọn", "Ảnh Box");
VD: MessageBox.Show(
  "Are you quit?",
  "Confirm",
  MessageBoxButton.YesNo,
  MessageBoxImage.Question
);
```

- Cách css trong WPF
  - App.xaml.cs là nơi để ta khai báo các css để apply cho hoàn loạt các TextBox, Button, ... và các thành phần dùng style nó sẽ tự động cập theo
  - CSS: Casscade Style Sheet: đổ domino hàng loạt
- Customize css trong app bằng cách thêm key, dùng `staticResourse Key` để sử dụng trong thẻ Button.

```javascript
<Button
  Content="Button"
  HorizontalAlignment="Left"
  Margin="163,52,0,0"
  VerticalAlignment="Top"
  Style="{StaticResource BlueButton}" // khi chúng ta mún tự customize Button
  Width="100"
  Height="55"
/>
```

```javascript
<DataGrid x:Name="StudentListDataGrid" Margin="107,198,107,164"
          SelectionChanged="StudentListDataGrid_SelectionChanged" AutoGenerateColumns="False">

    <DataGrid.Columns>
        <DataGridTextColumn Header="Mã SV" Width="70" Binding="{Binding Id}"  />
        <DataGridTextColumn Header="Tên SV" Width="120" Binding="{Binding Name}"  />
        <DataGridTextColumn Header="Năm Sinh" Width="70" Binding="{Binding Yob}"  />
        <DataGridTextColumn Header="Điểm TB" Width="70" Binding="{Binding Gpa}"  />
    </DataGrid.Columns>

</DataGrid>


- sử dụng thẻ <DataGridTextColumn Header ="name" Binding="{Binding Id}">

** Cách tạo ra các cột theo mong muốn:
- B1: Trong thẻ cha của <DataGrid></DataGrid> phải có thuộc tính `AutoGenerateColumns="False": để có thể customize column`, thêm thẻ <DataGrid.Columns></DataGrid.Columns>
- `AutoGenerateColumns=true`: tự lo tên cột cho DataGrid thay vì chỉ tự generate ra tên cột
- B2: có bao nhiu cột thì thêm bấy nhiu thẻ <DataGridTextColumn /> và gồm các thuộc tính như `Header: tên cột` và `Binding: field of column`
```

- thêm chức năng `delete student` bằng cách chọn vào student mún xóa sau đó hiển thị MessaageBox
