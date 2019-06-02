# android.Base-notes
android入门-包括第一行代码的第一章和第二章内容 (所有的android之小a为入门阶段~)
# 将以定位章节 和 自己的理解为主加以整理

## 1.1.1 Android的系统架构
* 1.Linux内核层：最底层的部分 主要用来给Android的各种硬件提供底层的驱动 比如常用的蓝牙驱动 wifi驱动 电源等   
* 2.系统运行库层：主要是通过底层的C/C++等为上层的Android提供一些特性的支持--> Android NDK 如SQLite提供了数据库的支持 其中还包括了 1.核心库也就是Libraries 这里用来给开发者使用JAVA语言编写Android应用 运行时库就是runtime 这里面也就包含了DVM 5.0以后为了热修复等改成了ART DVM的区别和JVM就是DVM基于寄存器而JVM基于栈 效率快   
* 3.应用框架层：主要就是各种SM 提供了各种可以被用到的API 开发者可以使用其编写程序    
* 4.应用层：所有被安装的程序都是属于这一层

## 1.3.4 Project模式下的项目结构     
![图片](https://github.com/pawNku/image.inGithub/blob/master/1.3.4.jpg?raw=true)
* 1..gradle和.idea：这两个不用管 都是一些自动生成的文件    
* 2.app：一句话开发都在这哦    
* 3.buid：也是自动的 是在编译的时候生成的 
* 4.gradle：这里我们首先来BB下啥是gradle和gradle wrapper Gradle：android用来构建项目的编程框架。这个玩意对于使用AS开发的，大家都清楚比如引入第三方依赖  没找到gradle，却总是能看见一个叫gradle wrapper的玩意 其实wrapper就是一手包装 因为嘛这个gradle是在快速迭代的 这样的话如果每次都去直接引用 那又要每次都更改版本肯定巨炸 因为毕竟每个项目不尽相同 而gradle的引入就是为了轻松 所以wrapper就出现了 目的就是读取配置文件中的gradle版本 然后就为我们自动的更新下载配置gradle  所以说不用提前下好 看看本地缓存再联网就下载对应的gradle了    
![图片](https://github.com/pawNku/image.inGithub/blob/master/1.3.4.png?raw=true)
* 5..gitignore：如其名 就是过滤不需要提交的文件 为了避免开发中不必要的冲突  忽略操作系统自动生成的文件  忽略编译生成的中间文     
```
local.properties：用来保存项目依赖信息
.gradle： 用来保存gradle的依赖信息
.idea： 用来保存开发工具的设置信息
build： 用来保存编译后的文件目录，所有build文件夹都不需要跟踪
*.iml： 是用来保存开发工具信息
注意：.gitignore文件要在文件提交之前设置才有效，如果文件已经提交，需要先把仓库里面的文件删除掉
```
* 6.build.gradle：这玩意也是不需要修改的 是全局的gradle构建脚本    
* 7.gradle.properties：全局的gradle配置文件 在这里修改的将会影响到上面的构建脚本   
* 8.gradlew和gradlew.bat：是用来在命令行界面中执行gradle命令的 gradlew是在Linux or Mac系统中的 而grawdlew.bat是在Windows中使用的   
* 9.*** .iml：说白了就是告诉你AS也是IntelliJ IDEA项目 反正你也不用动的     
* 10.local.properties：就是用来指定本机的Android SDK路径的 也是自动 也是不用动的   
* 11.settings.gradle：说白了现在有几个模块 就是说这里只有一个app模块 那就一个  反正也不用改 自动的   

![图片](https://github.com/pawNku/image.inGithub/blob/master/1.3.4(3).png?raw=true)     
* 1.build：就是用来自动生成一些 编译时的文件 只不过内容更加的复杂    
* 2.libs：就是一些第三方的依赖 在这个目录下的jar包会自动的加入到构建目录下    
* 3.androidTest：用来测试用例的 给项目一些自动化的测试  
* 4.java：不解释哦    
* 5.res：资源文件哦 图片有drawable 布局layout 字符串values    
* 6.AndroidManifest.xml：配置文件 比如所有的组件都要在这里注册 比如添加权限   
* 7.test：给项目的另一种自动测试的方式    
* 8..gitignore：还是个忽略文件 用于将app模块里指定的文件排除在版本控制之外   
* 9.app.iml：还是给IDEA宣布主权用的 不用管    
* 10.build.gradle：app模块的gradle构建脚步 会指定项目构建就是build相关的配置   
* 11.proguard-rules.pro：就是代码混淆规则啦
```
public class BaseActivity extends AppCompatActivity {
我们项目中的所有的活动都必须继承AppCompatActivity或者它的子类 才能拥有活动的特性 而AppCompatActivity是Activity的子类   
```

## 1.3.5 详解项目中的资源   
![图片](https://github.com/pawNku/image.inGithub/blob/master/1.3.5.png?raw=true)     
* mipmap都是用来放应用图标的 而values都是用来字符串样式颜色的  而hdpi xhdpi等等就是分辨率的高低放图片的一般情况下自己放xxhdpi就行  
```
<resources>
    <string name="app_name">ActivityLifeCycle</string>
</resources>
代码中：R.string.hello_world
XML中：@string/hello_world
```

## 1.3.6 详解build.gradle文件   
> 不同于Eclipse AS是用Gradle来构建项目的 是一个非常优秀的构建工具 是用领域特定语言DSL来声明的  而不是辣鸡XML
![图片](https://github.com/pawNku/image.inGithub/blob/master/1.3.6.jpg?raw=true)     
* repositories：就是仓库 这个里声明了jcenter的配置 其实就是一个代码托管仓库 其实很多开源的android项目都会托管在jcenter上面 所以这样我们就可以很high的引用各种的jcenter项目了    
* dependencies中的classpath中声明了一个Gradle 因为其实Gradle只是一个很好的构建工具但是不仅仅是给Android的 所以要用一个android的插件来做声明 最后的就是版本号  
* 一般不用动 除非是添加全局的项目构建 
![图片](https://github.com/pawNku/image.inGithub/blob/master/1.3.6(2).jpg?raw=true)  
* 首先第一行 有两种选择：.application是表示这是个应用程序模块可以直接玩 .library表示这是一个库模块只能依赖于别的application来玩  
* android闭包中 首先1.compileSdkVersion翻译哎就是编译版本 24为SDK也就是7.0的SDK buildToolsVersion项目构建工具的版本  defaultConfig这个闭包就是更多细节的配置 applicationId 项目包名后期可以修改 minSdkVersion项目最低兼容的版本 targetSdkVersion表示在该目标版本上已经充分无敌了 versionCode 也就是当前的项目的版本号在生成安装文件的时候很重要  接下来是buildTypes闭包-->生成安装文件的相关配置 这里其实有两个闭包 debug和release 前者是测试版本的安装配置 后者是正式版本的 前者一般可以省略  minifyEnabled是否对代码混淆 proguardFiles混淆的规则 getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'前者在SDK下是所有项目通用的混淆规则 而后者是在项目的根目录下的 里面是特有的混淆规则  还有最后一个dependenies 这里就是用来指定当前项目所有的依赖关系 包括本地依赖 库依赖 和远程依赖 compile fileTree-->本地依赖 compile-->远程依赖 testCompile-->就是一个测试库的依赖   

## 1.4.1 Log   
* Log中第一个参数是tag一般传入当前的类名用于过滤的 第二个参数是msg用来打印具体的内容   
* 可以通过过滤器 过滤tag   
* 搜索是搜索 msg中的关键字

## 2.2.3 在AndroidManifest中注册    
![图片](https://github.com/pawNku/image.inGithub/blob/master/2.2.3.png?raw=true)  
* .MainActivity是缩写 在最外层的<manifest>中已经通过package指定了包名是"com.example.activitylifecycle"  所以注册活动的时候可以省略   
* 主活动:
  ```
  <intent-filter>
                <action android:name="android.intent.action.MAIN"/>

                <category android:name="android.intent.category.LAUNCHER"/>
  </intent-filter>
  ```   
  
* 还可以使用android：label来指定活动的标题栏的内容 不仅会成为标题栏中的内容 还会成为启动器中应用程序显示的名称   

## 2.2.5 在活动中使用Menu  
> 因为这里是手机没有太多的地方 所以一手弹出菜单项就很好  
* 使用：1.res->New->Directory 新建文件夹 2.然后menu文件夹->New->Menu resource file 然后再main.xml中如下   
```
<?xml version="1.0" encoding="utf-8"?>
<menu xmlns:android="http://schemas.android.com/apk/res/android">
    <item
        android:id="@+id/add_item"
        android:title="Add"/>
    
    <item
        android:id="@+id/remove_item"
        android:title="Remove"/>

</menu>
```
* 这里创建了两个菜单项 <item>就是每个具体的菜单项 id就是唯一的标识符 title就是名称    
* 回到Activity中重写 crtl + O   
  
  ```
  @Override
    public boolean onCreateOptionsMenu(Menu menu) {
        getMenuInflater().inflate(R.menu.main,menu);
        return true;
    }
  ```
  
  * inflate第一个参数制动哪个资源文件来创建菜单 第二个参数用于指定我们的菜单项将添加到哪个Menu对象中 最后返回的true表示允许显示出     * 开始用了不仅仅是看：继续重写onOptionsItemSelected      
  
  ```
  @Override
    public boolean onOptionsItemSelected(MenuItem item) {
        switch (item.getItemId()){
            case R.id.add_item:
                Toast.makeText(this, "", Toast.LENGTH_SHORT).show();
                break;
            case R.id.remove_item:
                Toast.makeText(this, "", Toast.LENGTH_SHORT).show();
                break;
            default:
        }
        return true;
    }
  ```
* 通过item.getItemId()来判断点击的是哪个菜单项 并且加上对应的逻辑     

## 2.3.2 使用隐式Intent   
> 说白了不告诉你直接打开哪个活动 而是定义了一系列的action和category 这样通过匹配来开启对应的Activity   
* 所以我们要将活动加上一些<intent-filter> 代表当前活动可以被什么样的调用   
  ![图片](https://github.com/pawNku/image.inGithub/blob/master/2.3.2.png?raw=true)   
  
* 说白了 图中的是用来放被 被 被 被 被启动的那个activity的   
* action 表示可以享有哪些action 而category 表明了Intent中还能带有个category   
* 然后在主动方 开始隐式的设置一些action和category    
![图片](https://github.com/pawNku/image.inGithub/blob/master/2.3.2(2).png?raw=true)    
* 这里没有category是因为我上面传递的是Default默认的 而startActivty这个方法就已经将这个category传递进来了    
* Intent中只能有一个action但是却可以有多个category    
```
btn.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                Intent intent = new Intent("com.example.activity.ACTION_START");
                intent.addCategory("com.example.activity.MY_CATEGORY");
                startActivity(intent);
            }
        });
```    
* 如果没有程序响应会崩溃报错    

## 2.3.3 更多隐式Intent的用法  
* 可以通过setData把一个Uri对象传递进去 指定这个Intent操作的数据 而这些数据以字符串的形式传入到Uri.parse方法中解析得到  
```
btn.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                Intent intent = new Intent(Intent.ACTION_VIEW);
                intent.setData(Uri.parse("http://www.baidu.com"));
                startActivity(intent);
            }
        });
```   
* 对应的在被启动的活动中可以通过<data>标签来指定当前活动能够响应什么类型的数据   

![图片](https://github.com/pawNku/image.inGithub/blob/master/2.3.3.png?raw=true)  
```
<activity android:name=".MainActivity">
            <intent-filter>
                <action android:name="android.intent.action.MAIN"/>
                <category android:name="android.intent.category.LAUNCHER"/>
                <data android:scheme="http"/>
            </intent-filter>
        </activity>
```
* 这样这个活动也可以响应一个打开网页的Intent了     

## 2.3.4 向下一个活动传递数据   
* 一句话putExtra()方法 可以暂存在Intent中 然后在新启动的中在Intent取出即可  
```
btn.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                String data = "数据哦";
                Intent intent = new Intent(MainActivity.this, NormalActivity.class);
                intent.putExtra("extra",data);
                startActivity(intent);
            }
        });
```   
* putExtra()第一个参数是键key用来标识的 而data才是真正的值    
```
public class NormalActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.normal_layout);
        Intent intent = getIntent();
        intent.getStringExtra("extra");
    }
}
```   
* 取的时候记得按类型取就行了   

## 2.3.5 返回数据给上一个活动 
* 传递给新的 也可以同样返回给旧的  很稳   
```
btn.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
               Intent intent = new Intent(MainActivity.this,NormalActivity.class);
               startActivityForResult(intent,1);
            }
        });
```
* 同样启动新的活动 这里用的是startActivityForResult 第二个参数是请求码用于在之后的回调判断数据的来源   
![图片](https://github.com/pawNku/image.inGithub/blob/master/2.3.5.png?raw=true)   
* intent一样的putExtra 但是这里用了setResult来专门给旧的返回数据的 依旧还是键值对 key和value 而key一般只有RESULT_OK和RESULT_CANCELED  最后一定记得finish记得摧毁了   
* 接着在旧的也就是之前的进行回调了onActivityResult    
```
@Override
    protected void onActivityResult(int requestCode, int resultCode, Intent data) {
        switch (requestCode){
            case 1:
                if(resultCode == RESULT_OK){
                    String value = data.getStringExtra("key");
                }
                break;
            default:
        }
    }
```   
* 第一个参数请求码requestCode  用来标识是哪个活动返回的数据 刚刚上面有提 第二个参数 resultCode就是处理结果 第三个参数就是key用来返回value的

   





























