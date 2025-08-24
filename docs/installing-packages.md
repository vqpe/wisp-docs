# How to Install/Uninstall Packages

## Installing Packages

1. Open your Server's Panel
2. Locate the `Startup` Tab at the top (or left) bar of your Server's page
3. Locate the `Additional Python Packages` field
    This may appear different depending on which Egg your Server is running on
4. Put in all the packages that your [bot needs](#how-can-you-know-what-packages-your-bot-needs)
Make sure you only put Package names, seperated by Spaces, example: `datetime discord python-dotenv`
5. You might need to press "Save" if you're on the custom Panel, if you're on Pterodactyl, it will automatically save (indicated by a blue bar at the top)
6. These Packages will now be automatically installed upon next start of your Server

---
##### For Python Servers, there's another way of installing Packages;

1. Open your Server's Panel
2. Locate the `Files` Tab at the top (or left) bar of your Server's page
3. Create a `requirements.txt` file
4. Put in all the packages that your [bot needs](#how-can-you-know-what-packages-your-bot-needs)
Make sure you only put Package names, seperated by Newlines, example:
`datetime`
`discord`
`python-dotenv`
5. These Packages will now be automatically installed upon next start of your Server
If this is not the case, make sure that the `Requirements File` field in your Server's `Startup` Tab is correctly set to `requirements.txt`

## Uninstalling Packages

This varies between Server Eggs;

For Python, you need to delete the `.local` folder in your Server's filetree, as this folder holds all of your Packages.
If you want to uninstall a specific Package, you can go into `.local\lib\python3.12\site-packages\` and delete the specific Package folders there.

For Node.js, you can go back to the Startup Tab and find `Uninstall Node Packages`, and similar to the installing process, any Packages you list here will be uninstalled upon next start of your Server.
Or if you want to delete all Packages, simply delete the `node_modules` folder.

## Troubleshooting

##### Not installing

You might encounter that even though you have all Packages your bot needs in the 'Additional Python Packages' field, but it still says that X Package wasn't found.
This happens because if you put preinstalled modules (for example time or os), it'll error (as it can't be externally installed) and any other modules that you also have in the box won't get installed, because the process aborts due to an encountered error.

For example, if your 'Additional Python Packages' looks like this:
`time discord python-dotenv`
The `time` install will error due to it coming preinstalled with Python, causing `discord` & `python-dotenv` to not get installed.

This issue will also occur if you enter a non-existent Package, like `hagshdgsd`

---

##### No space left on device

You might see
`ERROR: Could not install packages due to an OSError: [Errno 28] No space left on device` 
when trying to install Packages, this could be caused because of 2 things:

1. The Node's total Storage might be full, which will then mean that there isn't any Space left for your Packages to be installed.
To fix this, you just have to wait, as cache is often cleared to free more Space.

2. Your Server's `TMPFS` (Temporary File System) size is too small to install your Packages (usually if the Packages you're trying to install are >500MB total)
To this, there's 2 Fixes:
        
    1. Install Packages in smaller batches, or one by one, this will reduce the total size of the Packages you're installing in that batch, thus less will be in the TMPFS, and it will successfully install.
    2. If one singular Package is bigger than your Server's TMPFS size, you can ask David to temporarily increase your Server's TMPFS size in order to install the Package.

---

##### Other installation issues
Though quite rare, it could happen that somehow your Package data gets messed up, thus causing weird errors when trying to install or use them.
You can attempt to fix this by deleting the `.local` & `.cache` folders (Python) or `node_modules` folder (Node.js) on your Server and attempt to reinstall all Packages.


## How can you know what packages your bot needs?

You will get an Error if you try and import a Package that you don't have installed.
For Python this will begin with something like: `/home/container/main.py", line 1, in <module> import discord ModuleNotFoundError: No module named 'discord'`
Or for Node.js it will have something like: `Error: Cannot find module 'discord.js'`

Then just add the Package name into the list for Pacakges to install.

Sometimes, the Package names in these Errors do not reflect the Package name used for installation, for example, the Pillow Package in Python:
It is installed via: `pip install Pillow`
But imported via: `import PIL`

For these cases, just search up the Package name in the Error to find out what the name for installing it is.