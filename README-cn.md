# Ultra Pull To Refresh

这是现在已经停止维护的下拉刷新项目的替代方案。继承于ViewGroup可以包含任何View。功能比SwipeRefreshLayout强大。

使用起来非常简单。良好的设计，如果你想定制自己的UI样式，非常简单，就像给ListView加一个Header View那么简单。

支持 `API LEVEL >= 8`。

[APK下载](https://raw.githubusercontent.com/liaohuqiu/android-Ultra-Pull-To-Refresh/master/ptr-demo/target/ultra-ptr-demo.apk)

**使用eclipse 无法编译demo项目的同学看这里:  http://www.liaohuqiu.net/cn/posts/compile-ultra-ptr-in-eclipse/ Intellij IDEA / Android Studio请忽略**

* 先上两张StoreHouse风格的截图! 感谢 [CBStoreHouseRefreshControl](https://github.com/coolbeet/CBStoreHouseRefreshControl).
    <div class='row'>
        <img src='http://srain-github.qiniudn.com/ultra-ptr/store-house-string-array.gif' width="300px" style='border: #f1f1f1 solid 1px'/>
        <img src='http://srain-github.qiniudn.com/ultra-ptr/store-house-string.gif' width="300px" style='border: #f1f1f1 solid 1px'/>
    </div>

* 5.0 Material 风格 2014-12-09 新增。**阴影效果，gif图看起来有些失真，看demo吧！**
    <div class='row'>
        <img src='http://srain-github.qiniudn.com/ultra-ptr/material-style.gif' width="300px"/>
    </div>

* **支持所有的View**: 

    ListView, GridView, ScrollView, FrameLayout, 甚至 TextView.
    <div><img src='http://srain-github.qiniudn.com/ultra-ptr/contains-all-of-views.gif' width="300px" style='border: #f1f1f1 solid 1px'/></div>

* 支持各种下拉刷新交互.
    * 下拉刷新(iOS风格)
        <div><img src='http://srain-github.qiniudn.com/ultra-ptr/pull-to-refresh.gif' width="300px" style='border: #f1f1f1 solid 1px'/></div>

    * 释放刷新(经典风格)
        <div><img src='http://srain-github.qiniudn.com/ultra-ptr/release-to-refresh.gif' width="300px" style='border: #f1f1f1 solid 1px'/></div>

    * 刷新时，头部保持(新浪微博)

        <img src='http://srain-github.qiniudn.com/ultra-ptr/keep-header.gif' width="300px"/>

    * 刷新时，头部不保持(微信朋友圈)

        <img src='http://srain-github.qiniudn.com/ultra-ptr/hide-header.gif' width="300px" sytle='border: #f1f1f1 solid 1px'/>

    * 自动刷新，进入界面时自动刷新

        <img src='http://srain-github.qiniudn.com/ultra-ptr/auto-refresh.gif' width="300px" sytle='border: #f1f1f1 solid 1px'/></div>

# 使用方式

#### 中央库依赖

项目已经发布到了Maven中央库，包括`aar`和`apklib`两种格式。在Maven或者Gradle下可如下直接引入:

`pom.xml` 文件中

```xml
1.0.4
    <version>1.0.5</version>
</dependency>
```
或者

```xml
<dependency>
    <groupId>in.srain.cube</groupId>
    <artifactId>ultra-ptr</artifactId>
    <type>apklib</type>
    <version>1.0.5</version>
</dependency>
```

gradle / Android Studio
```
compile 'in.srain.cube:ultra-ptr:1.0.5@aar'
```

#### 配置

有6个参数可配置:

* 阻尼系数

    默认: `1.7f`，越大，感觉下拉时越吃力。

* 触发刷新时移动的位置比例

    默认，`1.2f`，移动达到头部高度1.2倍时可触发刷新操作。

* 回弹延时

    默认 `200ms`，回弹到刷新高度所用时间

* 头部回弹时间

    默认`1000ms`

* 刷新是保持头部

    默认值 `true`.

* 下拉刷新 / 释放刷新

    默认为释放刷新

##### xml中配置示例

```xml
<in.srain.cube.views.ptr.PtrFrameLayout
    android:id="@+id/store_house_ptr_frame"
    xmlns:cube_ptr="http://schemas.android.com/apk/res-auto"
    android:layout_width="match_parent"
    android:layout_height="match_parent"

    cube_ptr:ptr_resistance="1.7"
    cube_ptr:ptr_ratio_of_header_height_to_refresh="1.2"
    cube_ptr:ptr_duration_to_close="300"
    cube_ptr:ptr_duration_to_close_header="2000"
    cube_ptr:ptr_keep_header_when_refresh="true"
    cube_ptr:ptr_pull_to_fresh="false" >

    <LinearLayout
        android:id="@+id/store_house_ptr_image_content"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:background="@color/cube_mints_333333"
        android:clickable="true"
        android:padding="10dp">

        <in.srain.cube.image.CubeImageView
            android:id="@+id/store_house_ptr_image"
            android:layout_width="match_parent"
            android:layout_height="match_parent" />
    </LinearLayout>

</in.srain.cube.views.ptr.PtrFrameLayout>
```

### 也可以在java代码中配置

```java
// the following are default settings
mPtrFrame.setResistance(1.7f);
mPtrFrame.setRatioOfHeaderHeightToRefresh(1.2f);
mPtrFrame.setDurationToClose(200);
mPtrFrame.setDurationToCloseHeader(1000);
// default is false
mPtrFrame.setPullToRefresh(false);
// default is true
mPtrFrame.setKeepHeaderWhenRefresh(true);
```

## StoreHouse 风格

* 使用字符串, 支持A-Z, 0-7 以及 `-` `.`

```java
// header
final StoreHouseHeader header = new StoreHouseHeader(getContext());
header.setPadding(0, LocalDisplay.dp2px(15), 0, 0);

/**
 * using a string, support: A-Z 0-9 - .
 * you can add more letters by {@link in.srain.cube.views.ptr.header.StoreHousePath#addChar}
 */
header.initWithString('Alibaba');
```

* 使用资源文件中的路径信息

```java
header.initWithStringArray(R.array.storehouse);
```

资源文件 `res/values/arrays.xml` 内容如下:

```xml
<resources>
    <string-array name="storehouse">
        <item>0,35,12,42,</item>
        <item>12,42,24,35,</item>
        <item>24,35,12,28,</item>
        <item>0,35,12,28,</item>
        <item>0,21,12,28,</item>
        <item>12,28,24,21,</item>
        <item>24,35,24,21,</item>
        <item>24,21,12,14,</item>
        <item>0,21,12,14,</item>
        <item>0,21,0,7,</item>
        <item>12,14,0,7,</item>
        <item>12,14,24,7,</item>
        <item>24,7,12,0,</item>
        <item>0,7,12,0,</item>
    </string-array>
</resources>
```

# 处理刷新

通过`PtrHandler`，可以检查确定是否可以下来刷新以及在合适的时间刷新数据。

检查是否可以下拉刷新在`PtrDefaultHandler.checkContentCanBePulledDown`中有默认简单的实现，你可以根据实际情况完成这个逻辑。

```
public interface PtrHandler {

    /**
     * 检查是否可以执行下来刷新，比如列表为空或者列表第一项在最上面时。
     * <p/>
     * {@link in.srain.cube.views.ptr.PtrDefaultHandler#checkContentCanBePulledDown}
     */
    public boolean checkCanDoRefresh(final PtrFrameLayout frame, final View content, final View header);

    /**
     * 需要加载数据时触发
     *
     * @param frame
     */
    public void onRefreshBegin(final PtrFrameLayout frame);
}
```

例子:

```java
ptrFrame.setPtrHandler(new PtrHandler() {
    @Override
    public void onRefreshBegin(PtrFrameLayout frame) {
        frame.postDelayed(new Runnable() {
            @Override
            public void run() {
                ptrFrame.refreshComplete();
            }
        }, 1800);
    }

    @Override
    public boolean checkCanDoRefresh(PtrFrameLayout frame, View content, View header) {
        // 默认实现，根据实际情况做改动
        return PtrDefaultHandler.checkContentCanBePulledDown(frame, content, header);
    }
});
```


# License

Apache 2

# 联系方式和问题建议

* 微博: http://weibo.com/liaohuqiu 欢迎关注
* QQ 群: 271918140
* srain@php.net
* twitter: https://twitter.com/liaohuqiu
* blog: http://www.liaohuqiu.net
