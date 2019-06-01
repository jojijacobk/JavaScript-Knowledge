# Offline

To make your application or website offline compatible - **progressive
enhancement**, design the application to sync with server periodically
when there is connection and store all offline needed assets locally. So
you app works always like its in offline mode by working with local
data, but syncs with server periodically. To determine whether you are
online/offline there is Network information HTML5 APIs
but [Offline.js](http://github.hubspot.com/offline/docs/welcome/) is a
better alternative. 

## Storing assets offline

App-Store apps in general (like Firefox OS apps) comes by default with
this capability to work offline. But, you can implement it yourself
through following ways.

1.  Application Cache. **AppCache manifest** file can be used to list all
    CSS, fonts, JS, image files you want to cache.
2.  Better solution is to **grab assets via XMLHttpRequest**, and
    **store them offline datastore** such as IndexedDB
3.  An even better solution is **Service Workers**.
