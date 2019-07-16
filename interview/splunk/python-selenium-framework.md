# Selenium Python Small Sample Project | Page Object Model POM

https://www.youtube.com/watch?v=BURK7wMcCwU

selenium

```
pip install selenium
```

html test runner

```
pip install html-testRunner
```

show one library

```
pip show selenium
```

check if broken

```
pip check selenium
```

文件结构

* Pages
* Tests
  * login.py

```python
from selenium import webdriver
import time

driver = webdriver.Chrome(executable_path=<chrome path>)
driver.implicity_wait(10)
driver.maximize_window()

driver.get(url)
driver.find_element_by_id("xxx").send_keys("xxx")

driver.find_element_by_id("xxx").click()

driver.find_element_by_link_text("xxx").click()

driver.close()
driver.quit()
```

step 2

```python
import unittest

class LoginTest(unittest.TestCase):
  
  @classmethod
  def setUpClass(cls):
    cls.driver = webdriver.Chrome(executable_path=<chrome path>)
    cls.driver.implicity_wait(10)
    cls.driver.maximize_window()
  
  def test_login_valid(self):
    self.driver.get(url)
    self.driver.find_element_by_id("xxx").send_keys("xxx")
    self.driver.find_element_by_id("xxx").click()
    self.driver.find_element_by_link_text("xxx").click()
  
  @classmethod
  def tearDownClass(cls):
    cls.driver.close()
    cls.dirver.quit()

if __name__ == "__main__":
  unittest.main() # run with python login.py directly
```

```shell
python -m unittest login.py

```

pages

loginPage.py

```python
class LoginPage():
  
  def __init__(self, driver):
    self.driver = driver
    self.user_textbox_id = "xxx"
    self.password_textbox_id = "xxx"
    self.login_button_id = "xxx"
    
  def enter_username(self, username):
    self.driver.find_element_by_id(self.user_textbox_id).send_keys(username)
    self.driver.find_element_by_id(self.user_textbox_id).click()
    self.driver.find_element_by_link_text(self.user_textbox_id).click()
  
  def enter_password(self, password):
    
  def click_login(self):
    self.driver.find_element_by_id(self.login_button_id).click()
```

homePage.py

```python
import locators.... # replace locator

class HomePage():
  
  def __init_(self, driver):
    self,driver = driver
    self.welcome_link_id = "welcome"
    self.logout_link_linkText = "Logout"
    
  def click_welcome(self):
    self.driver.find_element_by_link_text(self.user_textbox_id).click()
```

login.py

```python
import unittest
from selenium import webdriver
import pages...

class LoginTest(unittest.TestCase):
  
  @classmethod
  def setUpClass(cls):
    cls.driver = webdriver.Chrome(executable_path=<chrome path>)
    cls.driver.implicity_wait(10)
    cls.driver.maximize_window()
  
  def test_login_valid(self):
    driver = self.driver
    driver.get(url)
    login = LoginPage(driver)
    login.enter_username("xxx")
    login.enter_password("xxx")
    login.click_login()
  
  @classmethod
  def tearDownClass(cls):
    cls.driver.close()
    cls.dirver.quit()

if __name__ == "__main__":
  unittest.main() # run with python login.py directly
```

locators.py

```python
class Locators():
  driver = driver
  user_textbox_id = "xxx"
  password_textbox_id = "xxx"
  login_button_id = "xxx"
  
```

解决包找不到

```python
import sys
import os
sys.path.append(os.path.join(os.path.dirname(__file__), "..", ".."))
```

HTML test runner

```python
import HtmlTestRunner

if __name__ = "__main__":
  unittest.main(testRunner=HtmlTestRunner.HTMLTestRunner(output='<output>'))
```

