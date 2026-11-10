# Code in Motion — @motion.with.code

Full code snippets for every Reel in the series.

## Episodes

### Go

#### Go #1 — Goroutines in Motion (W1)
```go
var wg sync.WaitGroup
for i := 0; i < 6; i++ {
    wg.Add(1)
    go func(id int) {
        defer wg.Done()
        work(id)
    }(i)
}
wg.Wait()
```
> Concurrency bukan jalan sekaligus. Itu koordinasi.

#### Go #2 — Channel Handshake (W4)
```go
ch := make(chan string)
go func() { ch <- "hello" }()
msg := <-ch
fmt.Println(msg)
```

#### Go #3 — Select: Pick the Fastest (W7)
```go
select {
case msg1 := <-ch1:
    fmt.Println("received", msg1)
case msg2 := <-ch2:
    fmt.Println("received", msg2)
case <-time.After(1 * time.Second):
    fmt.Println("timeout")
}
```

#### Go #4 — Defer: Cleanup Order (W10)
```go
func process() {
    defer fmt.Println("cleanup 1")
    defer fmt.Println("cleanup 2")
    fmt.Println("working...")
}
// Output: working... cleanup 2 cleanup 1
```

#### Go #5 — Interface Satisfaction (W13)
```go
type Speaker interface {
    Speak() string
}

type Dog struct{}
func (d Dog) Speak() string { return "Woof!" }

func greet(s Speaker) { fmt.Println(s.Speak()) }
```

#### Go #6 — Error Wrapping (W16)
```go
err := fmt.Errorf("query failed: %w", dbErr)
if errors.Is(err, dbErr) {
    // handle
}
```

### JavaScript

#### JS #1 — Promise Chain Dance (W2)
```js
fetch('/api/data')
  .then(res => res.json())
  .then(data => transform(data))
  .catch(err => handleError(err));
```
> Then itu pipa. Catch itu pintu darurat.

#### JS #2 — Promise.all vs allSettled (W5)
```js
// all: fails fast on first rejection
Promise.all([p1, p2, p3])

// allSettled: waits for all, never rejects
Promise.allSettled([p1, p2, p3])
```

#### JS #3 — Event Loop in 30s (W8)
```js
console.log('1');
setTimeout(() => console.log('2'), 0);
Promise.resolve().then(() => console.log('3'));
console.log('4');
// Output: 1, 4, 3, 2
```

#### JS #4 — Destructuring: Unpack (W11)
```js
const {name, age} = user;
const [first, ...rest] = items;
```

#### JS #5 — Closure: Remember (W14)
```js
function counter() {
  let count = 0;
  return () => ++count;
}
const inc = counter();
inc(); // 1
inc(); // 2
```

#### JS #6 — Optional Chaining (W17)
```js
const city = user?.address?.city ?? 'Unknown';
```

### Python

#### Python #1 — List Comprehension in One Breath (W3)
```python
# Old way
result = []
for x in numbers:
    if x % 2 == 0:
        result.append(x * 2)

# New way
result = [x * 2 for x in numbers if x % 2 == 0]
```
> Brevity counts. Readability counts juga.

#### Python #2 — Decorator in One Breath (W6)
```python
def log(func):
    def wrapper(*args):
        print(f"Calling {func.__name__}")
        return func(*args)
    return wrapper

@log
def greet(name):
    return f"Hello, {name}"
```

#### Python #3 — Generator vs List (W9)
```python
# Eager: builds full list in memory
squares = [x**2 for x in range(1000000)]

# Lazy: yields one at a time
squares = (x**2 for x in range(1000000))
```

#### Python #4 — Unpacking: *args, **kwargs (W12)
```python
def greet(*args, **kwargs):
    print(args)    # tuple
    print(kwargs)  # dict

greet(1, 2, name="Chava")
```

#### Python #5 — Walrus Operator := (W15)
```python
# Without walrus
n = len(data)
if n > 10:
    print(n)

# With walrus
if (n := len(data)) > 10:
    print(n)
```

#### Python #6 — Context Manager: with (W18)
```python
with open('file.txt') as f:
    data = f.read()
# File auto-closed
```

## License
Code snippets are provided for educational purposes. Free to use and share.