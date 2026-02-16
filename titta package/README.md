# Titta Package
The titta package allows to use eye trackers with python and can be used to integrate Tobii Pro Lab in OpenSesame experiments. Note that Tobii does not work in every Python version, see [SOLO Research Wiki - Tobii and OpenSesame](

**titta_sampleexp.osexp** is an example OpenSesame task of how to use Titta with Tobii Pro Lab integration. We adapted the example psychopy coder file which can be accessed here: https://github.com/marcus-nystrom/Titta. Note that you also need to create an External Presenter project in Tobii  Pro Lab to record the data. As the plugin itself does not provide integration with Tobii Pro Lab, several python inlines need to be used to access the toolbox. For more information on Titta and OpenSesame, see https://github.com/dev-jam/opensesame-plugin-titta_eyetracking. 

##Opensesame
### Install required packages
First, you need to manually install the titta module in OpenSesame. You can do this in the console: 
```python
pip install titta
```

### Initialize Titta 
See the first inline "init". It is important to define which eye tracker you are using, e.g. `et_name = 'Tobii Pro Spark'`. Additionally, you need to define the name of your external presenter project in Tobii Pro Lab. If you define it as None, then it will simply use the project that is currently opened in Tobii Pro Lab, e.g. `project_name = None`. 

### Performing the Calibration 
Calibration is performed outside of Tobii Pro Lab via the Tobii module, see the Calibration inline. In this example task, images with calibration results are saved in the output folder. It is also possible to save the validation accuracy results using tracker.calibration_history(). 

### Starting the recording
See the start_recording inline. The Tobii Pro Lab recording needs to be started before the stimuli are presented. In this inline, the stimulus images are uploaded and optionally AOIs can be added to them. Make sure the images are stored in the same folder as your OpenSesame file.

### During the trial
During the stimulus presentation, the images are presented for a set duration, which is set with core.wait() in our example. For each stimulus, the recording id, onset time, media id and offset time are sent to Tobii Pro Lab as stimulus events.

### Stopping the recording
It is important to stop the recording in Tobii Pro Lab at the end of the experiment in an inline that is placed at the end of the experiment sequence (see the "session_end" inline). 

##Tobii Pro Lab 
You need to create an external presenter project in Tobii Pro Lab by going to Create new project - External Presenter - Create. Make sure to keep the project open and on the `Record` tab before starting the experiment in OpenSesame. The External Presenter box will change the status to "Connected" once the experiment started and OpenSesame successfully connected to Tobii Pro Lab. 