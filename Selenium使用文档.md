# Selenium使用文档

```
Selenium官网: https://www.selenium.dev/
```

## 环境配置

### 1.Python

1. 安装python运行环境

2. 配置python环境变量

3. 配置pip环境变量

4. 使用pip安装selenium模块

   ```
   python -V	查看python版本
   pip -V	查看pip版本
   pip install selenium	使用pip安装selenium模块
   ```

### 2.PyCharm开发工具

前往JetBrains官网下载

### 3.浏览器驱动

下载与浏览器版本对应的浏览器驱动

```
Chrome浏览器驱动官网: https://chromedriver.chromium.org/home
```

下载完解压缩存放再任意位置，并且配置到环境变量Path中

------

## Selenium WebDriver和浏览器的通信

1. Selenium的每一条脚本或http请求都会被创建并发送给浏览器驱动driver
2. 浏览器驱动包含一个HTTP Server用于接受请求
3. 浏览器驱动接受到请求就会根据请求操控对应的浏览器
4. 浏览器执行具体的操作步骤
5. 浏览器返回步骤执行结果给HTTP Server
6. HTTP Server就会将结果返回给Selenium的脚本，就会在控制台看见结果或者报错

**WebDriver 通信协议：**JSON Wire protocol

**通信数据格式：**JSON

------

## Selenium 4.2 属性

#### element 定位

```
find_element([定位方式],"[名称]")		取唯一或list集合的首个
find_elements([定位方式],"[名称]")		取list集合
```

| 定位方式             | 描述                                  |
| :------------------- | :------------------------------------ |
| By.ID                | 通过元素的id定位，唯一                |
| By.CLASS_NAME        | 通过元素的class定位，集合             |
| By.TAG_NAME          | 通过元素的标签(ul,li.....)定位，集合  |
| By.CSS_SELECTOR      | 通过css选择器                         |
| By.XPATH             | 通过XPATH定位                         |
| By.LINK_TEXT         | 通过link_text定位，超链接里的完整文本 |
| By.PARTIAL_LINK_TEXT | 通过link_text定位，超链接里的部分文本 |
| By.NAME              | 通过name定位                          |


```python
driver.find_element(By.ID,"id")	# 通过id定位元素
driver.find_element(By.CLASS_NAME,"classname")	# 通过类名定位元素
driver.find_element(By.TAG_NAME,"li")	# 通过html标签名称定位元素
driver.find_element(By.CSS_SELECTOR,"#id .classname")	# 通过css选择器
driver.find_element(By.XPATH,"xpath")	# 通过XPATH定位
driver.find_element(By.LINK_TEXT,"超链接里的完整text文本")	# 通过link_text定位
driver.find_element(By.PARTIAL_LINK_TEXT,"超链接里的部分text文本")	# 通过link_text定位
driver.find_element(By.NAME,"name")	# 通过name定位
```



### WebDriver 属性

| #    | 属性                         | 属性描述         |
| ---- | ---------------------------- | ---------------- |
| 1    | driver.name                  | 浏览器名称       |
| 2    | driver.current_url           | 当前url          |
| 3    | driver.title                 | 当前页面标题     |
| 4    | driver.page_source           | 当前页面源码     |
| 5    | driver.current_window_handle | 窗口句柄         |
| 6    | driver.window_handles        | 当前所有窗口句柄 |

------

### WebDriver 方法

| #    | 方法                                | 方法描述                 |
| ---- | ----------------------------------- | ------------------------ |
| 1    | driver.forward()                    | 浏览器前进               |
| 2    | driver.back()                       | 浏览器后退               |
| 3    | driver.refesh()                     | 浏览器刷新               |
| 4    | driver.close()                      | 关闭当前窗口tab          |
| 5    | driver.quit()                       | 退出浏览器               |
| 6    | driver.switch_to.frame()            | 切换到frame              |
| 7    | driver.switch_to.alert              | 切换到alert警告框        |
| 8    | driver.switch_to.active_element     | 切换到当前具有焦点的元素 |
| 9    | driver.switch_to.window('窗口句柄') | 切换窗口                 |
| 10   | driver.switch_to.default_content()  | 切换到主文档             |

#### **driver.switch_to.alert**

在调用 driver.switch_to.alert 之前，必须确保页面上确实有一个警告框、确认框或提示框。如果没有，WebDriver 会抛出一个 NoAlertPresentException 异常。

