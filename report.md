# Report for assignment 3

This is a template for your report. You are free to modify it as needed.
It is not required to use markdown for your report either, but the report
has to be delivered in a standard, cross-platform format.

## Project

Name: Json Iterator

URL: https://github.com/dd2480-group14-2024/java

The project contains a fast and efficient JSON parser and an api with some useful functions. 

## Onboarding experience

Did it build and run as documented?
    
See the assignment for details; if everything works out of the box,
there is no need to write much here. If the first project(s) you picked
ended up being unsuitable, you can describe the "onboarding experience"
for each project, along with reason(s) why you changed to a different one.

1. How easily can you build the project? Briefly describe if everything worked as documented or not:
(a) Did you have to install a lot of additional tools to build the software?
We needed maven to clean install, build and run the project, which we have used in previous projects.

(b) Were those tools well documented?
No, it was not well documented. The documentation provided in link shows the application of this jsoniter, rather than building the project.

(c) Were other components installed automatically by the build script?
No, only dependencies of Maven

(d) Did the build conclude automatically without errors?
No. Initially errors appeared regarding a outdated plugin:
groupId: org.apache.maven.plugins
artifactId: maven-compiler-plugin
source & target: 1.6, updated to 1.8

After this update, the build tests failed

(e) How well do examples and tests run on your system(s)?
They give a list of errors in different test classes as listed below:
TestString
TestGson
TestAnnotation
TestAnnotationJsonCreator
TestAnnotationJsonIgnore
TestAnnotationJsonObject
TestAnnotationJsonProperty
TestAnnotationJsonWrapper
TestAnnotationJsonUnwrapper
TestArray
TestDemo
TestExisting
TestGenerics
TestMap
TestNested
TestObject
TestReadAny
TestSpiPropertyDecoder
TestList
TestCollection
TestGenerics

Tests Run: 710, Failures: 5, Errors: 148. Build failed

2. Do you plan to continue or choose another project?
We plan to continue on this project

## Complexity

1. What are your results for five complex functions?
   * Did all methods (tools vs. manual count) get the same result?
   * Are the results clear?

| Function                                       | Lizard | Teodor | William |
| ---------------------------------------------- | ------ | ------ | ------- |
| `IterImpl.readStringSlowPath`                  | 28     | 28     | 28      |
| `IterImplForStreaming.readStringSlowPath`      | 27     | 27     | 27      |
| `CodegenImplObjectStrict.genObjectUsingStrict` | 26     | 26     | 25      |
| `GsonCompatabilityMode.createDecoder`          | 24     | 24     | 21      |
| `CodegenImplNative.genReadOp`                  | 23     | 24     | 23      |

2. Are the functions just complex, or also long?
The functions are also long. Their respective lengths are 110, 104, 128, 111 and 77 lines.

3. What is the purpose of the functions?
The purpose of the functions is not documented. Overall they all seem to work with reading streams of JSon tokens in different ways.
   
5. Are exceptions taken into account in the given measurements?
Try/catch blocks increase the complexity by one. Other than that, exceptions have not been taken into account. If exceptions were taken into account, the CC would increase, as each exception would be seen as another branch.

6. Is the documentation clear w.r.t. all the possible outcomes?
No. The documentation is more or less non-existent.


## Refactoring

5 out of the 10 functions below needed to be refactored. An issue was created in the project management repo for each function and the group members assigned themselves to one function that they would refactor. 

