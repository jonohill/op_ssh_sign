# op_ssh_sign

A script to generate ephemeral SSH keys, signed with a CA key from 1password.
Good for personal servers, not for teams (because it assumes you have the CA key stored in 1password).

## Dependencies

- Your SSH CA key must be stored in 1password.
- You need `ssh-agent` set up.
- These must be installed:
    - `op` - the 1password cli
    - `jq`

## Usage

The environment variables at the top of the script provide its configuration.
Before use, edit the script to set these values. Alternatively, set the environment variables outside of the script and those values will be used.

Then:

```
$ op_ssh_sign
```

Your new SSH key will be loaded into `ssh-agent`.
`ssh-add`'s output will be printed on success (with temporary paths shown, but these are cleaned up automatically).

## What does it do?

1. Generates a new SSH key pair.
2. Signs the public key with your SSH CA key from 1password (valid only for the configured time).
3. Loads this into ssh-agent (with expiry after the configured time).

## I don't understand what "SSH CA" means

SSH certificates are really great. Your keys can be short lived (hence this script) with no need to distribute keys.
If your servers are configured correctly you can also use SSH certificates to avoid the trust-on-first-use MITM problem.
To learn more, see the CERTIFICATES section of `man ssh-keygen`.
