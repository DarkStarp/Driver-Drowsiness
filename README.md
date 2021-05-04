
This library uses deep learning to detect drowsiness of a person

Before using this library make sure you have installed following libraries which are needed

    Tensorflowpip install tensorflow
    keras pip install keras
    pyaudio
        For windows users
            First install pipwin pip install pipwin
            then install pyaudio it with pipwin install pyaudio
        For linux users

           sudo apt-get install libasound-dev portaudio19-dev libportaudio2 libportaudiocpp0
           sudo apt-get install ffmpeg libav-tools
           sudo -s
           pip install pyaudio

    pyttsx3 pip install pyttsx3

To use this library just follow the steps

This library creates a new process by forking to perform predictions , but in windows process creation takes place differently by importing the script and executing it again so to avoid infinite loop initialize detector inside main condition as shown below

if __name__ == "__main__":
        initialize the detector here
        ......
        ....
        

    import it in your project

    from DrowsinessDetection.DrowsinessDetector import  getDetector

    initializing the detector

    detector = getDetector()(Audio="path to audio file, completely optional",UseAssistant=True)

    starting the detector in separate thread

    detector.start()

    Do any task and wait for detector to finish using this is a blocking call

    detector.join()

if you want to listen for changing state of person then set a callback function which will take boolean as argument and this function will get fired every time person drowsy state changes , it will trigger true for sleeping and false for awake

def My_Callback(sleep):
        print("recieved status sleeping --> "+str(sleep))

d = getDetector()(UseAssistant=True)
d.setCallbackForStateChange(My_Callback)

If you want to control the behaviour programmatically then there are few methods on detector object

    for setting sensitivitydetector.setSensitivity(any integer)
    for closing the detectordetector.quit()
    for observing state changesdetector.setCallbackForStateChange(My_Callback)

Use Voice Assistant to control the sensitivity of detector and for quiting

voice commands are

    sensitivity low
    sensitivity medium
    sensitivity high
    quit

one sample script

from DrowsinessDetection.DrowsinessDetector import   getDetector

if __name__ == "__main__":

    def My_Callback(sleep):
        print("recieved "+str(sleep))

    d = getDetector()(audio="audio-file-path",UseAssistant=True)
    d.setCallbackForStateChange(My_Callback)
    d.start()
    d.join()


# press q to quit the script


