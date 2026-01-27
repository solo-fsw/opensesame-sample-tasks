# PyGaze
PyGaze is a Python library that is used for eye tracking. PyGaze can be used in OpenSesame and comes preinstalled in the Windows version of OpenSesame. Note that Tobii does not work in every Python version, see [SOLO Research Wiki - Tobii and OpenSesame](https://researchwiki.solo.universiteitleiden.nl/xwiki/wiki/researchwiki.solo.universiteitleiden.nl/view/Software/OpenSesame/Tobii%20and%20OpenSesame/) for more information. 

PyGaze_sample_task.osexp is an example of how to use PyGaze. It includes the code necessary for Tobii. For more information on PyGaze and OpenSesame, see https://osdoc.cogsci.nl/4.1/manual/eyetracking/pygaze/. 

## Initialize PyGaze
Make sure to configure the pygaze_init object so that it communicates with the correct eye-tracker. Make sure the **Calibrate tracker** option is checked, so that the eye-tracker is calibrated at the start of the task. For EyeLink, make sure to set the **Pupil-size mode** to the same mode as set on the EyeLink host PC

## Logging Variables
There are several options when it comes to logging variables in the eye tracker data file with PyGaze. Below, some options and recommendations are given.

### Log Time
It is advised to add and Inline script at the start and end of the task in which the current OpenSesame time is logged:

```python
# Log the current OpenSesame time in the eye tracker data file
eyetracker.log_var('cur_os_time', clock.time())
```

By logging the OpenSesame time in the eye tracking data file, it is possible to adjust the timestamp of the time variables logged during the pygaze_log item to the eye tracker system time.

### Start Recording and Stop Recording
It is possible to send a message with the pygaze_start_recording and pygaze_stop_recording items. For example, these items can be used to send trial meta data information to the eye tracker data file. When you want to send a variable of which the value is not known yet at the start of the trial, this variable can be sent at the end of the trial at pygaze_stop_recording. See example below.
<img width="1242" height="352" alt="pygaze-stop-recording" src="https://github.com/user-attachments/assets/c37eed50-5e8a-45c0-88d8-dd87f3328598" />

### Other Logging Options
#### pygaze_log
With the pygaze_log item you can log OpenSesame variables.

When you want to log all variables, just check the box **Automatically log all variables**. When you want to log specific variables, you can specify them in the control window.

The **Pause between messages** allows you to set the time interval between logging each variable. Note that when you have a lot of variables, logging can take some time (also depends on this setting).

It is advised to place the pygaze_log item after the pygaze_stop_recording item. When the pygaze_log item is placed before the pygaze_stop_recording item, the eye tracker is still recording during logging, which could create a messy data file with eye tracking data samples in between the logged variables.

#### eyetracker.log and eyetracker.log_var
Another possibility is to use an Inline script and the eyetracker.log or eyetracker.log_var function. With the eyetracker.log function you can log a message: **eyetracker.log(msg)**. With the eyetracker.log_var you can log a variable-value pair: **eyetracker.log_var(var, val)**. See the [PyGaze OpenSesame documentation](https://osdoc.cogsci.nl/3.2/manual/eyetracking/pygaze/#function-eyetracker46log40msg41) for more information.

## Tobii
When you use a Tobii eye tracker with PyGaze, you need to register the eye-tracker's serial number. This can be done by adding a Python Inline script item at the start of the experiment sequence, and then adding the following code to it:

```python
"""
When using Tobii eye-trackers, add a Python inline script to the
top of the experiment with the code below. Change the serial number
to the one matching your device. Use the Tobii Eye Tracker Manager
to find the serial number:
  https://www.tobiipro.com/product-listing/eye-tracker-manager/
"""

from pygaze import settings
settings.TRACKERSERIALNUMBER = "X3120-XXXXXXXXXXXXX"
```

Make sure to change the serial number to one matching the eye-tracker you have and want to use. You can find the serial number in the [Eye Tracker Manager](https://researchwiki.solo.universiteitleiden.nl/xwiki/wiki/researchwiki.solo.universiteitleiden.nl/view/Software/Tobii/Tobii%20Pro%20Eye%20Tracker%20Manager/) when the eye-tracker is connected to the PC and turned on. 
<img width="1024" height="304" alt="Tobii-SerialNumber" src="https://github.com/user-attachments/assets/df06e660-333e-4f6d-8c7f-f7bc779f3731" />