#### Functions that need to be refactored
| CCN | length | location                                                                                                     |
| --- | ------ | ------------------------------------------------------------------------------------------------------------ |
| 28  | 110    | `IterImpl::readStringSlowPath@217-326@./src/main/java/com/jsoniter/IterImpl.java`                            |
| 27  | 104    | `IterImplForStreaming::readStringSlowPath@391-494@./src/main/java/com/jsoniter/IterImplForStreaming.java`    |
| 26  | 128    | `CodegenImplObjectStrict::genObjectUsingStrict@24-151@./src/main/java/com/jsoniter/CodegenImplObjectStrict.` |
| 24  | 111    | `GsonCompatibilityMode::createDecoder@335-445@./src/main/java/com/jsoniter/extra/GsonCompatibilityMode.java` |
| 23  | 77     | `CodegenImplNative::genReadOp@195-271@./src/main/java/com/jsoniter/CodegenImplNative.java`                   |
| 21  | 57     | `Parsed::parse@138-194@./src/main/java/com/jsoniter/spi/OmitValue.java`                                      |
| 20  | 50     | `IterImplForStreaming::readNumber@571-620@./src/main/java/com/jsoniter/IterImplForStreaming.java`            |
| 18  | 63     | `Config::updateBindings@394-456@./src/main/java/com/jsoniter/spi/Config.java`                                |
| 18  | 36     | `IterImplSkip::skip@19-54@./src/main/java/com/jsoniter/IterImplSkip.java`                                    |
| 18  | 62     | `Codegen::chooseImpl@120-181@./src/main/java/com/jsoniter/Codegen.java`                                      |
### `CodegenImplNative::genReadOp@195-271@./src/main/java/com/jsoniter/CodegenImplNative.java` 
This functions features quite a bit of logic to format the string to return and catch any exceptions that may occur in that process. The complexity can be reduced by about half by refactoring this logic to a new function.


Estimated impact of refactoring (lower CC, but other drawbacks?).
One drawback could be that the code becomes harder to read when logic is scattered in more places. The lack of tests also increases the risk that any bugs introduced by refactoring is not caught.

Carried out refactoring (optional, P+):
`CodegenImplNative::genReadOp@195-271@./src/main/java/com/jsoniter/CodegenImplNative.java`

### `CodegenImplObjectStrict::genObjectUsingStrict@24-151@./src/main/java/com/jsoniter/CodegenImplObjectStrict.`
This function was refactored by splitting it into two different functions, reducing the CC by about 50%. The downside of this is the same as for genReadOp, it feels a bit less readable when a function is split into two.

### `IterImplForStreaming::readNumber@571-620@./src/main/java/com/jsoniter/IterImplForStreaming.java`
This function was refactored by splitting it into multiple functions which reduced the complexity by about half. The drawback is that it can make the code harder to read as one would have to go to the helper functions to understand all the logic which could lead to more confusion because of context switching.

### `Parsed::parse@138-194@./src/main/java/com/jsoniter/spi/OmitValue.java`
**JODIE**
__Jodie__:
Function split into 3 separate functions to decrease CC of parse by 70%. Split into: parsePrimitive (to handle cases for primitive classes), parseWrapper(handle cases for non-primitive) and parse (logic for calling the above functions). Had all cases return defaultType as a variable, to be returned from parse in one line, rather than returning for each case.
Length and complexity of total code could not be decreased by large amount due to nature of code - many cases to consider, as each class has its own logic to handle.

### `IterImpl::readStringSlowPath@217-326@./src/main/java/com/jsoniter/IterImpl.java`
**LEO**
## Coverage

### Tools

In addition to our own tool we used JaCoCo to measure branch coverage on the project and on the specific methods. It was really easy to set up, just a matter of adding the plugin to the pom, then running the tests, and finally running mvn jacoco:report to generate the results in a viewable format. The tool was very well documented but we did not have to read much of it as it was so easy to integrate into the maven project.

### Your own coverage tool

