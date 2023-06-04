import java.util.*;
import java.io.*;
class Main{
	public static void main(String[] args) {
		File inputFile = new File("9.in"); //Onde colocar o arquivo
		Graph graph = new Graph(inputFile);
		Mst agm = new Mst(graph);
		} 
		
	
}
class Graph{
	int n = 0;
	//ArrayList<ArrayList<Aresta>> nodes = new ArrayList<ArrayList<Aresta>>();
	HashMap<String,Double> Nh = new HashMap<String,Double>();
	int nEdges=0;
	ArrayList<String> keys = new ArrayList<String>();
	ArrayList<Double> weights = new ArrayList<Double>();
	ArrayList<Integer> status = new ArrayList<Integer>();//-1 = Nao atingido / 0 No caminho / 1 finalizado
	Graph(File inputFile){
		try{

			BufferedReader fr = new BufferedReader(new FileReader(inputFile));
			String ln;
			String[] aux1;
			ln=fr.readLine();
			ln=fr.readLine();
			ln = (String)fr.readLine();
			aux1 = ln.split("=");
			putN(Integer.valueOf(aux1[1]));
			ln=fr.readLine();
			/*for (int i=0;i<=n;i++){
				nodes.add(new ArrayList<>());
			}*/
			while((ln=fr.readLine())!=null){
				insertnode(ln);
			}
		}catch(Exception e){
			e.printStackTrace();
		}

	}
	void putN(int x){
		this.n = x;
	}
	void insertnode(String ln){ 
		String[] node;
		node = ln.split(" ");
		int x = Integer.valueOf(node[0]);
		int y = Integer.valueOf(node[1]);
		double weight = Double.valueOf(node[2]);
		String key = node[0]+";"+node[1];
		Nh.put(key,weight);
		keys.add(key);
		weights.add(weight);
		nEdges++;
	}

}
class Mst {
	int n=0;
	ArrayList<String> A = new ArrayList<String>(); // Arestas de AGM
	ArrayList<String> L= new ArrayList<String>();
	ArrayList<Double> Lw= new ArrayList<Double>(); //Arestas L
	HashMap<String,Double> XywL = new HashMap<String,Double>();
	 //Map com as arestas de L
	int nEdges=0;
	double AGMcost = 0;
	CompConexa[] cmp;
	Mst(Graph g){
		this.n += g.n;
		this.nEdges += g.nEdges;
		fazO_L(g);
		doMST();
		calculateMSTcost(g);
	}
	void fazO_L(Graph g){

		for (int i=0;i<nEdges;i++){
			Double w = Collections.min(g.weights);
			int indexOFW = g.weights.indexOf(w);
			String auxKey = g.keys.get(indexOFW);
			L.add(auxKey);
			Lw.add(w);
			g.keys.remove(indexOFW);
			g.weights.remove(indexOFW);
			XywL.put(auxKey,w);
		}
}
	
	void doMST(){
		CompConexa[] cmp = new CompConexa[n+1];
		for (int k=0;k<=n;k++){
			cmp[k]= new CompConexa(k,0);
		}
		try{
			int z=0;
			int nAEdges = 0;
			while (nAEdges<n-1){
				String[] aux = ((String)L.get(z)).split(";");
				int x = findRt(cmp,Integer.valueOf(aux[0]));
				int y = findRt(cmp,Integer.valueOf(aux[1]));
				if (x!=y){
					String nodeA = aux[0]+";"+aux[1];
					A.add(nodeA);
					union(cmp,x,y);
					nAEdges++;
				}
				z++;
			}
		}catch(Exception e ){
			e.printStackTrace();
		}
	}
	int findRt(CompConexa[] cmp,int i){
		if (cmp[i].rep==i){
			return cmp[i].rep;
		}
		cmp[i].rep=findRt(cmp,cmp[i].rep);
		return cmp[i].rep;

	}
	void union(CompConexa[] cmp,int x,int y){
		int RX = findRt(cmp,x);
		int RY = findRt(cmp,y);
		if (cmp[RY].comp < cmp[RX].comp) {
            cmp[RY].rep = RX;
        }
        else if (cmp[RY].comp > cmp[RX].comp) {
            cmp[RX].rep = RY;
        }
        else {
            cmp[RY].rep = RX;
            cmp[RX].comp++;
        }
	}
	Double calculateMSTcost(Graph g){
		double cMST = 0;
		for (int x=0;x<(A.size());x++){
			String ln = (String)A.get(x);
			cMST += (Double)XywL.get(ln);
		}
		System.out.println(cMST);
		return cMST;
	} 
}
class CompConexa{
	int rep,comp;
	CompConexa(int x,int y){
		this.rep = x;
		this.comp = y;
	}
}
class Aresta{
	int x,y;
	double w;
	Aresta(int x,int y,double w){
		this.x = x;
		this.y = y;
		this.w = w;
	}
}
