Simple scripts to automate acquisition on our TIRF microscope using the SRRF camera.

The TIRF microscope control software and the camera control software (Micro-Manager) run on two different computers, without any communication between them.

The scripts here automate acquisition, from the camera (Micro-Manager) side, by controlling the microscope software via simple remote clicks.

It therefore consists of two parts:
* A simple click server which runs on the TIRF computer, receives click commands over a network port and performs the actual click.

* A beanshell script for MicroManager, which sets up and controls the camera, and invokes switching channels and live preview on the microscope by sending click commands.

How to set it up
================
 
On the microscope PC:
---------------------

* Make sure you have a running Java installation
* Download Beanshell from http://beanshell.org
* Adjust `SimpleClickServer.bsh` if needed (e.g. the port number)
* Start the SimpleClickServer.bsh with
```
java -classpath <path-to-bsh-XXX.jar> SimpleClickServer.bsh
```
* Optionally, put this command in the Windows Task Scheduler to start the `SimpleClickServer` automatically when the computer boots.

On the camera PC:
-----------------
* Run Micro-Manager configured for the Andor SRRF camera
* Adjust SRRF_and_TIRF.bsh (HOST: needs to be the IP of the microscope computer, and PORT: must match the port set in SimpleClickServer.bsh).
* Adjust SRRF_and_TIRF.bsh: Manually set the coordinates in the methods `toggleLive()` and `selectChannel()` to the respective screen coordinates of the microscope PC.
* Run SRRF_and_TIRF.bsh from within Micro-Manager.

