# Appium

https://www.youtube.com/playlist?list=PLUDwpEzHYYLsx_2JFNBMITjHqTnuszhb_

## IOS Setup

* download appium mac dmg

* download appium java client jars

* download selenium java

* Xcode

  * developer.apple.com

* UI catalog App

  * github.com/appium/ios-uicatalog

  open project in xcode

### start up appium server

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-28%20at%209.51.25%20AM.png?raw=true)

### scripting

eclipse - create java project - add dependencies

* appium java client
* selenium jar
* ...

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-28%20at%209.59.24%20AM.png?raw=true)

```java
List <WebElement> items = driver.findElementsByXPath("//...");
for (WebElement it: items) {
  System.out.println(it.getText());
}
driver.findElementByAccessibilityId("Alert Views").click();
driver.quit();
```

 