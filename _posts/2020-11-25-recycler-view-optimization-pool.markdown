---
layout: post
title:  "RecyclerView optimization using RecycledViewPool"
date:   2020-11-09 21:50:30 +0200
categories: android ui
---

In the previous post we have looked at how to clean up resources in **RecyclerView.ViewHolder** which makes sure we don't waste memory unnecessarily.
But that's not all of the things you can do to make **RecyclerView** scrolling more smooth, there are number of things we can still improve.

In this post we will specifically look at optimizations related to **RecyclerView.RecycledViewPool.**

## RecycledViewPool

So first a bit of theory.
Essentially whenever a downward scroll occurs inside **RecyclerView** the views that disappear on the top are recycled into the **RecycledViewPool** and then reused for the views appearing on the bottom.

Below are a couple of **RecycledViewPool** tricks you can use to optimize **RecyclerView**.

## Reusing RecycledViewPool with many RecyclerViews
Lets imagine we have a couple of **RecyclerViews** on the screen displaying the same type of the ViewHolder such as horizontally displayed apps on **Google Play**.

<img src="{{site.baseurl}}/images/multiple_recyclerviews.png" style="width: 50%; height: 50%">

By default both visible RecyclerViews will have their own pool which means they are not sharing views.
This leads to many views being unnecessarily being inflated and possibly resulting in laggy behaviour of the horizontal scroll.

In order to avoid that we care share the pool using [RecyclerView#setRecycledViewPool](https://developer.android.com/reference/androidx/recyclerview/widget/RecyclerView#setRecycledViewPool(androidx.recyclerview.widget.RecyclerView.RecycledViewPool)) method.

There are couple of additional things that we will need to keep in mind

* shared ViewHolders need to have the same **ViewType** <br />
This is because ViewHolder is picked from the RecycledViewPool based on the **ViewType** returned from [RecyclerView.Adapter#getItemViewType](https://developer.android.com/reference/androidx/recyclerview/widget/RecyclerView.Adapter#getItemViewType(int))

* every **RecyclerView.LayoutManager** that shares the pool needs to have [recycleChildrenOnDetach](https://developer.android.com/reference/kotlin/androidx/recyclerview/widget/LinearLayoutManager#setrecyclechildrenondetach) flag set to **true** <br />
As we can read in official documentation <br />
*If you are using a RecyclerView.RecycledViewPool, it might be a good idea to set this flag to true so that views will be available to other RecyclerViews immediately.*


## Setting the optimal RecycledViewPool size
By default RecycledViewPool can hold 5 ViewHolders of the same ViewType.

Since you might have more items of the same ViewType on the screen it might make sense to increase that number.
For a **ViewHolder** that is more rare and appears on the screen only once you could set the size of the pool to 1.
Otherwise, sooner or later, the pool will be filled with 5 of those rare ViewHolders, 4 of which will just sit unused, wasting precious memory.

We can set the pool size in the following way

~~~
recyclerView.recycledViewPool.setMaxRecycledViews(VIEW_TYPE, POOL_SIZE)
~~~
{: .language-kotlin}



<br /> <br />
That's all! You can finally enjoy the smooth scrolling experience in your app!<br />
In this article we have learned how to optimize **RecyclerView** using **RecyclerView.RecycledViewPool**!
