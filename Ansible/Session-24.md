### Ansible vault
We are giving the passwords in the terminal but it is unsecure, so we use vault in the ansible, nothing but storage of secrets, for example below 
- Encoding ---> A proper pattern to encode the text, in this everybody can guess the secret.
- Encryption ---> Generating a random text with mathematic algorithm, so we encrypt ansible vault, so those
  who know the password they can only Dycrypt the password.

### How to create ansible vault ?
ansible-vault create /path/some-name.yaml

### Points to remember
- We use ansible.cfg to minimize the commands while running the script in server.
- If esc button is not working while saving the file you can use "ctrl+esc" button
