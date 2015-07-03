title: Swift 中的函数及其外部参数名
category: 
- Swift
tags: Swift
---

# Swift 中的函数
## 函数是一等公民
```
func stepForward(input: Int) -> Int {
  return input + 1
}

func stepBackward(input: Int) -> Int {
  return input - 1
}

func chooseStepFunction(stepBackwards backwarks: Bool) -> (Int) -> Int {
  return backwarks ? stepBackward : stepForward
}

// 逐步获取
var stepFunction = chooseStepFunction(stepBackwards: true)
var result = stepFunction(100)
println(result)

// 直接调用
println(chooseStepFunction(stepBackwards: true)(122))
```
## 外部参数名的忽略
```
func stepForward(step input: Int) -> Int {
  return input + 1
}

func stepBackward(step input: Int) -> Int {
  return input - 1
}

func chooseStepFunction(stepBackwards backwarks: Bool) -> (Int) -> Int {
  return backwarks ? stepBackward : stepForward
}

// 直接调用原函数时, 需要是用外部参数名
stepBackward(step: 100)

// 直接调用时, 不用外部参数名
println(chooseStepFunction(stepBackwards: true)(122))

// 逐步获取, 不需要外部参数名, 本以为这种方式就能做类似类名推倒了
var stepFunction = chooseStepFunction(stepBackwards: true)
var result = stepFunction(100)
println(result)

```

虽然觉得这么处理挺丑的, 想想估计是没法应对外部参数名不一致的情况吧.