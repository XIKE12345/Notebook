1. （10分）写一个验证掷骰子概率的程序，同时投掷2颗6面骰子n次，计算其和得到各数字的概率。

```
public class RandomClass {
    // 2颗骰子，6面，N次
    // 可能出现的点数和 2，3，4，5，6，7，8，9，10，11，12
    public static void main(String[] args) {
        RandomClass.getResultNum(100);
    }

    /**
     * 求各点数的和及概率
     *
     * @param n
     */
    private static void getResultNum(int n) {
        int intArray[] = {0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0};
        // 获取1-6之间随机数
        for (int i = 0; i <= n; i++) {
            int ran1 = (int) (Math.random() * 6) + 1;
            int ran2 = (int) (Math.random() * 6) + 1;
            int res = ran1 + ran2;
            switch (res) {
                case 2:
                    intArray[0]++;
                    break;
                case 3:
                    intArray[1]++;
                    break;
                case 4:
                    intArray[2]++;
                    break;
                case 5:
                    intArray[3]++;
                    break;
                case 6:
                    intArray[4]++;
                    break;
                case 7:
                    intArray[5]++;
                    break;
                case 8:
                    intArray[6]++;
                    break;
                case 9:
                    intArray[7]++;
                    break;
                case 10:
                    intArray[8]++;
                    break;
                case 11:
                    intArray[9]++;
                    break;
                case 12:
                    intArray[10]++;
                    break;
            }
        }
        for (int arr = 0; arr <= intArray.length - 1; arr++) {
            int count = intArray[arr];
            double rate = new BigDecimal((float) count / n).setScale(2, BigDecimal.ROUND_HALF_UP).doubleValue();
            System.out.println(rate);
        }
    }
}

```

1. （10分）编写程序解决以下问题：长度为N的数组，随机放入值为1-50中间的任意整数，请编写程序找出其中的偶数数字，并按照该数字在数组中出现次数从多到少排序输出。
   ```

public class FileCount { public static void main(String[] args) {

        List<Integer> nums = new ArrayList<>();
        for (int i = 1; i <= 100; i++) {
            // 产生1-50的随机数
            int num = (int) (Math.random() * 50) + 1;
            nums.add(num);
        }
        // 挑出偶数
        List<Integer> evenNumbers = new ArrayList<>();
        for (Integer evenNum : nums) {
            if (evenNum % 2 == 0) {
                evenNumbers.add(evenNum);
            }
        }


        Map<Integer, Integer> map = new HashMap();
        for (Integer res : evenNumbers) {
            boolean flag = map.containsKey(res);
            if (!flag) {
                map.put(res, 1);
            } else {
                map.put(res, map.get(res) + 1);
            }
        }

        // 遍历map

// for (Map.Entry<Integer, Integer> entry : map.entrySet()) { // System.out.println(entry.getKey() + "出现了 " +
entry.getValue() + " 次"); // }

        // 排序 使用Compare
        List<Map.Entry<Integer, Integer>> list = new ArrayList<>(map.entrySet());
        Collections.sort(list, new Comparator<Map.Entry<Integer, Integer>>() {
            @Override
            public int compare(Map.Entry<Integer, Integer> o1, Map.Entry<Integer, Integer> o2) {
                return o1.getValue().compareTo(o2.getValue());
            }
        });
        for (Map.Entry s : list) {
            System.out.println(s.getKey() + "出现了" + s.getValue() + "次");
        }
    }

}

```


