# Supernote PDF Exporter & Manager for Google Colab

A Python-based script designed to run in Google Colab that automates the conversion of Supernote's proprietary `.note` files into standard PDF documents. It intelligently manages exports, archives old versions, and cleans up your folders, creating a seamless bridge between your Supernote and your digital archive on Google Drive.

## Features

* **Automatic PDF Conversion**: Converts all `.note` files in your Google Drive `Supernote/Note` folder to PDF.
* **Intelligent Change Detection**: Uses MD5 hashes to detect which `.note` files have changed, only converting new or modified files to save time and processing power.
* **Structured Archiving**: Instead of deleting old PDFs, the script archives them. When a `.note` file is updated, the previous PDF is moved to an `_Archive` folder with a timestamp.
* **Orphan File Management**: If a `.note` file is deleted from your Supernote, the corresponding PDF in your export folder is automatically moved to the archive instead of being deleted.
* **Configurable Retention**: Easily set the number of old PDF versions you want to keep in the archive for each note.
* **Directory Exclusion**: Specify subdirectories (like `Shapes` or `EXPORT`) to ignore during the conversion process.
* **Clean Folder Structure**: Organizes all generated files neatly, with internal folders like `_Archive` and `_MD5_Hashes` prefixed with an underscore to keep your main export directory clean.

## How It Works

The script operates on a simple and organized folder structure within your Google Drive.

* `/Supernote/Note/`: This is your **input** folder. Your Supernote device syncs its `.note` files here. The script reads from this directory and all its subdirectories.
* `/Supernote_Export/`: This is your **output** folder where the converted PDFs are placed, mirroring the folder structure of your `Note` directory.
* `/Supernote_Export/_Archive/`: When a `.note` file is updated or deleted, the corresponding PDF is moved here with a timestamp. This prevents data loss and keeps a version history.
* `/Supernote_Export/_MD5_Hashes/`: This internal folder stores a small hash file for each note that has been converted. This hash is used to check if a note has been modified since its last conversion.

## Requirements

* A Google Account with Google Drive.
* A Supernote device configured to sync with your Google Drive.
* Access to Google Colaboratory (Colab).

## How to Use

This script is designed to be run in a Google Colab notebook.

### Step 1: Set Up the Notebook
Open Google Colab and create a new notebook. Copy and paste the provided script cells into the notebook in the correct order (Cell 1, Cell 2, Cell 3, Cell 4).

### Step 2: Configure Your Settings (Cell 1)
In the first cell, you can adjust the configuration variables to match your needs:
* `EXCLUDE_SUBDIRECTORIES`: Add the names of any folders within your `Note` directory that you do not want to process.
* `ARCHIVE_COPIES_TO_KEEP`: Set the number of old PDF versions you want to keep for each note. The default is 5.

### Step 3: Run the Setup Cells
Run **Cell 1**, **Cell 2**, and **Cell 3** in order.
* **Cell 1** will mount your Google Drive, install the necessary tools, and set up your configuration.
* **Cell 2 & 3** will load the core conversion and management functions into memory.

### Step 4: Execute a Task (Cell 4)
Cell 4 is your main control panel. To run a task, uncomment the desired function call and then run the cell.
* **`convert_all_files()`**: This is the primary function. It scans your entire `Note` directory and intelligently converts only the files that are new or have been modified.
* **`clean_export_folder()`**: This function finds PDFs in your export folder that no longer have a corresponding `.note` file and moves them to the `_Archive` folder.
* **`clean_archive_folder()`**: This function cleans the `_Archive` folder by removing all versions of an archived note if its main PDF has also been deleted (or was never converted).

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
