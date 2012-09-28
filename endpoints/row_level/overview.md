##The Row-Level API for Buzzdata

In some cases, it makes more sense to update your data on a row by row basis rather than importing a whole dataset at once.
For example, perhaps you made a GPS application and once an hour want to update it with your location. You could use the 
row level API to insert only the new locations into the dataset.


##Staging your Updates

Before you get started with the Row-Level API you'll have to familiarize yourself with the concept of staging your update.
Every time you upload a dataset to buzzdata, it creates a new version in the history. If you have an application that 
updates the dataset frequently, you would end up with many, many versions that would pollute your dataset's history. To 
get around this, we ask that you stage your updates before commiting them.

You can think of staging as setting aside the data that you want to commit later. You start by creating a stage with a
REST call. Then you add your updates to the stage whenever you want. Once you are ready to create a new version and 
update the dataset, you call commit.

In the GPS example above, a good idea might be to stage a day's worth of updates, and then commit them at the end of the
day. It's up to you to decide when it makes sense for your dataset to be released as a new version!
