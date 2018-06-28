# objection-slug [![travis][travis-image]][travis-url] [![npm][npm-image]][npm-url] [![downloads][downloads-image]][downloads-url] [![javascript style guide][standard-image]][standard-url]

[travis-image]: https://img.shields.io/travis/feross/objection-slug/master.svg
[travis-url]: https://travis-ci.org/feross/objection-slug
[npm-image]: https://img.shields.io/npm/v/objection-slug.svg
[npm-url]: https://npmjs.org/package/objection-slug
[downloads-image]: https://img.shields.io/npm/dm/objection-slug.svg
[downloads-url]: https://npmjs.org/package/objection-slug
[standard-image]: https://img.shields.io/badge/code_style-standard-brightgreen.svg
[standard-url]: https://standardjs.com

### Automatically generate slugs for an Objection.js model

## Install

```
npm install objection-slug
```

## Why this package?

## Features

## Usage

```js
const objectionSlug = require('objection-slug')
const { Model } = require('objection')

// Create the mixin
const slugify = objectionSlug({
  sourceField: 'title',
  slugField: 'slug'
})

// Create the Model and add the mixin
class Post extends slugify(Model) {
  // ...code
}

const post = await Post
  .query()
  .insert({ title: 'How to Fry an Egg' })

console.log(post.slug)
// how-to-fry-an-egg
```

## API

## License

MIT. Copyright (c) [Feross Aboukhadijeh](https://feross.org).
