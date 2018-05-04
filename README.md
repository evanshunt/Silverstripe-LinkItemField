# SilverStripe 4 Link Item Field

Original Author: [Andrew Mc Cormack](https://github.com/Andrew-Mc-Cormack)

## Features

Provides a has_one Link object with the following options:
  - Anchor link
  - Internal Link
  - External Link
  - Email
  - Telephone
  - File
  - Image
  - Link target (_blank etc)

## Screen Shots

  - [Link Item Field Modal Open](/docs/images/modal-open.jpg)

## Installation

Add the following to your composer.json file and run /dev/buid?flush=all

```json
{  
    "require": {  
        "evanshunt/silverstripe-linkitemfield": "4.0.*"
    }
}
```

## Setup

The field references a has_one LinkItem relation on a DataObject. Make sure to include both the field and object namespaces in your class.

```php

use evanshunt\LinkItemField\Forms\LinkItemField;
use evanshunt\LinkItemField\Model\LinkItem;
use SilverStripe\ORM\DataObject;

class MyObject extends DataObject 
{
    private static has_one = [
        'MyRelation' => LinkItem::class
    ];
}
```

The field can easily be added to an DataObject / extension through getCMSFields() / updateCMSFields()  or similar.

```php
$fields->addFieldToTab('Root.Main', LinkItemField::create('MyRelationID', 'My Relation Title'));
```

The relation will expose 3 properties in your template - Link, Title, and Target.

```html
<% with MyRelation %>
<a href="$Link" target="$Target">$Title</a>
<% end_with %>
```

When calling Link the outputted URL will be formatted depending on the Link type

```html
<a href="#{TheURL}">For Anchor</a>
<a href="{TheURL}">For Internal</a>
<a href="{TheURL}">For External</a>
<a href="mailto:{TheURL}">For Email</a>
<a href="tel:+{TheURL}">For Telephone</a>
<a href="{TheURL}">For File</a>
<a href="{TheURL}">For Image</a>
```

## Todo

  - Add React