[Java Branch Coverage DIY](https://github.com/dd2480-group14-2024/java/tree/feature/issue-3/branch-coverage-diy)

The tool we implemented is really simple. For each function that we measured, we created a hashset that holds the id:s of the visited branches. In the functions, at each branching point we just make sure to add the id to the specific hashset. In the end, after all tests have been run the results are written to five txt files in the results/ directory.

The tool supports if, else if, else, switch, for, while, ... 

### Evaluation

1. How detailed is your coverage measurement?

The total number of branches and the total number of visited branches is presented along with a percentage showing the branch coverage. We also print out which branches was visited by their id:s.

2. What are the limitations of your own tool?

Well, having to manually go through the functions and find all branches is one big limitation as its time consuming and error prone. It also means that the source code has to be changed in order to measure coverage which is ugly. Ternary operators are not handled but could always be rewritten as if else if needed very easily. It would also be annoying if the program had to be modified or refactored in any way, this would require us to go through and insert new id:s everywhere and it would just be a mess.

3. Are the results of your tool consistent with existing coverage tools?

The results are somewhat consistent with existing coverage tools but not 100%.

## Coverage improvement

Test cases added:

__Teodor Morfeldt Gadler__:[Link to tests](https://github.com/dd2480-group14-2024/java/blob/feat/add-test-cases/src/test/java/com/jsoniter/TestWhatIsNext.java)
* `testWhatIsNextBoolean`
* `testWhatIsNextInteger`
* `testWhatIsNextFloat`
* `testWhatIsNextArray`

Branch coverage before: n/a

Branch coverage after: n/a

__William Nordwall__:[Link to tests](https://github.com/dd2480-group14-2024/java/blob/feat/add-test-cases/src/test/java/com/jsoniter/TestWhatIsNext.java)
* `testWhatIsNextInvalid`
* `testWhatIsNextLong`
* `testWhatIsNextNegativeLong`
* `testWhatIsNextNull`

Branch coverage before: n/a

Branch coverage after: n/a

__Leo Vainio__: [Link to tests](https://github.com/dd2480-group14-2024/java/blob/feat/add-test-cases/src/test/java/com/jsoniter/TestIterImpl.java)
* `testReadStringSlowPathEscapedb`
* `testReadStringSlowPathEscapedn`
* `testReadStringSlowPathEscapedf`
* `testReadStringSlowPathEscapedr`

Branch coverage before: 40%

Branch coverage after: 50%

Before adding these tests, the test suite did not cover all the possible escape characters in the `IterImpl.readStringSlowPath` function so I added a few tests to see that the function handles different escape characters in a correct way. 

__Luna Chen__:
* `testReadSimpleInteger`
* `testReadFloatingPointNumber`
* `testReadBufferExpansionNeeded`
* `testReadNonNumericCharactersTermination`

__Jodi:__
* `test_parseBooleanTypeWithTrueString`
* `test_parseBooleanTypeWithFalseString`
* `test_parseIntegerTypeWithZeroString`
* `test_parseFloatTypeWithZeroString`
* `parseDoubleTypeWithZeroString`

## Self-assessment: Way of working

Current state according to the Essence standard: In Place

Was the self-assessment unanimous? Any doubts about certain items?
The self-assessment was mostly unanimous. However, there could be a few doubts regarding the "Working Well" state, particularly about whether our adaptation of practices and tools suits our current context perfectly. Although we are consistent in our approach, there's room to better tailor our practices to specific project needs.

How have you improved so far?
When we first started, we didn't have basic principles we aligned on but by establishing rules to follow like java naming principles and using issue trackers we've been able to make significant progress. Initially, setting up communication channels, work distribution methods, and development protocols required deliberate effort. Over time, these elements have become second nature, facilitating smoother collaboration and task tracking. The creation and adherence to branch and commit conventions have particularly enhanced our code management efficiency and transparency. We've also been using our group chat consistently to ask questions and set up meetings.

Where is potential for improvement?
We could probably improve upon our communication even further as we only ended up meeting once synchronously for this assignment although we communicated asynchronously throughout. This would ensure we are all on the same page and reduce the number of questions asked. We also never established a leadership structure but so far it has worked well to split up tasks evenly among group members so everyone has a solid idea of their tasks for the assignment.

## Overall experience

What are your main take-aways from this project? What did you learn?
Our main take-aways from this project include understanding code complexity metrics and the importance of test coverage. We learned about cyclomatic complexity, which measures the number of linearly independent paths through a program's source code. Understanding these metrics helps in assessing the maintainability and potential testing effort required for a codebase. This project highlights the importance of achieving high test coverage to minimize bugs and improve software reliability. Tools like Lizard for complexity metrics and Jacoco for test coverage provided us with practical skills in measuring and improving code quality. The task of refactoring complex functions to reduce their complexity teaches valuable lessons in software design and architecture as well.

Is there something special you want to mention here?
