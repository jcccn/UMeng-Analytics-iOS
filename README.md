UMeng-Analytics-iOS
===================
这是一个[友盟统计](http://www.umeng.com/analytics)组件SDK的非官方镜像。

官方集成指南请参照[http://dev.umeng.com/analytics/ios-doc/integration](http://dev.umeng.com/analytics/ios-doc/integration)。

## 使用CocoaPods安装
[CocoaPods](http://cocoapods.org) 是开发 OS X 和 iOS 应用程序的一个第三方库的依赖管理工具。

要使用友盟统计组件SDK，推荐这样配置Podfile:

```ruby
# The front repo is prior if conflicted
# CocoaPods private repo
source 'https://github.com/jcccn/PodSpecs.git'
# CocoaPods master repo
source 'https://github.com/CocoaPods/Specs.git'

platform :ios,'7.0'

# ignore all warnings from all pods
inhibit_all_warnings!

pod 'UMAnalytics'

```

也可以这样配置Podfile:

```ruby
# CocoaPods master repo
source 'https://github.com/CocoaPods/Specs.git'

platform :ios,'7.0'

# ignore all warnings from all pods
inhibit_all_warnings!

pod 'UMAnalytics', :git => 'https://github.com/jcccn/UMeng-Analytics-iOS.git'

```

## 使用
在AppDelegate.m文件的 `- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions`方法中添加如下代码完成SDK的初始化：

```objective-c
#if (DEBUG)
    [MobClick startWithAppkey:UmengAppKey reportPolicy:REALTIME channelId:@"Development"];
#else 
    [MobClick startWithAppkey:UmengAppKey reportPolicy:REALTIME channelId:@"App Store"];
#endif
    
    [MobClick setAppVersion:[[[NSBundle mainBundle] infoDictionary] objectForKey:@"CFBundleShortVersionString"]];
```

页面的统计，在每个UIViewController或者自定义的BaseViewController中完成如下代码：

```objective-c
- (void)viewDidAppear:(BOOL)animated {
    [super viewDidAppear:animated];
    [MobClick beginLogPageView:NSStringFromClass([self class])];
}

- (void)viewDidDisappear:(BOOL)animated {
    [MobClick endLogPageView:NSStringFromClass([self class])];
    [super viewDidDisappear:animated];
}
```

详细的统计功能使用，请参考[官方文档](http://dev.umeng.com/analytics/ios-doc/integration)。
