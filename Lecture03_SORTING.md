### SORTING
-   <b>Sorting (Sắp xếp):</b> là quá trình bố trí lại các phần tử trong danh sách (mảng, ma trận,...) theo một thứ tự tăng dần hoặc giảm dần. <br/>
Có nhiều thuật toán sắp xếp. Mỗi thuật toán sẽ có thời gian thực hiện nhanh chậm khác nhau, không gian vùng nhớ dùng cho việc sắp xếp cũng khác nhau.
    -    C++: sort
    ```
    #include <algorithm>
    using namespace std;

    sort(iterator1, iterator2, option);
    ```
    Trong đó:
     <br/><b>iterator1:</b> Con trỏ vị trí bắt đầu sắp xếp.
     <br/><b>iterator2:</b> Con trỏ vị trí kết thúc sắp xếp.
     <br/><b>option:</b> Hàm định nghĩa cách thức so sánh giữa hai phần tử, dùng để xác định tiêu chuẩn sắp xếp.

    + Java: Arrays.sort hoặc Collections.sort
    ```
    import java.util.Collections;
    import java.util.Arrays;
    import java.util.Comparator;

    Arrays.sort[T[] a, int fromIndex, int toIndex, Comparator<? super T> c]

    Collections.sort(List<T> a, Comparator<? super T> c)
    ```
    Trong đó:
    <br/> - <b>a:</b> Mảng dữ liệu cần sắp xếp
    <br/> - <b>fromIndex, toIndex:</b> Sắp xếp dữ liệu thuộc đoạn [fromIndex, toIndex).
    <br/> - <b>c:</b> Hàm định nghĩa cách thức so sánh giữa hai phần tử, dùng để xác định tiêu chuẩn sắp xếp.
    + Python: list.sort hoặc sorted
    <br/>Sử dụng list.sort()   
    ```
    list.sort([cmp[, key[,reverse]]])
    ```
    Sử dụng sorted()
    ```
    sorted(iterable[, cmp[,key[,reverse]]])
    ```
    Trong đó: 
    <br/> - <b>list.sort():</b> Sắp xếp trên vùng nhớ của list, không trả về giá trị, chỉ có thể sắp xếp toàn bộ list, nên sử dụng khi muốn sắp xếp toàn bộ list.
    <br/> - <b>sorted():</b> Sắp xếp dữ liệu trong vùng iterable và trả về một list mới, có thể sắp xếp một sublist.