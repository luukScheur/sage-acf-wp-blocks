# Sage ACF Gutenberg Blocks
Generate ACF Gutenberg blocks just by adding templates to your Sage theme. This package is based heavily on [this article](https://medium.com/nicooprat/acf-blocks-avec-gutenberg-et-sage-d8c20dab6270) by [nicoprat](https://github.com/nicooprat).

## Installation
Run the following in your Sage 9-based theme directory:
```sh
composer require "mwdelaney/sage-acf-gutenberg-blocks"
```

## Creating blocks
Add blade templates to `views/blocks` which get and use ACF data. Each template requires a comment block with some data in it:
```blade
{{--
  Title:
  Description:
  Category:
  Icon:
  Keywords:
  Mode:
  Align:
  PostTypes:
  SupportsAlign:
  SupportsMode:
  SupportsMultiple:
--}}
```

### Example block template

```blade
{{--
  Title: Testimonial
  Description: Customer testimonial
  Category: formatting
  Icon: admin-comments
  Keywords: testimonial quote
  Mode: edit
  Align: left
  PostTypes: page post
  SupportsAlign: left right
  SupportsMode: false
  SupportsMultiple: false
--}}

<blockquote data-{{ $block['id'] }} class="{{ $block['classes'] }}">
    <p>{{ get_field('testimonial') }}</p>
    <cite>
      <span>{{ get_field('author') }}</span>
    </cite>
</blockquote>

<style type="text/css">
  [data-{{$block['id']}}] {
    background: {{ get_field('background_color') }};
    color: {{ get_field('text_color') }};
  }
</style>
```

## Creating ACF fields
Once a block is created you'll be able to assign ACF fields to it using the standard Custom Fields interface in WordPress. We recommend using [sage-advanced-custom-fields](https://github.com/MWDelaney/sage-advanced-custom-fields) to keep your ACF fields in version control with Sage.

## Filter block data
Block data can be altered via the 'sage/blocks/[block-name]/data' filter. For example, if your block template is called `my-block.blade.php`, you can alter the data this way:

```php
add_filter('sage/blocks/my-block/data', function ($block) { // Do your thing here. });
```
