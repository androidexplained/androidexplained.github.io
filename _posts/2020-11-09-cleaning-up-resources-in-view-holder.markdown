---
layout: post
title:  "Cleaning up resources in RecyclerView ViewHolder"
date:   2020-10-21 21:50:30 +0200
categories: android ui
---

In your journey you might have often wondered when exactly to clean up resources in a **RecyclerView ViewHolder**.<br />
The topic isn't easy and like most you probably tried to use **onViewAttachedToWindow** & **onViewDetachedFromWindow**, only to find it's not working and gave up hoping you'll get away with
no resource freeing mechanism.<br />
Sure there is this 1% of users of your app who get **OutofMemoryException** from time to time and on older phones scrolling through a list of items looks more like playing Tetris. <br />
You didn't really care until you get a negative review with 500 upvotes saying that your app is almost unusable.

But worry not, in this article we will look at how to cleanup resources in **RecyclerView ViewHolder** properly.

## Release the... resources
There are couple of methods that will be important to us in this article
* [RecyclerView.Adapter#onBindViewHolder](https://developer.android.com/reference/androidx/recyclerview/widget/RecyclerView.Adapter#onBindViewHolder(VH,%20int)) - called to display data at specified position, should update the contents of **ViewHolder** to reflect an item at position
* [RecyclerView.Adapter#onViewRecycled](https://developer.android.com/reference/androidx/recyclerview/widget/RecyclerView.Adapter#onViewRecycled(VH)) - called when **View** is recycled and put into the pool, since the **View** might sit in the pool for a while it might be a good idea to release heavy resources like bitmaps in this method

Lets look at a situation when user is scrolling downwards in a **RecyclerView.** <br />
We will assume that there are two ViewHolders of the same type displayed (**1 & 2**).<br />

* items are displayed on the screen - **onBindViewHolder** will be called for both **ViewHolder 1 & 2**
* user scrolls down and the top **ViewHolder 1** disappears, it will be put into the pool, after which the **onViewRecycled** method will be called on that ViewHolder
* at the same time new ViewHolder appears on the bottom - since we have **ViewHolder 1** in the pool it will be reused and **onBindViewHolder** will be called again to reflect the new position
* and so on and so on...

Therefore we can basically utilize these two above methods to initialise resources (**onBindViewHolder**) and cleanup them up (**onViewRecycled**) accordingly.

The below code can serve as an example of how this would look in practice

~~~
class MovieAdapter(private val movies: Array<String>) :
    RecyclerView.Adapter<MovieAdapter.ViewHolder>() {

    override fun onBindViewHolder(viewHolder: ViewHolder, position: Int) =
        viewHolder.onBind(movies[position])

    override fun getItemCount() = movies.size

    override fun onCreateViewHolder(parent: ViewGroup, viewType: Int): ViewHolder {
        val view = LayoutInflater.from(parent.context)
            .inflate(R.layout.movie_item, parent, false)

        return ViewHolder(view)
    }

    override fun onViewRecycled(holder: ViewHolder) {
        super.onViewRecycled(holder)

        holder.cleanup()
    }

    class ViewHolder(view: View) : RecyclerView.ViewHolder(view) {

        fun onBind(movie: String) {
            // initialise resources and adjust the view to reflect position in the RecyclerView
        }

        fun cleanup() {
            // release heavy resources like bitmaps etc.
        }
    }
}
~~~
{: .language-kotlin}

In this example we could for instance download a movie cover image and display it in the **onBindViewHolder** after which we would release the downloaded Bitmap in **onViewRecycled** method to cleanup this heavy object so it does not sit unused in the pool.

In this article we have learned how to clean up resources in **RecyclerView.ViewHolder**!
