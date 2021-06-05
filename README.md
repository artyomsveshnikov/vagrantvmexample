# Example virtual machines: OpenVPN Server (vpngateway) and some application server (server).

## Environment: HYPER-V, WINDOWS.

## Instructions:

1. Edit vagrant_machine.pub and insert your SSH public key.

2a. Execute the following command:

`vagrant up --provider=hyperv`

2b. If you want to create one VM:

`vagrant up VM_NAME --provider=hyperv`

Where VM_NAME:

vpngateway

server

## Troubleshooting.

Open issue to tell me about errors.
