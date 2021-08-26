# d365fo-template
Template for D365 FO (Microsoft Dynamics 365 Finance and Operations) projects (Git)

## Getting Started

1. Clone (or use the template) the repository on your development environment.
2. Add your models to the **Metadata** folder.

    Example structure:
    ```
    $/Metadata
    +---MyMainModule
    |   +---Descriptor
    |   |       MyMainModule.xml
    |   |
    |   +---MyMainModule
    |       +---AxClass
    |       |       MyClass.xml
    |       |
    |       \---AxTable
    |               MyMainTable.xml
    |
    \---MyOtherModule
        +---Descriptor
        |       MyOtherModule.xml
        |
        \---MyOtherModule
            \---AxClass
                    MyTestClass.xml
    ```
    
3. Create your Solutions and Projects on the **Projects** folder.
4. Edit the `registerSymbolicLink.ps1` and `unregisterSymbolicLink.ps1` script and change the `$AOSMetadataPath` to your `PackagesLocalDirectory` path. 
5. Open **Powershell** as administrator on the path of your repository and run the `registerSymbolicLink.ps1` script. 

    ```powershell
    > .\registerSymbolicLink.ps1
    ```

    This will create a symbolic link for the models on the **Metadata** folder to your `PackagesLocalDirectory` folder. That way, it would seem as if your model is still residing on the `PackagesLocalDirectory` folder.

6. Share your **Metadata** folder to Everyone and set the permission to **Read**.

### Adding new models to the repository

When creating a new model, you'll find the model on `PackagesLocalDirectory`. To add it to the repository, do the following:

1. Close Visual Studio.
2. Stop IIS, if necessary.
3. Stop Batch service, if necessary.
4. Cut the model from `PackagesLocalDirectory`.
5. Paste it to your `Metadata` folder.
6. Open **Powershell** as administrator on the path of your repository and run the `unregisterSymbolicLink.ps1` script. 

    ```powershell
    > .\unregisterSymbolicLink.ps1
    ```

    This will unregister all links from your Metadata folder to avoid issues when running the register script afterwards.

7. After unregistering your models, run the `registerSymbolicLink.ps1` script to register all models including the new model.
 
    ```powershell
    > .\registerSymbolicLink.ps1
    ```

8. Start IIS and the Batch service, if stopped.

9. Repeat these steps whenever you have to create a new model to include them on the repository.


