# Launching the main automation script

To run the deployment script, you need to open a terminal/command line and
navigate to the root of the folder of the toolkit. The Docker image that starts at the correct script folder location.

Before beginning, you need to sign into the Azure CLI tool using the following
command:

> `az login`

This prompts you to log in using the Azure web interface. 

If your account is associated with more than one subscription, you'll then need to set the default subscription you're deploying resources to after you login:

> `az account set --subscription {subscription GUID}`

Once this is complete, you can launch a deployment from the terminal/command-line interface by launching the [vdc.py](../vdc.py) script:

`[Linux/OSX]`

> `python3 vdc.py {command} {environment type} {arguments}`

`[Windows]:`

> `py vdc.py {command} {environment type} {arguments}`

`[Docker]`

> `python vdc.py {command} {environment type} {arguments}`

## Command

There are two commands you can supply. 

- `create` executes a deployment. 
- `validate` executes a validation of the deployment. Note that some resources may actu
ally be deployed during a validation.

## Environment types

The enviroment type is either `shared-services`, `on-premises`, or `workload`  indicating which
type of the archetype you are deploying. More details about environment types are [here](../0-understand/environment-types.md).

## Arguments

There are several required and optional arguments that you can pass for a
deployment:

```
-path
--configuration-file-path
```

[Required] - Path pointing to the root parameters file for the archetype you want to deploy.

```
-m
--module
```

[Optional] - Specifies a single module within the archetype to deploy. This value is limited to the list of modulesin the `orchestration.modules-to-deploy` array of the archetype's configuration file.
If this argument is not specified, the script processes each of the resources in the order they appear in the array.

In a production environment, you should follow separation of responsibilities. This means that a single users is not likely to have rights to deploy all of the modules in an archetype.

This argument should not be used when deploying a simulated on-premises environment.

```
-rg
--resource-group 
```

[Optional] - Specifies the name of the resource group where th resources will be created. If the group does not exist, the script creates it. If this parameter is not specified, the script creates a resource group named using a combination of the organization name you set in your main parameters file and the resource type being deployed.

```
-l
--location
```

[Optional] - Specifies the Azure region to use when deploying resources. If the region value in your main parameters file is blank, this parameter is required.

```
--deploy-dependencies
```
 [Optional] - Deploy module dependencies. If present, the script deploys any modules that are listed as dependencies for the module you're currently deploying. The dependencies for a modules are defined in each archetype's configuration file. Meaning that the dependencies for a module can vary by archetype. Look for the `dependencies` array in the module configuration in the archetype configuration file.

If the user running this command does not have the correct permissions to run all of the dependent modules, setting this argument can generate errors. In addition, if the dependent modules have already been run for this deployment, the script *redeploys* these resources using the latest parameter values.

```
--upload-scripts
```

[Optional] - If present, the [scripts](../../scripts) folder gets uploaded to the default storage account. Resource deployments will only upload the common toolkit scripts to Azure storage if this argument is included. It's important to use this when deploying any resources that depend on scripts to finish their configuration, like ADDS servers and NVAs. Note this will overwrite any existing scripts previously uploaded.

```
--prevent-vdc-storage-creation
```
[Optional] - By default, deployments will create a new storage account for output and scripts if one does not exist. Including this argument will prevent this, and only deploy if the target storage account exists. Storage account name is set in the archetype configuration file in the `vdc-storage-account-name` parameter.

## Example

This example deploys the paas archetype and uploads the scripts folder.

`[Docker]`

> `python vdc.py create workload -path ./archetypes/paas/archetype.json --upload-scripts`

`[Linux/OSX]`

> `python3 vdc.py create workdload -path ./archetypes/paas/archetype.json --upload-scripts`

`[Windows]:`

> `py vdc.py create workdload -path ./archetypes/paas/archetype.json --upload-scripts`

