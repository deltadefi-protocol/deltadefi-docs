---
description: The fork installs the same way as upstream Hummingbot from source.
---

# Installation

### Prerequisites

* Conda (Miniconda or Anaconda)
* Git
* A C compiler toolchain (for Cython compilation)

Refer to the [upstream source-install guide](https://hummingbot.org/installation/hummingbot-client/) for OS-specific toolchain notes.

### Clone and install

```bash
git clone https://github.com/deltadefi-protocol/hummingbot.git
cd hummingbot

# Run Setup & Deploy
make setup
make deploy

# Attach to the running instance
docker attach hummingbot
```

The conda environment is named `hummingbot`. Keep this exact name — the `sidan-gin` install step on the next page depends on activating it.

### Verify

```bash
bin/hummingbot_quickstart.py
```

The Hummingbot CLI should launch. Exit with `exit`.

{% hint style="warning" %}
Do **not** try to trade on Delta-DeFi yet. You must install `sidan-gin` first, otherwise orders will fail to sign.

Continue to Installing sidan-gin.
{% endhint %}
