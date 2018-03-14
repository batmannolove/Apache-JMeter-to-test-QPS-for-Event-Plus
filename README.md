


**Apache JMeter to test QPS for Event+**

Using Apache JMeter to handle 150 **QPS** (queries per second)

**Why do I use JUnit?**

Because I think testing is very important in industry so I tried to use JUnit to assure that my codes are working as expected.

**Why do I use JMeter?**

Because I think scaling is a very important metric and thus I used JMeter to evaluate the QPS of my server to get a sense of the scaling.

1. **Prerequisites:** Apache Jmeter

[**http://ftp.wayne.edu/apache//jmeter/binaries/apache-jmeter-3.3.zip**](http://ftp.wayne.edu/apache//jmeter/binaries/apache-jmeter-3.3.zip)

1. **Why write tests?**
2. To catch bugs (obvious, but not the most important)
3. To make you more productive
4. Reproduce bugs, and keep them from reappearing (your test case can be used later on for anyone modify or improve your code)
5. To improve design

- Unit tested code is more modular
- Tested APIs are more usable
- Design problems are exposed early （test myself.the funcitonality i added to the code library beore, will improve it before anyone use it.）

1. Tests do not rot like documentations.   Force you update it. easily  know input and output.
2. Helps you separate requirements from implementation (implementation is messy or changing all the time. The requirements if i want to know somehow at a point, i can know it in the test case.)
3. Example: A Small Unit Test using JUnit

![1](https://user-images.githubusercontent.com/6482545/37405380-e68720b4-276a-11e8-83f3-bf022bc8ee52.jpg)

1. **What are the different types of tests?**
2. Layered Testing

![2](https://user-images.githubusercontent.com/6482545/37405381-e6a2e7fe-276a-11e8-86cf-fa5e295ae737.jpg)

1. The Architecture of Laiproject



![3](https://user-images.githubusercontent.com/6482545/37405382-e6bb9984-276a-11e8-9acc-ad53537cb7f1.jpg)


1. The differences between each types

Unit Tests

- Test a component in isolation, control other factors.
- Are deterministic
- Usually map onto a single class
- Avoid dependencies on external resources (e.g. databases, files, network)
- Run quickly (&lt; 100ms)
- Can be run in any order
- Are the most important, and most neglected.

Integration Tests

- Test the interaction of a discrete set of components
- Test dependencies on external resources
- Run as quickly as possible ( &lt; 1 sec. if possible )

Functional Tests

- Test the entire system, end to end
- Though they sometimes stub out or fake &quot;difficult&quot; or non-performant layers
- Run as quickly as possible

1. **Who should write tests?**
2. Every SWE should write tests, not only the test engineers.
3. If you have tests on your resume, your interviewer will be surprised.
4. SWEs are responsible for writing unit tests and integration tests.
5. What does the test engineers do?

- They are mostly responsible for integration test and functional test. They focus on designing the infrastructure of the software and hardware testbed. And write the functional test based on the design doc.
- They are also responsible for monitoring the testbeds (all kinds of tests). If they notice test failures, they will identify the problem and issue bugs to corresponding team.

1. **What should we test?**
2. Positive cases (&quot;happy path&quot;)
3. Null cases
4. Edge cases
5. Failure cases
6. Anything that resulted in a bug being filed
7. Avoid tests that do not add additional confidence, e.g., do not test 1,2,3,4,5,6…
8. All of these test cases can be applied to algorithm interview as well

![4](https://user-images.githubusercontent.com/6482545/37405383-e6cb6602-276a-11e8-8b1b-212573357cf3.jpg)

1. **Expressive Test Cases**
2. Test one thing at a time

Avoid:

testMyClass

Instead:

testCannotContainSameElementTwice

testEndDateInPastNotAllowed

testAddNoDuplicatesAllowed

testSetEndDateCannotBeInPast

If cannot come up with a meaningful name, your unit test, or method, might cover too much

1. Tests can even serve as a form of documentation.

Test becomes a catalog of usage examples.

Unlike comments, the code will break if it&#39;s not updated.

1. **Create a JUnit Test in Eclipse**

 Simple test case for our RpcHelper class.

Download jsonassert-1.5.0.jar from

[**https://github.com/skyscreamer/JSONassert/releases**](https://github.com/skyscreamer/JSONassert/releases)

I would like a json object compare functionality which java doesn&#39;t provide. So I used  jsonassert

![5](https://user-images.githubusercontent.com/6482545/37405384-e6de8b4c-276a-11e8-9b20-38dc90836c21.jpg)

_drag jar file to lib folder._

In the Project Explorer, right click [**RpcHelper.java**](http://rpchelper.java/) -&gt; New -&gt; Others… -&gt; Java -&gt; JUnit -&gt; JUnit Test Case

For example to test getJSONArray function in rpchelper class



![6](https://user-images.githubusercontent.com/6482545/37405385-e6edf67c-276a-11e8-9e9e-8d59a541792c.jpeg)


1. Good input case 

![7](https://user-images.githubusercontent.com/6482545/37405386-e7066ba8-276a-11e8-95e4-22b69f9ce133.jpg)


Click the down arrow besides the Run button, and select Run As -&gt; JUnit Test.

 There is no need to run the tomcat server. Which is a benefit of Junit test.

We can also debug a Junit test



![8](https://user-images.githubusercontent.com/6482545/37405388-e717d992-276a-11e8-9db1-d2caa7440a5c.jpg)


 a green bar in the output, which shows all the tests has passed.

**What if a test fails?**

Try to modify the expected string in assertEquals, then run the RpcHelperTest again, you should see a red bar indicating there is something wrong.

1. Corner cases

Use the following test case to [**RpcHelperTest.java**](http://rpchelpertest.java/)


![9](https://user-images.githubusercontent.com/6482545/37405389-e72c72e4-276a-11e8-9a6b-4acfbb1169bd.jpg)

 
This test case includes empty case, single input case, etc.

1. **Benchmark**

Benchmarking is testing the performance of an system.

For web applications, performance can usually be measured by QPS (requests per seconds). Common interview question: how many servers do we need for this task?

For example Wikipedia seems to be 30000 to 70000 per second spread over 300 servers (100 to 200 requests per second per machine, most of which is caches). [[ **source**](http://stackoverflow.com/questions/373098/whats-the-average-requests-per-second-for-a-production-web-application)]

There are many benchmarking tools available. In this class we will use the widely-used **Apache Jmeter** to measure our website&#39;s QPS.

**JMETER**

1. Add a Thread Group to Jmeter test plan.

Right Click on Test Plan and Add -&gt; Threads (Users) -&gt; Thread Group

1. Next we will add a HTTP Request Sampler

Right click on Thread Group and Add -&gt; Sampler -&gt; HTTP Request



![10](https://user-images.githubusercontent.com/6482545/37405391-e73fb66a-276a-11e8-8cb3-401b95629f58.jpg)


Fill in the Server name as localhost, port number as 8080, and Path as

/Titan/search?user\_id=KT5RsjORnwTW6nhfKzMBLO8Da2u1&amp;lat=42.302159499999995&amp;lon=-83.0282224

1. Now to see the results as tables, we need to add a Listener &quot;View Results in Table&quot;

Right Click on HTTP Request and Add -&gt; Listener -&gt; View Results in Table

1. We can also add another Listener to see the summary report

Right Click on HTTP Request and Add -&gt; Listener -&gt; Summary Report



![11](https://user-images.githubusercontent.com/6482545/37405392-e752cba6-276a-11e8-82f4-fa3e460b5a94.jpg)


1. Now we can start generating the load for the server by going to the Thread Group section from the left panel.
2. Remember to comment out the login session related code.



![12](https://user-images.githubusercontent.com/6482545/37405395-e7630656-276a-11e8-8188-d8468284e68e.jpg)
![13](https://user-images.githubusercontent.com/6482545/37405396-e7731de8-276a-11e8-9ec4-d83e7d69557e.jpg)
![14](https://user-images.githubusercontent.com/6482545/37405397-e7833b38-276a-11e8-8867-2b399bde1c89.jpg)
![15](https://user-images.githubusercontent.com/6482545/37405398-e798737c-276a-11e8-9595-bf65d5f37f7a.jpg)
![16](https://user-images.githubusercontent.com/6482545/37405400-e7b547a4-276a-11e8-9aca-d39cf00723ad.jpg)
![17](https://user-images.githubusercontent.com/6482545/37405401-e7d0a620-276a-11e8-9a03-6631b464f960.jpg)


See 1000


![18](https://user-images.githubusercontent.com/6482545/37405402-e7f50380-276a-11e8-9dec-91eed5bb0a98.jpg)

![19](https://user-images.githubusercontent.com/6482545/37405403-e802fe18-276a-11e8-9ccc-358df60bc6ac.jpg)

The thumb rule to determine the QPS is to keep increasing the request per second to the system and find a saturation point where your throughput dramatically drops with the increase in response time.

From the Thread Group tab, I will increase the **concurrent users** starting with 100 and setting the **Ramp up period** to zero. We need to clear the outputs after each run.



![20](https://user-images.githubusercontent.com/6482545/37405404-e815ae14-276a-11e8-97e1-2b64de78d9b6.jpg)


1. Here is my summarized report of the experiment.



![21](https://user-images.githubusercontent.com/6482545/37405405-e8236c7a-276a-11e8-9812-15e2fb16da03.jpg)


We can see the **peak throughput** happens between 1000 and 2000 threads, so we can test more data points between 1000 and 2000 threads. The throughput will be around 150qps.

When I used 2500 threads, I got the following error, which means the memory size is my server&#39;s bottleneck:



![22](https://user-images.githubusercontent.com/6482545/37405406-e83366d4-276a-11e8-876d-64a1dbbcb8cc.jpg)


So QPS is not only determined by your code, it is also determined by the hardware, DB performance, network condition, etc. It needs to be measured from production.

**10. Other Test Topic**

1. A/B Test

A/B testing is when you test two (or more) different situations: situation A vs. situation B.

1. Alpha/Beta Test

**Alpha testing** is conducted within the organization and tested by representative group of end users at the developer&#39;s side and sometimes by Independent team of testing. **Beta testing** is conducted by the end users or other persons and they are not programmers, software engineers or testers.
