## Thuật toán Bellman-Ford

Thuật toán Bellman-Ford là thuật toán tìm đường đi có chi phí nhỏ nhất từ một đỉnh đến tất cả các đỉnh còn lại trong đồ thị có hướng hoặc vô hướng, có trọng số (trọng số có thể dương hoặc âm).

## Độ phức tạp: <b>O ( E. V )</b>
- E (Edges) là số lượng cạnh của đồ thị.
- V (Vertices) là số lượng đỉnh của đồ thị.

## Ý tưởng thuật toán

Xuất phát từ một đỉnh bất kỳ. Duyệt qua toàn bộ <b>cạnh đồ thị</b>.</br>
=> So sánh chi phí đường đi hiện tại với đường đi trong bảng chi phí (nếu nhỏ hơn thì cập nhật). </br>
=> Quay lại tiếp tục duyệt lại toàn bộ cạnh đồ thị. Duyệt qua <b>V - 1</b> lần thì dừng. Xuất kết quả bài toán.

** Có thể tiếp tục duyệt thêm lần nữa để kiểm tra chu trình âm. **

[wiki belman-ford](https://en.wikipedia.org/wiki/Bellman%E2%80%93Ford_algorithm)

## Example Extended traffic

Dhaka city is getting crowded and noisy day by day. Certain roads always remain blocked in congestion. In order to convince people avoid shortest routes, and hence the crowded roads, to reach destination, the city authority has made a new plan. Each junction of the city is marked with a positive integer (≤20) denoting the busyness of the junction. Whenever someone goes from one junction (the source junction) to another (the destination junction), the city authority gets the amount (busyness of destination - busyness of source)^3
​​  (that means the cube of the difference) from the traveler. The authority has appointed you to find out the minimum total amount that can be earned when someone intelligent goes from a certain junction (the zero point) to several others.

### Dữ liệu nhập
Input starts with an integer T( ≤ 50 ), denoting the number of test cases.

Each case contains a blank line and an integer n (1 < n ≤ 200) denoting the number of junctions. The next line contains nn integers denoting the busyness of the junctions from 1 to n respectively. The next line contains an integer m, the number of roads in the city. Each of the next m lines (one for each road) contains two junction-numbers (source, destination) that the corresponding road connects (all roads are unidirectional). The next line contains the integer q, the number of queries. The next q lines each contain a destination junction-number. There can be at most one direct road from a junction to another junction.

### Dữ liệu xuất
For each case, print the case number in a single line. Then print q lines, one for each query, each containing the minimum total earning when one travels from junction 1 (the zero point) to the given junction. However, for the queries that gives total earning less than 3, or if the destination is not reachable from the zero point, then print a ?

### Ví dụ

input
```
2

5
6 7 8 9 10
6
1 2
2 3
3 4
1 5
5 4
4 5
2
4
5

2
10 10
1
1 2
1
2
```

out put
```
Case 1:
3
4
Case 2:
?
```
### Tóm tắt đề : 
Cho bạn danh sách các điểm giao thông và trọng số tại mỗi điểm này. Tiếp theo cho bạn m tuyến đường khác nhau. Mỗi tuyến đường có trọng số bằng (trọng số điểm đích – trọng số điểm nguồn)3 (lũy thừa 3). Nhiệm vụ của bạn là tìm đường đi ngắn nhất từ điểm giao thông 1 đến q điểm được chỉ định.

Input : Dòng đầu tiên chứa số T (T ≤ 50) – số lượng bộ test. Mỗi bộ test có định dạng như sau:

- Dòng đầu chứa số n (1 < n ≤ 200) – số lượng điểm giao thông.
- Dòng tiếp theo chứa n số nguyên dương ≤ 20, với số thứ i đại diện cho tình trạng giao thông tại điểm giao thông thứ i (1 ≤ i≤ n). Số càng lớn chứng tỏ giao thông ở đó càng đông đúc.
- Dòng tiếp theo chứa số nguyên m – số lượng đường đi hai chiều.
- m dòng tiếp theo, mỗi dòng chứa 2 số tương ứng với đường đi từ (điểm nguồn – điểm đích). Có tối đa một đường đi nối giữa trực tiếp giữa hai điểm.
- Dòng tiếp theo chứa số q là số lượng truy vấn
- q dòng tiếp theo, mỗi dòng chứa 1 số là điểm giao thông mà bạn cần tìm đường đi ngắn nhất từ điểm giao thông thứ 1 đến điểm đó.

Output : Với mỗi truy vấn, in ra độ dài đường đi ngắn nhất từ đỉnh 1 đến đỉnh đó. Nếu không có đường đi hoặc chi phí của đường đi tìm được nhỏ hơn 3 thì bạn in ra “?”.


### Giải thích ví dụ

Lưu ý: Trọng số một cạnh được tính bằng (trọng số điểm đích – trọng số điểm nguồn) ^ 3

​​ . Do đó tùy thuộc vào thứ tự đề cho điểm nguồn và điểm đích mà trọng số của một cạnh có thể dương hoặc âm. Do đó tuy đề có đề cập chỉ có tối đa một đường đi nối trực tiếp giữa 2 điểm, đường đi đó có thể có tới 2 trọng số (một cách trực quan bạn có thể tưởng tượng mỗi trọng số đại diện cho một chiều của tuyến đường).

### Độ phức tạp: O (T * V * E)
với V là số đỉnh (số điểm giao thông), E là số đường đi, T là số bộ test.

```
import java.util.*;
import java.io.*;
 
public class Main {
    static final int MAX_V = 205;
    static final int MAX_E = 205 * 204;
    static class Edge {
        int source, target, weight;
 
        public Edge(int _source, int _target, int _weight) {
            this.source = _source;
            this.target = _target;
            this.weight = _weight;
        }
    }
 
    static int n, m;
    static int[] weight = new int[MAX_V];
    static int[] dist = new int[MAX_V];
    static Edge[] graph = new Edge[MAX_E];
 
    public static void BellmanFord(int s) {
        Arrays.fill(dist, Integer.MAX_VALUE);
        dist[s] = 0;
 
        for (int i = 0; i < n - 1; i++) {
            for (int j = 0; j < m; j++) {
                int u = graph[j].source;
                int v = graph[j].target;
                int w = graph[j].weight;
 
                if (dist[u] != Integer.MAX_VALUE) {
                    dist[v] = Math.min(dist[v], dist[u] + w);
                }
            }
        }
    }
 
    public static void main(String[] agrs) {
        Scanner in = new Scanner(System.in);
        int T = in.nextInt();
 
        for (int t = 1; t <= T; t++) {
            n = in.nextInt();
            for (int i = 1; i <= n; i++) {
                weight[i] = in.nextInt();
            }
 
            m = in.nextInt();
            for (int i = 0; i < m; i++) {
                int u = in.nextInt();
                int v = in.nextInt();
                graph[i] = new Edge(u, v, (int)Math.pow(weight[v] - weight[u], 3));
            }
 
            BellmanFord(1);
            System.out.println("Case " + t + ":");
            int q = in.nextInt();
 
            for (int i = 0; i < q; i++) {
                int f = in.nextInt();
                System.out.println(dist[f] != Integer.MAX_VALUE && dist[f] >= 3 ? dist[f] : "?");
            }
        }
    }
}
```