# Scripting with python and prefect

Prefect is a workflow orchestration framework for building resilient data pipelines in Python. Empowers developers to build and scale workflows quickly. For more information visit: [prefect](https://docs.prefect.io/3.0/get-started/quickstart)

Flows are defined as Python functions. They can take inputs, perform work, and return a result.
Adding @task decorators to any functions called by the flow converts them to tasks. The easiest way to convert a Python script into a workflow is to add a @flow decorator to the script’s entrypoint. This will create a corresponding flow. 

We define our script the next way:

```python
import shutil
import os
from prefect import task, flow

# Define a task to copy files from origin to dastination folder
@task
def copy_files(source_dir, target_dir):

    try:
        if not os.path.exists(target_dir):
            os.makedirs(target_dir)

        # Copy each file
        for filename in os.listdir(source_dir):
            file_path = os.path.join(source_dir, filename)
            if os.path.isfile(file_path):
                shutil.copy(file_path, target_dir)

                print(f"Archivo {filename} copiado a {target_dir}")

    except Exception as e:
        print(f"Error al copiar archivos: {str(e)}")

# We define our flow
@flow
def copy_files_flow():
    # Specify our origin and destination folders
    source_directory = "C:\\Users\\kim_j\\OneDrive\\Escritorio\\CTF\\Origin"
    target_directory = "C:\\Users\\kim_j\\OneDrive\\Escritorio\\CTF\\Dest"
    
    # Call the task we defined previously
    copy_files(source_directory, target_directory)


#copy_files_flow()
if __name__ == '__main__':
    copy_files_flow()
```

Flows are uniquely identified by name. You can provide a name parameter value for the flow, but if you don’t provide a name, Prefect uses the flow function name.

<br>

## Install Prefect

It's recommended to create a python virtual environment first and activate it. We can do it by executing the next lines (with Git Bash)
* `python -m venv virtual-environment-name`
* `source virtual-environment-name/scripts/activate`

Visit the [python-virtual-environment documentation](https://docs.python.org/3/library/venv.html) for more information

Now we can install prefect with: `pip install -U prefect`

![install prefect](https://github.com/CristopherLodbrok117/python-scripting-with-prefect/blob/799a02d754d105fad4e1b8ed3864cfd721aa3265/screenshots/0%20-%20install%20prefect.png)

Excecute `prefect server start` to connect to prefect

![prefect server](https://github.com/CristopherLodbrok117/python-scripting-with-prefect/blob/e2f40f1ff3c0847e431d4d0ff94c2500ae61829b/screenshots/999%20-%20prefect%20server.png)

Before visiting the prefect UI dashboard. Lets configure our workflows

<br>

## Deployment

Open a new terminal in VS code. And execute prefect init, choose your recipe and enter. In this example we're using the local option, 
![init](https://github.com/CristopherLodbrok117/python-scripting-with-prefect/blob/e2f40f1ff3c0847e431d4d0ff94c2500ae61829b/screenshots/03%20-%20init.png)

A yaml file is created automatically. Since we are using the default settings there's no need to modify the file . For more recipe or yaml configuration options visit [prefect deployments](https://docs.prefect.io/3.0/deploy/infrastructure-concepts/prefect-yaml#define-deployments-with-yaml)

<br>

To continue the condiguration
1. Execute the line `prefect deploy ` in the terminal.
2. Select the flow to deploy
3. Set a schedule for our flow run (in seconds)
4. Activate the deployment schedule (if you don't want to activate it immediately you can do it manually in the prefect dashboard later)

![deploy](https://github.com/CristopherLodbrok117/python-scripting-with-prefect/blob/e2f40f1ff3c0847e431d4d0ff94c2500ae61829b/screenshots/04%20-%20prefect%20deploy.png)


<br>

Select the work pool. If no list deploys, prefect will ask you to configure one quickly by asking a few questions like before. After choosing the work pool the next message is deployed with some interesting commands to execute and a link to the UI prefect deployment

![deployment condigured](https://github.com/CristopherLodbrok117/python-scripting-with-prefect/blob/e2f40f1ff3c0847e431d4d0ff94c2500ae61829b/screenshots/05%20-%20pool.png)


You can also create a work pool manually before the deployment configuration following this instructions [prefect-work-pool](https://docs.prefect.io/3.0/deploy/infrastructure-concepts/work-pools#configure-dynamic-infrastructure-with-work-pools)


* `windows_service_spring.jar`
* `WinSW.NET4.exe`
* `WinSW.NET4.xml` (originally it was sample-minimal.xml, but we need to rename it the same as the exe)

