---
title: Getting set up for the JASMIN Workshop
author: Matt Pritchard
---

> **_NOTE:_**  This exercise is written for participants of the **JASMIN Workshop** events. At these events, training accounts are temporarily assigned to course participants. In this way we can make sure that all participants have access to all the necessary resources and can minimise logistical issues during the events.
For continued use of JASMIN beyound the duration of these workshop events, or for use of the training materials outside of one of the organised events, users are asked to apply for their own, regular JASMIN account via the normal process if they don't already have one.

# Exercise 0: Getting set up for the JASMIN Workshop

### Scenario

I want to get my environment set up on my local machine so that I am ready to work through exercise 1 of the JASMIN Workshop.

### Objectives

After competing this exercise I will be able to:

 * Get hold of the resources I need for setting up my environment.
 * Set them up ready for working through exercise 1.

### JASMIN resources

 * Training account
    * You will be provided with access to an account which is already set up with all the privileges you need to complete the workshop exercises.
    * Normally, users manage their accounts and these privileges via the [JASMIN Accounts Portal](https://accounts.jasmin.ac.uk) - you may see or hear this mentioned in the exercises, but if you are using a training account you should not need to use it at least for exercises 1-5.

### Local resources

 * **Email address**
    * You will have been contacted in advance of the workshop event to provide an email address.
    * The JASMIN team will have linked your email address to one specific training account: you will be sent the details and credentials for this account.
 * **Training account credentials**. You will be sent the items in the list below, and the instructions in this exercise will cover how to set up your local machine to use them:
    * SSH Key pair
    * Passphrase for SSH Key
    * username for the training account
    * password for the training account


### Introduction

The [Overview presentation](../overview) given at the start of the workshop will cover much of the what / why / where / how questions you may have, so this initial exercise is about setting up what you will need in order to take part, rather than learning about how you can use JASMIN.

The course does assume some basic knowledge listed below. There are plenty of good learning resources and tutorials in existence already, so rather than duplicate these, we have concentrated in the workshop on aspects specific to working on JASMIN.

You may struggle to work on JASMIN without a basic knowledge of these topics:

   * Using a command-line (also known as terminal or shell) environment to execute commands to carry out tasks
      * If you have only ever used a computer in "point-and-click" mode, for example in Windows or MacOS, you will need to learn some basics about using command-line tools.
      * The operating system used on JASMIN is Linux (currently CentOS7).
      * The default shell used on JASMIN is `bash`.
      * We will show our recommended way of getting to a command-line environment on each of Windows, MacOS and Linux.
   * Concepts such as "client", "server", and that particular protocols (or methods) enable you to connect from your local machine (i.e. your laptop or desktop) to a remote machine and run commands on it.
   * Organising data into files and directories (also known as folders)

### Which tool should I use to connect to JASMIN?

This depends on whether the things you want to do on JASMIN are likely to need to display graphics, or whether the programs or applications you plan to use just produce text output.
You can use both, but your choice of tool might be different for each.

Here are our recommendations:

| Local machine | Text only | Graphical output |
| - | - | - |
| Windows | `MobaXterm`* | NoMachine Enterprise Client* |
| MacOS | `Terminal` | NoMachine Enterprise Client* |
| Linux | `Terminal` or `xterm`| NoMachine Enterprise Client* |

<br>

> **_NOTE:_**  We recommend using NoMachine Enterprise Client, in combination with specific servers on JASMIN, instead of [X11 graphics](https://en.wikipedia.org/wiki/X_Window_System) because performance is much better over the network to your local machine. This is particularly recommended if you need to use a graphical user interface to control an application, for example manipulating a large satellite image.

> **_NOTE:_**  We recognise that other applications are available for each of these choices, but in order to keep the instructions as similar as possible between different platforms, we would ask that you stick to these recommendations at least for use during the workshop. If you choose another option and it doesn't work as you hope, we may not be able to help.

For the options marked `*` above, **you'll need to download and install software to run on your own/local machine, to do this before taking part in the workshop**. You should check that you have sufficient privileges (permissions) on your local machine to do this. If in doubt, ask the IT support team responsible for your **local** machine.

We'll cover all of these combinations, so please follow the instructions relevant to your local machine to ensure you have everything you need for the workshop.

The overall concept is as follows. All the applications we'll cover follow the same overall process:

* You have an SSH key consisting of 2 parts: public and private.
   * The *private* key (`id_rsa_jasmin`) stays with you on your local machine.
   * For your training account, the *public* key `id_rsa_jasmin.pub` is already put into the right place at the JASMIN end for you.
* The software which you use to connect to JASMIN needs to "present" your private key, but to do that, first you have to load it, which involves "unlocking" it with its passphrase. 
> **_NOTE:_**  Private keys for accessing JASMIN must always be protected with a strong passphrase. **DO NOT** use an unprotected private key, and **DO NOT** share your key with anyone else. JASMIN has a strict **1 key, 1 user** policy.

You will also need to enable "agent forwarding", meaning that the same key can be used for onward connections to other machines as well as the first one. Different applications have different ways of applying this setting.
* When you use your application to connect to a JASMIN server, under the hood there's a check that the 2 halves of your key match. If they don't, you'll be denied access.
* Once you're connected, you can make onward connections to other machines inside JASMIN using the same key. But importantly, the private key does not need to be copied to JASMIN: it should stay **only** on your local machine. This helps to keep it secure.

The details of how each software tool does this may look different, but they're all essentially doing the same thing. Setting up each application will involve (not necessarily in the same order):
1. Installing the software, unless it's something built-in to your operating system
2. Telling it where your private key is, on your local machine
3. Loading that private key, using the passphrase, and enabling agent forwarding
4. (in some cases) Setting up "connection profiles" to connect to particular remote machines of your choice

In most cases, you are able to load your key into an "agent" or key manager, which means that your key remains loaded across any individual terminal sessions you open using that software. The alternative is that you need to load your key each time you open a new terminal session. Either should work, but the former can be more convenient as you only need to enter your passphrase when you first open the software, rather than for each connection.

Once all that is done, you're (almost) ready to make a connection to a remote machine.

For all the methods below, you will need to provide the location of the private key which the JASMIN team will have sent you prior to the workshop event. You should save this somewhere safe as follows: (create the directory indicated if it doesn't exist already)

|System|Location|
|-|-|
|Windows|`Desktop\ssh` (a folder called `ssh` on your Desktop)|
|MacOS|`~/.ssh` (a directory called `.ssh` in your `$HOME` directory)|
|Linux|`~/.ssh` (a directory called `.ssh` in your `$HOME` directory)|

> **_NOTE:_**  On MacOS, you may not see "hidden" directories in `Finder` unless you have enabled this in your Preferences, but you can temporarily enable this with `cmd + L-Shift + .` 

<br>

### Windows

Our recommended choice for a terminal application on Windows is **MobaXterm**.

#### Software installation
* Download from [MobaXterm](https://mobaxterm.mobatek.net/).
* Choose the "Home Edition" (free), then either the "Installer edition" or "Portable Edition" and follow the instructions.

[![MobaXterm v20.6 setup on Windows, loading private key](https://img.youtube.com/vi/yG8yyTt2R-0/0.jpg)](https://www.youtube.com/watch?v=yG8yyTt2R-0)

In the above video, you can see the steps needed to load the key, i.e:

* Tick "Use internal SSH agent "MobAgent"
* UN-tick "Use external Pageant"
* Tick "Forward SSH agents" **important**
* Click the "+" symbol to locate your private key file (i.e. wherever you put `id_rsa_jasmin`, above)
* Click OK to save the settings. MobaXterm will now need to restart.
* When you restart MobaXterm you will be prompted for the passphrase associated with your private key.

Click "Start local terminal".

You can then check that your key is correctly loaded with this command in the terminal window: 

> **_NOTE:_**  In this exercise, all the workshop exercises and in JASMIN documentation, when we're showing commands and their output, the `$` at the start of a line simply represents the command prompt: **it is not a character which you need to type**. Lines without the `$` at the start represent output from a command.


```
$ ssh-add -l
```
If you see a message similar to the following, your key is correctly loaded:
```
2048 SHA256:0y7Oh7J+kN6hPotWCerXsZBlRBL205UMGlJVZ1I0A8c you@somewhere.ac.uk (RSA)

```
If not, you will need to try again before you will be able to log in to a remote host using the key.

### MacOS

Our recommended choice for a terminal application on MacOS is the `Terminal` app. Find this by searching in the "spotlight search" (magnifying glass, usually top-right in the Apple menu bar). If you're using it regularly, it may help to right-click its Dock icon and select "Options > Keep in Dock".

In a new terminal window:
```
$ ssh-add ~/.ssh/id_rsa_jasmin
```
You can add the `-K` option here: this stores the passphrase in your KeyChain, so that it's available whenever you're logged in to your Mac. Obviously, **only** do this on a machine where your initial login after rebooting is protected by a strong password and/or fingerprint ID.

You'll be prompted for your passphrase at this point.

> **_NOTE:_**  [Advanced users] You can also add that same line to your `~/.bashrc` so that this is automatically done for you in each new terminal window you open. Only when you reboot your machine will you be prompted for your passphrase.
For full details see the `man` page for `ssh-add`.

In the same terminal window, check that your key is now loaded:

```
$ ssh-add -l
```
You should see output like this:
```
2048 SHA256:0y7Oh7J+kN6hPotWCerXsZBlRBL205UMGlJVZ1I0A8c you@somewhere.ac.uk (RSA)

```
If not, you will need to try again before you will be able to log in to a remote host using the key.

### Linux

The Linux platform has various terminal applications available depending on which flavour of Linux and which desktop manager you use: there are too many to cover them all, but the command-line instructions should be the same.

Start your terminal application (`Terminal` or `xterm`). If you're in a desktop environment, you may find this in a menu or by using the search.

Then, initiate an agent to store your key:
```
$ eval $(ssh-agent -s)
Agend pid XXX       (where XXX is some process ID)
```

Now, load your key, having stored it in your `~/.ssh` directory:
```
$ ssh-add ~/.ssh/id_rsa_jasmin
```

Check it's loaded
```
$ ssh-add -l
```
You should see output like this:
```
2048 SHA256:0y7Oh7J+kN6hPotWCerXsZBlRBL205UMGlJVZ1I0A8c you@somewhere.ac.uk (RSA)

```
If not, you will need to try again before you will be able to log in to a remote host using the key.

### Network Considerations

JASMIN is an academic research infrastructure primarily designed to be accessible from other acadmic research networks. As such, and as part of a layered approach to security, it is preferred that you access JASMIN from your institutional network. This means that if you are connecting from home via your home broadband internet service provider, it is preferred that you first access your insitutional network and then connect from a host there, or that you use your instutional Virtual Private Network (VPN) to obtain an IP address which belongs to your institutional network before making your connection.

Please consult the [documentation here](https://help.jasmin.ac.uk/article/190-check-network-details) about how to check whether your connection meets the criteria.

If it does, then you can use the "standard" login servers, `login[1,3,4].jasmin.ac.uk` and `nx-login[1,3].jasmin.ac.uk` (see below for what the `nx-` login servers are for).

If it does not, then you can use the "contingency" login servers, currently `login2.jasmin.ac.uk` and `nx-login2.jasmin.ac.uk`. You may not be able to use the transfer servers, however, so this may affect *some* of what you can do in [exercise 3](../ex03), and it's something you might need to sort out with your local IT support if you plan to register to use JASMIN longer-term after the workshop.

We'll cover how to actually connect to the login servers in [exercise 1](../ex01), but please bear this in mind for your choice of server to connect to. 

### Graphical desktop (Optional)

> **_NOTE:_**  We are aware of some problems with the software needed for this part of the set up: possibly due to a problem with the latest version of the software. We are investigating further. So if this doesn't work for you, don't worry, it's not essential. Just use one of the command-line terminal clients described above for now.

Using graphical applications over a wide-area network (such as the path between your university and JASMIN) can be very slow, and is not recommended or supported on JASMIN. This service helps by providing a graphical desktop *within* the JASMIN environment, instead of on the end-user’s local machine at the end of a long network path from JASMIN. A small client application enables you to connect to specific servers within JASMIN but send the graphics output back across the network to you in compressed form, resulting in much better performance.

In short: if you use this application for graphics, it'll work much better than using XWindows to your own machine (which may be what you're more used to doing)

The virtual desktop provided by this service also includes a web browser ("within" JASMIN) so provides a means of accessing web-based resources which are not available outside of JASMIN's internal network (some specialist applications require this, and it should not be used for general web-browsing).

So, why would you need to use this rather than the basic command-line terminal?
* If anything you plan to do on JASMIN involves viewing or interacting with graphical output.
* If you need to control an application using a graphical user interface
* If you need to access web resources only available inside JASMIN

To use this service (and we'll cover **how** to in [exercise 1](../ex01) ) you will need to use an application called NoMachine Enterprise Client: this is a *client* in the same way as the other SSH terminal clients mentioned above (i.e. it connects to a *server* within JASMIN), but with the extra feature of being able to display your virtual desktop for you.  

Each of the servers `nx-login[1,2,3].jasmin.ac.uk` has special software installed to enable connections made using the **NoMachine Enterprise Client**. So this client needs to be installed locally on your own machine if you want to use this service.

The instructions for downloading and installing the software vary by platform, but once it's installed, it operates nearly identically across Windows, Mac and Linux.

* Download the [NoMachine Enterprise Client](https://www.nomachine.com/download-enterprise#NoMachine-Enterprise-Client), choosing the right version for your local machine.
* Follow the instructions to install it on your machine
* Open the application
* Follow one of the videos below to set it up so that it can use your private key. You will see that they're all fairly similar.

For a full description of the steps involved, see also our [help documentation](https://help.jasmin.ac.uk/article/4810-graphical-linux-desktop-access-using-nx) for this service.

|Platform|Video|
|-|-|
|Windows| [![NoMachine Enterprise Client v7 on Windows](https://img.youtube.com/vi/-O-Ec4lZJuE/0.jpg)](https://www.youtube.com/watch?v=-O-Ec4lZJuE) |
|Mac| [![NoMachine Enterprise Client v7 on MacOS](https://img.youtube.com/vi/R9zb3LbrlJE/0.jpg)](https://www.youtube.com/watch?v=R9zb3LbrlJE)|
|Linux| [![NoMachine Enterprise Client v7 on Linux](https://img.youtube.com/vi/g22dDHX7Tt0/0.jpg)](https://www.youtube.com/watch?v=g22dDHX7Tt0)|


One final note: 

> **_NOTE:_**  Any account credentials but also scripts, configuration, code or data belonging to or created by your training account will be wiped after some short period (normally 48hrs) following the end of the workshop event. This is to preserve resources and clean up, but also to maintain security and to prepare the accounts for the next set of training users.
You will be reminded of this during the course and should make sure you retrieve or copy away any items that you want to keep either before the end of the course, or within the 48hrs following the end of the course.

<br>

Hopefully, if you've got this far, you should be good to go for the JASMIN Workshop. We look forward to seeing you there!

