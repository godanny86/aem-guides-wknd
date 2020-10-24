# WKND Sites Project - Tutorial Branch

You are on the Tutorial branch for the WKND Site. This branch contains chapter starter and solution code for the various chapters of the tutorial.

```
| 02-component-basics
    |-- start
    |-- solution
| 03-pages-templates
    |-- start
    |-- solution
| 04-front-end-workflow
| 05-style-system
| 06-custom-component
| 07-unit-testing
```

## Building for AEM 6.5/6.4

The projects has been designed for **AEM as a Cloud Service**. The project is also backward compatible with AEM **6.4.8** and **6.5.5** by adding the `classic` profile when executing a build, i.e:

    mvn clean install -PautoInstallSinglePackage -Pclassic

## Content Reset

By design the **start** and **solution** branches will reset any content and configurations on the target AEM environment. This is not standard for a real-world implementation. Review the `ui.content/filter.xml` file and the various [modes](https://jackrabbit.apache.org/filevault/importmode.html#Modes) that can be set.

## Tutorial Chapters

The tutorial where you can learn how to implement a website using the latest standards and technologies in Adobe Experience Manager (AEM):

1. [WKND Tutorial Overview](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html)
2. [Project Setup](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/project-setup.html)
3. [Component Basics](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/component-basics.html)
4. [Pages and Templates](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/pages-templates.html)
5. [Client-Side Libraries](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/client-side-libraries.html)
6. [Style a Component](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/style-system.html)
7. [Custom Component](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/custom-component.html)
8. [Unit Testing](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/unit-testing.html)


## How to build

Navigate into the project folder for the desired chapter and version:

    cd /02-component-basics/start

To build all the modules run in the project root directory the following command with Maven 3:

    mvn clean install

To build all the modules and deploy the `all` package to a local instance of AEM (Cloud Service), run in the project root directory the following command:

    mvn clean install -PautoInstallSinglePackage

To build all the modules and deploy the `all` package to a local instance of AEM **6.5/6.4**, run in the project root directory the following command:

    mvn clean install -PautoInstallSinglePackage -Pclassic

Or to deploy it to a publish instance, run

    mvn clean install -PautoInstallSinglePackagePublish

Or alternatively

    mvn clean install -PautoInstallSinglePackage -Daem.port=4503

Or to deploy only the bundle to the author, run

    mvn clean install -PautoInstallBundle

Or to deploy only a single content package, run in the sub-module directory (i.e `ui.apps`)

    mvn clean install -PautoInstallPackage

### Building for AEM 6.x.x

The project has been designed for **AEM as a Cloud Service**. The project is also backward compatible with AEM **6.4.8** and **6.5.5** by adding the `classic` profile when executing a build, i.e:

    mvn clean install -PautoInstallSinglePackage -Pclassic

### WKND Sample content

By default, sample content from `ui.content.sample` will be deployed and installed along with the WKND code base. The WKND reference site is used for demo and training purposes and having a pre-built, fully authored site is useful. However, the behavior of including a full reference site (pages, images, etc...) in source control is *unusual* and is **not** recommended for a real-world implementation.

Including `ui.content.sample` will **overwrite** any authored content during each build. If you wish to disable this behavior modify the [filter.xml](ui.content.sample/src/main/content/META-INF/vault/filter.xml) file and update the `mode=merge` attribute to avoid overwriting the paths.

```diff
- <filter root="/content/wknd" />
+ <filter root="/content/wknd" mode="merge"/>
```

### Upgrading versions

If upgrading to a new version of WKND, it is recommended up modify the filters in `ui.content.sample` to remove the `mode="merge"` attribute prior to deploying.

## Testing

There are three levels of testing contained in the project:

* unit test in core: this show-cases classic unit testing of the code contained in the bundle. To test, execute:

    ```
    mvn clean test
    ```

* server-side integration tests: this allows to run unit-like tests in the AEM-environment, ie on the AEM server. To test, execute:

    ```
    mvn clean verify -PintegrationTests
    ```

* client-side Hobbes.js tests: JavaScript-based browser-side tests that verify browser-side behavior. To test, go in the browser, open the page in 'Developer mode', open the left panel and switch to the 'Tests' tab and find the generated 'MyName Tests' and run them.


## Maven settings

The project comes with the auto-public repository configured. To setup the repository in your Maven settings, refer to:

    http://helpx.adobe.com/experience-manager/kb/SetUpTheAdobeMavenRepository.html
