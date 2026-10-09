# OLLAMA deployment guide
this file notice the steps of local model depolyment with Ollama on windows. 

## Structure of local AI model deployment

# Steps of deployment

## step 1 download the Ollama

Download the Ollama from Official website `https://ollama.com/download/windows?utm_source=chatgpt.com` 

You can also download the Ollama manually, and install the `ollama.exe` like normal software


### (option but recommand) Change the Ollama installation location

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
This will consume huge place on you C Disk, when you download the model in future. 

[Ollama Changing install location & model location](https://docs.ollama.com/windows)

After you create the `OLLAMA_MODELS` manually, the ollama application must be restarted, otherwise new location will not be used. 

### Setup the ollama to enviroment variable
If you want to use ollama command on arbitrary cmd location you need add the ollama install path to the enviroement variable `path` in **user account**. 



## Step 2 Download the Models
You can directly download the model via ollama and run it directly. For instance you want to run `qwen3:4b` model, you can simply type this command in console. 
If you run the model first time, it will automatically download the model file and save the model file to the path, which you have previously assigned. 

```
ollama run qwen3:4b
```

You can also manually download the model file and load it in to ollama, it is recommanded to do like this, beacuase you can manage the model briefly and use more model which not 
has been publicated on hugging face. 

On hugging face there are to types of model file
```
A. Safetensors
B. GGUF
```
They are used for different situation. 



**Safetensors** for instance look like that:
```
model-00001-of-00004.safetensors
model-00002-of-00004.safetensors
...
config.json
tokenizer.json
```
This is normally used for Hugging Face / Transformers enviroment. They are suitable for 
```
Transformers
PyTorch
traning
Tuinning
vLLM
```

**GGUF** Format for instance: 
```
Qwen3-8B-Q4_K_M.gguf
```
is suitable for following enviroment:
```
Ollama
llama.cpp
LM Studio
```

This tutorial use a GGUF format to deploy. 

The Model can be download in this link [Qwen3-8B-GGUF](https://huggingface.co/Qwen/Qwen3-8B-GGUF/tree/main)

After download the GGUF file, we put this file to the Ollama model path, which same as the `OLLAMA_MODELS` enviroment variable. 
Here for instance is the `OLLAMA_MODELS` value `H:\Ollama_Models` 

## Step 3: Create model file

Create a work direactory, which contain the model file, this directory is used for the ollama deployment. 

```
H:\Ollama_project\Qwen3-8B
```
Create a file without any suffix called: 
```
Modelfile
```
The contain of this file is simple: 
```
FROM H:\Ollama_Models\Qwen3-8B-Q8_0.gguf
```
This is the simple model file， ollama support use `FROM H:\Ollama_Models\Qwen3-8B-Q8_0.gguf` syntax to import a outside model


## Step 4: create ollama model
After the model has been downloaded, you need register the model as it's own model object. Which can be managed by ollama, this process is 
the model creation.

Go to the Modelfile directory and open cmd type following:

```
ollama create qwen3-8b-local -f Modelfile
```

after successful creation you can use following command to check the current available models: 
```
ollama list
```

the output should look like this:
```
NAME                         ID              SIZE      MODIFIED
qwen3-8b-local-64k:latest    84364e471a44    8.7 GB    13 minutes ago
```

### run the model
After the creation you can run the model locally with followign command:
```
ollama run <model-name>
```
The <model-name> is the name shown in `ollama list`. In this case for example:
```
ollama run qwen3-8b-local-64K
```
then you can start the conversation. 








