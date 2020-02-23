# Visual Studio Code - OpenLiberty remote debugging

Remote debugging in Visual Studio Code.

![openliberty-microprofile-debug-in-vs-code](images/openliberty-microprofile-debug-in-vs-code.gif)


Setup:

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

# Setup Visual Studio Code for Java Development and Debugging

VS Code extensions:

* [java extension pack](https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-java-pack)

    This extension also includes follwing extensions:

    * [vscode-java-debug](https://code.visualstudio.com/docs/java/java-debugging) and Configure attach to port '7777'

    * [Debugger for Java](https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-java-debug)

    * [maven for java](https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-maven)


# Visual Studio - Remote development

Here is a good blog post [Java development environments with containers](https://medium.com/@brunoborges/java-dev-environments-with-containers-66d6797b2753)

Configurtion of the `.devcontainer/devcontainer.json` file.

```json
{
	"name": "Java 11",
	"dockerFile": "Dockerfile",

	// Set *default* container specific settings.json values on container create.
	"settings": { 
		"terminal.integrated.shell.linux": "/bin/bash",
		"java.home": "/docker-java-home"
	},
	
	// Add the IDs of extensions you want installed when the container is created.
	"extensions": [
		"vscjava.vscode-java-pack"
	],

	// Use 'forwardPorts' to make a list of ports inside the container available locally.
	"forwardPorts": [8080,3000,7777],

	// Use 'postCreateCommand' to run commands after the container is created.
	"postCreateCommand": "java -version"

    ...
}
```