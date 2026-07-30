---
description: Add, organise and manage the files used by your website
icon: folder
---

# Resources

Resources include the images, fonts, documents, media and folders used by your website. You can manage them directly in RapidWeaver Elements.

{% embed url="https://www.youtube.com/watch?v=yDEEhLlVUuU" %}

{% hint style="success" %}
All resources added to a project will be included when publishing or exporting your website.
{% endhint %}

### Adding Local Resources

Open Resources in the left sidebar, then drag files or folders from Finder. Elements preserves their structure and names in the project and its exported output.

The resources you add will be copied and stored inside your project.

#### Supported File Types

Elements accepts all file types and folders in Resources, with additional support for certain formats:

* Images — PNG, SVG, JPG and other web formats
* Fonts — WOFF, WOFF2 and TTF
* YouTube URL — Individual videos and playlists
* Vimeo URL — Individual videos and playlists

{% hint style="danger" %}
If a warning triangle appears instead of a thumbnail, Elements could not generate a preview for that file. The most common cause is an unsupported or invalid format.

Elements will still export the file when publishing, even if it cannot generate a thumbnail.
{% endhint %}

#### Web-Safe Resource Naming

When publishing, Elements converts resource filenames to lowercase and replaces unsupported characters or spaces with a hyphen. For example:

* `my~file.png` would become `my-file.png`.
* `my file has spaces.png` would become `my-file-has-spaces.png`.
* `myFile.png` would become `myfile.png`.

Many Linux and Unix web servers treat `File.jpg` and `file.jpg` as different files. Windows and macOS file systems are often case-insensitive, so a mismatch may work locally but produce broken links after publishing.

Using lowercase filenames avoids these differences between hosting environments.

### Adding YouTube and Vimeo Videos

Add a YouTube or Vimeo video by dragging its URL from your browser into Resources. Playlist URLs are also supported.

Elements stores the video URL rather than downloading the media.

You can also right-click the **Resources** heading and select **Add Remote Resources**.

### Adding Custom Fonts

Add font files to Resources, then use the Resource Info panel to define the weight and, if required, width of each file. These fonts work with [Font Family in Theme Studio](theme-studio/font-family.md).

### Editing Metadata

Open the Resource Info panel to inspect a file. You can leave the panel open while browsing Resources.

You can change details such as:

* Filename (all file types)
* Caption (images)
* Alt Text (images)
* Author (images)
* Link URL (all file types)

### Creating Folders

Right-click in Resources and select **New Folder**.

### Adding Remote Resources

Right-click in Resources and select **Add Remote Resources**.

<figure><img src="../.gitbook/assets/CleanShot 2025-08-26 at 9 .36.58@2x.png" alt="Resources contextual menu with Add Remote Resources selected"><figcaption></figcaption></figure>

You can add one or more remote URLs at a time. Place each remote resource on a new line. The Remote Resources window also supports multiple Vimeo and YouTube URLs.

<figure><img src="../.gitbook/assets/CleanShot 2026-07-16 at 3 .15.23@2x.png" alt="Add Remote Resources dialog containing multiple media URLs on separate lines"><figcaption></figcaption></figure>

### Sorting Resources

Resources use manual ordering. To arrange the current contents of a folder, right-click it and choose a Sort option. New or moved items will not be sorted automatically.

#### Folder Sorting Options

* A-Z (Ascending)
* Z-A (Descending)
* Newest First
* Oldest First
