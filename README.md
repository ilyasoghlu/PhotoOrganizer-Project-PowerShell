# Photo Organizer

A simple PowerShell script that organizes photos into year and month folders based on the date recorded in each image's metadata.

The script scans photos from a source folder and copies them into a destination folder, organizing them chronologically without modifying or moving the original files.

## Features

- **Metadata-based date detection:** Uses the date recorded in the image metadata to determine when a photo was taken.
- **Automatic organization:** Sorts photos into folders by year and month.
- **Custom folder paths:** Specify your own source and destination directories.
- **Original file preservation:** Copies photos while keeping the originals in the source folder.
- **Simple execution:** Run the script directly in Windows PowerShell without setting up a separate application.

## Folder Structure

The destination folder will be organized as follows:

```text
Sorted Photos/
├── 2022/
│   ├── 01/
│   ├── 02/
│   ├── 03/
│   └── ...
├── 2023/
│   ├── 01/
│   ├── 02/
│   ├── 03/
│   └── ...
└── 2024/
    ├── 01/
    ├── 02/
    ├── 03/
    └── ...
```

Each year has its own folder, containing separate subfolders for each month. Photos are placed in the corresponding folders according to their metadata dates.

## Requirements

- Windows
- Windows PowerShell
- A source folder containing your photos
- An existing destination folder for the organized photos

## Tutorial: How to Use

### Step 1: Prepare Your Folders

Choose two folders:

- **Source folder:** Contains the photos you want to organize.
- **Destination folder:** An empty folder where the organized photos will be copied.

Example:

```text
D:\Photos
G:\Sorted Photos
```

Replace these example paths with your actual folder locations.

### Step 2: Open Windows PowerShell

1. Open the Windows Start menu.
2. Search for `Windows PowerShell`.
3. Open the application.

### Step 3: Configure the Script

Copy the script's code and paste it into the PowerShell window.

At the beginning of the code, locate the variables that specify the source and destination folders.

Update them with your folder paths. For example:

```powershell
$SourceFolder = "D:\Photos"
$DestinationFolder = "G:\Sorted Photos"
```

These variable names are examples. Use the actual names defined in your script.

Make sure the paths are correct and the destination folder exists before continuing.

### Step 4: Run the Script

Press `Enter` to execute the code.

The script will scan the photos in the source folder, read their recorded dates from image metadata, and copy them into the appropriate year and month folders in the destination directory.

The time required depends on the number of photos, their file sizes, and your storage device's speed.

### Step 5: Check the Results

Open the destination folder and verify that the photos have been organized correctly.

For example:

```text
G:\Sorted Photos\2023\07
```

This folder contains photos assigned to July 2023.

The original photos remain in the source folder.

## Important Notes

- Verify both folder paths before running the script.
- Ensure the destination drive has enough free space.
- Test the script with a small collection of photos before processing a large library.
- The organization process depends on the availability and format of the date metadata recorded in each image.
- Photos without usable date metadata may require separate handling, depending on the script's implementation.

## Project Goal

This project aims to make organizing large photo collections easier by automatically sorting images chronologically, reducing the need for manual file management.

## Open Source

This project is open source and is available for anyone interested in using, exploring, or improving the code.
