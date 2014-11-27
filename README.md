vaadin-idea-workspace
=====================

Here's instructions on how to get you up and running with Vaadin (7.3.x) development using IntelliJ IDEA 14.
If you find something to improve, please send a pull request. There might be cake available for all who contribute.

(tested and developed in OSX, so there might be differences to Windows)

### Features available
* Compile Vaadin (hurray!)
* Compile Themes and Widgetset (use the Ant build window)
* Run Development Server
* Run CodeServer for Super DevMode
* Debug client side inside IDEA
* Run Unit tests
* Run TB4 tests

### Known issues
* The ant script for unpacking GWT deletes build/gwt folder under which the gwt.iml file for the gwt module is located. Remember this if you need to change back and forth between GWT versions.

### Getting started
#### 0. Install IDEA 14 + IvyIDEA plugin


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
#### 3. Open vaadin folder in IDEA
(ignore possible warnings about missing JDK JavaSE-1.6)

#### 4. Setup project
- Open project properties
  - Select SDK of your choosing in Project -> Project SDK (tested to work with 1.7.0_51)
  - Set Project Compiler Output to vaadin/build/classes in Project -> Project compiler output
  - Delete Module vaadin from Modules
- Open IDEA Preferences
  - Open Project Preferences for IvyIDEA
  - Set Ivy Settings to use vaadin/ivysettings.xml
  - Add vaadin/build.properties using Properties -> Add File

#### 5. Add modules
- Select Import Module
  - Import vaadin/buildhelpers
  - Resolve dependencies by selecting IvyIDEA -> Resolve for buildhelpers module
- Repeat for module vaadin/gwt, vaadin/push, vaadin/shared
  - Note! At this point, don't include test/src folder with the modules. We will import those later.
  - For push and gwt we need to export their dependencies. Unfortunately that can't be done through the settings GUI, so we need to modify their .iml files. ````<orderEntry type="module-library">```` needs to be changed to ````<orderEntry type="module-library" exported="">````
- Import Module vaadin/server
  - Add gwt, push, shared as Module dependencies (if they aren't automatically added)
- Import Module vaadin/client
  - Exclude GWT facets (the GWT 4 xml files)
  - Add gwt, shared, server as dependencies (if they aren't automatically added)

> Unfortunately we can't use the builtin GWT features because our sources for the widgetset is divided between two modules: shared + client.

#### 6. Getting the widgetset to compile
- Import module vaadin/client-compiler
  - Add dependencies to client, shared, gwt, server (if they aren't automatically added)
- Change the output path to build/classes for modules buildhelpers, client, shared, server, client-compiler
  - Module settings -> Paths
- Open the Ant Build window from View -> Tool Windows -> Ant Build
  - Add vaadin/build/ide.xml
- Run targets from ide.xml

> build/classes is the path ide.xml searches for classes when compiling the widgetset.

### Setting up debugging
#### 7. Running the Development Server
- Import module vaadin/server/tests
  - Rename the module to server-tests (optional)
  - Mark src folder as Sources instead of Tests in Module Settings -> Sources
  - Manually add IvyIDEA facet that points to vaadin/server/ivy.xml
  - Add dependencies to shared, push, gwt, server (if they aren't automatically added)
- Import module vaadin/uitest
  - Ignore GWT facet
  - Add dependencies to all modules we have imported
- Add Run Configuration from Run -> Edit Configurations
  - Add -> Application
  - Main class: com.vaadin.launcher.DevelopmentServerLauncher
  - VM options: -ea
  - Use classpath of module: uitest
  - Select Single Instance only
- Run for Profit

> We need to define sources inside server-tests and uitest as __sources__ instead of __tests__ because otherwise they won't be included in the module classpath when using the module as a dependency.

#### 8. Running CodeServer for Super DevMode
> This is a bit tricky because we need source directories from multiple modules to be added to the classpath and IDEA doesn't really support that. So we basically need to use a custom classpath:

- Add Run Configuration from -> Run Edit Configurations
  - Add -> Application
  - Main class: ````com.google.gwt.dev.codeserver.CodeServer````
  - VM options: ````-Xmx512M -XX:MaxPermSize=256M  -classpath "shared/src:client/src:uitest/src:build/classes:build/gwt/gwt-dev.jar:build/gwt/gwt-user.jar:build/gwt/gwt-elemental.jar:/Users/Saulis/.ivy2/cache/org.ow2.asm/asm/jars/asm-5.0.3.jar:/Applications/IntelliJ IDEA 14.app/Contents/lib/idea_rt.jar"```` <- __you need to replace paths to asm-5.0.3.jar and idea_rt.jar with ones that are correct for your environment__
  - Program arguments: ````com.vaadin.DefaultWidgetSet  -bindAddress 0.0.0.0 ````
  - Use classpath of module: ````client````
- Run for Profit

#### 9. Debugging client side code inside IDEA

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
