# Android-Code
Android实用代码片段

## 网上收集
+ [Android实用代码片段整合](http://www.eoeandroid.com/thread-570919-1-1.html?_dsign=907052b3)
+ [36个Android开发常用代码片段](http://www.phpxs.com/code/1001775/)

## 个人整理
+ 隐藏输入法键盘：

  ```java
  public void hideKeyboard(View view) {
      if (view != null) {
          InputMethodManager inputManager = (InputMethodManager) getSystemService(Context.INPUT_METHOD_SERVICE);
          inputManager.hideSoftInputFromWindow(view.getWindowToken(), InputMethodManager.HIDE_NOT_ALWAYS);
      }
  }
  ```
