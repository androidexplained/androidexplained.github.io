---
layout: post
title:  "Android 11 Scoped Storage - Saving Files To Shared Storage"
date:   2020-09-29 21:50:30 +0200
categories: android android11 scoped-storage
---

By now probably all of you had to hear about the dreaded changes to file storage on Android 11. <br />
So what exactly changed? <br />
According to Google apps now ***"have access only to the app-specific directory on external storage, as well as specific types of media that the app has created."***

In other words if your application freely allows the users to save files in shared storage, I hate to be the one that tells you this - you may have a problem sir. <br />
This is the case especially if you've been using
`Environment.getExternalStoragePublicDirectory(Environment.DIRECTORY_*)` in your code. <br />
The `getExternalStoragePublicDirectory` no longer returns a path to a publicly accessible folder so if you save a file in that location the user simply won't see it.

But worry not, there are some alternatives which I will talk about in this article.

There are two recommended approaches when it comes to shared storage file saving on Android 11
* for **Media Files (Images, Videos, Audio, Downloads)** use [MediaStore](https://developer.android.com/reference/kotlin/android/provider/MediaStore)
* for **Documents and Other Files** use [Storage Access Framework](https://developer.android.com/guide/topics/providers/document-provider) (this is simply a system file picker)

If you're already using them you should be fine and you can simply skip reading further.

### MediaStore API
Let's assume you want to save a bitmap as an image named `screenshot.jpg` inside the pictures directory. <br />
In order to do that using `MediaStore` API you can use the below snippet.

~~~
@Suppress("DEPRECATION")
private fun saveImageToStorage(
    bitmap: Bitmap,
    filename: String = "screenshot.jpg",
    mimeType: String =  "image/jpeg",
    directory: String = Environment.DIRECTORY_PICTURES,
    mediaContentUri: Uri = MediaStore.Images.Media.EXTERNAL_CONTENT_URI
) {
    val imageOutStream: OutputStream
    if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.Q) {
        val values = ContentValues().apply {
            put(MediaStore.Images.Media.DISPLAY_NAME, filename)
            put(MediaStore.Images.Media.MIME_TYPE, mimeType)
            put(MediaStore.Images.Media.RELATIVE_PATH, directory)
        }

        contentResolver.run {
            val uri =
                contentResolver.insert(mediaContentUri, values)
                    ?: return
            imageOutStream = openOutputStream(uri) ?: return
        }
    } else {
        val imagePath = Environment.getExternalStoragePublicDirectory(directory).absolutePath
        val image = File(imagePath, filename)
        imageOutStream = FileOutputStream(image)
    }

    imageOutStream.use { bitmap.compress(Bitmap.CompressFormat.JPEG, 100, it) }
}
~~~
{: .language-kotlin}

In a case when saving other type of media file you might need to modify  `filename`, `mimeType` and `mediaContentUri` accordingly. <br />
It is worth noting that the function will work both on the **scoped** as well as **legacy** storage systems.


### Storage Access Framework (SAF)
As mentioned above you should generally use **SAF** for documents and other types of files. <br />
The following snippet can be used to launch system file picker and allow the user to pick a directory where the file will be stored.

~~~
const val CREATE_FILE = 1

private fun createFile(pickerInitialUri: Uri) {
    val intent = Intent(Intent.ACTION_CREATE_DOCUMENT).apply {
        addCategory(Intent.CATEGORY_OPENABLE)
        type = "application/pdf"
        putExtra(Intent.EXTRA_TITLE, "invoice.pdf")

        // Optionally, specify a URI for the directory that should be opened in
        // the system file picker before your app creates the document.
        putExtra(DocumentsContract.EXTRA_INITIAL_URI, pickerInitialUri)
    }
    startActivityForResult(intent, CREATE_FILE)
}
~~~
{: .language-kotlin}

It's not over yet!<br />
After the user has picked a directory we still need to handle the result `Uri` in on `onActivityResult` method.

~~~
override fun onActivityResult(
        requestCode: Int, resultCode: Int, resultData: Intent?) {
    if (requestCode == CREATE_FILE && resultCode == Activity.RESULT_OK) {
        // The result data contains a URI for directory that
        // the user selected.
        resultData?.data?.also { uri ->
            // save your data using the `uri`
        }
    }
}
~~~

Yes that's it!<br />
Essentially use the above two approaches whenever you want to save files in directories that you want the user to have access to.

In this post we have learned how to save files in shared storage on Android 11.

Resources:
<https://developer.android.com/guide/topics/data>
