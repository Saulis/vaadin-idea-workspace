vaadin-idea-workspace
=====================

Here's a collection of IDEA project files in order to get you up and running with Vaadin (7.2) development.
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

### Getting started
#### 1. Clone repos
````sh
git clone https://github.com/vaadin/vaadin.git
git clone https://github.com/vaadin/gwt.git
git clone https://github.com/vaadin/gwt-tools.git
````
#### 2. Build GWT
In order for everything to work pretty, we need to compile and unpack GWT outside IDEA.
````sh
cd gwt
ant
ant elemental
cd ../vaadin
ant -f gwt-files.xml unpack.gwt
````
#### 3. Copy workspace files from the internets
````sh
wget https://github.com/Saulis/vaadin-idea-workspace/archive/master.zip
unzip master.zip
cp -R vaadin-idea-workspace-master/ .
rm -rf vaadin-idea-workspace-master
````

This archive contains .idea files, .iml files and a file called __build/idea.xml__, which is a modified version
of __build/ide.xml__. In idea.xml, __${gwt.eclipse.basedir}__ has been replaced with __${gwt.basedir}__ - you can also do this modification by hand to your ide.xml if you want. This modification changes ide.xml to search for GWT classes from directory which contains the classes compiled by running Ant and it is not necessary if you're using Eclipse in the same workspace and eclipse has compiled GWT under __${gwt.eclipse.basedir}__.

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
