一道面试题，手写一个容器，实现最多10个消费者线程和两个生产者线程之间交互

可以用sync，但是不好精确唤醒，毕竟线程有点多，用lock的condition实现精确唤醒，还有泛型

最多十个消费者意味着容器的上限是10，然后每次生产者生产完了以后就马上唤醒消费者

同样道理，消费者消费完了马上叫生产者

```` 
package 生产者消费者;

import java.util.ArrayList;
import java.util.List;
import java.util.concurrent.TimeUnit;
import java.util.concurrent.locks.Condition;
import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReentrantLock;

public class ContainerLock<T> {
  private final int max=10;
  private int count=0;
  private List<T> list=new ArrayList<>();

  private Lock lock=new ReentrantLock();
  private Condition producer=lock.newCondition();
  private Condition consumer=lock.newCondition();

  public ContainerLock() {
  }

  public void put(T item){

    try {
      lock.lock();
      //刚好等于10个，生产者停止生产
      while(count==max){
        producer.await();

      }

      //生产者生产,叫消费者过来拿
      list.add(item);
      count++;
      System.out.println("生产者 "+Thread.currentThread().getName()+" 生产了了一个item"+ " 现在的size是 "+list.size());
      consumer.signal();
    } catch (Exception e) {
      e.printStackTrace();
    } finally {
      lock.unlock();
    }
  }

  public void get(){

    try {
      lock.lock();
      //没东西拿，消费者线程阻塞，生产者线程生产
      while(count==0){
        consumer.await();
      }

      //消费者消费,少于10个了，让生产者生产
      list.remove(0);
      count--;
      System.out.println("消费者"+Thread.currentThread().getName()+" 消费了一个item" + " 现在的size是 "+list.size());
      producer.signal();
    } catch (Exception e) {
      e.printStackTrace();
    } finally {
      lock.unlock();
    }
  }

}

class Test{

  public static void main(String[] args) throws InterruptedException {
    ContainerLock containerLock=new ContainerLock();


    //10个消费者
    for(int i=0;i<10;i++){
      new Thread(()->{
        for(int j=0;j<5;j++){
          containerLock.get();

        }
      },"consumer"+i).start();
    }

    TimeUnit.SECONDS.sleep(2);

    //多个生产者
    for(int i=0;i<2;i++){
      new Thread(()->{
        for(int j=0;j<25;j++){
          containerLock.put("item");

        }
      },"producer"+i).start();
    }



  }
}

````

