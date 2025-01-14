# DLLirant

**[IMPORTANT]** I am currently working on the new .NET version, so I recommend you to compile the project by yourself if you want to have a more stable version

DLLirant is a tool to automatize the DLL Hijacking and DLL Proxying researches on a specified binary.

![alt text](https://raw.githubusercontent.com/Sh0ckFR/DLLirant/main/screenshot.png)
![alt text](https://raw.githubusercontent.com/Sh0ckFR/DLLirant/main/screenshot2.png)
![alt text](https://raw.githubusercontent.com/Sh0ckFR/DLLirant/main/screenshot3.png)

## Live Demo

![alt text](https://raw.githubusercontent.com/Sh0ckFR/DLLirant/main/live.gif)

## How to install

* Install LLVM for Windows: https://llvm.org/builds/
* Do not forget to check the "Add LLVM to the system PATH for current user" during the installation.
* Install pefile from pip (only for the old python version):

```
pip3 install pefile
```

## How to use (.NET version)

Left click, left click and left click again.

Just in case, if you want to use the DLL Proxying feature, do not forget to use names like "proxy.dll" in the textbox or absolute paths like "C:\\Windows\\System32\\yourdll.dll".

And you have only 10 seconds to click on each error dialogs generated by your targeted application (I must fix it later).

You can also create an `import` directory and place the missing DLL files that your application if necessary (the DLL files will be copied automatically in the `output` directory with the targeted binary).

## How to use (Python version)

Use the `cd` command to your DLLirant directory and to test a binary:

```
python3 DLLirant.py -f "C:\THEFULLPATH\YourBinary.exe"
```

If you want to create a proxy dll, you can use the -p option on the original vulnerable dll (read https://itm4n.github.io/dll-proxying/ for more informations):

```
python3 DLLirant.py -p "C:\THEFULLPATH\VulnerableDLL.dll"
```

## How it works (Python version but .NET is similar)

The script will create an output directory in the same directory of DLLirant.py, copy the targeted binary to the output directory.

Via the pefile library, the script will extract the dll names required by the binary, and test each imports functions available one by one by compilate a custom DLL with the required exported functions.

If a function required by the binary is executed, the custom DLL will create a `C:\\DLLirant\\output.txt` file and display a MessageBox to be sure that a DLL Hijacking is possible.

A `results.txt` will be also created in the DLLirant directory with all potential DLL Hijacking available.

A file `admin-required.txt` will also be available for the potential DLL Hijacking who require specific privileges.

If a binary require a DLL from the system or another one, you can create a `import` directory in the same directory of `DLLirant.py` the script will copy all your DLL files in the `output` directory with your targeted binary.

## Know issues

- ERROR: The process "39456" not found. -> This is a normal behavior, DLLirant try to kill the process automatically, if the process is already killed, you will see this exception, just ignore it.

## Technical posts (in French)

* https://sh0ckfr.com/pages/martine-a-la-recherche-de-la-dll-hijacking-perdue/
* https://sh0ckfr.com/pages/martin-et-le-dll-proxying-de-cristal/

## Credits

* [am0nsec](https://twitter.com/am0nsec)
* DallasFR
* Justin Bui from SpecterOps for his blogpost and the idea: https://posts.specterops.io/automating-dll-hijack-discovery-81c4295904b0
* itm4n for his blogpost about DLL Proxying: https://itm4n.github.io/dll-proxying/
* [bik3te](https://twitter.com/bik3te)
* The authors of the pefile library: https://github.com/erocarrera/pefile
