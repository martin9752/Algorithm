package closest_pair;

import java.util.ArrayList;
import java.util.Arrays;
import java.util.Comparator;
import java.util.Scanner;


public class closest_pair {

	public static void main(String[] args) {
		@SuppressWarnings("resource")
		Scanner cin = new Scanner(System.in);
		int point_num = cin.nextInt();
	    point[] points = new point[point_num];
		for (int i = 0; i < point_num; i++) {
			points[i] = new point();
			points[i].x = cin.nextInt();
			points[i].y = cin.nextInt();
		}
		System.out.println(Closest_Pair(points));
	}

	public static int Closest_Pair(point[] points) {
		point[] pointx = points.clone();
		Arrays.sort(pointx, compare_x);
		point[] result = Closest_Pair_Rec(pointx);
		return distance(result);
	}

	public static point[] Closest_Pair_Rec(point[] pointx) {
		
		//if|P|<=3，直接计算最小距离的点对
		if (pointx.length <= 3) {
			int mindistance_three = Integer.MAX_VALUE;
			int points_i = 0;
			int points_j = 0;
			for (int i = 0; i < pointx.length; i++) {
				for(int j = i + 1;j<pointx.length;j++){
					if(mindistance_three > distance(new point[]{pointx[i], pointx[j]})){
						mindistance_three = distance(new point[]{pointx[i], pointx[j]});
						points_i = i;
						points_j = j;
					}
				}
			}
			point[] p = new point[]{pointx[points_i],pointx[points_j]};
			return p;
		}
		
		//构造Qx，Qy，Rx，Ry
		point[] Q = Arrays.copyOfRange(pointx, 0, pointx.length/2);
		point[] R = Arrays.copyOfRange(pointx, pointx.length/2, pointx.length);
        
		point[] Qx = Q.clone();
		Arrays.sort(Qx, compare_x);
		
		point[] Rx = R.clone();
		Arrays.sort(Rx, compare_x);
		
		//进行递归分别得到Q和R最小距离点对
		point[] Q_result = Closest_Pair_Rec(Qx);
		point[] R_result = Closest_Pair_Rec(Rx);
		
		//Q和R点对之间的小值
		int mindistance = Math.min(distance(Q_result), distance(R_result));
		point min_i = null;
		point min_j = null;
		
		//假如中间区域不存在比QR最小距离更小的值，则返回点集便是QR中距离更小的点集
		if(mindistance == distance(Q_result)){
			min_i = Q_result[0];
			min_j = Q_result[1];
		}
		if(mindistance == distance(R_result)){
			min_i = R_result[0];
			min_j = R_result[1];
		}
		
		//Q中点的最大x坐标
		int Q_max_x = Q[Q.length-1].x;
		
		//构造与线x=Q_max_x距离小于mindistance的点集S
		ArrayList<point> List_S = new ArrayList<point>();
		for(int i=0;i<pointx.length;i++){
			if(Math.abs(pointx[i].x-Q_max_x)<mindistance){
				List_S.add(pointx[i]);
			}
		}
		
		//把list转换为数组
		point[] S = (point[])List_S.toArray(new point[List_S.size()]);
		//point[] S = List_S.toArray(new point[0]);
		
		//对S进行y的排序
		point[] Sy = S.clone();
		Arrays.sort(Sy,compare_y);
		
		//找15个点之内的点，并比较距离,找出最小距离的的点 
		int mindistance_mid = Integer.MAX_VALUE;
		point min_mid_i = null;
		point min_mid_j = null;
//		for(int i=0;i<Sy.length;i++){
//			for(int j=i+1;j<i+15;j++){
//				if(mindistance_mid>distance(new point[]{Sy[i],Sy[j]})){
//					mindistance_mid = distance(new point[]{Sy[i],Sy[j]});
//					min_mid_i = Sy[i];
//					min_mid_j = Sy[j];
//				}
//			}
//		}
		for(int i=0;i<Sy.length;i++){  
            point basep = Sy[i];  
            for(int j=i+1;j<Sy.length;j++){  
                point compp = Sy[j];  
                if((compp.y-basep.y < 2*mindistance)&&Math.abs(compp.x-basep.x)<2*mindistance){  
                    if(mindistance_mid>distance(new point[]{basep,compp})){  
                    	mindistance_mid = distance(new point[]{basep,compp});  
                        min_mid_i = compp;  
                        min_mid_j = basep;  
                    }  
                }  
            }  
        } 
		
		//判断QR中的最小距离和中间区域的最小距离哪个更小并返回
		if(mindistance_mid<mindistance){
			return new point[]{min_mid_i,min_mid_j};
		}else{
			return new point[]{min_i,min_j};
		}
	}

	public static int distance(point[] points) {
		int distance = (points[0].x - points[1].x) * (points[0].x - points[1].x)
				+ (points[0].y - points[1].y) * (points[0].y - points[1].y);
		return distance;
	}

	public static Comparator<point> compare_x = new Comparator<point>() {
		@Override
		public int compare(point o1, point o2) {
			if (o1.x < o2.x) {
				return -1;
			} else if (o1.x > o2.x) {
				return 1;
			}
			return 0;
		}
	};

	public static Comparator<point> compare_y = new Comparator<point>() {
		@Override
		public int compare(point o1, point o2) {
			if (o1.y < o2.y) {
				return -1;
			} else if (o1.y > o2.y) {
				return 1;
			}
			return 0;
		}
	};
}

class point {
	int x;
	int y;
}
