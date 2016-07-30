# Android-Code
Android实用代码片段

## 网上收集
+ [Android实用代码片段整合](http://www.eoeandroid.com/thread-570919-1-1.html?_dsign=907052b3)
+ [36个Android开发常用代码片段](http://www.phpxs.com/code/1001775/)

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
  
+ String添加文字  
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
