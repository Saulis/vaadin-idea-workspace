vaadin-idea-workspace
=====================

Here's instructions on how to get you up and running with Vaadin (7.3) development using IntelliJ IDEA 14.
If you find something to improve, please send a pull request. There might be cake available for all who contribute.

(tested and developed in OSX, so there might be differences to Windows)

### Features available
* Compile Vaadin (hurray!)
* Compile Themes and Widgetset (use the Ant build window)
* Run Development Server
* Run SDM
* Debug client side in IDEA
* Run TB4 tests

### Known issues
* The ant script for unpacking GWT deletes build/gwt folder under which the gwt.iml file for the gwt module is located.

### Getting started
#### 0. Install IDEA 14 (duh) + IvyIDEA plugin


#### 1. Clone the vaadin repo
````sh
git clone https://github.com/vaadin/vaadin.git
````
#### 2. Unpack GWT
In order for everything to work pretty, we need to compile and unpack GWT outside IDEA.
````sh
ant -f gwt-files.xml unpack.gwt
````
### Getting the first modules to compile
#### 1. Open vaadin folder in IDEA
(ignore possible warnings about missing JDK JavaSE-1.6)

#### 2. Setup project
- Open project properties
  - Select SDK of your choosing in Project -> Project SDK (tested to work with 1.7.0_51)
  - Set Project Compiler Output to vaadin/build/classes in Project -> Project compiler output
  - Delete Module vaadin from Modules
- Open IDEA Preferences
  - Open Project Preferences for IvyIDEA
  - Set Ivy Settings to use vaadin/ivysettings.xml
  - Add vaadin/build.properties using Properties -> Add File

#### 3. Add your first modules
- Select Import Module
  - Import vaadin/buildhelpers
  - Resolve dependencies by selecting IvyIDEA -> Resolve for buildhelpers module
  

### Getting the widgetset to compile
- build folders

### Running the Development Server
- uitest + server-test modules

### Running Super DevMode
- classpath

### Debugging client side in IDEA

### Running Tests
#### 5a. Set screenshot directory for running TB3 tests in JUnit
1. Edit Configurations...
2. Select __Defaults__
3. Select __JUnit__
4. Add VM parameter -Dcom.vaadin.testbench.screenshot.directory=__your screenshot directory__

#### OR

#### 5b. Set screenshot directory for running TB3 tests using properties file
1. Copy eclipse-run-selected-test.properties to __work__ directory
2. Set com.vaadin.testbench.screenshot.directory=__your screenshot directory__ in eclipse-run-selected-test.properties

#### 6. Profit!
