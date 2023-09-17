# PyLangchainAudio
Just an example to extract audio transcript


### Install both LangChain and the AssemblyAI Python package

pip install langchain
pip install assemblyai


### Set your AssemblyAI API key
You can get your free API Key (https://app.assemblyai.com/login/)

### Create a python file main.py and add the following code

import assemblyai as aai

# replace with your API token
aai.settings.api_key = f"Your API Key"

# URL of the file to transcribe
FILE_URL = "https://github.com/AssemblyAI-Examples/audio-examples/raw/main/20230607_me_canadian_wildfires.mp3"

transcriber = aai.Transcriber()
transcript = transcriber.transcribe(FILE_URL)

print(transcript.text)




### Run the application



python3 demo.py



You should see the transcript of the audio link we provided in the application.

## Using Openai:
### Add Question & Answer Capabilities Using OpenAI

Get the OpenAI API key and set it.

On your terminal inside the application folder, set the OPENAI API key.

export OPENAI_API_KEY=<Your API Key>


Then, add the following code to your main.py file:


from langchain.document_loaders import AssemblyAIAudioTranscriptLoader
from langchain.llms import OpenAI
from langchain.chains.question_answering import load_qa_chain

FILE_URL = "https://github.com/AssemblyAI-Examples/audio-examples/raw/main/20230607_me_canadian_wildfires.mp3"

loader = AssemblyAIAudioTranscriptLoader(FILE_URL)
docs = loader.load()

llm = OpenAI()
qa_chain = load_qa_chain(llm, chain_type="stuff")

answer = qa_chain.run(input_documents=docs,
                      question="Where did the wildfire start?")
print(answer)


Run the application with the command `python3 main.py` and you should see the following output. It should be an answer to your question.

Credits to: pavanbelagatti - https://dev.to/pavanbelagatti/
