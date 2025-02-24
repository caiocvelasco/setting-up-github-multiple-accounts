# Steps to Set Up SSH for Multiple GitHub Accounts (Personal and Work)

## 1. **Generate a New SSH Key for Work**

- Open Git Bash.
- Run the following command to generate the new SSH key:
  ```bash
  ssh-keygen -t ed25519 -C "your_work_email@example.com"
  ```
  - For the file location, enter:  
    ```bash
    /c/Users/<YOUR_USER>/.ssh/id_ed25519_NAME_OF_YOUR_OTHER_ACCOUNT
    ```
  - Skip passphrase (or enter one for extra security).

## 2. **Add SSH Key to SSH Agent**

- Start the SSH agent:
  ```bash
  eval "$(ssh-agent -s)"
  ```
- Add your new SSH key:
  ```bash
  ssh-add /c/Users/<YOUR_USER>/.ssh/id_ed25519_NAME_OF_YOUR_OTHER_ACCOUNT
  ```

## 3. **Add the SSH Key to GitHub (Work)**

- Copy the SSH public key:
  ```bash
  cat /c/Users/<YOUR_USER>/.ssh/id_ed25519_NAME_OF_YOUR_OTHER_ACCOUNT
  ```
- Copy the output and go to GitHub:
  - **GitHub → Settings → SSH and GPG keys → New SSH key**.
  - **Title**: "Work Laptop".
  - **Key**: Paste the copied key.
  - Click "Add SSH Key".

## 4. **Configure SSH for Multiple Accounts**

- Open the SSH config file:
  ```bash
  nano ~/.ssh/config
  ```
- Add the following configuration:
  ```bash
  # Personal GitHub configuration
  Host github
      HostName github.com
      User git
      IdentityFile ~/.ssh/id_rsa

  # Work GitHub configuration
  Host github-YOUR_OTHER_ACCOUNT
      HostName github.com
      User git
      IdentityFile ~/.ssh/id_ed25519_NAME_OF_YOUR_OTHER_ACCOUNT
  ```
- Save and exit: `CTRL + X`, then `Y`, and `Enter`.

## 5. **Clone the Work Repository**

- Navigate to the folder where you want to clone the repo:
  ```bash
  cd "<YOUR_LOCAL_FOLDER_FOR_REPOS_PATH>"
  ```
- Clone the repository using the work GitHub configuration:
  ```bash
  git clone <THE_REPO_YOU_WANT_TO_CLONE.GIT>
  ```

## 6. **Verify SSH Authentication**

- Test the connection:
  ```bash
  ssh -T github-YOUR_OTHER_ACCOUNT
  ```
  You should see:
  ```bash
  Hi username! You've successfully authenticated, but GitHub does not provide shell access.
  ```

