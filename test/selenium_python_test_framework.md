## 环境搭建

###  Selenium环境搭建

```
python install selenium
```

python chrome driver 放在 python 安装目录下

`/usr/local/bin`

```
from selenium import webdriver
driver = webdriver.Chrome()
driver.get("http://www.baidu.com")
```

### 需求分析

![](/Users/jizheng/Library/Application Support/typora-user-images/image-20190818200314624.png)

### 设计用例

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-08-19%20at%207.05.57%20AM.png?raw=true)

### 检查页面正确

* title

```
from selenium.webdriver.support import expected_conditions as EC

EC.title_contains()
EC.title_is()
```

* 页面元素

### 定位方式

```
driver.find_element_by_id()
driver.find_element_by_class_name()
```

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-08-19%20at%207.23.15%20AM.png?raw=true)

### expected_condition

```
EC.visibility_of_element_located(element) // 是否可见
EC.prsence_of_element_located() // 是否在 dom 中

locator = (By.CLASS_NAME, "controls")
WebDriverWait(driver, 10).until(EC.visibility_of_element_located(locator))
```

### random

```
import random

''.join(random.sample('123456789abcdefg', 5)) # 合并随机字符数组
```

### 验证码

```
pip install Pillow
```

```
driver.save_screenshot("e:/xx.png")
code_element = driver.find_element_by_id("sss")
left = code_element.location['x']
top = code_element.location['y']
right = code_element.size['width'] + left
height = code_element.size['height'] + top
```

### 配置文件

```
pip install Configparser

class ReadIni:
	def __init__(self, filename = none):
		self.config = self.load_ini(filename)
		
	def load_ini(self, filename):
		cp = configparser.ConfigParser()
		cp.read(filename)
		return cp
		
	def get_value(self, key):
		data = self.config.get(key)
		return data
```

### 根据配置定位

```
class FindElement:
	def __init__(self, driver):
		self.driver = driver
		
	def get_element(self, key):
		read_ini = ReadIni()
		data = read_ini.get_value(key)
		by = data.split('>')[0]
		value = data.split('>')[1]
		try:
			if by == 'id':
				return self.driver.find_element_by_id(value)
		except:
			return none
```

### 批量执行 Case

```
suite.add...
```

```
class RunCase(unittest.TestCase):
	def test_case01(self):
		case_path = os.path.join(os.getcwd(), 'case)
		suite = unittest.defaultTestLoader.discover(case_path, 'unittest_*.py')
		unittest.TextTestRunner().run(suite)
		
if __name__ == '__main__':
	unittest.main()
```

### 出错截图

```
for method_name, error in self._outcome.errors:
	if error:
		case_name = self._testMethodName
		file_path = os.path.join(os.getcwd() + "/report/" + case_name + '.png')
		self.driver.save_screenshot()
```

### 数据驱动

```
pip install ddt
```

```
		@ddt.data(
        ['a', 'b'],
        ['c', 'd']
    )
    @ddt.unpack
    def test_ddt_1(self, a, b):
        print(','.join([a, b]))
```

### Excel

```
import xlrd

				self.data = xlrd.open_workbook(excel_path)
        self.table = self.data.sheet_by_name("data")
        self.rows = self.table.nrows
        for i in range(self.rows):
          col = self.table.row_values(i)
          result.append(col)
          
        data = self.table.cell(3, 4).value
```

```
pip install xlutils
```

