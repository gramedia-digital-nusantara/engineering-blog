JMeter Testing
##############

:date: 2017-06-13 10:20
:modified: 2017-06-13 18:40
:tags: JMeter, load test, automated test, performance test
:category: QA
:slug: jmeter-testing
:authors: Marco Hudaya, Monika Evelin
:summary: Getting started with JMeter to load testing

Intro
^^^^^
In order to achieve the target of 2000 request per second (10.000 concurrent users), we need to setup certain method to test if our code-architecture meet the criteria. For this reason, we use JMeter because it allows us to manipulate and simulate the scenario of large traffic request in short period of time.

JMeter Installation
^^^^^^^^^^^^^^^^^^^
Get JMeter here: `<http://jmeter.apache.org/download_jmeter.cgi>`_

JMeter is ‘installed’ by running jmeter.bat (Windows) or jmeter (Mac/Linux)

For Windows user, make sure to allow JMeter to access network

Test Plan Creation
^^^^^^^^^^^^^^^^^^
You can change Test Plan name  by click on Test Plan then change Name field.

    .. image:: /images/1_test_plan_rename.png
         :alt: TestPlan
         :width: 100%

* Making a thread

A thread represents a User, so Thread Group represents a group of Users. We can configure how the group behave in Thread Group configuration such as number of traffic, and time period. Add a new Thread Group by right-click on Test Plan → Add → Thread (Users) → Thread Group.

    .. image:: /images/2_add_thread_group.png
         :alt: ThreadGroup
         :width: 100%

You can setting configuration in Thread Properties.

    .. image:: /images/3_thread_properties.png
         :alt: ThreadGroupConfigs
         :width: 100%

Example:
  - Number of Thread (users) : 50
  - Ramp-Up Period : 10
  - Loop Count : 1

It means that there are 50 users loaded by JMeter  in 10 seconds, or we can say that every 5 users will be loaded after every 1 seconds (10 seconds / 50 users = 0.2 seconds).
Loop Count describes how many times your test plan will be executed.

* Sampler

Add a new Sampler, example HTTP Request by right-click on Thread Group → Add → Sampler → HTTP Request

    .. image:: /images/4_add_sampler.png
         :alt: SamplerAdd

    - Fill Server Name or IP (ex: www.google.com)
    - (Optional) fill Path (ex: /)

    .. image:: /images/5_setting_http_request.png
         :alt: HttpReqConf
         :width: 100%

* Listeners

To see the result you can use Listener, usually View Result Tree and Graph Result. Right-click on Thread Group (or Test Plan) → Add → Listener → choose Listener you want.

    .. image:: /images/6_add_listener.png
         :alt: ListenersAdd
         :width: 100%

* Running the Test

    - Run testing by clicking the “Start” button above (Note :  You must save the
      test plan project before running the test).

    .. image:: /images/7_run_testing.png
         :alt: RunTest
         :width: 100%

    - The green circle on the upper right- hand corner show that the test is
      running. When the test is done, the circle should be grey.
    - Go to View Result Tree to see the result.

    .. image:: /images/8_testing_result_1.png
         :alt: TestResult1
         :width: 100%

    .. image:: /images/9_testing_result_2.png
         :alt: TestResult2
         :width: 100%

There are green color and red color request displayed. Green color means that the request is executed successfully and becomes pass, red color means that there are some error during execution of request and becomes fail.

    - There is an example of Graph Results.

    .. image:: /images/10_graph_result.png
        :alt: ResultGraph
        :width: 100%

    - If you want to clear the result before running another test, just click the broom icon above.



Simulation Recording
^^^^^^^^^^^^^^^^^^^^
You can record test activity using Recording Controller.

* Set up the Firefox Browser
    - Open Tools → Options → Advanced → Network.
    - Select “Manual Proxy Configuration”
    - Set HTTP Proxy = Localhost and Port = 8080
    - If you use Chrome, you can also use Foxy Proxy

* Set up JMeter configuration
    - Add HTTP(S) Test Script Recorder to see the test result by right-click on WorkBench → Add → Non-Test Elements → HTTP(S) Test Script Recorder.
    - Port : 8080 (Port number must be same as the browser connection settings)

    .. image:: /images/20_add_recorder.png
         :alt: JmeterRecord1
         :width: 100%

    - Right-click on HTTP(S) Test Script Recorder → Add → Logic Controller → Recording Controller. The recorded steps will be saved here.

    .. image:: /images/21_add_recording_controller.png
         :alt: JmeterRecord2
         :width: 100%

* Record the test
    - Go to HTTP(S) Test Script Recorder, click “Start” button.

    .. image:: /images/22_run_testing.png
         :alt: StartRecord
         :width: 100%

    - Open browser, do the desired steps.
    - Steps should be displayed in the recording controller
    - Click STOP to terminate recording
    - You can clear previously recorded steps by clicking Clear All Record Samples

CSV Data for Variables
^^^^^^^^^^^^^^^^^^^^^^

If the scenario requires the test to be executed on multiple endpoints, or need variables with various value, we can use a CSV file as the data source for the test. To do so, we need to add CSV Data Set Config element into the test plan. CSV Data Set Config is the JMeter element that allows us to use external data source in CSV format. In this case, we will setup CSV file for testing the product detail page links individually.

* Add -> Config Element -> CSV Data Set Config
* Setup the configuration according to the data

    - Filename: the path to the CSV file (relative to the .jmx file, or use absolute path)
    - Variable Names: the variable name we will refer to in JMeter
    - Delimiter: set whether the file is , or ; separated
    - Recycle on EOF: set whether if the thread count still runs after EOF, starting from top again
    - Stop thread on EOF: set whether if the thread should stop if EOF is reached

    .. image:: /images/csvdatasetconf.png
       :width: 100 %
       :alt: CSVSetUp

Here we set up a CSV file for the product URL slug, and refer to the variable ‘products’. In the HTTP Request, we use the variable by calling ${products} in the requested URL.

    .. image:: /images/httpreqdata.png
       :width: 100 %
       :alt: CSVSetUp2

Running the Test from Server
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

To Be Updated....




