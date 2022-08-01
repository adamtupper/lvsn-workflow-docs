# Connecting to Workstations and Compute Nodes via SSH

## Prerequisites

If you've never used SSH before, GitHub provides some great documentation on [getting started with SSH](https://docs.github.com/en/authentication/connecting-to-github-with-ssh).

## Configuring Your SSH CLient

LVSN workstations and compute nodes can all be accessed via Secure Shell (SSH) [[Windows](https://docs.microsoft.com/en-us/windows/terminal/tutorials/ssh), [macOS](https://support.apple.com/en-ca/guide/mac-help/mchlp1066/12.0/mac/12.0)]. This section describes *one* way to configure SSH on a personal device so that you can easily access, i.e. *SSH into*, these machines. Example SSH configurations for Windows, Linux, and macOS are provided below. These provide a configuration for `pika`, the proxy server through which other machines on the department network are accessed and `lv3-32187`, one of the Institute intelligence et données (IID) compute nodes. See  [Available Compute Nodes](available_compute_nodes.md) for a full list of available compute nodes you can configure.

<details>
<summary>Windows/Linux</summary>

```ssh-config
Host *
    AddKeysToAgent yes
    IdentityFile ~/.ssh/id_ed25519

Host pika
    HostName pika.gel.ulaval.ca
    ForwardAgent yes
    User IDUL
    ServerAliveInterval 120
    IdentityFile ~/.ssh/id_ed25519

Host iid187
    HostName lv3-32187.gel.ulaval.ca
    ForwardAgent yes
    User IDUL
    ServerAliveInterval 120
    IdentityFile ~/.ssh/id_ed25519
    ProxyJump pika
```

</details>

<details>
<summary>macOS</summary>

```ssh-config
Host *
    AddKeysToAgent yes
    UseKeychain yes
    IdentityFile ~/.ssh/id_ed25519

Host pika
    HostName pika.gel.ulaval.ca
    ForwardAgent yes
    User IDUL
    ServerAliveInterval 120
    IdentityFile ~/.ssh/id_ed25519

# IID compute cluster
Host iid187
    HostName lv3-32187.gel.ulaval.ca
    ForwardAgent yes
    User IDUL
    ServerAliveInterval 120
    IdentityFile ~/.ssh/id_ed25519
    ProxyJump pika
```

</details>

## Testing Your Setup

Once you've setup your SSH configuration, you can test it out by trying `ssh pika` and/or `ssh iid187` from the terminal.

## Related Topics

- [Available Compute Nodes](available_compute_nodes.md)
- [Reserving Compute Nodes](reserving_compute_nodes.md)
