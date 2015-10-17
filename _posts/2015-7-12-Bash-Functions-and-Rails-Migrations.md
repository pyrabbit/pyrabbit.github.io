---
layout: post
title: Bash Functions and Rails Migrations
---


Open and edit your last migration with a single command! If you hate opening migrations as much as I do then you will love this tip. Since migrations begin with a datetime group, create an easy to use bash function to quickly edit that migration.

Run `vim ~/.bashrc` and add the following function:
```
function elm()
{
  vim `ls db/migrate/*.rb | tail -n 1`
}
```

Finally, reload your ~/.bashrc file: `source ~/.bashrc`. Tada! Now all you have to do is run the `elm` command to edit the last migration you created.

Now I can't take all the credit but I found this solution on StackOverflow and was answered by Michaël Witrant.
http://stackoverflow.com/questions/14099155/edit-rails-migration-file-in-one-command
