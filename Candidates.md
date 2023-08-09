[[_TOC_]]

###  **What is Automated Test Candidate Guide?**

Automated Test Candidate Guide is a set of standards and procedures across QA teams follow by the principle of **Why**, **What** and **How** to propose a testcase to be implemented and included in Automated test suites. A good test automation should:

- add value to the applications under the test 
- be baked into Agile Software Development Product Life Cycle
- enable team (CDS) to get strong ROI from implementing and maintaining it

The general principle of test automation describes as the following:
 
- High impact/Low risk
- Stable/Reliable
- Repeatable
- Focus/Informative
- Maintainable /Cost efficient
  
 
### **When Should a Test Case Be Automated?**

A test case should be considered as automation candidate if it has the following qualifications:

- The test reflects high impact to: 
   - Business and customers
   - System
   - Other functional areas
- The test is repetitive; (Test will be run in every build/releases in future)
- The test is time consuming, automating it saves time significantly.
- The test is subject to human error;
- The test has low risk of being exposed by security, legal, operation and other critical measurement;
- The test is maintainable and sustainable in the long term. 

### **What is a good automation candidate:** 

A test scenario consists a lot of complex and repetitive manual steps that requires to run in every release regression , such as " Design a cake as identified user, check the order confirmation in Email and cancel the order"

### **When should a Test Case Not Be Automated ?**

The following are some signs that a test may be better as a manual test:

- UX tests
- Exploratory tests
- Content validation (image, style, color, text), automated tests should focus on testing the functionality, not content.
- The test requires data setup and the expected result is highly data dependent (Sitecore, Fusion92, E-recipe, BOGO deals, promo banners)
- The test is only run for one or few releases (A bug fix, unless it needs to be tested in every future release)
- The test is validating similar functionality that's already been covered by other tests.(Determined by the underlying API)
- The test does not produce a predictable and consistent result (the development of the feature is still undergoing)  
- The test is easier to be manually "eyeballed" than to be validated by automation script.
- The test cannot be 100% automated should not be automated at all (Test involves in phone verification)
- Edge case or false positive testcase (The test scenario that customers normally would not repeatedly do)

### **Automation candidate prioritization criteria and metrics**

Combining above principles, the proposed automation candidate will placed into three categories: 

   1. Must have (high priority item, will be refined for next release)
   2. Nice to have (medium to low priority, but worth automating, will be placed to backlog for future refinement) 
   3. Will not automate (Not following Automated Test Candidate Principle due to cannot/will not be automated) 

###**Process to have automation candidate added to typical automation suites:**

1. QA lead from feature teams propose the test candidate(could be testcases or small functional area) in form of PBI/Feature in any time of a sprint.
2. Automation team will evaluate the proposed candidates based on above principles and take the following steps:
   - Must have / Nice to have, place it into backlog for refinement (Friday)
   - Will not automate
   - Request additional information about the test scenarios
3. QA lead who provides the automation candidate will be invited to join (optional) the following sprint activities through out the agile cycle:

    - Backlog refinement (for test scenario details and clarification)
    - Sprint Planning (for prioritization and regression coverage notification)
    - Sprint Review (for reviewing the scripts and collecting feedback) 

###**What information should be provided in automation candidate PBI/Feature ?**

Providing the following information will help get automated test scripts implemented as quick and stable as possible:

-    Reference of the original Dev/QA PBI (related link)
-    Screenshot in comparison between new and old functional area in which the test takes place
-    BDD steps or manual test scenario steps in Acceptance Criteria 
-    Prerequisites to execute the testcase such as: testing data, search term, product URL
-    Feature flag info: Is it behind flag ? When the flag be on ? What percentage of audience

**Sample Automation Candidate PBI**

![screenshot PBI.PNG](/.attachments/screenshot%20PBI-e4a99605-7807-44bb-8fba-238d1dbf9b7a.PNG)

###**End Goal**

Test Automation team implement and maintain a large number of test suites to support QA for all feature teams, this number is increasing each release. 

Every time we create an automated test script, we are committing to maintain it for the rest of its lifecycle. 
Successfully follow this guide will greatly improve our QA process in the role of Agile fast release cycle and reduce communication cost across the CDS organization. 

The final decision on automation candidate prioritization will also be impacted by the release decision from management.



