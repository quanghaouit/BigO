## Thuật toán Dijkstra

Dijkstras Algorithm (thuật toán Dijkstra): là thuật toán tìm đường đi có chi phí nhỏ nhất từ một đỉnh đến tất cả các đỉnh còn lại trong đồ thị có trọng số (trọng số không âm).

## Độ phức tạp thuật toán Dijkstra
Thuật toán Dijkstra bình thường sẽ có độ phức tạp là O(V^2). Tuy nhiên ta có thể sử dụng kết hợp các cấu trúc dữ liệu khác để giảm độ phức tạp:
-   Dùng Heap (priority queue) có độ phức tạp: O(ElogV).
-   Dùng kết hợp với cấu trúc dữ liệu cây nhị phân tìm kiếm độ phức tạp là: O(ElogV).

## Ý tưởng của thuật toán
Xuất phát từ một đỉnh bất kỳ. Đi đến các đỉnh kề của đỉnh này.
Ta khởi tạo một mảng lưu chi phí đường đi đến các đỉnh kề với giá trị là vô cực. Và một mảng path lưu vết đường đi khởi tạo bằng -1.
So sánh tổng chi phí đường đi đến đỉnh kề đang xét với chi phí đường đi hiện tại. Nếu nhỏ hơn ta thêm vào kho (heap hoặc cây nhị phân).
Thực hiện lưu vết và đem đỉnh mới ra xét.
[Wiki Dijkstra](https://vi.wikipedia.org/wiki/Thu%E1%BA%ADt_to%C3%A1n_Dijkstra)

## Example: Travelling Cost

The government of Spoj_land has selected number of locations in the city for road construction and numbered those locations as 0, 1, 2, 3, ..., 500.

Now, they want to construct roads between various pairs of location (say A and B) and have fixed the cost for travelling between those pair of locations from either end as W unit.

Now, Rohit being a curious boy wants to find the minimum cost for travelling from location U (source) to Q number of other locations (destination).

### Dữ liệu nhập

First line contains N, the number of roads that government constructed.

Next N line contains three integers A, B and W. A and B represent the locations between which the road was constructed and W is the fixed cost for travelling from A to B or from B to A.

Next line contains an integer U from where Rohit wants to travel to other locations.

Next line contains Q, the number of queries (finding cost) that he wants to perform.

Next Q lines contain an integer V (destination) for which minimum cost is to be found from U.

Constraints
<br/> 1 ≤ N ≤ 500
<br/> 0 ≤ A,B ≤ 500
<br/> 1 ≤ W ≤ 100
<br/> 0 ≤ U, V ≤ 500
<br/> 1 ≤ Q ≤ 500

### Dữ liệu xuất
Print the required answer in each line.

If he can't travel from location U to V by any means then, print 'NO PATH' without quotes.

### Ví dụ
input
```
7
0 1 4
0 3 8
1 4 1
1 2 2
4 2 3
2 5 3
3 4 2
0
4
1
4
5
7
```

output
```
4
5
9
NO PATH
```
### Giải thích ví dụ
Query #1 <br/>
0->1: cost = 4

Query #2 <br/>
0->4 = 0->1->4 cost = 4 + 1 = 5

Query #3 <br/>
0->5 = 0->1->2->5 cost = 4 + 2 + 3 = 9

Query #4 <br/>
0->7 . No path exists between 0 and 7

### Hướng dẫn giải
Đề cho biết các địa điểm được đánh số từ 0 đến 500 và danh sách các đường đi, vậy ta có thể thấy đây là một đồ thị có 501 đỉnh và các con đường sẽ là các cạnh của đồ thị.

Từ danh sách cạnh, tạo đồ thị, sau đó chạy Dijkstra từ đỉnh U. Sau khi chạy xong dựa vào mảng chi phí distdist để tìm chi phí đến các đỉnh cần tìm. Nếu đỉnh nào chi phí là vô cực (INF) thì sẽ không có đường đi đến đó.

### Độ phức tạp: 
O(E∗log(V)) với E là số lượng cạnh (cung), V là số lượng đỉnh trong đồ thị.

```
import java.util.*;
 
public class Main {
    static final int MAX = 505;
    static final int INF = Interger.MAX_VALUE;
    static final int[] dist = new int[MAX];
 
    static class Node implements Comparable<Node> {
        int id, weight;
 
        public Node(int _id, int _weight) {
            this.id = _id;
            this.weight = _weight;
        }
 
        @Override
        public int compareTo(Node other) {
            return this.weight - other.weight;
        }
    }
 
    static ArrayList<Node> graph[] = new ArrayList[MAX];
 
    public static void Dijsktra(int s) {
        PriorityQueue<Node> pq = new PriorityQueue<>();
        pq.add(new Node(s, 0));
        dist[s] = 0;
 
        while (!pq.isEmpty()) {
            Node top = pq.poll();
            int u = top.id;
            int w = top.weight;
 
            for (Node neighbor : graph[u]) {
                if (w + neighbor.weight < dist[neighbor.id]) {
                    dist[neighbor.id] = w + neighbor.weight;
                    pq.add(new Node(neighbor.id, dist[neighbor.id]));
                }
            }
        }
    }
 
    public static void main(String[] agrs) {
        Scanner sc = new Scanner(System.in);
        int N = sc.nextInt();
 
        for (int i = 0; i < MAX; i++) {
            dist[i] = INF;
            graph[i] = new ArrayList<Node>();
        }
 
        for (int i = 0; i < N; i++) {
            int A = sc.nextInt();
            int B = sc.nextInt();
            int W = sc.nextInt();
            graph[A].add(new Node(B, W));
            graph[B].add(new Node(A, W));
        }
 
        int S = sc.nextInt();
        Dijsktra(S);
        int Q = sc.nextInt();
         
        for (int i = 0; i < Q; i++) {
            int V = sc.nextInt();
            System.out.println(dist[V] != INF ? dist[V] : "NO PATH");
        }
    }
}
```