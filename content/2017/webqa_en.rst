Web Functionality Testing with Selenium
#######################################

:date: 2017-06-16
:modified: 2017-06-16
:tags: functionality test, selenium, unittest, python
:category: QA
:slug: web-automated-test
:authors: Marco Hudaya, Monika Evelin
:summary: Web automated testing

Intro
^^^^^

To maintain quality, it is required to check previous/other functionality with every feature release. For web apps, we can use Selenium to interact with webpage elements from the code. Selenium is a suite for web browser automation, commonly it used for automation in testing purposes, but not limited to that. Several routine tasks that requires web browser can also be automated. To control the interaction with the browser, we can use programming language like Java or Python, in this tutorial we will use the latter.
Java and Python also provides additional testing framework to work with. Java is JUnit, Python is unittest. Testing framework provides us with convenience in managing test cases, managing test executions, and reviewing test results.


Prerequisites
^^^^^^^^^^^^^
* Selenium server : from http://www.seleniumhq.org/download/ .
* Webdriver: either GeckoDriver or ChromeDriver
* For Java: newest version of JDK, Intelli J IDEA
* For Python: newest version of Python, PyCharm. Get PyCharm from https://www.jetbrains.com, better choose the Professional version.

Setup
^^^^^
* For this tutorial we will use Python. After installing Python and PyCharm, create a new project in PyCharm.

  Add new python file into the project

* Import unittest framework and selenium webdriver component into the project.

  Unittest framework consist of three major flow:

  - Setup: the configuration and instance is set up.
  - Test cases: the test scenario is defined and executed here.
  - Tear down: the instance is closed and tests terminate.

First, let’s set up the Setup and Tear down routines, in this case we will test against http://staging.gramedia.com.

As we can see in above example, the Chrome Driver path is supplied as argument in the Webdriver configuration in the SetupClass method.


First Test
^^^^^^^^^^

There is an example of  basic settings usually used before running any test.

In the base file.

.. code-block:: python

          import os
          from selenium import webdriver

          class ChromeDrivenMixin:

          BASE_PATH = "https://staging.gramedia.com"

          @classmethod
          def setUpClass(self):
                self.driver = webdriver.Chrome(os.environ.get("CHROME_DRIVER"))
                self.driver.get(os.environ.get("BASE_PATH"))
                self.driver.implicitly_wait(5)


Then in the testing file.

.. code-block:: python

       import unittest
       import re
       import time
       import os
       from base.test_drivers import ChromeDrivenMixin

       class FirstWebDriverTest(ChromeDrivenMixin, unittest.TestCase):
           def test_search_by_title(self):
               driver = self.driver
               search_box = driver.find_element_by_name("q")
               search_box.send_keys("pycon")
               search_box.send_keys(Keys.RETURN)
               assert "No results found." not in driver.page_source


          def tearDown(self):
              self.driver.close()




ChromeDrivenMixin is a class where base path and driver been setting up, so you just need to call that class when making a new test case / test file. (?)


There is an example for login test.

.. code-block:: python

    #click button Masuk, to go to Login Page from Home Page

    def test_click_Masuk(self)
        driver = self.driver
        #find button Masuk
        button_masuk = self.driver.find_element_by_css_selector("div.container div.row div.col-md-2 ul.nav.justify-content-end li.nav-item a.nav-link")
        try:
            button_masuk.click()
            time.sleep(2)
            print("button found")
            break
        except ElementNotVisibleException:
            print("button not visible:)
        except WebDriverException:
            print("click duplicate")

    #insert username and password

    def test_login(self)
       Try:
           #find input text for email
           email_box = self.driver.find.element_by_css_selector("div.content.fieldset div.input-box input#email.input-text.required-entry.validate-email")
           #find input texy for password
           password_box = self.driver.find.element_by_css_selector("div.content.fieldset div.input-box input#pass.input-text.required-entry.validate-password")
           email_box.send_keys("email@gmail.com") #insert username
           password_box.send_keys("password") #insert password

           button_login = self.driver.find_element_by_css_selector("div.buttons-set button#send2.button")
           button_login.click() #click button Log In
           time.sleep(2) #wait for some seconds before the another line is executed

     #if email or password wrong (get some text)
       Except WebDriverException:
           Error_message = self.driver.find_element_by_css_selector("div.account-login li.error-msg ul li span")