```python
# 假设页面上有一个警告框  
alert = driver.switch_to.alert  
print(alert.text)  # 打印警告框的内容  
alert.accept()     # 关闭警告框

# 假设页面上有一个确认框  
alert = driver.switch_to.alert  
print(alert.text)  # 打印确认框的内容  
alert.accept()     # 点击确定按钮  
# 或者  
alert.dismiss()    # 点击取消按钮

# 假设页面上有一个提示框  
alert = driver.switch_to.alert  
alert.send_keys('your_text')  # 在提示框中输入文本  
print(alert.text)             # 打印提示框的内容（包括用户输入的文本）  
alert.accept()               # 关闭提示框  
# 或者  
alert.dismiss()              # 不保存输入并关闭提示框
```

#### driver.switch_to.active_element

首先，你需要确保页面上有一个元素具有焦点。这通常是因为用户已经与该元素进行了交互

```python
# 获取当前具有焦点的元素  
active_element = driver.switch_to.active_element

# 假设active_element是一个输入框，你可以这样输入文本  
active_element.send_keys('Hello, World!')  
  
# 或者获取它的属性，比如ID  
element_id = active_element.get_attribute('id')  
print(element_id)  
  
# 或者检查它是否是某个特定的元素类型  
if active_element.tag_name == 'input':  
    print('焦点元素是一个input标签。')
```

#### driver.switch_to.window('窗口句柄')

```python
# 在拥有两个或以上的窗口
window_handles = self.driver.window_handles # 获取所有窗口句柄的list集合
        i = 0;
        while i != 3:	# 遍历循环切换窗口
            for w in window_handles:
                self.driver.switch_to.window(w)
                sleep(0.5)
            i += 1
```



------

### WebElement 属性

| #    | 属性     | 属性描述   |
| ---- | -------- | ---------- |
| 1    | id       | 标示       |
| 2    | size     | 宽高       |
| 3    | rect     | 宽高和坐标 |
| 4    | tag_name | 标签名称   |
| 5    | text     | 文本内容   |

```python
语法格式:
driver.find_element(By.ID,"id").[属性]
driver.find_element(By.ID,"id").size		元素宽高
```

------

### WebElement 方法

| #    | 方法                               | 方法描述        |
| ---- | ---------------------------------- | --------------- |
| 1    | send_keys('值')                    | 设置值          |
| 2    | clear()                            | 清空内容        |
| 3    | click()                            | 单击            |
| 4    | get_attribute('属性名')            | 获得属性值      |
| 5    | is_selected()                      | 是否被选中      |
| 6    | is_enabled()                       | 是否可用        |
| 7    | is_displayer()                     | 是否显示        |
| 8    | value_of_css_property('css属性名') | 获取css的属性值 |

```python
语法格式:
driver.find_element(By.ID,"id").[方法]
driver.find_element(By.ID,"id").send_keys('值')		设置值
```

------

### Select 标签下拉列表

| #    | 方法/属性              | 方法/属性 描述 |
| ---- | ---------------------- | -------------- |
| 1    | select_by_value()      | 根据值选择     |
| 2    | select_by_index()      | 根据索引选择   |
| 3    | select_by_visible_text | 根据文本选择   |
| 4    | select_by_value        | 根据值反选     |
| 5    | select_by_index        | 根据索引反选   |
| 6    | select_by_visible_text | 根据文本反选   |
| 7    | deselect_all           | 反选所有       |
| 8    | options                | 所有选项       |
| 9    | all_selected_options   | 所有选择选项   |
| 10   | first_selected_option  | 第一个选择选项 |

------

## 各场景操作步骤

### 使用驱动实例开启会话

```
driver = webdriver.Chrome()  谷歌浏览器
```

### form表单测试

1. 定位表单元素
2. 输入测试值
3. 判断表单元素属性
4. 获得表单元素属性
5. 提交表单进行验证

### checkbox和radio

```python
    # 直接点击元素选择，is_selected判断元素是否选择
    def test_checkbox(self):
        swimmingEle = self.driver.find_element(By.NAME,"swimming")
        readingEle = self.driver.find_element(By.NAME,"reading")
        if not swimmingEle.is_selected():
            swimmingEle.click()
        if not readingEle.is_selected():
            readingEle.click()

    def test_radio(self):
        self.test_checkbox()
        genderEleList = self.driver.find_elements(By.NAME,"gender")
		
        # radio有排它性，选一个另一个就会取消选择
        genderEleList[0].click()
        sleep(0.7)
        genderEleList[1].click()

        self.driver.find_element(By.ID, "submit").click()
        sleep(0.7)
        self.driver.switch_to.alert.accept()  # 点击确定按钮

    def __del__(self):
        sleep(2)
        self.driver.quit()

```

