# Coach

## Describe an important project you've worked on

### Build automation framework from 0 - 1

#### project introduction

Quoting system. It provides a way for prospective buyers to see what costs would be for the BOM. This quotation will be made by the company using the information of the BOM, regarding the relevant elements that may affect the price, which includes:

* customer profile
* pricing engine
* materials information - category, vendor...

#### quoting system modules

* customer informaiton from SAP ECC/CRM
* BOM management: upload template, input on the page, change date, quantity...
* Call pricing
* Book order
* other functions: CRUD...

#### advantages and main functionality of the test framework

* Provide End-to-End solution for UAT test. automatic the difficult things.
* blackbox test for main functions
* save effort from 3 man/day to 2 hours.
* tracable result

#### tools, technologies, and platform used

UFT, QC

#### modules description

* Object repositories - maintainance, stability
* test data management
* Exception recovery
* Log
* Email notification for issues in realtime
* Email report

#### challenges in the project

* Slowness. SAP can be slow. Call pricing can be slow. Add additional wait and check modules to speed up tests execution
* complex of business. each case is different. HP, Cisco, EMC… steps are different, data is different. Create common steps in public module and customize for each
* test data management for different environment. put in config file

#### personal contribution and your role in the project

* design the framework
* develop main modules
* mentor team for scripting

#### number ofr people in the project

5

#### amount of time it took for the project

3 weeks. Agile.

#### improvements in the future for the present system

* increase stability

#### drawbacks

* not open source framework.
* use VBscript

### Automation framework using Selenium

### Most challenging project

#### project introduction

Part of new SAP project. A warehouse management system needs performance test.

* transaction processing
* storage management
* directed task mangement: pick, pack, ship
* RF device

#### advantages and the main functionality of your applicaiton

* carry out the performance test, simulate the peak business scenarios using VMs
* integration tests with multiple systems: SAP ECC

#### tools, technologies, and plaform used

Loadrunner, VMware, QTP, Shell, Python, MySQL (for monitoring)

#### personal contribution and your role in the project

design/maintain the infrastructure. carry out the tests. 

#### challenges in the project

40 VMs. design the automation scripts to manage.

test data management. need to prepare data from SAP ECC

#### number of people in the project

7 (US and China)

#### amount of time it took for the project

4 weeks

#### improvements in the furue for the present system

Get rid of VMs.

#### drawbacks

VMs

### BW Chain monitor system

