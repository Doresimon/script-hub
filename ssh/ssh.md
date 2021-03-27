# SSH - Secure Shell Host

- default key path
  - `$user/.ssh`

## Base commands

- `ssh-agent`
  - `ssh-agent bash`
  - `ssh-agent -s`
- `ssh-add`
- `ssh-keygen`

## Generate keypair

```bash
ssh-keygen -o
```

## Add PEM file to SSH key chain

```bash
ssh-add /path/to/pemfile.pem
```
