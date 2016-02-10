---
layout: post
title: "Using a service to lazy load dependencies"
date: 2016-02-10 09:45:00
---
{% raw %}
You may have areas of your application that require additional dependencies for image uploading, image editing, displaying charts, etc.  Not every user will necessarily need these things every time they boot your app so why load them initially.  It is actually pretty easy to lazily load them, here is the technique we have been using:

## The service

```js
// app/services/image-uploader.js

export default Ember.Service.extend({
  loadFilepickerPromise: Ember.computed(function loadFilepickerPromise() {
    return injectScript('//api.filepicker.io/v2/filepicker.js')
    .then(()=> {
      window.filepicker.setKey(filepickerApiKey);
    })
    .then(function() {
      return window.filepicker;
    });
  }),

  getImageUploadPromiseFromDomFile(domFile) {
    return new Ember.RSVP.Promise((resolve)=> {
      this.get('loadFilepickerPromise').then((fp)=> {
        fp.store(
          domFile,
          function onFilePickerSuccess(blob) {
            resolve(blob.url);
          }
        );
      });
    });
  }
});

```

There are a couple things to note here:
* Check out the [ember-inject-script](https://github.com/minutebase/ember-inject-script) addon to easily import a script using promises.  There may be other addons or javascript libraries that do something similar and it may be pretty easy to write this yourself, but we have had good luck with this addon.
* You want to make a computed property that returns the promise which imports the dependency script.  This will cache the promise and make sure you don't import the script a second time the second time you use the service.  The second time you use the service you will benefit from an immediately resolving promise!
* I actually added an additional function to abstract away filepicker/filestack which will probably be beneficial in a lot of cases.

## Using the service

```js
// app/components/my-upload-component.js

export default Ember.Component.extend({
  imageUploaderService: Ember.inject.service('image-uploader'),

  selectedImages: Ember.computed(function selectedImages() {
    return this.$('.fileInput')[0].files;
  }).volatile(),

  actions: {
    filesSelected() {
      var files = this.get('selectedImages');
      for(var i=0; i < files.length; i++) {
        this.sendAction('imageUploading', this.get('imageUploaderService').getImageUploadPromiseFromDomFile(files[i]));
      }
    }
  }
});
```

It's really as easy as that, now the first time a user selects a file to upload it will download the filepicker scripts and upload the file!
{% endraw %}
