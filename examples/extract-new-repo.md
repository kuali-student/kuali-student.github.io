---
layout: default
---

# Extract New Repository from archived-from-svn
Checkout the full repository locally as a bare repository.

```
$ git clone --bare https://github.com/kuali-student/archived-from-svn.git
```


Create the new sub set repository locally:

```
$ git init --bare myplan
```

Register the remote in the archived repo:


{% highlight shell %}
$ cd archived-from-svn
$ git remote add mp ../myplan
{% endhighlight %}

Now select the contrib_myplan prefixed branches and send them to the myplan repo:

```
$ git branch | grep " contrib_myplan" | grep -v "@" | xargs git push mp
```

The grep -v "@" part is to exclude deleted branches.


