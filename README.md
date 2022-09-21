<h1 align="center"><b>Process answering chatbot applications</b></h1>

Streamlit application available [here](https://huggingface.co/spaces/rkrstacic/Chatbot-integration-built-on-processes).

Gradio application available [here](https://huggingface.co/spaces/rkrstacic/Software-module-for-answering-questions-on-processes).

## **:information_source: About :information_source:**

Made by [Rafael Krstačić](https://github.com/rkrstacic)
within the course [Web aplikacije](https://ntankovic.unipu.hr/wa)
on the [Faculty of Informatics in Pula](https://fipu.unipu.hr/).

Built applications ware developed with the goal of answering question around business processes in the form of a chatbot. The project is based on a [machine learning module](https://github.com/rkrstacic/Software-module-for-answering-questions-on-processes) (built by [Rafael Krstačić](https://github.com/rkrstacic)) was built with [Gradio](https://gradio.app/) and [Streamlit](https://streamlit.io/) frameworks and is hosted on [Hugging Face Spaces](https://huggingface.co/spaces).

Mentor: doc. dr. sc. [Nikola Tanković](https://ntankovic.unipu.hr)

<br />

## **:scroll: Feature description :scroll:**

One and only feature of this chatbot is to give an answer to the user query. A user query consists of a question and the process to which the question refers.

The implementation includes 2 separated applications that communicate with each other to achieve the goal. When the user submits a query on the Streamlit applicaiton, the application sends a HTTP POST request to the Gradio application that then feeds the query to the machine learning module. Module output is then returned and Gradio applicaiton sends a response with the answer in the body of the response.

These 2 apps communicate via Hugging Face Spaces (Gradio based) API `https://hf.space/embed/rkrstacic/Software-module-for-answering-questions-on-processes/+/api/predict`. It is a `HTTP POST` endpoint that accepts input payload: `"data": [question, process]` and returns object with `data` attribute with the list of 1 element, being the answer itself.

The request is being handled as following:

```py
import requests
import json

url = 'https://hf.space/embed/rkrstacic/Software-module-for-answering-questions-on-processes/+/api/predict'


def _query(payload):
    data = json.dumps(payload)
    response = requests.request("POST", url, data=data)
    return json.loads(response.content.decode("utf-8"))


def get_answer(question, process):
    return _query({"data": [question, process]})["data"][0]

```

<br />

## **:computer: How to run it on the local machine :computer:**

### Gradio application

Download [the Python script](https://huggingface.co/spaces/rkrstacic/Software-module-for-answering-questions-on-processes/blob/main/app.py), open it in the editor ([PyCharm](https://www.jetbrains.com/pycharm/), [VS Code](https://code.visualstudio.com/)), install all of the [necessary dependecies](https://huggingface.co/spaces/rkrstacic/Software-module-for-answering-questions-on-processes/blob/main/requirements.txt) (`pip install <module_name>`) and run the script.

### Streamlit application

Download [the repository](https://huggingface.co/spaces/rkrstacic/Chatbot-integration-built-on-processes/tree/main), open it in the editor ([PyCharm](https://www.jetbrains.com/pycharm/), [VS Code](https://code.visualstudio.com/)), install Streamlit (`pip install streamlit`) and run the script with [the Streamlit command](https://docs.streamlit.io/knowledge-base/using-streamlit/how-do-i-run-my-streamlit-script) (`streamlit run .../<path>/app.py`).
