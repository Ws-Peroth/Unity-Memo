# Task 기초

## Task란

* Task : 비동기 작업을 나타내는 클래스로 ```System.Threading.Tasks``` 네임스페이스 안에 있습니다.
* 값을 반환하는 작업일 경우 ```Tast<TReasult>``` 를 사용합니다.
* task에 주어진 작업은 ```task.Start();```로 호출하여 다른 스레드에서 task작업을 수행할 수 있습니다.
  그리고, ```task.Wait()```을 통해 해당 task가 종료될 때 까지 대기할 수 있습니다.

### 간단한 예시

```csharp
using UnityEngine;
using System.Threading.Tasks;

public class TaskTest : MonoBehaviour
{
    public void Start()
    {
        print("Call Start");
        Task<int> task = new Task<int>(() => this.TaskProcess(5));

        task.Start();  // 다른 스레드에서 task 실행

        print("대기중");

        task.Wait();   // task가 종료될때까지 대기

        Debug.Log("task Result = " + task.Result);
    }


    public int TaskProcess(int countNumer)
    {
        print("start Process");

        for(int i = 0; i <= countNumer; i++)
        {
            print("Count : " + i);  // 0 부터 countNumer까지 수를 출력하는 프로그램
        }

        print("End Process");
        return countNumer;
    }
}
```

프로그램이 실행되면 자동적으로 실행이 되는 Start()함수 안에 실행코드를 구성하여 실행되도록 하였습니다.

Task를 이용해 비동기로 작동시킬 함수는 ```TaskProcess```로 int 라는 반환값이 있으니 ```Task<TResult>```형식을 이용하였습니다.

먼저 task변수가 Task의 결과로 int 형을 반환핟을 수 있도록 task의 타입을  ```Task<int>``` 로 해 주었고, task가 실행시킬 ```TaskProcess```를 넘겨주었습니다.



이 코드는 ```task.Start();```로 ```TaskProcess```를 실행시켜 다른 스레드에서 작업을 수행하고 기존에 있던 스레드에서는 ```print("대기중");```를 실행시킵니다. 그리고 ```task.Wait();```가 선언되어있으니, task의 작업이 끝날 때 까지 대기합니다.

task의 작업이 끝나면 ```task.Result```를 이용하여 결과를 출력해 주었습니다.


만약 반환값이 없는 함수라면  ```Task task = new Task(() => this.TaskProcess(5));``` 와 같은 방법으로 사용이 가능합니다.

반환값이 없으니 task또한 ```task.Result``` 가 없습니다.