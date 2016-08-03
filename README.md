# Android-Code
Android实用代码片段

## 网上收集
+ [Android实用代码片段整合](http://www.eoeandroid.com/thread-570919-1-1.html?_dsign=907052b3)
+ [36个Android开发常用代码片段](http://www.phpxs.com/code/1001775/)
+ [Android开发最佳实践-胡凯](http://hukai.me/android-dev-patterns/)

## 个人整理
+ 隐藏输入法键盘

  ```java
  public void hideKeyboard(View view) {
      if (view != null) {
          InputMethodManager inputManager = (InputMethodManager) getSystemService(Context.INPUT_METHOD_SERVICE);
          inputManager.hideSoftInputFromWindow(view.getWindowToken(), InputMethodManager.HIDE_NOT_ALWAYS);
      }
  }
  ```

+ 打印log
  ```java
  StackTraceElement st[] = Thread.currentThread().getStackTrace();
  for (int i = 0; i < st.length; i++) {
    android.util.Log.i("silion", "trace: " + st[i].toString());
  }
  android.util.Log.i("silion", "--------boundary--------");
  ```

+ 文字带下划线  
  String
  ```xml
  <resources>  
    <string name="hello"><u>phone: 1390123456</u></string>  
    <string name="app_name">MyLink</string>  
  </resources>
  ```
  
  Java
  ```java
  TextView textView = (TextView)findViewById(R.id.testView);
  textView.setText(Html.fromHtml("<u>"+"hahaha"+"</u>"));
  ```
  
+ EditText 去掉下划线
  ```java
  android：background="@null"
  ```
  
+ String添加文字(字符串格式化)  
  String
  ```xml
  <string name="hello">你好，我是%1$s。</string>
  ```
  Java
  ```java
  String.format(context.getString(R.id.hello), "silion")
  ```

+ 判断字符串是否为空(去掉首尾空格)
  ```java
  TextUtils.isEmpty(string.trim())
  ```
  
+ String中的部分文字设置成超链接  
  String
  ```xml
  <string name="silion_blog">这是<a href = "http://blog.csdn.net/xilove102">silion</a>的博客</string>  
  ```
  
  Java
  ```java
  TextView hyperlinkTextView = new TextView(this);  
  hyperlinkTextView.setText(Html.fromHtml(getResources().getString(R.string.silion_blog)));  
  hyperlinkTextView.setMovementMethod(LinkMovementMethod.getInstance()); 
  ```

+ 自定义ListView divider  
  drawable/divider_listitem.xml
  ```xml
  <insert xmlns:android=“http://schemas.android.com/apk/res/android"  
    android:insert="0dp">  
  
    <shape android:shape="rectangle">  
        <solid android:color="@color/ca" />  
    </shape>  
  </insert>  
  ```
  
  布局
  ```xml
  <ListView  
    android:id="@+id/listView"  
    android:layout_width="match_parent"  
    android:layout_height="wrap_content"  
    android:divider="@drawable/divider_listitem"  
    android:dividerHeight="2px" />  
  ```
  
+ URI
  ```java
  Log.d(TAG, "performActionLink, actionLink = " + "voc://view/main");  
  
  URI uri = null;  
  try {  
    uri = new URI(actionLink.trim());  
  } catch (URISyntaxException e) {  
    Log.e(TAG, e.getMessage(), e);  
  }  
  if (uri == null) {  
    return;  
  }  
  
  String scheme = uri.getScheme() != null ? uri.getScheme() : "";  
  String function = uri.getHost() != null ? uri.getHost() : "";  
  String path = uri.getPath() != null ? uri.getPath() : "";  
  if (path.length() > 1) {  
    path = path.substring(1);  
  }  
  ```
  
+ 定时重复执行Timer() and TimerTask
  ```java
  mViewPagerScrollTimer = new Timer();  
  mViewPagerScrollTimer.scheduleAtFixedRate(new TimerTask() {  
    @Override  
    public void run() {  
        mHandler.post(new Runnable() {  
            @Override  
            public void run() {  
            }  
        });  
    }  
  }, 5000, 5000);  
  ```
  
+ 字符串编码转换
  ```java
  new String(str.getBytes("iso8859-1"), "utf-8")
  ```
  
+ URL编码
  ```java
  URLEncode.encode(str, "UTF-8)
  ```
  
+ 获取状态栏高度
  ```java
  /**  
   * 用于获取状态栏的高度。  
   *  
   * @return 返回状态栏高度的像素值。  
   */  
  private int getStatusBarHeight() {  
    if (mStatusBarHeight == 0) {  
        try {  
            Class<?> clazz = Class.forName("com.android.internal.R$dimen");  
            Object object = clazz.newInstance();  
            Field field = clazz.getField("status_bar_height");  
            int x = (int) field.get(object);  
            mStatusBarHeight = getResources().getDimensionPixelSize(x);  
        } catch (Exception e) {  
            e.printStackTrace();  
        }  
    }  
    return 0;  
  }  
  ```

+ 播放声音(播放音乐)
  ```java
  public void playAudio(View view) {
      mMediaPlayer = new MediaPlayer();
      Uri uri = Uri.parse("android.resource://" + getPackageName() + "/" + R.raw.sample);
      switch (view.getId()) {
          case R.id.btVoiceCall:
              try {
                  mMediaPlayer.setDataSource(this, uri);
                  mMediaPlayer.setAudioStreamType(AudioManager.STREAM_VOICE_CALL);
                  mMediaPlayer.prepare();
              } catch (IOException e) {
                  e.printStackTrace();
              }
              break;
          case R.id.btMusic:
              try {
                  mMediaPlayer.setDataSource(this, uri);
                  mMediaPlayer.setAudioStreamType(AudioManager.STREAM_MUSIC);
                  mMediaPlayer.prepare();
              } catch (IOException e) {
                  e.printStackTrace();
              }
              break;
          default:
              break;
      }
        mMediaPlayer.start();
        mHandler.postDelayed(new Runnable() {
          @Override
          public void run() {
              if (mMediaPlayer.isPlaying()) {
                  mMediaPlayer.stop();
              }
              mMediaPlayer.release();
              mMediaPlayer = null;
          }
      }, 5000);
  }
  ```
