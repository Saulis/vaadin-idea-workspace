vaadin-idea-workspace
=====================

### Features available
* Compile Vaadin (hurray!)
* Compile Themes and Widgetset
* Run TB3 tests

### Missing features
* Run DevMode
* Something else probably

### Getting started
#### 1. Clone repos
````sh
git clone https://github.com/vaadin/vaadin.git
git clone https://github.com/vaadin/gwt.git
git clone https://github.com/vaadin/gwt-tools.git
````
#### 2. Build GWT
````sh
cd gwt
ant
ant elemental
cd ../vaadin
ant -f gwt-files.xml unpack.gwt
````
#### 3. Copy project files
This archive contains .idea files, .iml files and a file called build/idea.xml, which is a modified version
of build/ide.xml. In idea.xml, ${vaadin.eclipse.basedir} has been replaced with ${vaadin.basedir} - you can also do this
modification by hand to your ide.xml if you want. This modification changes ide.xml to search for GWT classes from directory which contains the classes compiled by running Ant and it is not necessary if you're using Eclipse in the same workspace and eclipse has compiled GWT under ${vaadin.eclipse.basedir}.
````sh
wget https://github.com/Saulis/vaadin-idea-workspace/archive/master.zip
unzip master.zip
cp -R vaadin-idea-workspace/ .
rm -rf vaadin-idea-workspace
````


#### 4. Fix JUnit defaults screenshot directory


