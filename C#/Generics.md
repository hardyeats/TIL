## 제네릭 사용의 이점

```c#
// C# 1.1 방식으로 리스트 만들기(제네릭은 2.0부터 도입):
System.Collections.ArrayList list1 = new System.Collections.ArrayList();
list1.Add(3);
list1.Add(105);

System.Collections.ArrayList list2 = new System.Collections.ArrayList();
list2.Add("It is raining in Redmond.");
list2.Add("It is snowing in the mountains.");
```

`ArrayList` 클래스의 인스턴스는 밸류 타입이건 레퍼런스 타입이건 자유롭게 저장할 수 있다. 하지만 저장되는 순간 해당 아이템은 `Object` 타입으로 업캐스트된다. 그리고 밸류 타입이라면 리스트에 추가될 때 박싱 되고, 



## Reference

[Generics (C# Programming Guide)](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/generics/)