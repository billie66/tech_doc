### manage packages

* install a package `meteor add package`

* uninstall a package `meteor remove package`

You can also add or remove packages manually editing the file `packages` in the .meteor directory

### publish and subscribe

By default, users have admin priority, and have access to all of data stored within database on client side in the Console, it
would be easy for bad guys to make some harmful behaviors. For example, get all the users' info:

    Posts.find().fetch()

For the sake of security, we have to disable this feature provided by the package `autopublish`.
Within the command line, run the following command to remove this package:

    meteor remove autopublish

As a result, the data from the `Lists` collection will not show up.

###

### unique template name

```
Uncaught Error: There are multiple templates named 'navigation'. Each template needs a unique name.
```

### update to meteor 1.2.0.1

run command `meteor update` to update, the process was easy and quick, serveral
packages were added, like hot-code-push, meteor-base, mobile-experience,
standard-minifiers, and meteor-platform was removed.

### upload image

<https://medium.com/@victorleungtw/how-to-upload-files-with-meteor-js-7b8e811510fa>

### docs

<https://adilapapaya.wordpress.com/2014/03/12/things-i-wish-someone-told-me-when-i-first-started-learning-meteor-js/>

<http://stackoverflow.com/questions/15374066/importing-a-json-file-in-meteor>

<http://dweldon.silvrback.com/get-text>

