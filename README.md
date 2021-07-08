# practice
日程
6.28 环境
  看入职手册
  jdk  海鸥里面的是32位的 坑 自己下载64的不然跑项目的时候会出错
  JAVA_HOME中配jdk安装目录  path中配 bin和jre/bin
  as 4.2.1  个性化设置  设置内存等
  gradle 4.10.1  版本太高的话 aura不支持
6.29
  看arua文档 了解宿主 公共库 插件关系 了解插件化开发
  申请代码仓库   lib 和 客户端主程序
  申请周报查看权限
  下载git clone代码  调环境
6.30
  申请usb权限
  跑代码  git上clone下来的代码 没有gradle文件夹  本地新开个项目 复制粘贴过去  不然报错
  gradle-wrapper.properties设置gradle版本
  ADB 远程调试成功
  看首页bottomnavigationview代码
  首页继承关系
  FragmentActivity -> BaseActivity -> MyActivity -> MainFrameActivity
  首页 MainFrameActivity的onAttachFragment()绑定JDNavigationFragment

  JDNavigationFragment 的onCreate()中调用navigationInit()进行导航栏初始化
  navigationInit()调用CreateNaviBar()创建导航栏,储存用NavigationBase包装的按钮
  NavigationButton(按钮)是CreateNaviBar()调用getCustomNaviBar()创建的
  getCustomNaviBar()通过createCustomNaviBtn()获取skin皮肤 id btn
  createCustomNaviBtn()通过Pass化取得的服务器信息？

  NavigationButton初始化完后 navigationInit() 又调用了JDNavigationFragment 的commit()
  commit中往radiogroup中添加按钮并且注册点击事件监听


7.5  settlement中 newFillOrder网络请求逻辑
 	 activity->getPresenter()->new Interactor -> new Controller
  网络请求进行了三次封装
  Presenter和Interactor都是ui与数据之间的逻辑封装
  controller：请求网络数据具体业务封装 通过把实现了MyHandler的任务类存入全局变量group统一处理
  
  QueryCurrentOrderMyHandler查询商品详情
  QAdditionalOrderMyHandler
  uSubmitOrderMyHandler
  都是list的内部类 都继承了MyHandler基类 重写了run方法
  @Override
  public void run() {
    if(当前list全局标量的event不是自己要处理的)
      return;
      处理入参...
      .....
      把入参、监听 具体等设置存入setting变量
      加入group
  }
  
  加入group中之后 没找到在哪执行 group是activity中直接get出来默认的  不知道是不是加入之后自动就执行了

  京粉 用retrofit网络请求  eventBus通信  H5显示页面

7.6
  京粉需求  小程序分享时图片无白边
    代码测量imageView宽高后设置给底部view(不太行)。最后设置imageVIew的scaleType属性解决
    retrofit jxjclient call接口
    liveData  JDVIewMode

7.8
    首页逻辑伪代码
    lodingActivity -> SlidingTabActivity{
        判断需要显示的弹窗
        是否登陆
        设置toolbar
        设置tab小红点
        缓存cookie 等
        ......
        new SlidingTabPresenter(){
            retrofit请求网络数据 {
                getJxjClient()获取主机地址
                JxjClient中添加retrofit需要的请求方法
                call返回接口{
                    处理返回数据
                    ......
                    eventBus.post 跳转 到对应的fragment的presenter
                    presenter中处理后跳转到fragment
                }
            }
        }
        tab.setFragmentAdapter(new SlidingTabAdapter()){
            设置图标 点击事件
            getFragment 中 返回每个Fragment的实例
        }
    }->每个tab

    首页注册了eventBus 判断是否弹窗

    设备唯一标识：getAndroidId().hashCode(), ((long) getDeviceId().hashCode() << 32) | getDeviceId().hashCode()拼起来的
    
    DeviceId: 是获取网络的mac地址  如果没有的话 就拿androidID
    androidID: Settings.Secure.getString(Resolver(),Settings.Secure.ANDROID_ID); 




















    
