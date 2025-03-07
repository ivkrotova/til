# How to configure different Git accounts on the same machine.

## 1. Generate SSH keys for each account.

```bash
ssh-keygen -t rsa -C "your-email1@example.com" -f "id_rsa_account1"
ssh-keygen -t rsa -C "your-email2@example.com" -f "id_rsa_account2"
```

## 2. Add the SSH keys to the SSH agent.

```bash
# Start the SSH agent
eval "$(ssh-agent -s)"

# Add each private key to the agent
ssh-add ~/.ssh/id_rsa_account1
ssh-add ~/.ssh/id_rsa_account2
```

## 3. Add public keys to GitHub.

```bash
cat ~/.ssh/id_rsa_account1.pub
cat ~/.ssh/id_rsa_account2.pub
```

## 4. Create an SSH Config File

```bash
# Open or create the SSH config file
nano ~/.ssh/config

# Add entries for each account
Host github.com-account1
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_rsa_account1

Host github.com-account2
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_rsa_account2
```

## 5. Clone Repositories Using Different Accounts

```bash
git clone git@github.com-account1:your-username/your-repo.git
git clone git@github.com-account2:your-username/your-repo.git
```

## 6. Configure Git for Each Account

```bash 
# Navigate to a repository directory
cd /path/to/repo1

# Set user details for repo1
git config user.name "Your Name 1"
git config user.email "your-email1@example.com"

# Navigate to another repository directory
cd /path/to/repo2

# Set user details for repo2
git config user.name "Your Name 2"
git config user.email "your-email2@example.com"
```