1. （10分）编写程序列出一个目录下所有的文件，包括所有子目录下的文件，并打印出文件总数。
```

public class FileName { public static void main(String[] args) { int sumCount = 0; FileName listfile = new FileName();
int count = listfile.listJavaFile("/Users/huike/apache-maven-3.6.0/conf"); sumCount += count; System.out.println("总数为："
+ sumCount); } public int listJavaFile(String fileName) { int count = 0; File file = new File(fileName); if (
file.isDirectory()) { File[] files = file.listFiles(); for (int i = 0; i < files.length - 1; i++) { String name =
files[i].getName(); System.out.println(name); if (files[i].isDirectory()) { String path = files[i].getPath(); // 递归
listJavaFile(path); } } count = files.length; } return count; } }

```
1. （20分）有一张班级学生表有3个字段分别为学生姓名：STUDENT、性别：GENDER、身高：STATURE。请编写程序为该班学生排座位，规则如下：
        1）教室共4排座位，每个座位都可以坐2人（有同桌）
        2）身高矮的同学坐在前排，身高高的坐后面
        3）同桌必须为同性别同学，若同性别人员为奇数，只允许最后一排位置一个人坐
1. （10分）找出这样的数字：一个数字等于它的各分解项相加。示例数字 28可分解为1、2、4、7、14，1+2+4+7+14=28。同样，数字6分解为:1、2、3，1+2+3=6。用代码找出1-500以内的所有符合这样条件的数字。
```

public class NumClass { public static void main(String[] args) { int num = 500; NumClass.print(num); }

    public static void print(int num) {
        int s;
        // 500以内的数
        for (int i = 6; i <= num; i++) {
            s = 0;
            // 因式分解
            for (int j = 1; j < i; j++) {
                if (i % j == 0)
                    s += j;
            }
            if (i == s)
                System.out.println(i);
        }
    }

}

```
1. （6分）请编写一个函数，能将字符串main-action-holder，转换为mainActionHolder
```public class Hump2Line {
       public static void main(String[] args) {
           String s = Hump2Line.lineToHump("sgsdf-sfd-et");
           System.out.println(s);
       }
       public static String lineToHump(String str) {
           // 转换成小写
           str = str.toLowerCase();
           // 以"-"分割
           String[] split = str.split("-");
           String resStr = "";
           for (int i = 0; i < split.length; i++) {
               String s = split[i].substring(0, 1).toUpperCase() + split[i].substring(1);
               resStr += s;
           }
           return resStr;
       }
   }
```

1. （20分）简单实现在线购买电影票，请重点考虑多人同时购买一个座位的情况，可以使用伪代码

```

public class Ticket implements Runnable {
    private static int ticket = 10;
    @Override
    public void run() {
        for (int i = 1; i <= 100; i++) {
            try {
                Thread.sleep(500); //线程休眠500毫秒，以便观察输出
            } catch (InterruptedException e) { //需要处理异常
                e.printStackTrace();
            }
            synchronized (this) { //同步代码块+对象锁（this表示对象锁）
                if (ticket <= 0) {
                    break;
                }
                System.out.println(Thread.currentThread().getName() + " 买了第" + ticket + "张票");
                ticket--;
            }
        }
    }
    public static void main(String[] args) {
        Ticket ticket = new Ticket();
        new Thread(ticket, "1号窗口").start();
        new Thread(ticket, "2号窗口").start();
        new Thread(ticket, "3号窗口").start();
    }
}
```

1. （7分）学生表：STUDENT(ID,USER_NAME)和考试表：EXAM(ID,USER_ID,SCORE)
   表，STUDENT表主键为ID字段，EXAM表中外键USER_ID为STUDENT的ID字段值，编写SQL查询每位学生的成绩，缺考的以0分处理（缺考的考试表中无记录）
   ```  Select * from STUDENT s Left Join EXAM e on  s.id = e.USER_ID```
1. （7分）已知用户表USER(ID,USER_NAME,AGE),通过sql语句查询表中相同年龄（AGE）存在两条以上记录的用户年龄及用户个数，并按照统计数量倒排序

```
SELECT * FROM (
    SELECT `USER_NAME`,`AGE`, count(`AGE` ) FROM USER  GROUP BY `AGE` HAVING COUNT(`AGE`)>0 ORDER BY `AGE` DESC
    ) s
 ```
 