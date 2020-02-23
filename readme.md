# Visual Studio Code - OpenLiberty remote debugging

Remote debugging in Visual Studio Code.

![openliberty-microprofile-debug-in-vs-code](images/openliberty-microprofile-debug-in-vs-code.gif)


## Setup:

- configure the maven extension
- configure the [Debug extension for Java](https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-java-debug). Here you need the OpenLiberty debug port **7777**

```json
{
    "type": "java",
    "name": "Debug (Attach)",
    "request": "attach",
    "hostName": "localhost",
    "port": 7777
}
```

- Enable the [liberty-maven plugin](https://github.com/OpenLiberty/ci.maven) in the pom.xml and configure the server information, if needed.

```xml
	<build>
		....
        <!--Plugins -->
        <plugins>  
            <!-- Enable liberty-maven plugin -->
            <!-- tag::libertyMavenPlugin[] -->
            <plugin>
                <groupId>io.openliberty.tools</groupId>
                <artifactId>liberty-maven-plugin</artifactId>
				<!-- tag::libertyMavenConfiguration[] -->
				<configuration>
                	<serverName>authorsDevServer</serverName>
					<configFile>liberty/server.xml</configFile>
            	</configuration>
				<!-- end::libertyMavenConfiguration[] -->
            </plugin>
            <!-- end::libertyMavenPlugin[] -->
            <!-- Enable liberty-maven-plugin -->
        </plugins>
	</build>
```