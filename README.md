### C/C++在Java项目、Android和Objective-C三大平台下实现混合编程
http://www.taoweiji.cn/2016/08/02/ndk 


##### 第六步：编写JNI接口
```
package cn.taoweiji.nativemodule;

/**
 * 包名和类名称一定要和前面的C++头文件对应
 * cn_taoweiji_nativemodule_NativeDemo.h
 */
public class NativeDemo {
    public static native int add(int param1, int param2);

    public static native void say(String name);

    public static native String getInfo();

    public static native void nativeToJava(NativeDemo nativeDemo);

    public int subtract(int param1, int param2) {
        System.out.println("NativeDemo:" + String.format("%s - %s = %s", param1, param2, param1 - param2));
        return param1 - param2;
    }
}
```

##### 第七步：调用C++
```
public class Main {

    static {
        System.load("/Users/Wiki/Library/Developer/Xcode/DerivedData/DEMO_MAC_JNI-clxymnzifegyfaajsaattzgxqfbr/Build/Products/Debug/DEMO_MAC_JNI");
    }

    public static void main(String[] args) {
        System.out.println("Hello World!");
        int result = NativeDemo.add(1, 2);
        System.out.println("1+2=" + String.valueOf(result));
        NativeDemo.say("Hello,I am Java.");
        System.out.println("getInfo:" + NativeDemo.getInfo());
        NativeDemo.nativeToJava(new NativeDemo());
    }
}
```
