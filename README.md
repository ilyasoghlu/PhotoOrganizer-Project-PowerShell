# Photo Organizer

A PowerShell script that automatically organizes photos into year and month folders based on their original capture dates.

The script scans one or more source folders, searches for supported image files recursively, reads their EXIF date metadata when available, and moves them into a structured destination directory.

If the original capture date cannot be read, the script falls back to the file's creation date.

## Features

- **Automatic date-based organization:** Organizes photos into folders by year and month.
- **EXIF metadata support:** Uses the `DateTimeOriginal` EXIF property to identify when a photo was originally taken.
- **Fallback date handling:** Uses the file creation date when the EXIF capture date is unavailable or cannot be read.
- **Multiple source folders:** Processes photos from multiple configured directories.
- **Recursive scanning:** Searches through nested subfolders without requiring a fixed folder depth.
- **Supported image formats:** Includes JPG, JPEG, PNG, BMP, GIF, TIF, TIFF, HEIC, and WEBP extensions.
- **Automatic directory creation:** Creates the required year and month folders in the destination directory.
- **Duplicate filename handling:** Prevents filename collisions by adding numbered suffixes to files with the same name in the same destination folder.
- **Progress reporting:** Displays a progress bar while processing files.
- **Error logging:** Records processing errors in an `errors.log` file.
- **Execution summary:** Displays processing statistics and the total execution time.

## How It Works

For each supported image, the script:

1. Scans the configured source folders and their subdirectories.
2. Attempts to read the photo's original capture date from its EXIF metadata.
3. Uses the file creation date if the EXIF date is unavailable or cannot be read.
4. Determines the corresponding year and month.
5. Creates the required destination folders if they do not already exist.
6. Checks whether a file with the same name already exists in the destination folder.
7. Moves the photo into the appropriate folder.
8. Records any processing errors in the log file.

## Example Folder Structure

After execution, the destination directory may look like this:

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

Each year folder contains monthly subfolders numbered from `01` to `12`. Photos are moved into the folder corresponding to their detected year and month.

## Requirements

- Windows
- Windows PowerShell
- Read access to the source folders
- Write and delete permissions for moving files from the source to the destination
- Sufficient free space on the destination drive

The script uses the .NET `System.Drawing` library to read image metadata. Actual image-format support may vary, particularly for formats such as HEIC and WEBP.

## Tutorial: How to Run the Script

### Step 1: Prepare Your Folders

Choose the source folder or folders containing the photos you want to organize.

Also, choose a destination folder where the organized photos will be stored. The script creates the required year and month subfolders automatically.

Example:

```text
Source:      D:\Photos
Destination: G:\Sorted Photos
```

The destination folder does not have to be empty, but using a separate destination directory is recommended.

### Step 2: Open Windows PowerShell

1. Open the Windows Start menu.
2. Search for `Windows PowerShell`.
3. Launch PowerShell.

Administrator privileges are generally unnecessary unless your folder permissions require them.

### Step 3: Configure the Source and Destination Paths

Open the script in a text editor and locate the `CONFIGURATION` section at the beginning of the code.

Update `$SourceFolders` with the paths of the folders you want to scan, and set `$DestinationRoot` to your destination directory.

Example:

```powershell
#region CONFIGURATION

$SourceFolders = @(
    "D:\Photos",
    "E:\Camera Backup",
    "F:\Telegram Photos"
)

$DestinationRoot = "G:\Sorted Photos"

$ErrorLog = Join-Path $PSScriptRoot "errors.log"

#endregion
```

Replace the example paths with your actual directory locations.

You can add as many source folders as needed by adding their paths to the `$SourceFolders` array.

**Important:** Keep the destination folder separate from the source folders. This helps prevent unintended file-processing behavior.

### Step 4: Execute the Script

There are two ways to run the script.

**Option A — Paste the code into PowerShell**

1. Copy the complete script.
2. Paste it into the PowerShell window.
3. Press `Enter` to execute it.

**Option B — Run the saved script**

1. Save the code as `PhotoOrganizer.ps1`.
2. Open PowerShell.
3. Navigate to the directory containing the script, for example:

```powershell
cd "C:\Scripts"
```

4. Execute the script:

```powershell
.\PhotoOrganizer.ps1
```

Make sure you have configured the source and destination paths before execution.

### Step 5: Monitor the Progress

While the script runs, PowerShell displays a progress bar containing:

- The file currently being processed.
- The percentage of completion.
- The number of processed files relative to the total number of supported image files found.

Processing time depends on the number of files, disk performance, and metadata availability.

### Step 6: Review the Results

When processing finishes, the script displays a summary similar to the following:

```text
=========================================
Completed
=========================================
Processed : 1500
Success   : 1495
Skipped   : 0
Errors    : 5
Time      : 00:02:35
Error Log : C:\Scripts\errors.log
=========================================
```

These numbers are illustrative only. Actual results depend on your photo collection.

- **Processed:** Number of supported image files processed.
- **Success:** Number of files successfully moved.
- **Skipped:** Reserved counter; the current script does not increment it.
- **Errors:** Number of files that encountered processing or moving errors.
- **Time:** Total execution time.
- **Error Log:** Location of the error log.

## Duplicate Filename Handling

If a file with the same name already exists in the destination month folder, the script generates a unique filename by adding a numbered suffix.

For example:

```text
IMG_1001.jpg
IMG_1001 (1).jpg
IMG_1001 (2).jpg
```

This prevents the script from overwriting an existing destination file because of a filename collision.

The script does not compare image contents, so differently named files containing identical photos are not identified as duplicates.

## Error Logging

Errors encountered during file processing are written to `errors.log`, located in the directory containing the saved script.

Each logged entry includes a timestamp, the affected file path, and the error message.

Review this file if some photos could not be processed successfully.

**Note:** The script deletes an existing `errors.log` at startup before creating a new log for the current run. Save any previous log you need to retain before running the script again.

## Important Notes

- **This script moves files, not copies them.** Successfully processed photos are removed from their original source locations and placed in the destination directory.
- Back up important photos before running the script.
- Test the script with a small collection before processing your entire photo library.
- The EXIF `DateTimeOriginal` property is preferred over the filesystem creation date.
- When EXIF metadata is unavailable or unreadable, the filesystem creation date is used instead. This date may not represent the original capture date.
- The script does not delete files that are already present in the destination folder.
- Keep the source and destination paths correctly configured to avoid unintended file operations.

## Project Goal

Photo Organizer was created to simplify the organization of large, mixed photo collections by automatically arranging images chronologically.

The goal is to reduce manual work and provide a straightforward way to maintain a structured photo archive using PowerShell.

## Open Source

This project is open source. The code is available for anyone interested in using, studying, or contributing to its development.
