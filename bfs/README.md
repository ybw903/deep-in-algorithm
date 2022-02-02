## BFS

BFS는 인근에 위치한 노드를 모두 탐색한 이후, 다음 노드로 이동, 탐색을 반복하는 알고리즘입니다.

[BOJ2178 미로탐색](https://www.acmicpc.net/problem/2178)

```java
import java.io.*;
import java.util.*;

public class Main {
  static int n;
  static int m;
  static int[][] map;
  static boolean[][] visited;
  static int[] dy = { -1, 1, 0, 0 };
  static int[] dx = { 0, 0, -1, 1 };

  public static void main(String args[]) throws IOException {
    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    StringTokenizer st = new StringTokenizer(br.readLine());
    n = Integer.parseInt(st.nextToken());
    m = Integer.parseInt(st.nextToken());

    map = new int[n][m];
    for (int i = 0; i < n; i++) {
      String s = br.readLine();
      for (int j = 0; j < m; j++) {
        map[i][j] = s.charAt(j) - '0';
      }
    }
    visited = new boolean[n][m];
    visited[0][0] = true;
    bfs(0, 0);
    System.out.println(map[n - 1][m - 1]);
  }

  public static void bfs(int y, int x) {
    Queue<int[]> q = new LinkedList<>();
    q.add(new int[] { y, x });

    while (!q.isEmpty()) {
      int cur[] = q.poll();
      for (int i = 0; i < 4; i++) {
        int nextY = cur[0] + dy[i];
        int nextX = cur[1] + dx[i];
        if (isOutborder(nextY, nextX)) continue;

        q.add(new int[] { nextY, nextX });
        map[nextY][nextX] = map[cur[0]][cur[1]] + 1;
        visited[nextY][nextX] = true;
      }
    }
  }

  private boolean isOutBorder(int ny, int nx) {
    return (
      ny < 0 ||
      nx < 0 ||
      ny >= n ||
      nx >= m ||
      visited[ny][nx] ||
      map[ny][nx] == 0
    );
  }
}
```
