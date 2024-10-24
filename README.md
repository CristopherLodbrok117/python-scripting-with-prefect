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

## Install Prefect

It's recommended to create a python virtual environment first and activate it. We can do it by executing the next lines (with Git Bash)
* `python -m venv virtual-environment-name`
* `source virtual-environment-name/scripts/activate`

Visit the [python-virtual-environment documentation](https://docs.python.org/3/library/venv.html) for more information

Now we can install prefect with: `pip install -U prefect`

![install prefect](https://github.com/CristopherLodbrok117/python-scripting-with-prefect/blob/799a02d754d105fad4e1b8ed3864cfd721aa3265/screenshots/0%20-%20install%20prefect.png)

Excecute `prefect server start` to connect to prefect

Vefore visiting the prefect UI dashboard. Lets configure our workflows

## Deployment


* `windows_service_spring.jar`
* `WinSW.NET4.exe`
* `WinSW.NET4.xml` (originally it was sample-minimal.xml, but we need to rename it the same as the exe)

