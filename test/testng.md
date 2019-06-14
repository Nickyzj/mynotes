# TestNG

[TestNG Framework](https://www.youtube.com/playlist?list=PLFGoYjJG_fqp25buwscrsKA5q8qsLsuUy)

```java
	@BeforeSuite
    public void setUp() {
        System.out.println("BeforeSuite - Setup system property for chrome");
    }

    @BeforeTest
    public void login() {
        System.out.println("BeforeTest - Login method");
    }

    @BeforeClass
    public void launchBrowser() {
        System.out.println("BeforeClass - Launch chrome browser");
    }

    @BeforeMethod
    public void enterURL() {
        System.out.println("BeforeMethod - Enter URL");
    }

    @Test
    public void sum() {
        int a = 10;
        int b = 20;
        Assert.assertEquals(30, a + b);
    }

    @AfterMethod
    public void logout() {
        System.out.println("AfterMethod - Logout");
    }

    @AfterClass
    public void closeBrowser() {
        System.out.println("AfterClass - Close browser");
    }

    @AfterTest
    public void deleteAllCookies() {
        System.out.println("AfterTest - Delete all cookies");
    }

    @AfterSuite
    public void generateTestReport() {
        System.out.println("AfterSuite - Generate test report");
    }
```



```java
@Test(priority = 1) // Control test sequences
@Test(priority = 1, groups = "Test")
@Test(priority = 2, groups = "Google", dependsOnMethods = "googleTitleTest") // Dependency failed then test after failed (skipped).
@Test(invcationCount = 10) // Run 10 times
@Test(timeOut = 2000) // 2 seconds
@Test(expectedExceptions=NumberFormatException.class) // Exception no fail
```

[Idea+TestNg配置test-output输出](https://www.cnblogs.com/veitch-623/p/6192601.html)

```java
        Assert.assertEquals(title, "Google", "message to output if failed");
        Assert.assertTrue(b, "Message");

```

```xml
<!DOCTYPE suite SYSTEM "http://testng.org/testng-1.0.dtd">
<suite name="Test Maven Suite">
    <test verbose="2" name="Test Maven Testing">
<!--        <packages>-->
<!--            <package name="com.test.*"></package>-->
<!--        </packages>-->
        <classes>
            <class name="com.test.GoogleTest"/>
        </classes>
    </test>
</suite>
```

test-output

```xml
			<plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-surefire-plugin</artifactId>
                <version>3.0.0-M3</version>
                <configuration>
                    <suiteXmlFiles>
                        <suiteXmlFile>src/main/resources/testng.xml</suiteXmlFile>
                    </suiteXmlFiles>
                    <reportsDirectory>./test-output</reportsDirectory>
                </configuration>
            </plugin>
```

testng.xml paramters

```xml
<!DOCTYPE suite SYSTEM "http://testng.org/testng-1.0.dtd">
<suite name="Test Maven Suite">
    <test verbose="2" name="Test Maven Testing">
        <!--        <packages>-->
        <!--            <package name="com.test.*"></package>-->
        <!--        </packages>-->
        <parameter name="url" value="http://www.google.com"/>
        <parameter name="username" value="testid"/>
        <classes>
            <class name="com.test.GoogleTest"/>
        </classes>
    </test>
</suite>
```

```java
 	@Test(priority = 1, groups = "Google")
    @Parameters({"url", "username"})
    public void googleTitleTest(String url, String username) {
        String title = driver.getTitle();
        System.out.println(title);
        Assert.assertEquals(title, "Google", "message to output if failed");
        System.out.println(String.format("url: %s", url));
        System.out.println(String.format("username: %s", username));
    }

	public void googleTitleTest(@Optional("http://baidu.com") String url, String username) 
```

## Dataprovider

