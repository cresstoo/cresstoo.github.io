title: iOS动画入门学习

date: 2015-07-29 18:19:24

tags: [Swift, Animation]
-----
学习了林永坚老师的[iOS动画入门](http://www.imooc.com/learn/392)、[iOS动画进阶](http://www.imooc.com/learn/395)两个课程，包含iOS几种基础动画的实现方法。

### iOS基本动画方法

![image](http://7qn9uj.com1.z0.glb.clouddn.com/githubiOSAnimation.png)

* #### position 位置

   ```objective-c
   UIView.animateWithDuration(1, animations:{
   self.greenSquare.center.x = self.view.bounds.width - self.greenSquare.center.x
    })
   ```

* #### opacity 透明度

    ```objective-c
    UIView.animateWithDuration(1, animations: {
        self.greenSquare.alpha = 0.1
    })
    ```

* #### scale 缩放

    ```objective-c
    UIView.animateWithDuration(1, animations: {
        self.greenSquare.transform = CGAffineTransformMakeScale(2.0, 2.0)
    })
    ```

* #### color 变色

    ```objective-c
    UIView.animateWithDuration(1, animations: {
        self.greenSquare.backgroundColor = UIColor.redColor()
        self.name.textColor = UIColor.whiteColor()
    })
    ```

* #### rotation 旋转

   ```objective-c
   func rotation(){
   UIView.animateWithDuration(0.5, delay: 0, options: .CurveLinear, animations: {
        self.spin.transform = CGAffineTransformRotate(self.spin.transform, CGFloat(M_PI))
    }) {(finished) -> Void in
            self.rotation()
    }}
   override func viewDidAppear(animated: Bool) {
        super.viewDidAppear(animated)
    	self.rotation()

   }
   ```

* #### repeat 重复

    ```objective-c
    UIView.animateKeyframesWithDuration(1, delay: 0, options: .Repeat, animations: {
        self.redSquare.center.x = self.view.bounds.width - self.redSquare.center.x
    }, completion: nil)

    UIView.animateKeyframesWithDuration(1, delay: 0, options: .Repeat | .Autoreverse, animations: {
        self.greenSquare.center.x = self.view.bounds.width - self.greenSquare.center.x
        }, completion: nil)
    ```

* #### easing 缓动动画

   ```objective-c
   	UIView.animateWithDuration(1, delay: 0, options: .CurveEaseIn, animations: {
   	self.redSquare.center.x = self.view.bounds.width - self.redSquare.center.x
        }, completion: nil)// EaseIn Animation
    
   UIView.animateWithDuration(1, delay: 0, options: .CurveEaseOut, animations: {
   	self.greenSquare.center.x = self.view.bounds.width - self.greenSquare.center.x
        }, completion: nil)// EaseOut Animation
    
   UIView.animateWithDuration(1, delay: 0, options: .CurveEaseInOut, animations: {
        self.yellowSquare.center.x = self.view.bounds.width - self.yellowSquare.center.x
        }, completion: nil)// EaseIn and EaseOut Animation
   ```

* #### spring 弹性动画

    ```objective-c
    UIView.animateWithDuration(5, delay: 0, usingSpringWithDamping: 0.1, initialSpringVelocity: 0, options: nil, animations: {
        self.redSquare.center.x = self.view.bounds.width - self.redSquare.center.x
    }, completion: nil)

    UIView.animateWithDuration(5, delay: 0, usingSpringWithDamping: 0.1, initialSpringVelocity: 1, options: nil, animations: {
        self.greenSquare.center.x = self.view.bounds.width - self.greenSquare.center.x
        }, completion: nil)
    ```

#### What I Learned

通过3个小时学习

1. 对操作TableView和UIView动画基础代码比较熟悉

2. 对缓动动画和弹性动画的原理和实现有了初步了解

### 旋转动画实例

![image](http://7qn9uj.com1.z0.glb.clouddn.com/rotation.gif)

rotation这个例子对我来说略微复杂的地方在于，为了实现重复执行360°旋转，老师在这里封装了一个函数来循环执行。事后需要从头补下课。

### 缓动动画和弹性动画实例

![image](http://7qn9uj.com1.z0.glb.clouddn.com/easing.gif)

![image](http://7qn9uj.com1.z0.glb.clouddn.com/spring.gif)

easing和spring理解和书写都挺简单的，主要是要理解：

**缓动动画三种属性**

- `option: .CurveEaseIn // 缓进`

- `option: .CurveEaseOut // 缓出`

- `option: .CurveEaseInOut // 缓进缓出`


**弹力动画两个重要属性（iOS7以上版本支持）**

- `usingSpringWithDamping //阻尼大小`
- `initialSpringVelocity //初始速度` 