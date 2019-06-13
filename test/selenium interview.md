# Selenium

[Selenium Interview Questions with Answers - Rahul Shetty](<https://www.youtube.com/watch?v=Hy7w-ls1cbc>)

## Part 1 - Selenium Tool Interview Questions

### Difference between get and navigate method in Selenium?

```
get("google.com") 
Wait until all the values are loaded. click elements may be failed.

navigate("google.com") can do back, forward, refresh
Hits the url and immediately start next step.
```

### Difference between quit and close methods in Webdriver?

- Both browser closed.
- Close - only close the browser on focus.
- Quit - all the browsers closed.

### What is implicit wait?

```java
driver.manage().Timeout().implicitwait(TimeUnit.seconds, 5);
```

- Beginning of test, define wait for 10 seconds. Apply to each step.
- When element is ready in 3 seconds, go to next step immediately.

### Difference between implicit and explicit wait?

target only to the specific step. Use together implicit and explicit

### In how many ways we can handle frames in the application using webdriver methods

Selenium cannot handle frame directly.

```java
driver.switchTo().frame(id); //id, name, frame webelements
```

### Code to handle 3 child window?

Selenium will be on first window - (which it opens)

```java
Set<String> s = Driver.getWindowHandles();
it = s.iterator();
String window1 = it.next();
String window2 = it.next();
String window3 = it.next();

Driver.switchTo().window(window2);
```

### How to handle https certifications?

```java
DesiredCapabilities cap = DesiredCapabilities.chrome();

// Set ACCEPT_SSL_CERTS variable to true
cap.setCapability(CapabilityType.ACCEPT_SSL_CERTS, true)
```

### Different type of locators present in webdriver?

Xpath, css, id, classname, linkText, name

### Write Syntax for xpath and CSS if id and tag are given

```
xpath syntax = //tagname[@id='value']
css = tagname[id=value]
```

### How to use contains regular expression to xpath

```
//tagname[contains(@id, 'value')]
```

### How to use regula expression to CSS?

```
Tagname[id*='value']
```

### What is the class available in selenium to handle dropdowns?

```
select
```

### What is the method to check if checkbox is selected?

```
Driver.findElement("locator").isSelected()
```

### How to validate if element is visible or hidden in webpages?

```java
Driver.findElement("locator").isDisplayed()
```

### How to get the count of similiar objects list in the web page

```java
Driver.findElement(By.className("value")).size()
```

### Importance of desiredcapabilities Mechanism

A class describes browser and os 

Run test parallelly, distribute across multiple machines/OS by Selenium Grid

### How to enter the text in caps lock?

```java
Driver.findElement(By.xpath("value")).sendKeys(keys.SHIFT, "hello");
```

### How to mouse over on the web element on page?

```java
Actions a = new Actions(driver);
a.moveToElement().build().perform();
```

### Methods to handle Java Alert?

```java
Driver.swithTo.Alert();
```

### How to get links count in the page

```java
Driver.findElement(By.tagName("a")).size();
```

### How to validate if we are navigated to child window successfully?

```java
Driver.getTitle();
```

### Difference between relative and absolute xpath

Absolute xpath - html/body - to actual element

relative xpath 

### Write down the sample xpaht syntax to handle parent from child object?

```
//parant/child
```

### What driver is must to run tests in Firefox browser?

Geckodriver

### What driver is must to run tests in chrome browser

chrome driver

### How do you set driver in Firefox and chrome drivers through script?

```java
System.setProperty("Webdriver.chrome.driver", path to chrome driver);
```

### Difference between find element and find elements

### List out any 2 methods available in explicit wait

```
visibilityOfElement located, 
PresenceofElement located, 
invisibilityofElementlocated
```

### How to take screenshots with selenium webdriver

```java
File src = ((TakesScreenshot)driver).getScreenshotAs(OutputType.File);
try {
    //copy to screenshot to desired location using copyFile
    FileUtils.copyFile(src, new file("c:/selenium/error.png"));
} catch (IOException e) {
    System.out.println(e.getMessage());
}
```

### How to hit enter from webdriver commands

```java
Driver.findElement(By(Locator).sendKeys(Keys.ENTER))
```



## Part 2 - Selenium Framework Interview Questions







## Part 3 - Core Java Interview Questions

