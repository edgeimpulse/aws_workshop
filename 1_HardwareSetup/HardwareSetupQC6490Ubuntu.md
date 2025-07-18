## Ubuntu-based QC6490 platforms

First, please flash your QC6490 device per your manufacturers instructions to load up Ubuntu onto the device.

### Additional Setup

Once you have your Ubuntu platform installed and running, please run these commands to add some required dependencies:

	sudo apt update	
	sudo apt install -y curl unzip
	sudo apt install -y gcc g++ make build-essential nodejs sox gstreamer1.0-tools gstreamer1.0-plugins-good gstreamer1.0-plugins-base gstreamer1.0-plugins-base-apps
	
Additionally, we need to install the prerequisites for AWS IoT Greengrass "classic":

	sudo apt install -y default-jdk 

Lastly, its recommended to update your linux device with the latest security patches and updates if available. 

We are now setup!  Before we continue, please save off the following JSONs. These JSONs will be used to configure our AWS Greengrass deployment.

#### QC Camera configuration

	{     
	   "Parameters": {
	      "node_version": "20.18.2",
	      "vips_version": "8.12.1",
	      "device_name": "MyQC6490UbuntuEdgeDevice", 
	      "launch": "runner",
	      "sleep_time_sec": 10,
	      "lock_filename": "/tmp/ei_lockfile_runner",
	      "gst_args": "qtiqmmfsrc:name=camsrc:camera=0:!:video/x-raw,width=1280,height=720:!:videoconvert:!:jpegenc",
	      "eiparams": "--greengrass --force-variant float32 --silent",
	      "iotcore_backoff": "-1",
	      "iotcore_qos": "1",
	      "ei_bindir": "/usr/local/bin",
	      "ei_sm_secret_id": "EI_API_KEY",
	      "ei_sm_secret_name": "ei_api_key",
	      "ei_poll_sleeptime_ms": 2500,
	      "ei_local_model_file": "__none__",
	      "ei_shutdown_behavior": "__none__",
	      "ei_ggc_user_groups": "video audio input users",
	      "install_kvssink": "no",
	      "publish_inference_base64_image": "no",
	      "enable_cache_to_file": "no",
	      "cache_file_directory": "__none__",
	      "enable_threshold_limit": "no",
	      "metrics_sleeptime_ms": 30000,
	      "default_threshold": 65.0,
	      "threshold_criteria": "ge",
	      "enable_cache_to_s3": "no",
	      "s3_bucket": "__none__"
	   }  
	}     

#### USB-attached Camera configuration

	{     
	   "Parameters": {
	      "node_version": "20.18.2",
	      "vips_version": "8.12.1",
	      "device_name": "MyQC6490UbuntuEdgeDevice", 
	      "launch": "runner",
	      "sleep_time_sec": 10,
	      "lock_filename": "/tmp/ei_lockfile_runner",
	      "gst_args": "v4l2src:device=/dev/video0:!:video/x-raw,width=640,height=480:!:videoconvert:!:jpegenc",
	      "eiparams": "--greengrass --force-variant float32 --silent",
	      "iotcore_backoff": "-1",
	      "iotcore_qos": "1",
	      "ei_bindir": "/usr/local/bin",
	      "ei_sm_secret_id": "EI_API_KEY",
	      "ei_sm_secret_name": "ei_api_key",
	      "ei_poll_sleeptime_ms": 2500,
	      "ei_local_model_file": "__none__",
	      "ei_shutdown_behavior": "__none__",
	      "ei_ggc_user_groups": "video audio input users",
	      "install_kvssink": "no",
	      "publish_inference_base64_image": "no",
	      "enable_cache_to_file": "no",
	      "cache_file_directory": "__none__",
	      "enable_threshold_limit": "no",
	      "metrics_sleeptime_ms": 30000,
	      "default_threshold": 65.0,
	      "threshold_criteria": "ge",
	      "enable_cache_to_s3": "no",
	      "s3_bucket": "__none__"
	   }  
	}     

#### Non-Camera configuration

	{     
	   "Parameters": { 
	      "node_version": "20.18.2",
	      "vips_version": "8.12.1",
	      "device_name": "MyQC6490UbuntuEdgeDevice",
	      "launch": "runner",
	      "sleep_time_sec": 10,
	      "lock_filename": "/tmp/ei_lockfile_runner",
	      "gst_args": "filesrc:location=/home/ggc_user/data/testSample.mp4:!:decodebin:!:videoconvert:!:videorate:!:video/x-raw,framerate=2200/1:!:jpegenc",
	      "eiparams": "--greengrass",
	      "iotcore_backoff": "-1",
	      "iotcore_qos": "1",
	      "ei_bindir": "/usr/local/bin",
	      "ei_sm_secret_id": "EI_API_KEY",
	      "ei_sm_secret_name": "ei_api_key",
	      "ei_poll_sleeptime_ms": 2500,
	      "ei_local_model_file": "/home/ggc_user/data/currentModel.eim",
	      "ei_shutdown_behavior": "wait_on_restart",
	      "ei_ggc_user_groups": "video audio input users system",
	      "install_kvssink": "no",
	      "publish_inference_base64_image": "no",
	      "enable_cache_to_file": "no",
	      "cache_file_directory": "__none__",
	      "enable_threshold_limit": "no",
	      "metrics_sleeptime_ms": 30000,
	      "default_threshold": 50,
	      "threshold_criteria": "ge",
	      "enable_cache_to_s3": "no",
	      "s3_bucket": "__none__" 
	   }  
	}  

OK!  Lets continue by getting our Edge Impulse project setup! Let's go!

[Back](./HardwareSetup.md) [Next](../2_EdgeImpulseProjectBuild/EdgeImpulseProjectBuild.md)