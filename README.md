[![Build Status](https://travis-ci.org/davidpett/ember-data-contentful.svg?branch=master)](https://travis-ci.org/davidpett/ember-data-contentful)
[![npm version](https://badge.fury.io/js/ember-data-contentful.svg)](https://badge.fury.io/js/ember-data-contentful)
[![Ember Observer Score](http://emberobserver.com/badges/ember-data-contentful.svg)](http://emberobserver.com/addons/ember-data-contentful)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](http://makeapullrequest.com)
[![FastBoot Ready](https://img.shields.io/badge/FastBoot-ready-brightgreen.svg)](http://ember-fastboot.com)
# ember-data-contentful

This is an Ember Data adapter/serializer that uses the **READ ONLY** Content Delivery API from [contentful](http://contentful.com)

## Setup in your app
```
ember install ember-data-contentful
```

After installing the addon, configure your Contentful Space ID and Access Token in `config/environment.js`:
```
contentful: {
  space: 'YOUR-CONTENTFUL-SPACE',
  accessToken: 'YOUR-CONTENTFUL-ACCESS-TOKEN',
  previewAccessToken: 'YOUR-CONTENTFUL-PREVIEW-ACCESS-TOKEN',
  usePreviewApi: false
}
```

Once you have configured this, you can use the normal Ember Data requests of `findRecord`, `findAll`, `queryRecord`, and `query`. For example:
```
model() {
  return this.store.findAll('project');
}
```
or
```
model(params) {
  return this.store.findRecord('project', params.project_id);
}
```

If you want to use pretty urls and the `slug` field in contentful, you can make your query like so:
```
model(params) {
  return this.store.queryRecord('page', {
    'fields.slug': params.page_slug
  });
},
serialize(model) {
  return { page_slug: get(model, 'slug') };
}
```
and ensure that you declare your route in `router.js` like this:
```
this.route('page', { path: ':page_slug' });
```

For more information on the contentful Content Delivery API and the available queries, look here: https://www.contentful.com/developers/docs/references/content-delivery-api/