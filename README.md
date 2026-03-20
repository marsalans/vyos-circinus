# VyOS 1.5 (Circinus) Auto-Builder 🚀

This repository contains an automated GitHub Actions CI/CD pipeline for compiling a custom, bleeding-edge **VyOS 1.5 (Circinus)** image from source, with full support for the **VPP (Vector Packet Processing)** dataplane.

## 📖 Overview
VyOS has moved its stable LTS releases behind a subscription model, while keeping the bleeding-edge `current` branch free and open source. This branch contains the highly anticipated VPP integration, which drastically improves packet forwarding performance by processing packets in batches (vectors) rather than one by one, bypassing the standard Linux kernel bottleneck.

Building VyOS locally requires a dedicated Linux environment, Docker, and massive amounts of disk space. This repository solves that by offloading the entire compilation process to GitHub's free cloud runners.

## ✨ Features
* **Zero Local Infrastructure:** Compiles entirely on GitHub Actions.
* **VPP & DPDK Ready:** Pulls the `current` 1.5 branch which natively includes Vector Packet Processing.
* **Storage Optimized:** Includes a step to free up runner disk space to prevent `Exit Code 100` failures during the build.
* **Modern Target:** Uses the updated `generic` build target to successfully output a `.hybrid.iso` artifact.

## ⚙️ How to Use This Builder

1. **Fork or copy** this repository to your own GitHub account.
2. Navigate to the **Actions** tab at the top of the repository.
3. On the left sidebar, click on **Build VyOS Stream 2026.03** (or whatever the workflow is named).
4. Click the **Run workflow** dropdown on the right and click the green **Run workflow** button.
5. Grab a coffee ☕. The build will take approximately **30 to 45 minutes**.
6. Once the build finishes with a green checkmark, scroll down to the **Artifacts** section of the run summary.
7. Download the generated `.zip` file, extract the `live-image-amd64.hybrid.iso`, and flash it to a USB drive using Rufus or BalenaEtcher.

## 🖥️ Verifying VPP on Hardware
Once you have installed the custom ISO on your routing hardware (e.g., an HP ProLiant or Dell server), log in and verify the VPP dataplane is active:

```bash
show system acceleration vpp
