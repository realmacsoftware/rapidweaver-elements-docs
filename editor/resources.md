---
icon: folder
---

# Resources

Website resources include anything from image files to PDFs and folders. All of your resources can be managed right inside RapidWeaver Elements.

{% hint style="success" %}
All resources added to a project will be included when publishing or exporting your website.
{% endhint %}

### Adding Resources

Open the resources list in the left-hand sidebar, and drag and drop in files (and folders), from the Finder. The structure and naming of your files will be the same in-app and when it's exported to the finder.

The resources you add will be copied and stored inside your project.

#### Supported File Types&#x20;

Elements supports adding all files types (including Folders) to the resources browser. However, some file types have extra support.

* Images - png, svg, jpg, etc.
* Fonts - WOFF, WOFF2, TTF
* YouTube URL - Single video's and playlists
* Vimeo URL - Single video's and playlists

{% hint style="danger" %}
If you see a warning triangle for your resource instead of a thumbnail it means Elements can't generate a thumbnail for that file. This can happen for a variety of reasons, the most common being the resource is not in the correct format.

Even if Elements can't generate a thumbail for the file, it will still export it when published.
{% endhint %}

#### Websafe Resource Naming

When Publishing, Elements will lowercase all resource filenames and ensure they are websafe by swapping out foreign characters and spaces with an underscore. For example:

* `my~file.png` would become `my_file.png`.
* `my file has spaces.png` would become `my_file_has_spaces.png`.
* `myFile.png` would become `myfile.png`.

Many web servers (Linux/Unix based) treat File.jpg and file.jpg as two different files. However, on Windows or macOS (i.e. Elements), the filesystem often isn’t case-sensitive, so it _looks_ fine locally, but when uploaded, it can cause broken links and 404 errors.

By using lowercase files, you’ll ensure they will ALWAYS work on different environments (Windows, Linux, macOS), this could be very important depending on the hosting platform you have chosen.

### Adding YouTube and Vimeo Videos

You can add YouTube or Vimeo videos by dragging and dropping the URL from your web browser to the Resources area in RapidWeaver Elements. A playlist URL can also be dropped into the resources area.

YouTube and Vimeo videos are not downloaded and store in Elements, the URL to video(s) is stored and saved.

### Adding Custom Fonts

Add your font files to the resources area in Elements, and use the media inspector to define a weight (and width if required) for each of the font files. These fonts work in conjunction with [Font Family in the Theme Studio](../elements-app/theme-studio/font-family.md).

### Editing Metadata

To inspect a file, the Resource Info panel needs to be visible. This panel (or window) can be left open while you browse through files in the Resources area.

* Filename (All file types)
* Caption (images)
* Author (images)

### Creating Folders

Right-click in the Resources area and select the "New Folder" option from the contextual menu.

### Adding Remote Resources

Right-click in the Resources area and select "Add Remote Resource" from the contextual menu.

You can add single or multiple remote url's at a time, just ensure each remote resource is on a new line.

<figure><img src="../.gitbook/assets/CleanShot 2025-08-26 at 9 .36.58@2x.png" alt=""><figcaption></figcaption></figure>

### Sorting Resources

Resources are always manually sorted. However, you can run a one-time sort action to quickly arrange them in a chosen order. To do this, right-click on a Folder in the Resources area and choose a Sort option from the contextual menu. The sort will be applied to the current items in that Folder, but any new items you add (or items you move) will not stay automatically sorted.

#### Folder Sorting Options:

* Alphabetical
* Newest First
* Oldest First

