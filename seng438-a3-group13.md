**SENG 438 - Software Testing, Reliability, and Quality**

**Lab. Report #3 – Code Coverage, Adequacy Criteria and Test Case Correlation**

| Group \#: 13      |     |
| -------------- | --- |
| Student Names: |     |
| Tien Dat Johny Do               |     |
| Tommy Dinh               |     |
| Stuart Johnstone               |     |
| Sina Tavakol Moghaddam               |     |



# 1 Introduction

In this lab, we are asked to explore the technique of white-box coverage criteria. Unlike assignment 2 where unit tests had to be made without knowing the source code(black-box testing), white-box testing allows us to create unit tests based on the source code of a class or method. The idea of white-box testing is to let the test developer write tests that will ensure that they execute most of the source code. The three types of coverage that we are exploring through our white-box testing are: Statement Coverage, Branch Coverage, and Condition Coverage. Statement Coverage can be seen as how much of the source code the unit tests cover. We can think of it as “how many lines of code do the unit tests cover?”. Branch Coverage can be seen as how many different branch paths were executed. This mainly refers to if-statements where there are multiple paths that an if-statement can go down. Condition Coverage focuses on evaluating whether all possible outcomes of a Boolean expression have been tested. In other words, condition coverage measures the extent to which each individual condition (or combination of conditions) in a decision statement has been exercised during testing.

