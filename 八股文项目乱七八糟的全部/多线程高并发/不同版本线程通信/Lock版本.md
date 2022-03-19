condition精确唤醒

 
```` 
package 生产者消费者;

import java.util.concurrent.TimeUnit;
import java.util.concurrent.locks.Condition;
import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReentrantLock;

//lock 手动关锁，释放了锁
public class LockVersion {
  private static Lock lock=new ReentrantLock();
  private static Condition condition1=lock.newCondition();
  private static Condition condition2=lock.newCondition();
  private static Thread t1,t2;

  public static void main(String[] args) throws InterruptedException {


    char[] chars1="12345".toCharArray();
    char[] chars2="ABCDE".toCharArray();

    t1=new Thread(()->{
      try {
        lock.lock();
        for(char c : chars1){
          System.out.print("  "+c);
          condition2.signalAll();
          condition1.await();

        }
      } catch (Exception e) {
        e.printStackTrace();
      } finally {
        lock.unlock();
      }

    });



    t2=new Thread(()->{
      try {
        lock.lock();
        for(char c : chars2){
          System.out.print("  "+c);
          condition1.signalAll();
          condition2.await();

        }
      } catch (Exception e) {
        e.printStackTrace();
      } finally {
        lock.unlock();
      }
    });

    t1.start();
    TimeUnit.SECONDS.sleep(1);
    t2.start();



  }

}

````




