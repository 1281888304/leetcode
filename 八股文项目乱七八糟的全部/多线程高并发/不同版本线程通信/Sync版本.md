Sync：wait notify，记得最后要notify，唤醒另外一个，和上面有一个一摸一样我就不复制了（上面：notify不释放锁）

最后唤醒了也不释放锁，但是往下一步这个方法执行完了，也会释放锁

容器那里最后不需要通信是因为方法走完了自动把锁放出来，lock不需要最后通信是因为unlock自动解锁。这也是为什么lock好用一丢丢

```` 
package 生产者消费者;

import java.util.concurrent.TimeUnit;
import java.util.concurrent.locks.Condition;

public class SyncVersion {
  private static Thread t1,t2;
  private static final Object lock=new Object();

  public static void main(String[] args) throws InterruptedException {
    char[] chars1="12345".toCharArray();
    char[] chars2="ABCDE".toCharArray();

    t1=new Thread(()->{
      synchronized (lock){
        for(char c : chars1){
          System.out.print("  "+c);
          try {
            lock.notify();
            lock.wait();
          } catch (InterruptedException e) {
            e.printStackTrace();
          }

        }
        lock.notify();
      }

    },"t1");

    t2=new Thread(()->{
      synchronized (lock){
        for(char c : chars2){
          System.out.print("  "+c);
          try {
            lock.notify();
            lock.wait();
          } catch (InterruptedException e) {
            e.printStackTrace();
          }

        }
      }
    },"t2");

    t1.start();
    TimeUnit.SECONDS.sleep(1);
    t2.start();

  }


}
````




