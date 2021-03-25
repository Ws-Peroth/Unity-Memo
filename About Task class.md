# Task란

* Task : 비동기 작업을 나타내는 클래스로 ```System.Threading.Tasks``` 네임스페이스 안에 있습니다.
* 값을 반환하는 작업일 경우 ```Tast<TReasult>``` 를 사용합니다.
* task에 주어진 작업은 ```task.Start();```로 호출하여 다른 쓰레드에서 task작업을 수행할 수 있습니다.
  그리고, ```task.Wait()```을 통해 해당 task가 종료될 때 까지 대기할 수 있습니다. 
* Add information