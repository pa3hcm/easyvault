# Easyvault

This is a simple shell script which allows you to store EasyRSA keys and certificates in HashiCorp Vault. It may help you to run your own local CA; you can enjoy the simplicity of EasyRSA while using the security and flexibility of Vault to manage and provide your keys and certificates.

## Vault setup

HashiCorp Vault and EasyRSA should be initialized/configured already.

* Create a KV2 keystore in your HashiCorp Vault instance.
* Create a secret named 'ca-secrets', with the following key-value pairs:

  ```
  ca_passphrase: <the passphrase for your CA>
  cert_passphrase: <the passphrase used to encrypt your certificate keys>
  ```

* Copy `easyvault` and `.easyvaultrc` to your EasyRSA CA directory (that's where the `easyrsa` script is).
* Review the settings in your `.easyvaultrc` file.

  ```
  VAULT_URL=https://vault.mydomain.com:8200/  # URL of your Vault instance
  VAULT_IMAGE=hashicorp/vault:latest          # Docker image used for communicating with Vault
  MOUNT=kv                                    # Name of your kv2 store
  DATAPATH=ca-certs                           # Base path in your kv2 store for all keys/certs
  SECRETSPATH=ca-secrets                      # Secret path in your kjv2 store that holds your passphrases
  ```

* Set your `VAULT_TOKEN` environment variable.

You probably want to create an ACL in Vault to limit access to your CA data. This configuration strongly depends on your Vault setup, so can't be mentioned here.

## Usage

Run `./easyvault save` to save your current keys and certificates to secrets under `ca-certs` in your KV2 store.

Run `./easyvault load` to load all certificates from Vault into EasyRSA.

Run `./easyvault list` to list all certificates currently stored in Vault.

## License: GPL 3.0

Copyright (C) Ernest Neijenhuis PA3HCM

Easyvault is free software: you can redistribute it and/or modify it under the
terms of the GNU General Public License as published by the Free Software
Foundation, either version 3 of the License, or (at your option) any later
version.

Easyvault is distributed in the hope that it will be useful, but WITHOUT ANY
WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A
PARTICULAR PURPOSE. See the GNU General Public License for more details.

You should have received a copy of the GNU General Public License along with
Easyvault. If not, see `http://www.gnu.org/licenses/`.

## Project information

Author: Ernest Neijenhuis
Code on Github: `https://github.com/pa3hcm/easyvault`
