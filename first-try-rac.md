title: ReactiveCocoa 第一次小实践
date: 2014-08-29 22:19:43
categories: 
- TECH
- ReactiveCocoa
tags: [ObjectiveC,ReactiveCocoa]
---
#实现的目的功能
------
1. 限制用户手机号的输入长度, 限定在11位
2. 在输入的手机号的长度为11位时, enable获取验证码按钮.

#具体实现的比较
------
##传统思路实现
- 进行监听, 并且绑定回调的函数 
```
[self.phoneNumberInput addTarget:self
                          action:@selector(textFieldLimit11Characters:)
                forControlEvents:UIControlEventEditingChanged];
```
- 实现回调的函数
```
- (void)textFieldLimit11Characters:(UITextField *)textField {
    if (textField.text.length >= 11) {
        // 限制11位长度
        textField.text = [textField.text substringToIndex:11];
        // 手机号长度满足11位时, 取消获取验证码按钮的禁用
        self.getCheckNumber.enabled = YES;
    } else {
        self.getCheckNumber.enabled = NO;
    }
}
```

##使用 ReactiveCocoa 实现
```objc
// 限制11位长度
[self.phoneNumberInput.rac_textSignal subscribeNext:^(NSString *number) {
    if (number.length >= 11) {
        self.phoneNumberInput.text = [number substringToIndex:11];
    }
}];

// 手机号长度满足11位时, 取消获取验证码按钮的禁用
RAC(self, getCheckNumber.enabled) =
    [RACSignal combineLatest:@[self.phoneNumberInput.rac_textSignal]
                      reduce:^(NSString *number) {
                          return @(number.length >= 11);
                      }];
```


  [1]: http://segmentfault.com/img/bVcShM
  [2]: http://segmentfault.com/img/bVcShN
