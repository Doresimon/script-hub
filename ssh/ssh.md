# SSH - Secure Shell Host

- default key path
  - `$user/.ssh`

## Base commands

- `ssh`
  - `ssh $destination`
  - `ssh $destination -i $private_key`
  - `ssh $destination -i $pemfile`
- `ssh-agent`
  - `ssh-agent bash`
  - eval \`ssh-agent\`
  - `ssh-agent -s`
- `ssh-add`
  - `ssh-add $key`
  - `ssh-add -l`
- `ssh-keygen`

## Generate keypair

```bash
ssh-keygen -o
```

## Add PEM file to SSH key chain

```bash
ssh-add /path/to/pemfile.pem
```
