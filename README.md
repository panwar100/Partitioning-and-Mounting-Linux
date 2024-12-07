# Partitioning-and-Mounting-Linux
This repository provides a comprehensive guide on managing disk partitions, creating file systems, and configuring logical volumes in Linux. It covers essential topics such as MBR and GPT partitioning, file system mounting, and advanced techniques like LVM (Logical Volume Management) and swap space creation.

## Table of Contents

[1.Basic Partitioning](#1.basic-partitioning)

[2.File System Creation and Mounting](#2.file-system-creation-and-mounting)

[3.Dynamic Partitioning (LVM)](#3.dynamic-partitioing-lvm)

[4.Swap Creation](#4.swap-creation)

# 1.Basic Partitioning

## a)Concepts:
- Partition Types:
   - MBR (Master Boot Record): Supports up to 4 primary partitions.
   - GPT (GUID Partition Table): Allows up to 128 partitions and supports larger disk sizes.
- Primary Partition: Contains bootable and critical system files.
- Extended Partition: Used to create additional logical partitions.

### Adding a Hard Disk to Your VMware Virtual Machine
1.**Go to setting**
   
   - click on **Settings** and then click **Add**.

![Screenshot from 2024-12-07 21-22-34](https://github.com/user-attachments/assets/477289f1-28a8-4452-a006-1cf41974b6ce)
2.**Select Hard Disk**
  
   - Choose **Hard Disk** and click **Next**.
![Screenshot from 2024-12-07 21-22-52](https://github.com/user-attachments/assets/11efb2cb-db7b-41ed-9c3d-9e5c0681e44d)

3.**Choose the Disk Type**
   
  - Select **SATA** and click **Next**.
![Screenshot from 2024-12-07 21-23-00](https://github.com/user-attachments/assets/8f7b00f2-afdd-4477-bd79-7981ac6fb0b3)

4.Create a **New Virtual Disk**.
   
   - Choose **Create a new virtual disk** and click **Next**.
![Screenshot from 2024-12-07 21-23-15](https://github.com/user-attachments/assets/a5eddfef-11f4-448d-a20f-b9e2070437ef)

5.**Specify the Disk Size**
     
   - Enter the desired disk size and click **Next**.
![Screenshot from 2024-12-07 21-24-09](https://github.com/user-attachments/assets/321e3366-6c28-47f4-92ed-e8de480c6c6e)

6.**Finish Adding the Disk**
 
   - Review the settings and click **Finish**.
![Screenshot from 2024-12-07 21-24-34](https://github.com/user-attachments/assets/30696daa-18fe-4432-baa6-9f3eadbf9fca)

7.**Verify the New Hard Disk**
  
  - You will now see the newly added hard disk in the list.
![Screenshot from 2024-12-07 21-24-47](https://github.com/user-attachments/assets/61c29a18-bbd3-4e8d-bd4a-a9e489fe0bca)

8.**Add Additional Disks** (Optional)
  
  - Repeat the steps to add more hard disks if needed.
![Screenshot from 2024-12-07 21-26-23](https://github.com/user-attachments/assets/8b39a217-ee4a-4ca5-9857-da63fc375546)

Commands:

## b)View Disks and Partitions:

Lists all block devices

![Screenshot from 2024-12-07 22-02-31](https://github.com/user-attachments/assets/41063c26-458f-44f2-87fe-2b106ef9eb5f)


Lists partition details

![Screenshot from 2024-12-07 22-03-00](https://github.com/user-attachments/assets/1a0904a3-9f34-4b8b-9576-3f8a210f8890)


## c)Create a New Partition with fdisk:

![Screenshot from 2024-12-07 22-06-21](https://github.com/user-attachments/assets/ad6914cb-a1a8-4725-8471-9ef233d5a3b3)

Steps:

Press n for a new partition.

Choose p for Primary or e for Extended.

Specify Partition Number (default: 1).

Define First and Last Sector (e.g., +8G for size).

Save with w.

---

Verify the changes

![Screenshot from 2024-12-07 22-07-24](https://github.com/user-attachments/assets/f1dd2c32-4c21-422e-b26c-02498d91af18)


## d)Partition Types and Operations:

![Screenshot from 2024-12-07 22-10-55](https://github.com/user-attachments/assets/b828a808-80fe-4fa4-9cf6-70896e600406)
![Screenshot from 2024-12-07 22-11-37](https://github.com/user-attachments/assets/79b20646-544e-4a9e-991d-e17731530d4b)
![Screenshot from 2024-12-07 22-11-56](https://github.com/user-attachments/assets/c66fde7b-ec1e-4787-829b-96bdd559e796)

View Partitions: p

List Types: l

Change Type: t (e.g., switch 83 to 82 for swap)

Delete Partition: d

Show Free Space: F

Detect Errors: v

Quit Without Saving: q


## e)Using gdisk:

![Screenshot from 2024-12-07 22-15-57](https://github.com/user-attachments/assets/43ae3ac4-7517-442f-8804-558dc670765f)

Steps:

Press n for a new partition.

Enter Partition Number (default: 1).

Define First and Last Sectors (e.g., +15G for size).

Enter Hex Code for Type (e.g., 8300 for Linux filesystem).

Save with w.

---

Verify the changes.

![Screenshot from 2024-12-07 22-16-53](https://github.com/user-attachments/assets/e12d0605-19eb-424b-8afb-3d6f14bbdcc4)

# 2.File System Creation and Mounting



## a)Create File System:

![Screenshot from 2024-12-07 22-24-33](https://github.com/user-attachments/assets/dce4fa32-30ea-420e-bf23-0f13a631a29c)


## b)Mount Partition:

![Screenshot from 2024-12-07 22-25-56](https://github.com/user-attachments/assets/b0d9a23f-363c-4bbd-9034-f414e08c275b)

![Screenshot from 2024-12-07 22-26-26](https://github.com/user-attachments/assets/1efead45-8445-46bc-b017-3535875d15e6)

It is temporary; it will be gone after a restart.

## c)Temporary and Persistent Mounting:

- Check Mounted Disks:

![Screenshot from 2024-12-07 22-28-47](https://github.com/user-attachments/assets/0c2e0067-39f3-4447-98ec-8cc132ec062c)

- View UUID:

![Screenshot from 2024-12-07 22-30-03](https://github.com/user-attachments/assets/7b644f44-f02b-44a2-956a-22ef0a6bbd10)


- Add to /etc/fstab for persistent mounting:

vim /etc/fstab

![Screenshot from 2024-12-07 22-32-49](https://github.com/user-attachments/assets/65802dd6-83e8-48c3-a097-22286409a962)


- Apply changes:

![Screenshot from 2024-12-07 22-34-43](https://github.com/user-attachments/assets/353b22f3-2251-4636-b49d-d6031262c9c6)

---

- Unmount and Clean Up All:

![Screenshot from 2024-12-07 22-39-11](https://github.com/user-attachments/assets/c98ee718-1bf7-4d8a-8fa4-9be6e0ef2648)

![Screenshot from 2024-12-07 22-40-36](https://github.com/user-attachments/assets/f4254574-5dad-474b-934e-08331c502d3b)


### Choosing the Right File System

- Enterprise storage: XFS, ZFS, or Btrfs.
- Desktop usage: ext4.
- Compatibility: FAT32 or exFAT.
- Snapshots and advanced features: Btrfs or ZFS.

# 3.Dynamic Partitioning (LVM)

## a)Prepare Physical Volumes:

![Screenshot from 2024-12-07 22-42-58](https://github.com/user-attachments/assets/490bd7fd-c9ac-48d6-ab30-be3733dd201c)

n   # Create new partition

p   # Print partition

w   # Write and exit

Repeat for /dev/sdb, /dev/sdc.

![Screenshot from 2024-12-07 22-44-18](https://github.com/user-attachments/assets/a376ff8a-216b-4f58-a8ac-defc08ad7eda)


## b)Initialize Physical Volumes:

![Screenshot from 2024-12-07 22-46-01](https://github.com/user-attachments/assets/1edaa0b0-34fb-4367-a0a2-b34b7ae1391e)


## c)Create Volume Group:

![Screenshot from 2024-12-07 22-46-48](https://github.com/user-attachments/assets/b9e073fc-f2ac-40cf-b753-b589c3444a70)


## d)Create Logical Volume:

![Screenshot from 2024-12-07 22-48-03](https://github.com/user-attachments/assets/62950dcc-27d0-49a1-9dc0-5005b447280b)

![Screenshot from 2024-12-07 22-48-54](https://github.com/user-attachments/assets/d625f1f8-b6c8-41ae-9cbd-466da2097589)

## e)Format and Mount:

![Screenshot from 2024-12-07 22-49-39](https://github.com/user-attachments/assets/013d41eb-c290-489b-ae9d-09b4477577a4)

![Screenshot from 2024-12-07 22-50-23](https://github.com/user-attachments/assets/46b951e0-5683-4167-a448-f2b1a1fdeedc)

## f)Clean Up:

![Screenshot from 2024-12-07 22-51-58](https://github.com/user-attachments/assets/7d7399af-8e75-4329-ac4c-3c4cfb5c10bc)


# 4.Swap Creation

## a)Create Swap Partition:

![Screenshot from 2024-12-07 22-54-41](https://github.com/user-attachments/assets/15ecb8e7-2de5-4a2f-b907-df3842e50158)

Change Type: t 

Hex Code: 8200 (for swap)

w   # Save

## b)Enable Swap:

![Screenshot from 2024-12-07 22-58-23](https://github.com/user-attachments/assets/bfc1a7c6-866e-4b6b-bb32-628f272be671)


## c)Verify:

![Screenshot from 2024-12-07 22-59-20](https://github.com/user-attachments/assets/38418f8b-9887-45e8-9d55-35bd9d673d68)

![Screenshot from 2024-12-07 23-00-06](https://github.com/user-attachments/assets/ac437785-9cbc-4528-b44f-e63a73102f74)

## d)Disable Swap:

![Screenshot from 2024-12-07 23-00-40](https://github.com/user-attachments/assets/2526854d-de7d-48ec-bc4f-c9458d5b70fd)

