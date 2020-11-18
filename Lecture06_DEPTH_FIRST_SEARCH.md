### Depth-First Search
Depth-first search (Thuật toán tìm kiếm theo chiều sâu): là thuật toán tìm kiếm đường đi trên đồ thị <b>vô hướng</b> hoặc <b> có hướng</b>, <b>không trọng số</b>.<br/>
Thuật toán DFS luôn tìm kiếm được đường đi từ một đỉnh bất kì cho trước tới các đỉnh khác (nếu các đỉnh thuộc cùng thành phần liên thông với nhau). Nhưng không chắc chắn đường đi tìm được sẽ là đường đi ngắn nhất.</br>
<b>Độ phức tạp: O(V+E)</b>
-   V (Vertices): Số lượng đỉnh của đồ thị.
-   E (Edges): Số lượng cạnh của đồ thị.

<b>Ý tưởng thuật toán:</b>
Xuất phát từ 1 đỉnh bất kỳ, đi tới tất cả các đỉnh kề của đỉnh này và lưu các đỉnh kề này lại.
[Wiki DFS](https://vi.wikipedia.org/wiki/T%C3%ACm_ki%E1%BA%BFm_theo_chi%E1%BB%81u_s%C3%A2u)

### Example: Bishu and his Girlfriend

There are N countries 1,2,3,4....N and N−1 roads(i.e depicting a tree)

Bishu lives in the Country 1 so this can be considered as the root of the tree.

Now there are Q girls who lives in various countries (not equal to 1) .

All of them want to propose Bishu. But Bishu has some condition.

He will accept the proposal of the girl who lives at minimum distance from his country.

Now the distance between two countries is the number of roads between them.

If two or more girls are at the same minimum distance then he will accept the proposal of the girl who lives in a country with minimum id.

No two girls are at same country.

<b>Dữ liệu nhập</b> <br/>
First line consists of N, i.e number of countries.

Next N-1 lines follow the type u v which denotes there is a road between u and v.

Next line consists of an integer Q

Next Q lines consists of an integer x where the girls live.

Contraints: <br/>
2 ≤ N ≤ 1000 <br/>
1 ≤ u,v ≤ N <br/>
1 ≤ Q ≤ (N−1) <br/>

<b>Dữ liệu xuất</b> <br/>
Print the idid of the country of the girl who will be accepted.

<b>Ví dụ:</b>
<br/>input
```
6
1 2
1 3
1 4
2 5
2 6
4
5
6
3
4
```
<br/> output
```
3
```
### Hướng dẫn
Chạy thuật toán DFS, sau đó lấy lần lượt từng vùng đất của các cô gái rồi tìm đường đi tới vùng đất số 1. Lấy vùng đất có lượng đường đi qua các đỉnh là ít nhất. Để chọn ID nhỏ thì chỉ khi vùng đất nào thật sự lớn hơn vùng đất hiện tại bạn mới cập nhật lại. Nếu bằng thì cũng không cập nhật.

Bạn cũng có thể cải tiến một chút bằng cách chạy thuật toán từ vùng đất số 1 mà Bishu đang đứng để lấy kết quả đường đi đến các vùng đất mà các cô gái đang đứng. Cách này sẽ đỡ phải mất thời gian chạy đi chạy lại DFS nhiều lần.

<b>Độ phức tạp: O(V + E + Q) </b>với <br/>V là số lượng đỉnh của cây<br/> E = V - 1 là số lượng cạnh của cây <br/> Q là số lượng vùng đất cô gái đang ở.

```
import java.util.*;

public class Main {
    static final int MAX = 1000 + 5;
    static int V, E;
    static boolean[] visited = new boolean[MAX];
    static int[] dist = new int[MAX];
    static ArrayList<Integer> graph[] = new ArrayList[MAX];

    public static void DFS(int scr) {
        Stack<Integer> s = new Stack<>();
        visited[scr] = true;
        s.add(scr);

        while (!s.isEmpty()) {
            int u = s.pop();

            for (int v : graph[u]) {
                if (!visited[v]) {
                    visited[v] = true;
                    dist[v] = dist[u] + 1;
                    s.add(v);
                }
            }
        }
    }

    public static void main(String[] agrs) {
        Scanner sc = new Scanner(System.in);;
        V = sc.nextInt();
        E = V - 1;

        for (int i = 0; i < MAX; i++) {
            graph[i] = new ArrayList<>();
        }

        for (int i = 0; i < E; i++) {
            int u = sc.nextInt();
            int v = sc.nextInt();
            graph[u].add(v);
            graph[v].add(u);
        }

        DFS(1);
        int ans = 0;
        int min_dist = MAX;
        int Q = sc.nextInt();

        for (int i = 0; i < Q; i++) {
            int u = sc.nextInt();

            if (dist[u] < min_dist || (dist[u] == min_dist && u < ans)) {
                min_dist = dist[u];
                ans = u;
            }
        }

        System.out.print(ans);
    }
}
```

