# Selenium Grid

Cross browser testing in parallel mode

one hub server, multiple nodes. JSON Wire/HTTP

DesiredCapabilities: win/FF/52, mac/safari/7, linux/chrome/31

RemoteWebDriver, WebDriver

geckodriver.exe

chromedriver.exe

IEDriver.exe



Selenium server jar file on both Hub and Node, same version

start server on hub

register a node with hub

code:

- Give the address/URL of HUB
- DesiredCap
- ChromeOptions

download Selenium Standalone Server jar file 3.8.1

```
java -jar selenium-server-standalone-3.8.1.jar -role hub
```

http://172.25.99.61:4444

```
java -Dwebdriver.chrome.driver="C:\Program Files (x86)\Google\Chrome\Application\chromedriver.exe" -jar selenium-server-standalone-3.141.59.jar -role node -hub http://172.25.99.61:4444/grid/register/ -port 5556
```

 New Maven project

name: GridSetupTest

pom.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>GridSetupTest</groupId>
    <artifactId>GridSetupTest</artifactId>
    <version>1.0-SNAPSHOT</version>

    <dependencies>
        <!-- https://mvnrepository.com/artifact/org.seleniumhq.selenium/selenium-java -->
        <dependency>
            <groupId>org.seleniumhq.selenium</groupId>
            <artifactId>selenium-java</artifactId>
            <version>3.141.59</version>
        </dependency>

    </dependencies>
</project>
```



```java
// Define Des Cap
        DesiredCapabilities cap = new DesiredCapabilities();
        cap.setBrowserName("chrome");
        cap.setPlatform(Platform.WIN10);

        // Chrome Option
        ChromeOptions options = new ChromeOptions();
        options.merge(cap);

        String hubUrl = "http://172.25.99.61:4444/wd/hub";
        WebDriver driver = new RemoteWebDriver(new URL(hubUrl) , options);

        driver.get("http://www.python.org");
        System.out.println(driver.getTitle());
```

