# HOW TO CONFIGURE TWO OR MORE SSH KEYS TO HAVE MULTIPLE GIT ACCOUNTS ON THE SAME COMPUTER? (WINDOWS, LINUX, AND MACOS)

![Banner](./images/banner.png)

- [See on Medium](https://medium.com/@tanabebruno/como-configurar-duas-ou-mais-chaves-ssh-para-ter-diversas-contas-git-no-mesmo-computador-b9567621ce13)
- [See in Portuguese](README-PTBR.md)

If you've ever tried to manage more than one account on **GitHub**, **GitLab**, or any other version control service, you know it can be a challenge. One moment you're contributing to a personal project, the next you need to make a serious commit to your work account, and then... ❌ *“Permission denied (publickey)”*. Git simply doesn't know which key to use, and you're there, switching accounts, copying and pasting commands, or worse, logging in and out all the time. 😩

But don't worry! ✋ There's a practical, elegant, and definitive solution: **set up multiple SSH keys** on your computer. That way, each account will have its own identity, and Git will know exactly which one to use in every situation. **No conflicts, no frustrating errors, and best of all, no need to repeat configurations every time.**

In this guide, we'll show you the **step by step** to set up two or more SSH keys and manage multiple Git accounts on the same computer. Whether on **Windows, Linux, or MacOS**, you'll learn how to create, organize, and use your SSH keys efficiently, ensuring your commits always go to the right place. ✅

So, let’s solve these permission issues and get everything running smoothly? 🚀

---

## 📌 Table of Contents

🔍 **Let’s see what you’ll find in this guide?**

- [1. Why might you need multiple SSH keys? :key:](#1-why-might-you-need-multiple-ssh-keys-key)
- [2️. What are SSH keys and how do they work? :gear:](#2️-what-are-ssh-keys-and-how-do-they-work-gear)
- [3. Prerequisites :computer:](#3-prerequisites-computer)
- [4. Organizing the Repositories :package:](#4-organizing-the-repositories-package)
- [5. Generating the SSH Keys :lock:](#5-generating-the-ssh-keys-lock)
- [6. Creating Configuration Files for Each Git Account :page\_with\_curl:](#6-creating-configuration-files-for-each-git-account-page_with_curl)
- [7. Creating the General Configuration File and Redirecting Git :link:](#7-creating-the-general-configuration-file-and-redirecting-git-link)
- [8. Copying the SSH Keys to Add Them to the Services :cloud:](#8-copying-the-ssh-keys-to-add-them-to-the-services-cloud)
- [9. Adding SSH Keys to Services (GitHub, GitLab, Bitbucket, etc) :cloud:](#9-adding-ssh-keys-to-services-github-gitlab-bitbucket-etc-cloud)
- [10. Next Steps :rocket:](#10-next-steps-rocket)
- [Who is Bruno Tanabe?](#who-is-bruno-tanabe)

---

## 1. Why might you need multiple SSH keys? :key:

If you've ever tried to manage two or more accounts on **GitHub, GitLab, BitBucket**, or any other version control service on the same machine, you’ve probably encountered that fateful **“Permission denied (publickey)”**. ❌ This happens because your computer doesn’t know which SSH key to use when you have multiple accounts.

Now, imagine you have **two GitHub accounts**:

- 🏠 **One personal**, where you keep your projects and that repository full of experiments.
- 💼 **One for work**, where the commits need to be serious and professional (no more *final-final-v2-THIS-IS-THE-ONE* 🙈).

Another common scenario: you work for **multiple clients or projects** and need access to repositories on different services, each with its own credentials. Having separate keys avoids headaches, as each account can have its own SSH identity **without conflicts**. ✅

If you've been through this, relax. **You're not alone!** Git wasn’t designed to handle multiple accounts easily by default, but the good news is **there’s a solution**. And no, **you don't need to keep copying and pasting keys or logging in and out all the time**. 😌

Configuring **multiple SSH keys** on your computer is the secret to keeping your digital life organized, avoiding annoying mistakes, and ensuring your commits go to the right place. **And the best part: after setting it up, you won’t need to worry about it anymore!** 🎉

In this guide, you’ll learn how to set everything up correctly to **switch between accounts automatically, without a headache**. 🤩

---

## 2️. What are SSH keys and how do they work? :gear:

Before you start generating keys and configuring everything, it’s worth quickly understanding what **SSH** is and why it’s so useful for Git. 🧐

Imagine you have an **exclusive club**, and to get in, you need a special invitation that only you have. In the tech world, **SSH (Secure Shell)** works kind of like this: instead of typing passwords every time you want to access a server or a Git repository, you use a **pair of cryptographic keys** that ensure only you have permission to get in. 🔐

This key pair works like this:

- 🔑 **Private key:** Stored on your computer, like a secret only you know.
- 🔓 **Public key:** Goes to the server (**GitHub, GitLab, etc.**) and works as a **“lock”** that can only be opened by your private key.

When you try to connect, the server checks if your **private key** matches the **public key registered**. If they match, **access granted!** ✅

The best part? **You don’t need to type your password every time**, and the process is much more secure than storing passwords everywhere. 🔒 Now that you know how it works, let’s configure your **SSH keys the right way**? 😃

---

## 3. Prerequisites :computer:

Before you start setting up SSH keys, we need to ensure that **Git** is installed on your machine. Without it, nothing works. Here’s the **simple, no-nonsense step-by-step**:

### On Windows

1. [Go to the official **Git download page for Windows**](https://git-scm.com/downloads/win).
2. Download the version that matches your computer, **32-bit or 64-bit**.
3. After downloading, click the `.exe` file and run it as **Administrator**.
4. The classic installer will open with a lot of “Next” buttons. Just keep clicking **Next, Next, Next** and accepting everything — the default settings work just fine.
5. Once it’s done, open the terminal (**Command Prompt or PowerShell**) and type:

   ```bash
   git --help
   ```

If you see a list of Git commands, **all good!** If there’s an error, try restarting the computer and running the command again. 🔄

### On Linux

1. Open the terminal and type:

   ```bash
   git --help
   ```

If you see all the instructions and Git commands, **congratulations! Git is already installed.** 🎉

If the terminal says the command doesn’t exist, just install it with:

```bash
sudo apt install git
```

(This command is for Debian-based distributions like Ubuntu. If you're using a different distro, adjust it for your package manager.) 🐧

After that, type `git --help` again to confirm. If you see the long list of commands, **success** — Git is now ready to go! 🚀

### On MacOS

1. First, open the **Terminal** (you can search for "Terminal" in Spotlight or open it via Launchpad).
2. Type the following command and press **Enter**:

   ```bash
   git --help
   ```

If Git is already installed, it will show the list of commands and options — in other words, **everything’s good.** ✔️

If the terminal says the command doesn’t exist or asks to install command-line tools, it will likely pop up a window asking if you want to install **Xcode Command Line Tools**. You can accept it without fear, just click **Install** and follow the instructions. 📲

Once the installation finishes, test it again:

```bash
git --help
```

If you see the Git command list, you're all set! **It’s installed.** 🎉

**Note:** On Mac, Git usually comes pre-installed on most versions, so you might already have it without even knowing. 😉

---

## 4. Organizing the Repositories :package:

Now that we have Git installed, let’s organize the mess. The idea here is simple: **create a folder structure on your computer** to separate the repositories for each Git account you use — whether it’s **GitHub, GitLab, Bitbucket**, or all of the above.

For example, I have **two accounts**: one **personal** and another for **work**. So, I’ll create two folders, one for each account. But if you have three, four, or fifteen accounts (who knows, right?), just repeat the process for each one.

### Important

This **isn't the only way** to organize multiple Git accounts, but honestly, it's the **most practical, clean, and headache-free way** I know of. Can you use the same SSH key for two accounts? Sure. But **it’s not recommended**. Mixing keys can lead to a huge mess with permissions and security — not to mention that if you plan to use **GPG keys** later (I’ll talk about that at the end of the tutorial), everything will already be set up properly. 🔑

I like to create a folder called **Workspace** in the root of my user directory and keep everything there. But you can organize it however you want, wherever you want. 📂

### On Windows, Linux, and MacOS (same process)

Let’s go step by step. It works the same on **Windows, Linux, and MacOS**, so there’s no difference between systems here.

In this case, I’ll show you how I do it based on my folder structure, but feel free to do the steps however you want, including using the interface if that’s easier. If you want to follow my structure, just follow the steps below.

1. In the terminal, first go to the root of your user directory:

   ```bash
   cd ~
   ```

2. Now, create a folder called **Workspace** (or whatever name you prefer):

   ```bash
   mkdir Workspace
   ```

3. Enter the folder you just created:

   ```bash
   cd Workspace
   ```

4. Now let’s create the folders for each account. In my case, I’ll call them **Personal** and **Work**, but you can name them whatever you want, just make sure you know the folder names and their locations:

   ```bash
   mkdir Personal
   mkdir Work
   ```

Folders created, **organization is on point**. Now each folder will belong to the right account, with no risk of mixing different accounts in different projects. **Let’s create the SSH keys!**

---

## 5. Generating the SSH Keys :lock:

Now it’s time to generate the famous **SSH keys** — the ones that will ensure **Git** recognizes who you are without asking for your password every time. 🔑

Just like creating folders, you can generate these keys anywhere, as long as you configure the path correctly in the Git file (we’ll do that in step 7).
But, to keep everything organized and avoid headaches, I recommend following the standard that people use: store everything inside the hidden **.ssh** folder in the root of your user directory. It’s clean, practical, and works with most services. 👨‍💻

If you want to do it differently, that’s fine! Just don’t forget to write down the path and name of the keys, because we’ll need that later.

### On Windows, Linux, and MacOS

Let’s go through the steps — just like the previous step, the commands work the same on **Windows, Linux, or MacOS**:

1. Go back to the root of your user directory:

   ```bash
   cd ~
   ```

2. Create the **.ssh** folder (if it already exists, you can skip this command):

   ```bash
   mkdir .ssh
   ```

3. Enter the **.ssh** folder:

   ```bash
   cd .ssh
   ```

Now comes the important part: generating an SSH key for each account you’ll be using. 🔑

In my case, I have a **personal** account and a **work** account, so I’ll create two keys. The file names can be whatever you want — I like to give them names that help me remember which is which (but again, write down or remember the name and path of the file, you’ll need it later).

To generate the key for the **personal** account:

  ```bash
  ssh-keygen -f personal_ssh_key
  ```

To generate the key for the **work** account:

  ```bash
  ssh-keygen -f work_ssh_key
  ```

When you run each command, the terminal will ask if you want to set a **passphrase** for the key. This passphrase is **optional**. If you don’t want to type it every time (like I don’t), just press **Enter** twice.

The terminal will show a message like this:

  ```bash
  bruno-tanabe@Windows-Tanabe:~/.ssh$ ssh-keygen -f test_key
  Generating public/private ed25519 key pair.
  Enter passphrase (empty for no passphrase):
  Enter same passphrase again:
  Your identification has been saved in test_key
  Your public key has been saved in test_key.pub
  The key fingerprint is:
  SHA256:cuw52mK3WSC6iCDDL2/0Hjq18lxlc9slxlIlB1uimkw bruno-tanabe@Windows-Tanabe
  The key's randomart image is:
  +--[ED25519 256]--+
  |             +.+ |
  |            . B  |
  |         E . o   |
  |       .o o o    |
  |      o SB o + . |
  |.  . o =ooo = o  |
  |+.. +...+ .. .   |
  |o+.=o+=o.+       |
  |. =+*=.o+.       |
  +----[SHA256]-----+
  ```

Each key you generate will create **two files**:

- `your_key` → your **private key** (don’t share it with anyone! 🚫)
- `your_key.pub` → your **public key** (this is the one you’ll upload to GitHub, GitLab, etc. 🌐)

Repeat the process for each account you have.

Done! **Your SSH keys are created** and saved on your computer. In the next step, we’ll create the Git configuration files.

---

## 6. Creating Configuration Files for Each Git Account :page_with_curl:

Now that you’ve created your folders and generated your SSH keys, let’s move on to the next step: **creating the configuration files** for each Git account you have.

Basically, each account will have its own file with its information — **name, email, and which SSH key it should use**. This is what will allow Git to know which account to use for each project on the same machine, without getting confused. 💼

Once again: you can create these files wherever you want and name them whatever you like.

But, to keep things neat, I like to put them in a folder called **.git** in the root of my user directory. So, in this tutorial, we’ll follow that path — but feel free to organize it however you want. 🏡

### On Windows, Linux, and MacOS (common part)

1. First, go back to the root of your user directory:

   ```bash
   cd ~
   ```

2. Create the folder where the configuration files will be stored:

   ```bash
   mkdir .git
   ```

3. Enter that folder:

   ```bash
   cd .git
   ```

Now, let’s create the configuration files. The process varies a bit depending on your system:

### On Windows

1. To create the file for the **personal** account:

   ```bash
   echo > .gitconfig-personal
   ```

2. Open the file with **Notepad** (or any editor you prefer):

   ```bash
   notepad .gitconfig-personal
   ```

Inside the file, paste this information, adapting it to your personal account details (Remember when I asked you to write down or remember the name and path of the file? You’ll use that here, and if you followed the instructions, you won’t need to go back to check) 📋:

  ```ini
  [user]
      name = your personal account name
      email = your personal account email
  [core]
      sshCommand = "ssh -i path_to_your_ssh_key/your_ssh_key_name"
  ```

If you followed my setup, you’ll have a file similar to this:

  ```ini
  [user]
      name = Bruno Tanabe
      email = brunotanabe@personal.com
  [core]
      sshCommand = "ssh -i ~/.ssh/personal_ssh_key"
  ```

Save and close.

Now, I’ll repeat the process for my **work** account:

  ```bash
  echo > .gitconfig-work
  notepad .gitconfig-work
  ```

And inside the file:

  ```ini
  [user]
      name = Bruno Tanabe Work
      email = brunotanabe@work.com
  [core]
      sshCommand = "ssh -i ~/.ssh/work_ssh_key"
  ```

Save and done! ✅

**Reminder:** You need a `.gitconfig-reference` file for **each account** you want to configure, and inside it, you’ll put the **name, email, and SSH key path** for each. That way, Git will know exactly which account to use for each project.

### On Linux and MacOS

1. To create the file for the **personal** account:

   ```bash
   touch .gitconfig-personal
   ```

2. Open the file in any editor you prefer (I’ll use **Nano** here):

   ```bash
   nano .gitconfig-personal
   ```

Inside the file, paste this information, adapting it to your personal account details 📋:

  ```ini
  [user]
      name = personal account name of the information you are configuring
      email = email of the information you are configuring
  [core]
      sshCommand = "ssh -i path_to_your_ssh_key/your_ssh_key_name"
  ```

If you’re following the same setup as I am, your file will look similar to this:

  ```ini
  [user]
      name = Bruno Tanabe
      email = brunotanabe@personal.com
  [core]
      sshCommand = "ssh -i ~/.ssh/personal_ssh_key"
  ```

Save it (in Nano, press **CTRL + O**, then **ENTER**, and **CTRL + X** to exit). 💾

Now, I’ll repeat the process for my **work** account:

  ```bash
  touch .gitconfig-work
  nano .gitconfig-work
  ```

And inside the file:

  ```ini
  [user]
      name = Bruno Tanabe Work
      email = brunotanabe@work.com
  [core]
      sshCommand = "ssh -i ~/.ssh/work_ssh_key"
  ```

Save it, and you’re done! ✅

**Reminder:** You need a `.gitconfig-reference` file for **each account** you want to configure, and inside it, you’ll put the **name, email, and SSH key path** for each. That way, Git will know exactly which account to use for each project.

---

## 7. Creating the General Configuration File and Redirecting Git :link:

Alright, now that you’ve got the individual configurations for each account ready, it’s time to tie everything together. This file will be the central point, the file that tells your machine:

> “Hey, when I’m working in this folder, use this account. When I’m in that other one, use the other account.” 📂➡️👥

Unlike the previous steps, this file **must** be in the **root of your user** and named exactly **.gitconfig** — no fancy names, no moving it elsewhere.

### On Windows, Linux, and MacOs (common part)

First, return to the root of your user (as usual):

  ```bash
  cd ~
  ```

### On Windows

1. Create the file:

   ```bash
   echo > .gitconfig
   ```

2. Open it with **Notepad** (or any editor you prefer):

   ```bash
   notepad .gitconfig
   ```

Now, inside the file, you’ll add an **includeIf** block for each account you’ve set up. Basically, you’re saying:

“If the project is in this folder, use this configuration.” 📂⚙️

Fill in the file with the location of your folders and each of your configuration files:

  ```ini
  [includeIf "gitdir:path_to_your_personal_project_folder"]
      path = path_to_your_personal_config_file
  [includeIf "gitdir:path_to_your_work_project_folder"]
      path = path_to_your_work_config_file
  ```

Example of how it should look (if you followed the structure we’ve used so far):

  ```ini
  [includeIf "gitdir:~/Workspace/Personal/"]
      path = ~/.git/.gitconfig-personal
  [includeIf "gitdir:~/Workspace/Work/"]
      path = ~/.git/.gitconfig-work
  ```

**Important:**

- The folder you put in `gitdir` must be exactly the same as the one you created in the directory creation step. 📁
- The path in `path` must correctly point to the configuration file you created for each account.

Save and close the file.

### On Linux and MacOs

1. Create the file:

   ```bash
   touch .gitconfig
   ```

2. Open it with **Nano** (or any editor you prefer):

   ```bash
   nano .gitconfig
   ```

Now, inside the file, you’ll add an **includeIf** block for each account you’ve set up. Again, you’re saying:

“If the project is in this folder, use this configuration.” 📂⚙️

Fill in the file with the location of your folders and each of your configuration files:

  ```ini
  [includeIf "gitdir:path_to_your_personal_project_folder"]
      path = path_to_your_personal_config_file
  [includeIf "gitdir:path_to_your_work_project_folder"]
      path = path_to_your_work_config_file
  ```

Example of how it should look (if you followed the structure we’ve used so far):

  ```ini
  [includeIf "gitdir:~/Workspace/Personal/"]
      path = ~/.git/.gitconfig-personal
  [includeIf "gitdir:~/Workspace/Work/"]
      path = ~/.git/.gitconfig-work
  ```

**Important:**

- The folder you put in `gitdir` must be exactly the same as the one you created in the directory creation step. 📁
- The path in `path` must correctly point to the configuration file you created for each account.

Save and close it (in Nano, press **CTRL + O**, then **ENTER**, and **CTRL + X** to exit). 💾

---

## 8. Copying the SSH Keys to Add Them to the Services :cloud:

This step is quick: basically, you’ll copy the public part of the SSH key you created and paste it into the settings panel of the service you use. 🔑💻

The key you need to send to the service is always the file that ends with **.pub** (e.g., `personal_ssh_key.pub` or `work_ssh_key.pub`).

### On Windows, Linux, and MacOs

1. First, return to the root of your user (again):

   ```bash
   cd ~
   ```

2. Go to the folder where you store your SSH keys (in my case, they’re all stored in a hidden **.ssh** folder in the root of my user, so after the command below, I’ll be inside it):

   ```bash
   cd .ssh
   ```

3. Use this command to display the content of your public key and copy it, for example:

   ```bash
   cat personal_ssh_key.pub
   ```

The response from this command will be your public key, and it will look something like this (don’t share this key with anyone! No, this isn’t my actual key). 🤫

  ```txt
  ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIOVd+GSxOHO0ajlagl4DnHz8rgU/Ied1uSII7a+GfeXW brunotanabe@Windows
  ```

Or, if you want to copy the one for your work:

   ```bash
   cat work_ssh_key.pub
   ```

I recommend that you copy each key and add it to the corresponding service, alternating between steps 8 and 9. 🔄

---

## 9. Adding SSH Keys to Services (GitHub, GitLab, Bitbucket, etc) :cloud:

Good news: all the configuration on your computer is done! Now, there’s just one detail left to make everything work smoothly — let the version control services (GitHub, GitLab, Bitbucket, or any other) know that you have an SSH key and that they can trust it. 🔑💻

Now that you've copied the keys, it's time to paste them into your favorite service:

Here’s how to add the keys to the most popular version control services, but if you're using another, just find a similar section and add the keys there.

### GitHub

1. Go to: [https://github.com/settings/keys](https://github.com/settings/keys)
2. Click on **New SSH key**.
3. Give the key a name (e.g., **Personal** or **Work**).
4. Paste the public key content into the **Key** field.
5. Click **Add SSH key**. Done! ✅

### GitLab

1. Go to: [https://gitlab.com/-/profile/ssh_keys](https://gitlab.com/-/profile/ssh_keys)
2. In the **Key** field, paste your public key.
3. Give it a title to identify it (e.g., **Macbook Personal** or **Work**).
4. Click **Add key**. 🔑

### BitBucket

1. Go to: [https://bitbucket.org/account/settings/ssh-keys/](https://bitbucket.org/account/settings/ssh-keys/)
2. Click **Add key**.
3. In the **Label** field, give your key a name.
4. In the **Key** field, paste your public key.
5. Save it. 💾

And that's it! Now your machine and the version control service are speaking the same language. The next time you clone, push, or pull, the magic will happen without needing to type a password. ✨

**Note**: If you receive the following message when trying to interact with a repository in the cloud, just reply with **yes**.

```txt
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
```

---

## 10. Next Steps :rocket:

Now that you've configured everything, your machine is ready to go! You can clone repositories, make commits, push, pull… everything without a password, all smooth and working. 🎉

But… (there’s always a “but,” right? 😉)
Some companies like an extra layer of security and require you to sign your commits with a **GPG key** in addition to SSH authentication.

### What’s this GPG key?

In short: it's another layer of security that ensures the commit was really made by you and not by someone malicious who has access to the repository and wants to impersonate you. 🔐

When you sign a commit with GPG, it appears on GitHub, GitLab, or Bitbucket with a **"Verified"** badge — like a **blue check** on Twitter, but actually useful. ✅

### Advantages of Using GPG

- Adds more trust to the project history. 📜
- Prevents someone with repository access from making a commit “pretending to be you.” 🕵️‍♂️
- Some companies only accept **PRs** with signed commits. 🔒

If you want to learn how to generate, configure, and use GPG keys across multiple accounts (following the same simple approach), I also wrote an article on Medium about it. Here’s the link:

[Configuração de Chaves GPG para múltiplas contas Git (still under development)](https://medium.com/@tanabebruno)

That way, you’ll have your machine 100% secured and ready for any scenario. 🛡️

---

## Who is Bruno Tanabe?

If you’ve made it this far and haven’t wondered yet “Who the heck is this guy who made me configure all this?”, congratulations on your patience! But, if you’re curious, let me introduce myself quickly. 👋

I’m **Bruno Tanabe**, a backend and AI-focused developer, always creating scalable and innovative solutions (or at least trying to). If you liked the tutorial and want to chat, here are my contacts:

Find me here:

- [LinkedIn](https://www.linkedin.com/in/tanabebruno/)
- [GitHub](https://github.com/BrunoTanabe)
- [Email](mailto:tanabebruno@gmail.com)
- [Medium](https://medium.com/@tanabebruno)

Mission accomplished! 🎯

---
