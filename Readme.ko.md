# C# Tips

[English](https://github.com/phillyai/csharp-tips/blob/master/Readme.md) | [한국어](https://github.com/phillyai/csharp-tips/blob/master/Readme.ko.md)

## 키워드

- [TypedReference](#TypedReference)
- [__arglist](#__arglist)

## 신택스

- [Null 병합 연산자](#Null-병합-연산자)
- [Null 조건부 연산자](#Null-조건부-연산자)

## 언어 기능

- [익명 타입](#익명-타입)

---

## TypedReference

```csharp
static void Main()
{
    int i = 0;
    Foo(__makeref(i));
    Console.WriteLine(i); // 42를 출력
}

static void Foo(TypedReference i)
{
    __refvalue(i, int) = 42;
}
```

## __arglist

```csharp
static void Main()
{
    Foo(__arglist(1, 2, 3));
}

static void Foo(__arglist)
{
    ArgIterator iter = new ArgIterator(__arglist);
    for (int n = iter.GetRemainingCount(); n > 0; n--)
        Console.WriteLine(TypedReference.ToObject(iter.GetNextArg()));
}
```

## Null 병합 연산자

```csharp
var val = value1 ?? value2 ?? value3 ?? "";
```

## Null 조건부 연산자

```csharp
event Action<int> Clicked;

void Click()
{
    /* 원래는
    if (Clicked != null)
        Clicked(0);
    */
    Clicked?.Invoke(0);
}
```

## 익명 타입

```csharp
int[] arr = { 1, 2, 3 };
var dict = new Dictionary<string, int>() {
    { "A", 100 },
    { "B", 80 },
    { "C", 60 }
}
```