# 2 Manual data-flow coverage calculations for Range.combine() and DataUtilities.calculateColumnTotal() methods
## Range.combine()
### Data Flow Graph
![image](https://user-images.githubusercontent.com/81772838/222837455-ff0fab1d-5dba-4c1a-8339-7c684321d631.png)

### Def-Use Sets Per Statement
DEF(1) = {range1, range2}, USE(1) = {range1}\
DEF(2) = {}, USE(2) = {range2}\
DEF(3) = {}, USE(3) = {range2}\
DEF(4) = {}, USE(4) = {range1}\
DEF(5) = {l}, USE(5) = {range1,range2}\
DEF(6) = {u}, USE(6) = {range1, range2}\
DEF(7) = {}, USE(7) = {l, u}

### DU-Pairs Per Variable
![image](https://user-images.githubusercontent.com/81772838/222838705-d1d67d89-8bbf-43a3-938b-a53332e91ea0.png)

### Test with Pair Cover
![image](https://user-images.githubusercontent.com/81772838/222842162-b9f902e3-fc72-4202-9eae-967bede2e1e5.png)

### DU-Pair Coverage Calculation
Total c-use: 8 \
Total p-use: 2\
Infeasible p-use: 0\
Infeasible p-use: 0\
Covered c-use: 8\
Covered p-use: 2\
DU-Pair coverage = (covered c-use + covered p-use) / ((total c-use + total p-use) - (infeasible c-use + infeasible p-use))\
DU-Pair coverage = (8 +2) / ((8 + 2) - (0 + 0))\
DU-Pair Coverage = 100%

## DataUtilities.calculateColumnTotal()
### Data Flow Graph
![image](https://user-images.githubusercontent.com/81772838/222837514-fa35b7d2-4bfa-4aa5-a9a6-48022683371a.png)

### Def-Use Sets Per Statement
DEF(1) = {data, column, validRows}, USE(1) = {data}\
DEF(2) = {total}, USE(2) = {}\
DEF(3) = {}, USE(3) = {total}\
DEF(4) = {total}, USE(4) = {}\
DEF(5) = {rowCount}, USE(5) = {data}\
DEF(6) = {v}, USE(6) = {v, validRows}\
DEF(7) = {row}, USE(7) = {validRows, v}\
DEF(8) = {}, USE(8) = {row, rowCount}\
DEF(9) = {n}, USE(9) = {data, row, column}\
DEF(10) = {}, USE(10) = {n}\
DEF(11) = {total}, USE(11) = {n}\
DEF(12) = {v}, USE(12) = {}\
DEF(13) = {}, USE(13) = {total}

### DU-Pairs Per Variable
![image](https://user-images.githubusercontent.com/81772838/222838810-6cbb3416-74c0-4897-b577-b39dd294d8b7.png)

### Test with Pair Cover
![image](https://user-images.githubusercontent.com/81772838/222862355-a2e30ac3-d9f1-4037-b5f6-48a4ccba282f.png)

### DU-Pair Coverage Calculation
Total c-use: 9\
Total p-use: 7\
Infeasible p-use: 2\
Infeasible p-use: 0\
Covered c-use: 7\
Covered p-use: 7\
DU-Pair coverage = (covered c-use + covered p-use) / ((total c-use + total p-use) - (infeasible c-use + infeasible p-use))\
DU-Pair coverage = (7 +7) / ((9 + 7) - (2 + 0))\
DU-Pair Coverage = 100%



# 3 A detailed description of the testing strategy for the new unit test

Our test plan involves initially identifying the current branch, statement, and condition coverage in our test files. Once this assessment is complete, we will proceed to select different methods that we have not previously tested and develop individual test cases to evaluate if we can enhance our coverage metrics as well as creating more test cases for methods previously evaluated in lab 2. After determining how to improve each coverage type, we will distribute the necessary number of test cases among ourselves and perform pair-programming(Tommy/Tien Dat & Stuart/Sina), similar to previous labs. In this lab, we will use EclEmma, which involves the use of statement, branch, and method coverages, having method coverage replacing condition coverage.

# 4 A high level description of five selected test cases you have designed using coverage information, and how they have increased code coverage
## Range.combine()
Range.combine() was a function that was not tested in assignment 2, which is why when we run our initial coverage test on the method, there was 0% statement coverage.
![image](https://user-images.githubusercontent.com/81772838/222869403-9cf3663f-c85d-46cc-9bcf-0143565f9d83.png)

### combineTestOne()
Running our first test on Range.combine() with combineTestOne() allowed us to set our arguments where we chose range1 to be not null and range2 to be null. This test authorized the source code to call one of the return functions inside of the second if-statement. This resulted in the increase of statement coverage from 0% to 23.1%.
![image](https://user-images.githubusercontent.com/81772838/222869536-18887d62-c700-4076-b9e2-5cd6356dfa42.png)

### combineTestTwo()
Running our second test on Range.combine() with combineTestTwo() allowed us to set our arguments where we chose range1 to be null and range2 to be not null. This test authorized the source code to call the other return functions inside of the first if-statement. This resulted in the increase of statement coverage from 23.1% to 30.8%.
![image](https://user-images.githubusercontent.com/81772838/222869739-baa8df3d-7d8c-4a61-be4a-75e72bf43925.png)

### combineTestThree()
The last test for Range.combine() being combineTestThree() allowed us to set our arguments where we chose range1 to be a normal Range object (not null) and range2 to be a normal Range object (not null). This test authorized the source code to access the untouched code, which accessed the last return statment. This resulted in the increase of statement coverage from 30.8% to 100%
![image](https://user-images.githubusercontent.com/81772838/222869940-1ed7f800-ac65-485c-9100-a9046a225f5a.png)

## Range.equals()
Range.equals() was already a method that was previously tested in assignment 2. Before the start of white-box testing, this method had a statement coverage of 84.6%.
![image](https://user-images.githubusercontent.com/81772838/222870181-c09d3854-d6c1-41d1-a187-14f2b5890faf.png)

### equalsDifferentObjectTest()
The first additional test case used was equalsDifferentObjectTest(). This tested how the method would react if the input argument accepted an object that was not a Range object. By passing in an int object instead, we are able to cover the first return statement inside of the method. The result of this test caused the statement coverage of Range.equals() to go from 84.6% to 92.3%.
![image](https://user-images.githubusercontent.com/81772838/222870368-9bcdfeed-afda-426a-a473-7d5ff9e8ff6d.png)

### equalsSameLowerDifferentUpper()
The second additonal test case used was equalsSameLowerDifferentUpper(). This tested how the method would react if the Range object it was compared to had the same lower bound, but a different upper bound. With this test we are able to reach the second return statement of the method. The result of this test caused the statement coverage of Range.equals() to go from 84.6% to 92.3%.
![image](https://user-images.githubusercontent.com/81772838/222870474-810379f1-8dae-40fa-9d54-0f6786f2f640.png)


# 5 A detailed report of the coverage achieved of each class and method (a screen shot from the code cover results in green and red color would suffice)
## Statement, Branch, and Method Coverage
### DataUtilities Statement Coverage 
![image](https://user-images.githubusercontent.com/81772838/222799703-932bc04b-4e8d-4279-ab2b-06274c4a614c.png)

### DataUtilites Branch Coverage
![image](https://user-images.githubusercontent.com/81772838/222799816-f4ed2d22-3001-48e0-b90f-95ca2de02ec6.png)

### DataUtilities Method Coverage
![image](https://user-images.githubusercontent.com/81772838/222800050-a1c535a5-4f3a-4f5d-be10-362ece9b08b9.png)


### Range Statement Coverage
![image](https://user-images.githubusercontent.com/81772838/222640308-b78efef7-943c-4932-ae90-e4faaf5f9fb5.png)

### Range Branch Coverage
![image](https://user-images.githubusercontent.com/81772838/222640362-37a2b9a0-3b39-4a14-81b0-fcc76ce7eb99.png)

### Range Method Coverage
![image](https://user-images.githubusercontent.com/81772838/222640404-a71c461f-10dd-48e6-b119-54dd2a3ba024.png)

## Code Coverage
### DataUtilities
![image](https://user-images.githubusercontent.com/81772838/222805819-99625bf8-ebef-496c-b45b-d9a471558822.png)
![image](https://user-images.githubusercontent.com/81772838/222805852-294529d3-15e8-4151-8e8c-9936adc7a68f.png)
![image](https://user-images.githubusercontent.com/81772838/222805898-d29bb8b6-6785-4f88-b47b-6bb73fd6572b.png)
![image](https://user-images.githubusercontent.com/81772838/222805943-95a705c2-b7fa-436b-8c5b-90ecbe0d1465.png)
![image](https://user-images.githubusercontent.com/81772838/222805971-f596247b-e8d7-46e5-a343-39976e01cd0c.png)
![image](https://user-images.githubusercontent.com/81772838/222806028-18ec7e98-041a-4849-b9f9-727f690f3d87.png)
![image](https://user-images.githubusercontent.com/81772838/222806048-ee839e65-df3e-458f-93ea-a4e07b22a6b1.png)


### Range
![image](https://user-images.githubusercontent.com/81772838/222804763-5a9b6f98-57fd-4b65-90e6-709539c62e17.png)
![image](https://user-images.githubusercontent.com/81772838/222804815-eb922890-53fb-4c27-96fd-489e03e397b9.png)
![image](https://user-images.githubusercontent.com/81772838/222804843-4ceadf5b-cc76-4874-8468-237be22b2669.png)
![image](https://user-images.githubusercontent.com/81772838/222804879-42bee853-e197-4255-9dd0-feec3b50d346.png)
![image](https://user-images.githubusercontent.com/81772838/222805003-481a7160-a42b-4b15-a63b-d16ecc6a8891.png)
![image](https://user-images.githubusercontent.com/81772838/222805029-1699bfe3-f4f2-4a9f-ad18-b700e592a5e0.png)
![image](https://user-images.githubusercontent.com/81772838/222805071-3997f8fc-2d50-4122-a1b1-bb9db479bd19.png)
![image](https://user-images.githubusercontent.com/81772838/222805119-7750ab48-d927-4c66-8972-9f64b8d172ea.png)
![image](https://user-images.githubusercontent.com/81772838/222805157-02b955e5-5345-483f-8789-cb80f0755eaf.png)
![image](https://user-images.githubusercontent.com/81772838/222805196-d58dddc5-9021-4f1e-8252-8cad87e4b5bb.png)
![image](https://user-images.githubusercontent.com/81772838/222805221-0d72e484-f0b5-43ee-a74f-fb35d1825ab2.png)

See [9] for more information on why our statement coverage did not reach 90%.

# 6 Pros and Cons of coverage tools used and Metrics you report
EclEmma facilitated our examination of test case coverage, and its compatibility with mock objects enabled us to retain most of our initial test cases while conducting white-box testing to improve functionality. The coverage data proved to be a valuable asset in assessing the effectiveness of our test cases. Additionally, EclEmma provided a graphical display of code coverage across the source code, simplifying the identification of areas requiring more coverage. The tool was easy to use, straightforward, and beneficial. However, EclEmma's coverage options are restricted, meaning that we had to focus on method coverage rather than condition coverage.

# 7 A comparison on the advantages and disadvantages of requirements-based test generation and coverage-based test generation.

Requirements-based test generation has several advantages. It ensures that the software system satisfies the specified requirements, which is crucial in meeting the user's needs. It also helps to verify that all features, functions, and behaviors of the system meet the user's needs. However, there are some limitations to this approach. For instance, it may not cover all parts of the codebase or test all possible scenarios, leading to incomplete testing.

Coverage-based test generation, on the other hand, has its own advantages. It provides a systematic approach to testing by focusing on specific parts of the codebase that need to be covered, ensuring that all parts of the codebase are executed and evaluated. This approach can also help identify untested paths, conditions, and exceptions in the code. However, coverage-based test generation does not guarantee that the system is meeting the user's needs or requirements. Additionally, it can result in a large number of test cases, many of which may not be relevant or useful.

In conclusion, both requirements-based test generation and coverage-based test generation have their benefits and drawbacks. The choice of approach depends on the specific goals and objectives of the testing effort, as well as the resources available. Ultimately, it is essential to ensure that testing is comprehensive and effective in identifying and mitigating potential issues in the software system.

# 8 A discussion on how the team work/effort was divided and managed

To ensure that everyone in our group gained experience in coverage testing and to prevent overlapping work, we divided the tasks among ourselves. This entailed assigning specific functions to each team member, with those not involved in writing the report taking on additional functions. This approach proved effective as it allowed us to utilize coverage tools while delegating work efficiently. Upon completion of individual assignments, we conducted pair-testing to ensure the quality of our work. Tommy and Tien Dat formed one pair, while Stuart and Sina formed the other.

# 9 Any difficulties encountered, challenges overcome, and lessons learned from performing the lab

One of the greater difficulties encountered by our group within this lab is with infeasible code. Some of the methods were poorly written which practically made it impossible to write unit tests that would trigger specific parts of the code. For example, in the Range class there are many instances where methods check to see if the lower bound is greater than the upper bound and if so, should throw an exception. This can be seen in methods such as getUpperBound(), getLowerBound() and getLength(). What made this so difficult was that the exception would already be caught when the Range object gets instantiated, meaning that there is no possible way to pass a Range object with incorrect parameters to the methods stated above. This caused our group not being able to meet the 90% statement coverage mark since we were only able to achieve 86.6% statement coverage for the Range class. Similarly, DataUtilities also had methods that had code that was infeasible to access. For example, calculateColumnTotal() had a part where the variable “total” was set, which was immediately followed by an if-statement. This made it impossible to test the other branch of the if-statement since we were not able to change the value of “total”. This resulted in our DataUtilities class only getting a statement coverage of 89.1%. The biggest lesson learnt from this challenge is that if code is poorly written, it might be impossible to test. This means that not everything can be tested for so we must ensure that the programs or methods we write are written at a high quality and make logical sense.

# 10 Comments/feedback on the lab itself

Completing this assignment proved to be an effective method to familiarize with setting up code coverage. Despite encountering some difficulties while setting up, the assignment's overall structure was straightforward to comprehend. To achieve more precise testing of a package, it would be preferable to provide its source code already within the package instead of a compiled version that needs to be imported to the IDE. This approach would enhance compatibility across IDEs and provide an opportunity for individuals to gain experience with setting up complex Java projects.
