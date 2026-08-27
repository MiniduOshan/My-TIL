# TIL: Copy-on-Write Filesystems and QCOW2 Backing Chains

📅 Date: 2026-08-28

Today I learned about **Copy-on-Write (CoW)** storage technologies, which allow snapshots, clones, and virtual machines to be created without immediately copying an entire disk or filesystem.

## What is Copy-on-Write?

**Copy-on-Write (CoW)** is a technique where existing data is shared instead of being duplicated. When a snapshot or clone is created, it initially references the original data. Only when data is modified is a new copy of the affected block created.

This makes cloning and snapshot operations much faster and more storage-efficient than traditional full copies.

```text
Original Data
     │
     ├── Snapshot / Clone
     │       │
     │       └── Shares unchanged blocks
     │
     └── New writes → New blocks
```

## ZFS and Btrfs

**ZFS** and **Btrfs** are filesystems that support CoW-based snapshots and cloning.

For example, with ZFS:

```bash
zfs snapshot pool/vm@base
zfs clone pool/vm@base pool/vm-new
```

The clone initially consumes very little additional storage because it shares the existing blocks with the snapshot. Additional storage is used only when data changes.

This can replace workflows such as:

```text
Large VM archive
      ↓
Download
      ↓
Extract
      ↓
Copy
      ↓
Start VM
```

with:

```text
Base snapshot
      ↓
Instant clone
      ↓
Start VM
```

## QCOW2 — QEMU Copy-On-Write

**QCOW2 (QEMU Copy-On-Write version 2)** is a virtual disk image format commonly used with **QEMU/KVM** and virtualization platforms.

A QCOW2 image can use another image as a **backing file**. The backing image is treated as the base, while the new image stores only the changes made by the VM.

```bash
qemu-img create -f qcow2 \
  -b base-vm.qcow2 \
  -F qcow2 \
  new-vm-overlay.qcow2
```

The structure looks like:

```text
Base VM Image
base-vm.qcow2
      │
      ▼
Overlay Image
new-vm-overlay.qcow2
      │
      ▼
VM writes
```

If the VM reads data that has not changed, the data comes from the base image. If the VM modifies a block, the modified version is stored in the overlay.

## QCOW2 Backing Chains

Multiple QCOW2 images can be chained together:

```text
Base Image
    │
    ▼
Template
    │
    ▼
VM Snapshot
    │
    ▼
Current Overlay
```

Each layer stores only the differences from its parent.

This is called a **backing chain**.

Backing chains are useful for creating VM templates and rapidly provisioning multiple virtual machines without making a full copy of the base disk.

## Thin Provisioning and Sparse Files

**Thin provisioning** allocates storage only when it is actually needed rather than reserving the entire virtual disk size immediately.

For example, a virtual disk can have a logical size of:

```text
100 GB
```

while initially consuming only:

```text
5 GB
```

of physical storage.

**Sparse files** use a similar concept at the filesystem level by avoiding physical allocation for unused regions.

Inside virtual machines, tools such as:

```bash
fstrim
```

can help communicate unused blocks to the underlying storage system so that space can potentially be reclaimed.

## OverlayFS

**OverlayFS** provides another form of layered storage, commonly used by container systems.

It combines:

* A read-only lower layer
* A writable upper layer

```text
        Container
           │
    ┌──────┴──────┐
    │             │
 Writable Layer  Read-only Layer
    │             │
    └──────┬──────┘
           │
       Base Image
```

Instead of copying the entire base filesystem, containers share the base layers and store only their changes.

## Why CoW Matters

Copy-on-Write technologies are useful for:

* ⚡ Fast VM provisioning
* 💾 Reducing storage consumption
* 📸 Creating snapshots
* 🔄 Creating VM templates
* 🐳 Container image layering
* 🧪 Testing isolated environments
* ☁️ Cloud infrastructure
* 🖥️ Virtual machine management

### Key Takeaway

**Copy-on-Write avoids unnecessary duplication by sharing unchanged data and copying only modified blocks.**

ZFS/Btrfs provide CoW at the filesystem level, QCOW2 provides CoW virtual disk images and backing chains, and OverlayFS provides filesystem layering for containers.

Instead of repeatedly **copying → compressing → extracting → deploying** large environments, CoW technologies allow infrastructure to be **snapshotted, cloned, and provisioned almost instantly** while consuming storage primarily for the differences.
