## 内部类、静态内部类
public class Boss {
    //内部类
    
    public class Demo1{

    }
    //属性私有化
    private Boss(){
    }
    //充分利用静态内部类的特性,在内部类里面实例化Boss
    //只会被实例化一次
    //只有当静态内部类的属性被调用才会加载静态内部类

    //静态内部类
    static class Singleton{
        private final static Boss instance=new Boss();
        public static Boss getInstance(){
            return Singleton.instance;
        }
    }
}
- 枚举类

public enum Weekday {
    SUN(0),MON(1),TUS(2),WED(3),THU(4),FRI(5),SAT(6);

    private int value;

    private Weekday(int value){
        this.value = value;
    }

    public static Weekday getNextDay(Weekday nowDay){
        int nextDayValue = nowDay.value;

        if (++nextDayValue == 7){
            nextDayValue =0;
        }

        return getWeekdayByValue(nextDayValue);
    }

    public static Weekday getWeekdayByValue(int value) {
        for (Weekday c : Weekday.values()) {
            if (c.value == value) {
                return c;
            }
        }
        return null;
    }
}

class Test2{

    public static void main(String[] args) {
        System.out.println("nowday ====> " + Weekday.SAT);
        System.out.println("nowday int ====> " + Weekday.SAT.ordinal());
        System.out.println("nextday ====> " + Weekday.getNextDay(Weekday.SAT)); // 输出 SUN

        //输出：
        //nowday ====> SAT
        //nowday int ====> 6
        //nextday ====> SUN
    }
}

//单例模式
- 实现单利最重要的一点是构造方法是private的，
- 这使得实例不能被外界所创建。
- 常用的单利有：懒汉式、饿汉式、线程安全式、双重检查式和登记式。
- [单例模式实例代码](https://blog.csdn.net/qq_37169817/article/details/78903119)
