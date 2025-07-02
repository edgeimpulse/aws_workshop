## Running

After the deployment is initiated, on the FIRST invocation of a given deployment, expect to wait several moments (upwards of 5-10 min in fact) while the component installs all of the necessary pre-requisites that the component requires... this can take some time so be patient. You can also log into the edge gateway, receiving the component, and examine log files found in /greengrass/v2/logs. There you will see each components' current log file (same name as the component itself... ie. EdgeImpulseLinuxServiceComponent.log...) were you can watch the installation and invocation as it happens... any errors you might suspect will be shown in those log files. 

While the components are running, in addition to the /greengrass/v2/logs directory, each component has a runtime log in /tmp.  The format of the log file is: "ei\_lockfile\_[linux | runner | serial]\_\<EI DEVICE\>.log.  Users can "tail" that log file to watch the component while it is running. 

Additionally, for Jetson-based devices where the model has been compiled specifically for that platform, one can expect to have a 2-3 minute delay in the model being loaded into the GPU memory for the first time.  Subsequent invocations will be very short. 

[Back](../6_CustomComponentDeployment/CustomComponentDeployment.md) [Next](../8_Summary/Summary.md)