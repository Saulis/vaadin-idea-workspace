vaadin-idea-workspace
=====================

Here's a collection of IDEA project files in order to get you up and running with Vaadin (7.3) development.
If you find something to improve, please send a pull request. There might be cake available for all who contribute.

(only tested these with IDEA 13.1 Ultimate in OSX)

### Features available
* Compile Vaadin (hurray!)
* Compile Themes and Widgetset (use the Ant build window)
* Run TB3 tests

### Missing features
* Run DevMode
* An automatic shell script to run all these nasty installation steps
* Something else probably

### Known issues
* The ant script for unpacking GWT deletes build/gwt folder under which the gwt.iml file for the gwt module is located.

### Getting started
#### 1. Clone the vaadin repo
````sh
git clone https://github.com/vaadin/vaadin.git
````
#### 2. Unpack GWT
In order for everything to work pretty, we need to compile and unpack GWT outside IDEA.
````sh
ant -f gwt-files.xml unpack.gwt
````
#### 3. Copy workspace files from the internets
````sh
curl -S https://raw.githubusercontent.com/Saulis/vaadin-idea-workspace/master/install.sh | bash
````

#### 4. Open vaadin folder in IDEA
Note! When opening the project for the first time, you might get a warning about missing test modules and IDEA will ask if you would like to remove them. Keep all, they will be loaded automatically later.

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
