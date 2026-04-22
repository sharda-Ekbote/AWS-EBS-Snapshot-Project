##AWS Cross-AZ Data Recovery using EBS Snapshots## Project Overview
This project demonstrates the lifecycle of data backup and disaster recovery within Amazon Web Services. It covers creating a point-in-time backup (Snapshot) of an EBS volume and restoring that data onto a new EC2 instance located in a different Availability Zone (AZ).
## Prerequisites

* An active AWS Account.
* An existing EBS volume containing data.
* SSH Client (like Putty or Terminal).

## Step-by-Step Implementation## Phase 1: Environment Setup

   1. Launch EC2: Deploy a new Linux-based EC2 instance.
   2. Strategic Placement: Ensure this instance is in a different Availability Zone (e.g., us-east-1b) than your original data source (e.g., us-east-1a) to simulate a recovery scenario.

## Phase 2: Snapshot & Volume Restoration

   1. Capture Data: Navigate to EBS > Volumes, select your source volume, and select Create Snapshot.
   2. Monitor Progress: Wait for the snapshot status to change from pending to available.
   3. Restore Volume: Select the snapshot and click Create Volume from Snapshot.
   * Critical: Set the Availability Zone to match your new EC2 instance.
   4. Attach: Once created, select the new volume and Attach Volume to your running instance.

## Phase 3: OS-Level Mounting

   1. Access: Log in to your instance via SSH/Putty.
   2. Identify: Run lsblk to list block devices and find your attached volume (e.g., /dev/xvdf).
   3. Mount:
   * Create a mount point: sudo mkdir /mnt/recovery_data
      * Mount the drive: sudo mount /dev/xvdf /mnt/recovery_data
   4. Verify: Navigate to the directory and run ls to confirm the original files are present.

## Phase 4: Clean Up (Resource Management)
To avoid unnecessary AWS charges:

   1. Unmount: sudo umount /mnt/recovery_data
   2. Detach & Delete: Detach the volume from the EC2 console and delete it.
   3. Final Removal: Delete the EBS Snapshot and Terminate the EC2 instance.

