---
layout: post
title:  "Room Database - Backup & Restore Features"
date: 2020-10-03 13:50:30 +0200
categories: android room
---

Not that long ago I wanted to implement Backup & Restore features in my new application called [Notably Notepad](https://play.google.com/store/apps/details?id=com.notepad.notably). <br />
I thought such basic features will be well-documented and supported - I mean every app  containing a database would want to allow the user to move his data to a new phone. <br />
Yet again I was wrong, there is very little information about how to perform backup of **Room Database** and nothing in official android documentation.<br />

The information that is available is incomplete, at least in my case, it wasn't working - I had to compile information from many sources in order to get my code working. <br /> <br />
Which why I wrote this article, hopefully someone will find it helpful.


## Backup Database
In order for the backup feature to work as expected the following is necessary
* Database is created in **Truncated** journal mode
* **Checkpoint query** has been executed on the database
* Backup file has been saved on in shared storage

### Database is created in **Truncated** journal mode
First thing that needs to be done is to create the database with appropriate journal mode.

~~~
Room.databaseBuilder(context, AppDatabase::class.java, name)
    .setJournalMode(RoomDatabase.JournalMode.TRUNCATE)
    .build()
~~~
{: .language-kotlin}

When it comes to journal modes there are three options available:
* `JournalMode.AUTOMATIC` - default mode, **Room** will automatically choose journal modes based on the API and available device RAM
* `JournalMode.TRUNCATE` - stores the database in one file
* `JournalMode.WRITE_AHEAD_LOGGING` - in this mode your database is stored inside two files - a database file and write ahead log file (database_name.wal) file making it impossible for you to back up your database to one file

It is important that the database is created with `JournalMode.TRUNCATE` mode, since other modes might use two files for database storage - for user & implementation convenience it is much easier to work with one file.

### **Checkpoint query** has been executed on the database
When the option to create a database backup is chosen by the user the following **checkpoint query** needs to be executed to ensure all of the pending transactions are applied.

For this a following method needs to be added to the database `Dao` interface
~~~
interface UserDao {
    @RawQuery
    fun checkpoint(supportSQLiteQuery: SupportSQLiteQuery?): Single<Int>
}
~~~
{: .language-kotlin}

Then the method needs to be called with the following **SQL query**
~~~
userDao.checkpoint((SimpleSQLiteQuery("pragma wal_checkpoint(full)")))
~~~
{: .language-kotlin}

Once the checkpoint method has succeeded the database backup file can finally be saved.

### Backup file has been saved on in shared storage
The database backup file can be retrieved using the following code

~~~
File(database.openHelper.writableDatabase.path)
~~~
{: .language-kotlin}

The file then needs to be copied into the location picked by the user.

## Restore Database
Now that the database is backed up to a file it is possible to restore it.

There are number of ways you can allow the user to pick the backup file (any file picker library, Storage Access Framework). <br />
In my case [Storage Access Framework](https://developer.android.com/guide/topics/providers/document-provider) was used

~~~
fun tryOpenFile() {
    val intentType = "application/octet-stream"
    val intent = Intent(Intent.ACTION_OPEN_DOCUMENT).apply {
        addCategory(Intent.CATEGORY_OPENABLE)
        type = intentType
        putExtra(Intent.EXTRA_MIME_TYPES, arrayOf(intentType))
    }

    activity.startActivityForResult(intent, OPEN_FILE_CODE)
}
~~~
{: .language-kotlin}

The important part would be to set the intent `type` and pass `EXTRA_MIME_TYPES` to limit files visible by the user to those that are an `application/octet-stream`, which is the type used for database files.


That's all you need to add **backup and restore** features to your application!

In this article we have learned how to **backup and restore Room database.**



Resources:
<https://developer.android.com/guide/topics/providers/document-provider>
