# tropology-dfs
package Labtask_1;
import java.util.*;
public class DFS_arylist {
 static Scanner sc = new Scanner(System.in);
 static ArrayList<Integer> temp= new ArrayList<Integer>();
 static ArrayList<Integer> Color= new ArrayList<Integer>();
 static ArrayList<Integer> Prev= new ArrayList<Integer>();
 static ArrayList<Integer> F= new ArrayList<Integer>();
 static ArrayList<Integer> D= new ArrayList<Integer>();
 static ArrayList<Character> TopologicalOrder= new ArrayList<Character>();
 static ArrayList<Character> Nodes= new ArrayList<Character>();
 static ArrayList<ArrayList<Integer>> List= new ArrayList();
 static int time = 0;
 static int nd;
 static int row = 0;
 static char c;
 private static void initialize()
 {
 System.out.println("Enter the number of nodes: ");
 nd = sc.nextInt();
 System.out.println("Enter the node characters:");
 for(int i=0; i<nd; i++)
 {
 List.add(new ArrayList<>());
 c = sc.next().charAt(0);
 Nodes.add(c);
 Color.add(0);
 Prev.add(-1);
 D.add(99999);
 F.add(99999);
 }
 adj_matrix();
 }
 private static void adj_matrix()
 {
 for (int i =0; i<nd; i++)
 {
 System.out.println("Enter the number of child for node 
"+Nodes.get(i)+":");
 int child = sc.nextInt();
 assign(child);
 }
 }
 private static void assign(int lp)
 {
 if (lp<=0)
 {
 List.get(row).add(0);
 row++;
 }
 else
 {
 System.out.println("Enter the values for child: ");
 for(int i=1; i<=lp; i++)
 {
 temp.add(sc.nextInt());
 }
 inst_list(lp);
 }
 }
 private static void inst_list(int num)
 {
 for(int i=0; i<num; i++)
 {
 List.get(row).add(temp.get(i));
 }
 temp.clear();
 row++;
 }
 private static void Run_DFS(int u)
 {
 System.out.print(Nodes.get(u)+" ");
 Color.set(u, 1);
 time++;
 D.set(u, time);
 for(int i=0; i<List.get(u).size(); i++)
 {
 int V = List.get(u).get(i);
 if(Color.get(V)==0)
 {
 Prev.set(V, u);
 Run_DFS(V);
 }
 }
 Color.set(u, 2);
 time++;
 F.set(u, time);
 TopologicalOrder.add(Nodes.get(u));
 }
 private static void tpg_ord()
 {
 for(int i=0; i<TopologicalOrder.size(); i++){
 System.out.print(TopologicalOrder.get(i)+" ");
 }
 }
 public static void main(String[] args) {
 initialize();
 for(int i=0; i<nd; i++)
 {
 if(Color.get(i)==0){
 Run_DFS(i);
 System.out.println("\nTopological Order: ");
 tpg_ord();
 }
 }
 }
}
