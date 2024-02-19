# Report for assignment 3

This is a template for your report. You are free to modify it as needed.
It is not required to use markdown for your report either, but the report
has to be delivered in a standard, cross-platform format.

## Project

Name:

URL:

One or two sentences describing it

## Onboarding experience

Did it build and run as documented?
    
See the assignment for details; if everything works out of the box,
there is no need to write much here. If the first project(s) you picked
ended up being unsuitable, you can describe the "onboarding experience"
for each project, along with reason(s) why you changed to a different one.


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
4. Are exceptions taken into account in the given measurements?
Try/catch blocks increase the complexity by one. Other than that, exceptions have not been taken into account. If exceptions were taken into account, the CC would increase, as each exception would be seen as another branch.

5. Is the documentation clear w.r.t. all the possible outcomes?
No. The documentation is more or less non-existent.


## Refactoring

Plan for refactoring complex code:
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



Estimated impact of refactoring (lower CC, but other drawbacks?).

Carried out refactoring (optional, P+):

git diff ...

## Coverage

### Tools

Document your experience in using a "new"/different coverage tool.

How well was the tool documented? Was it possible/easy/difficult to
integrate it with your build environment?

### Your own coverage tool

Show a patch (or link to a branch) that shows the instrumented code to
gather coverage measurements.

The patch is probably too long to be copied here, so please add
the git command that is used to obtain the patch instead:

git diff ...

What kinds of constructs does your tool support, and how accurate is
its output?

### Evaluation

1. How detailed is your coverage measurement?

2. What are the limitations of your own tool?

3. Are the results of your tool consistent with existing coverage tools?

## Coverage improvement

Show the comments that describe the requirements for the coverage.

Report of old coverage: [link]

Report of new coverage: [link]

Test cases added:

git diff ...

Number of test cases added: two per team member (P) or at least four (P+).

## Self-assessment: Way of working

Current state according to the Essence standard: ...

Was the self-assessment unanimous? Any doubts about certain items?

How have you improved so far?

Where is potential for improvement?

## Overall experience

What are your main take-aways from this project? What did you learn?

Is there something special you want to mention here?
