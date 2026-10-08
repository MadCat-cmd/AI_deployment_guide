# OLLAMA deployment guide
this file notice the steps of local model depolyment with Ollama on windows. 

## Structure of local AI model deployment

# Steps of deployment

## step 1 download the Ollama

Download the Ollama from Official website `https://ollama.com/download/windows?utm_source=chatgpt.com` 

You can also download the Ollama manually, and install the `ollama.exe` like normal software


### Change the Ollama installation location

If you use Ollama installation `exe` file manually install ollama, it doesn't provide any option the change your installation location. 
But you can use the following command to change the Ollama installation location. 

```
OllamaSetup.exe /DIR="d:\some\location"
```

### Change the Ollama Model location

To change where Ollama stores the downloaded models instead of using your home directory, set the environment variable `OLLAMA_MODELS` in your **user account**. 
The enviroment variable `OLLAMA_MODELS` must be created in user account. 

For instance if you want to store the ollama models in self defined location `D:\AI\Ollama\Models` you can assign the `OLLAMA_MODELS` variable with following value in enviroment variable

```
D:\AI\Ollama\Models
```

If you didn't create this enviroment variable manuelly, OLLAMA will store the models file automatically in this location:
```
	C:\Users\<Your-Username>\.ollama\models
```
This will consume huge place, when you download the model in future

[https://docs.ollama.com/windows](Ollama Changing install location & model location)








