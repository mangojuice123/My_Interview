- [常见问题](#常见问题)
  - [序列化是如何实现的？](#序列化是如何实现的)
  - [为什么要进行序列化？](#为什么要进行序列化)
  - [serialVersionUID 有什么用？不写会怎么样？](#serialversionuid-有什么用不写会怎么样)
  - [HashMap 中为什么要使用 transient 关键字？](#hashmap-中为什么要使用-transient-关键字)
- [序列化与反序列化的一个例子](#序列化与反序列化的一个例子)


</br></br>


# 常见问题
## 序列化是如何实现的？
答：
- Java 类通过实现 `java.io.Serialization` 接口来启用序列化功能，未实现此接口的类将无法将其任何状态或者信息进行序列化或者反序列化。
- 序列化的实现依赖于 `java.io.ObjectOutputStream` 这个类，这个类被一个更低层次的字节流处理类所包装，通过这个类，可以将需要的类的状态保存成二进制流，方便存储或再网络上传输。当我们进行反序列化时，调用 `java.io.ObjectOutputStream` 将字节流还原类的状态。
- 在序列化过程中，如果被序列化的类中定义了 `writeObject` 和 `readObject` 方法，虚拟机会试图调用对象类里的 `writeObject` 和 `readObject` 方法，进行用户自定义的序列化和反序列化。

## 为什么要进行序列化？
答：
- 序列化可以实现分布式对象：利用序列化运行远程主机上的服务，就像在本机上运行对象一样（Remote Method Invocation）
- 统一保存和传输数据：序列化以后就是字节流了，可以使用通用的格式方便保存和传输，下次需要实例化时只需要将字节流反序列化到内存中即可。
- 递归保存对象引用的每个对象的数据：序列化可以实现对对象的「深复制」，即复制对象本身及引用的对象本身。序列化一个对象可能得到整个对象序列。

## serialVersionUID 有什么用？不写会怎么样？
答：
- 在进行反序列化时，JVM 会把传来的字节流中的 `serialVersionUID` 与本地相应实体类的 `serialVersionUID` 进行比较，如果相同就认为是一致的，可以进行反序列化，否则就会出现序列化版本不一致的异常，即是 `InvalidCastException`。
- 如果不写的话，系统会自动生成一个默认的 `serialVersionUID`，导致抛出异常。`serialVersionUID` 是用来验证版本一致性的，在兼容性升级的时候，不能改变其值；在版本升级时（非兼容性升级），需要修改其值。

## HashMap 中为什么要使用 transient 关键字？
答：
- 由 get/put 方法知道，读/写元素是根据 `Object.hashcode()` 来确定从哪个 bucket 读/写的，这是一个 native 方法，不同的 JVM 里的实现可能不同。
- 因此，在不同的 JVM 中，内存分布是可能不一样的，所以需要使用 transient 关键字，不保存数组，只保存 key/value，然后重新生成 HashMap。


</br></br>


# 序列化与反序列化的一个例子
```
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.ObjectInputStream;
import java.io.ObjectOutputStream;
import java.io.Serializable;
import java.util.Calendar;
import java.util.Date;

public class Main {
    public static void main(String[] args) {
        new FlattenTime("time.ser");

        try {
            Thread.sleep(1000);
        } catch (InterruptedException e) {
            // TODO Auto-generated catch block
            e.printStackTrace();
        }

        new InflateTime("time.ser");
    }

    public static class InflateTime {
        String fileName = "";
        PersistentTime time = null;
        FileInputStream fis = null;
        ObjectInputStream in = null;

        public InflateTime(String fileName) {
            this.fileName = fileName;
            try {
                fis = new FileInputStream(fileName);
                in = new ObjectInputStream(fis);
                // 必须进行类型转换。
                time = (PersistentTime) in.readObject();
                in.close();
            } catch (IOException | ClassNotFoundException e) {
                // TODO Auto-generated catch block
                e.printStackTrace();
            }

            System.out.println("Flattened time: " + time.getTime());
            System.out.println();
            System.out.println("Current time: " + Calendar.getInstance().getTime());
        }
    }

    public static class FlattenTime {
        String fileName = "";
        PersistentTime time = null;
        FileOutputStream fos = null;
        ObjectOutputStream out = null;

        public FlattenTime(String fileName) {
            this.fileName = fileName;
            this.time = new PersistentTime();
            try {

                fos = new FileOutputStream(fileName);
                out = new ObjectOutputStream(fos);
                out.writeObject(time);
                out.close();
            } catch (Exception e) {
                // TODO: handle exception
                e.printStackTrace();
            }
        }

    }

    public static class PersistentTime implements Serializable {
        private Date time;

        public PersistentTime() {
            time = Calendar.getInstance().getTime();
        }

        public Date getTime() {
            return time;
        }
    }
}
```