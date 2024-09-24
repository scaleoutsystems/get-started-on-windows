# get-started-on-windows
Tutorial for getting started with FEDn in Windows

## Prerequisites: python environment and install FEDn

1. Go to python's official page https://www.python.org/ftp/python/3.12.6/python-3.12.6-amd64.exe to download the latest release for windows
2. Click on the downloaded executable installer file to start installation
3. Open Windows PowerShell, and test your new python install by running:
```console
python --version
```

if this does not work or if it shows you a earlier version than <3.12.6, you need to add the python install folder into you PATH environment variable:
REPLACE <Username>
```console
$env:Path += ';C:\Users\<Username>\AppData\Local\Programs\Python\Python312\'
```
Try again:
```console
python --version
```
4.  Next, make sure the python package manager "pip" is installed and is pointing to the correct python version (3.12):
```console
pip --version
```
5.  Create a python virtual environment (to avoid changing system wide python dependencies):
```console
python -m venv .venv
```

A new folder ".venv" should have been created.
Activate the new venv:
```console
.venv/Scripts/Activate.ps1
```

OBS! If you get a permission denied error, it means your user don't have the right permissions to run scripts in the PowerShell environment. 
Either try to run PowerShell as Admin or in CMD.exe run:
```console
.venv/Scripts/activate.bat
```

You know that the venv is activated when is says (.venv) in the beginning of the command line. 
6. Install Scaleout software FEDn by running:
```console
pip install fedn
```

7. Test fedn:
```console
fedn --version
```

## During Workshop/hands-on session
1. Sign-up at https://fedn.scaleoutsystems.com
2. In the "Project" for the workshop go to "clients" in the sidebar and click "Connect client". Click  the "Download" button. A "client.yaml" file should be located in your downloads folder. 
3.  Make sure you have the venv activated (see step 5)
4. Make a new folder:
```console
mkdir demo
```
```console
cd demo
```
5. Copy or move the downloaded "client.yaml" into the "demo" folder.
6. Start the fedn client:
```console
fedn client start -in client.yaml --secure=True --force-ssl
```

## Tutorial: FEDn package

1. Clone the fedn repository:
```console
git clone https://github.com/scaleoutsystems/fedn.git
```
2. Move into the mnist-pytorch example:
```console
cd fedn\examples\mnist-pytorch
```
3.  Run the "build" entrypoint of the project:
```console
fedn run build -p client --keep-venv
```
This command will create and compile the pytoch model needed as the initial model/seed of the federated workflow.

4. Next lets run the startup entrypoint, this entrypoint always runs at client startup:
```console
fedn run startup -p client
```
This will fetch the training data needed for the client in this example.

5. Finally lets test the train entrypoint:
```console
fedn run train -p -i seed.npz -o updated_model.npz
```

This command will test the train entrypoint why passing the seed model as input and updated_model.npz as the new updated (trained) model. 


