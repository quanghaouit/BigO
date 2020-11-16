### STACK (ngăn xếp)
-   Stack là dãy phần tử hoạt động theo cơ chế LILO (Last In First Out) vào sau ra trước, có thể hình dung stack giống như ngăn tủ xếp đồ trong thực tế.

```
import java.util.Stack;

Stack<Integer> s = new Stack<Integer>();
// add giá trị vào stack
s.push(5);
s.push(7);

// lấy giá trị và xoá phần tử ở trên cùng khỏi stack
int value = s.pop(); //7

// Lấy giá trị phần tử ở trên cùng stack. Không xoá
int see = s.peek();//5

```

### QUEUE (hàng đợi)
-   Queue (hàng đợi): là dãy phần tử hoạt động theo cơ chế FIFO (First In First Out) vào trước ra trước, có thể hình dung queue giống như hàng đợi xếp hàng mua vé trong thực tế.

```
import java.util.LinkedList;
import java.util.Queue;

Queue<E> q = new LinkedList<E>();

// thêm giá trị vào queue
q.add(5);
q.add(7);

// Lấy giá trị và xoá phần tử đầu tiên của queue.
E value = q.remove(); // 5

// Lấy giá trij phần tử đầu tiên của queue. Không xoá
E value = q.peek(); // 7
```