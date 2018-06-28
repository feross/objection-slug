# objection-slug [![travis][travis-image]][travis-url] [![npm][npm-image]][npm-url] [![downloads][downloads-image]][downloads-url] [![javascript style guide][standard-image]][standard-url]

[travis-image]: https://img.shields.io/travis/feross/objection-slug/master.svg
[travis-url]: https://travis-ci.org/feross/objection-slug
[npm-image]: https://img.shields.io/npm/v/objection-slug.svg
[npm-url]: https://npmjs.org/package/objection-slug
[downloads-image]: https://img.shields.io/npm/dm/objection-slug.svg
[downloads-url]: https://npmjs.org/package/objection-slug
[standard-image]: https://img.shields.io/badge/code_style-standard-brightgreen.svg
[standard-url]: https://standardjs.com

### Automatically generate slugs for an [Objection.js](https://vincit.github.io/objection.js/) model

This plugin will automatically generate slugs for your model based on a source
field and a slug field. It will ensure that the slugs are unique by checking to
see if the slug already exists in the model's table. If so, it will attempt to
append a number to the end of the slug.

For example, if the source field is `'How to Fry an Egg'`, then the slug will be
`'how-to-fry-an-egg'`. However, if that slug already exists in the model's table
then the slug will be `'how-to-fry-an-egg-1'` (note that `-1` was appended). If
that slug also exists, then the slug would be `'how-to-fry-an-egg-2'` and so
on...

## Install

```
npm install objection-slug
```

## Why this package?

This package was inspired by
[`objection-slugify`](https://github.com/combine/objection-slugify) but it's
different in the following ways:

1. Appends a number instead of a UUID.

   Instead of attempting to append a UUID to the end of the slug, which does not
   look nice, this package appends a sequential number to the end of duplicate
   slugs.

2. Removed unwanted features

   There are several options which aren't useful and were removed. For example,
   instead of changing the slug when the source field changes (which breaks any
   URLs based on the slug, which is very bad for SEO), this package never
   changes the slug after it is generated.

3. Handles many more unicode symbols by default, because it uses the `mollusc`
   library instead of `slugify`.

## Usage

```js
const objectionSlug = require('objection-slug')
const { Model } = require('objection')

// Create the mixin
const slug = objectionSlug({
  sourceField: 'title',
  slugField: 'slug'
})

// Create the Model and add the mixin
class Post extends slug(Model) {
  // ...code
}

const post = await Post
  .query()
  .insert({ title: 'How to Fry an Egg' })

console.log(post.slug)
// how-to-fry-an-egg
```

## API

### `slug = objectionSlug([opts])`

Create a slug mixin to be used with
[Objection.js](https://vincit.github.io/objection.js/) models. See usage example
above.

#### `opts.sourceField` (required)

The source of the slugged content.

#### `opts.slugField` (defaults to `'slug'`)

The field to store the slug on.

## License

MIT. Copyright (c) [Feross Aboukhadijeh](https://feross.org).
