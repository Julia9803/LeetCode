### Drw0 Count One For 11 Pow N

![img](https://oss.1point3acres.cn/forum/201909/13/151808ej8une65i5xe996f.png)

Rule: 

11

121
1331
14641
161051
1771561
19487171
214358881
2357947691

Number for each index is the above array t[i-1] + t[i], except for last index, which is always 1. Do remember to keep a carry bit as the sum of two numbers may be larger than 10.

```java
public class Main {
    // 数11的n次方里有多少个1
    public static void main(String[] args) {
	// write your code here
        int num = 9;
        System.out.println(countOne(num));
    }
    public static int countOne(int num) {
        String[] target = new String[num+1];
        target[1] = "11";
        for(int i = 2;i <= num;i++) {
            char[] t = target[i-1].toCharArray();
            char[] tmp = new char[i+1];
            tmp[i] = '1';
            int carry = 0;
            for(int j = i - 1;j >= 1;j--) {
                int sum = t[j-1] - '0' + t[j] - '0' + carry;
                carry = sum/10;
                tmp[j] = (char) (sum%10 + '0');
            }
            tmp[0] = (char) (t[0] + carry);
            target[i] = String.valueOf(tmp);
            System.out.println(target[i]);
        }
        System.out.println(target[num]);
        char[] r = target[num].toCharArray();
        int count = 0;
        for(int i = 0;i < r.length;i++) {
            if(r[i] == '1') count++;
        }
        return count;
    }
}
```

##### Date 2020.9.5