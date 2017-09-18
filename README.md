faketui
=======

Built from a template for a simple Vaadin application.
A single @Push annotaion enables websocket push-messages.
I need them for debugging a websocket application.

Workflow
========
ensure you have 'mvn' in your path (Windows users have to point to _MAVEN_DIR_/bin)

from command prompt:

* git clone <repo-url> _somedir_
* cd _somedir_
* mvn jetty:run
* open http://localhost:8080/ (/?debug for debug console) or do whatever you need
* Press Ctrl-C in the command prompt window to stop Jetty

On Windows Java x64 took about 150 MB RAM for running this server.
On first run Maven will have to download about 115 MB of build/run dependecies.

Minor nuicance: every 5 minutes Jetty will spew
'java.net.SocketTimeoutException: Timeout on Read' and a stack trace.
Client window continues working.

From Vaadin template file:

Client-Side compilation
-------------------------

The generated maven project is using an automatically generated widgetset by default. 
When you add a dependency that needs client-side compilation, the maven plugin will 
automatically generate it for you. Your own client-side customisations can be added into
package "client".

Debugging client side code
  - run "mvn vaadin:run-codeserver" on a separate console while the application is running
  - activate Super Dev Mode in the debug window of the application

Developing a theme using the runtime compiler
-------------------------

When developing the theme, Vaadin can be configured to compile the SASS based
theme at runtime in the server. This way you can just modify the scss files in
your IDE and reload the browser to see changes.

To use the runtime compilation, open pom.xml and comment out the compile-theme 
goal from vaadin-maven-plugin configuration. To remove a possibly existing 
pre-compiled theme, run "mvn clean package" once.

When using the runtime compiler, running the application in the "run" mode 
(rather than in "debug" mode) can speed up consecutive theme compilations
significantly.

It is highly recommended to disable runtime compilation for production WAR files.
