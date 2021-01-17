[![HomeTracker](https://circleci.com/gh/Owl-e/hometracker-application-plugin/tree/main.svg?style=svg)](https://circleci.com/gh/Owl-e/hometracker-application-plugin/tree/main)
[![Download](https://api.bintray.com/packages/hometracker/java/hometracker-application/images/download.svg) ](https://bintray.com/hometracker/java/hometracker-application/_latestVersion)
# HomeTracker Application Plugin

## Overview.
The HomeTracker Application Plugin give help to deploy HomeTracker's modules.

## Table of Content.
* [Getting Started Using the Plugin](#start)
    * [Step 1](#start-1)
    * [Step 2](#start-2)
    * [Step 3](#start-3)
    * [Step 4](#start-4)
* [Plugins Documentation](#doc)
    * [Closures section](#closures)
        * [module](#closures-module)
    * [Tasks section](#tasks)
        * [generateModuleYml](#tasks-generateModuleYml)
## Getting Started Using the Plugin. <a id="start"></a>
### *Step 1: Apply the plugin to your Gradle build script.* <a id="start-1"></a>
To apply the plugin, please add this following part of code.
```groovy
buildscript {
    repositories {
        maven {
            url  'https://dl.bintray.com/hometracker/java'
        }
        dependencies {
            classpath 'fr.owle:hometracker-application:+'
        }
    }
}

group 'your.group'
version '1.0.0'

apply plugin: 'hometracker-application'
```

### *Step 2: Add the module configuration to your project.* <a id="start-2"></a>
Add the below **module** closure with your module's information inside.
```groovy
module {
    moduleName = 'MyAwesomeModule'
    version = '1.0.0'
    authors = ['Wicket', 'Nippet']
    main = 'com.your.module.MainClass'
}
```

### *Step 3: Run the build task.* <a id="start-3"></a>
The **hometracker-application** plugin include the **java-library** plugin. Therefore, you have access to all **java-library**'s tasks include the **build** task.  
Run this following command.
```bash
$> ./gradlew build
```

### *Step 4: Use your module.* <a id="start-4"></a>
Take the built module and put it in the *modules* file of your HomeTracker server.  

> Enjoy 🦉

## Plugins Documentation. <a id="doc"></a>

In this section we will see more information about its closures and added tasks.

## Closures section. <a id="closures"></a>
### module. <a id="closures-module"></a>
The module closure represent the *module.yml* file inside your module.
```yaml
name: MyAwesomeModule
version: 1.0.0
authors:
  - Wicket
  - Nippet
main: com.your.module.MainClass
```
The above example part of code can be replaced by the below closure.
```groovy
module {
    moduleName = 'MyAwesomeModule'
    version = '1.0.0'
    authors = ['Wicket', 'Nippet']
    main = 'com.your.module.MainClass'
}
```
The following array was the exhaustive list of **module**'s parameters.  
|       Key        | Description                                              | Equivalent of YAML |                                  Default value |
|:----------------:|:---------------------------------------------------------|:------------------:|-----------------------------------------------:|
| moduleName       | Module name.                                             |        name        |                      Your Gradle project name. |
| version          | Module version.                                          |       version      |                   Your Gradle project version. |
| authors          | Module authors.                                          |       authors      |                                        ['you'] |
| main             | Module main.                                             |        main        | Concat the project group and the project name. |
| dependencies     | Module dependencies.                                     |     dependencies   |                                     void list. |
| softDependencies | Module soft dependencies.                                |   softDependencies |                                     void list. |
| target           | The output folder for the generated **module.yml** file. |        none        |                           'src/main/resources' |

## Tasks section. <a id="tasks"></a>
### generateModuleYml. <a id="tasks-generateModuleYml"></a>
This Task generate the **module.yml** file.
