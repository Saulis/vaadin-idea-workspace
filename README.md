vaadin-idea-workspace
=====================

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
This archive contains .idea files, .iml files and a file called __build/idea.xml__, which is a modified version
of __build/ide.xml__. In idea.xml, __${vaadin.eclipse.basedir}__ has been replaced with __${vaadin.basedir}__ - you can also do this modification by hand to your ide.xml if you want. This modification changes ide.xml to search for GWT classes from directory which contains the classes compiled by running Ant and it is not necessary if you're using Eclipse in the same workspace and eclipse has compiled GWT under __${vaadin.eclipse.basedir}__.
````sh
wget https://github.com/Saulis/vaadin-idea-workspace/archive/master.zip
unzip master.zip
cp -R vaadin-idea-workspace-master/ .
rm -rf vaadin-idea-workspace-master
````

#### 4. Open vaadin folder in IDEA
Note! When opening the project for the first time, you might get a warning about missing test modules and IDEA will ask if you would like to remove them. Keep all, they will be loaded automatically later.

#### 5a. Set screenshot directory for running TB3 tests in JUnit
1. Edit Configurations...
2. Select __Defaults__
3. Select __JUnit__
4. Add VM parameter -Dcom.vaadin.testbench.screenshot.directory=__your screenshot directory__

#### 5b. Set screenshot directory 
1. Copy eclipse-run-selected-test.properties to __work__ directory
2. Set com.vaadin.testbench.screenshot.directory=__your screenshot directory__ in eclipse-run-selected-test.properties

#### 6. Profit!
