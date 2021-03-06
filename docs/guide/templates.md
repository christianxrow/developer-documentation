# Templates

## Templating basics

To apply a template to any part of your webpage, you need three (optionally four) elements:

1. An entry in the configuration that defines which template should be used in what situation
1. The template file itself
1. Assets used by the template (for example, CSS or JS files, images, etc.)
1. (optional) A custom controller used when the template is read which allows you more detailed control over the page.

Each template must be mentioned in a configuration file together with a definition of the situation in which it is used. You can use the `ezplatform.yml` file located in the `app/config/` folder, or create your own separate configuration file in that folder that will list all your templates.

!!! note

    If you decide to create a new configuration file, you will need to import it by including an import statement in `ezplatform.yml`. Add the following code at the beginning of `ezplatform.yml`:

    ``` yaml
    imports:
        - { resource: <your_file_name>.yml }
    ```

!!! tip

    If you are using the recommended .yml files for configuration, here are the basic rules for this format:

    The configuration is based on pairs of a key and its value, separated by a colon, presented in the following form: key: value. The value of the key may contain further keys, with their values containing further keys, and so on. This hierarchy is marked using indentation – each level lower in the hierarchy must be indented in comparison with its parent.

A short configuration file can look like this:

``` yaml
# Sample configuration file
ezpublish:
    system:
        default:
            user:
                layout: pagelayout.html.twig
            content_view:
                full:
                    article:
                        template: full\article.html.twig
                        match:
                            Identifier\ContentType: [article]
                    blog_post:
                        controller: app.controller.blog:showBlogPostAction
                        template: full\blog_post.html.twig
                        match:
                            Identifier\ContentType: [blog_post]
                line:
                    article:
                        template: line\article.html.twig
                        match:
                            Identifier\ContentType: [article]
```

This is what individual keys in the configuration mean:

- `ezpublish` and `system` are obligatory at the start of any configuration file which defines views.
- `default` defines the SiteAccess for which the configuration will be used. "default", as the name suggests, determines what views are used when no other configuration is chosen. You can also have separate keys defining views for other SiteAccesses.
- `user` and `layout` point to the main template file that is used in any situation where no other template is defined. All other templates extend this one.
- `content_view` defines the view provider.

!!! note

    In earlier version `location_view` was used as the view provider. It has been deprecated since eZ Platform 1.x.

- `full` and `line` determine the kind of view to be used (see below).
- `article` and `blog_post` are the keys that start the configuration for one individual case of using a template. You can name these keys any way you want, and you can have as many of them as you need.
- `template` names the template to be used in this case, including the folder it is stored in (starting from `app/Resources/views`).
- `controller` defines the controller to be used in this case. Optional, if this key is absent, the default controller is used.
- `match` defines the situation in which the template will be used. There are different criteria which can be used to "match" a template to a situation, for example a Content Type, a specific Location ID, Section, etc. You can view the full list of matchers here: [View provider configuration](content_rendering#view-provider-configuration). You can specify more than one matcher for any template; the matchers will be linked with an AND operator.

In the example above, three different templates are mentioned, two to be used in full view, and one in line view. Notice that two separate templates are defined for the "article" Content Type. They use the same matcher, but will be used in different situations – one when an Article is displayed in full view, and one in line view. Their templates are located in different folders. The line template will also make use of a custom controller, while the remaining cases will employ the default one.

##### Full, line and other views

Each Content item can be rendered differently, using different templates, depending on the type of view it is displayed in. The default, built-in views are **full** (used when the Content item is displayed by itself, as a full page), **line** (used when it is displayed as an item in the list, for example a listing of contents of a folder), and **embed** (used when one Content item is embedded in another). Other, custom view types can be created, but only these three have built-in controllers in the system.

See [View provider configuration](content_rendering#view-provider-configuration) for more details.

### Template file

Templates in eZ Platform are written in the Twig templating language.

!!! note "Twig templates in short"

    At its core, a Twig template is an HTML frame of the page that will be displayed. Inside this frame you define places (and manners) in which different parts of your Content items will be displayed (rendered).

    Most of a Twig template file can look like an ordinary HTML file. This is also where you can define places where Content items or their fields will be embedded.

The configuration described above lets you select one template to be used in a given situation, but this does not mean you are limited to only one file per case. It is possible to include other templates in the main template file. For example, you can have a single template for the footer of a page and include it in many other templates. Such templates do not need to be mentioned in the configuration .yml file.

!!! tip

    See [Including Templates](http://symfony.com/doc/current/book/templating.html#including-templates) in Symfony documentation for more information on including templates.

The main template for your webpage is placed in a pagelayout.
You can define the pagelayout per SiteAccess using the `ezpublish.system.<SiteAccess>.pagelayout` setting.
This template will be used by default for those parts of the website where no other templates are defined.

A `pagelayout.html.twig` file exists already in Demo Bundles, but if you are using a clean installation, you need to create it from scratch. This file is typically located in a bundle, for example using the built-in AppBundle: `src/AppBundle/Resources/views`. The name of the bundle must the added whenever the file is called, like in the example below.

Any further templates will extend and modify this one, so they need to start with a line like this:

``` html
{% extends "AppBundle::pagelayout.html.twig" %}
```

!!! note

    Although using AppBundle is recommended, you could also place the template files directly in `<installation_folder>/app/Resources/views`. Then the files could be referenced in code without any prefix. See [Best Practices](best_practices.md) for more information.

!!! tip "Template paths"

    In short, the `Resources/views` part of the path is automatically added whenever a template file is referenced. What you need to provide is the bundle name, name of any subfolder within `/views/`, and file name, all three separated by colons (:)

    To find out more about the way of referencing template files placed in bundles, see [Referencing Templates in a Bundle](http://symfony.com/doc/current/book/templating.html#referencing-templates-in-a-bundle) in Symfony documentation.

Templates can be extended using a Twig [`block`](http://twig.sensiolabs.org/doc/functions/block.html) tag. This tag lets you define a named section in the template that will be filled in by the child template. For example, you can define a "title" block in the main template. Any child template that extends it can also contain a "title" block. In this case the contents of the block from the child template will be placed inside this block in the parent template (and override what was inside this block):

``` html
<!--pagelayout.html.twig-->
{# ... #}
    <body>
        {% block title %}
            <h1>Default title</h1>
        {% endblock %}
    </body>
{# ... #}
```

``` html
<!--child.html.twig-->
{% extends "AppBundle::pagelayout.html.twig" %}
{% block title %}
    <h1>Specific title</h1>
{% endblock %}
```

In the simplified example above, when the `child.html.twig` template is used, the "title" block from it will be placed in and will override the "title" block from the main template – so "Specific title" will be displayed instead of "Default title."

!!! tip

    Alternatively, you can place templates inside one another using the [`include`](http://twig.sensiolabs.org/doc/functions/include.html)function.

    See [http://twig.sensiolabs.org/doc/templates.html\#](http://twig.sensiolabs.org/doc/templates.html) for detailed documentation on how to use Twig.

##### Embed content in templates

Now that you know how to create a general layout with Twig templates, let's take a look at the ways in which you can render content inside them.

There are several ways of placing Content items or their Fields inside a template. You can do it using one of the [Twig functions described in detail here](twig_functions_reference.md).

As an example, let's look at one of those functions: [ez\_render\_field](twig_functions_reference.md#ez_render_field). It renders one selected Field of the Content item. In its simplest form this function can look like this:

``` html
{{ ez_render_field( content, 'description' ) }}
```

This renders the value of the Field with identifier "description" of the current Content item (signified by "content"). You can additionally choose a special template to be used for this particular Field:

``` html
{{ ez_render_field(
       content,
       'description',
       { 'template': 'AppBundle:fields:description.html.twig' }
   ) }}
```

!!! note

    As you can see in the case above, templates can be created not only for whole pages, but also for individual Fields.

Another way of embedding Content items is using the `render_esi` function (which is not an eZ-specific function, but a Symfony standard). This function lets you easily select a different Content item and embed it in the current page. This can be used, for instance, if you want to list the children of a Content item in its parent.

``` html
{{ render_esi(controller('ez_content:viewAction', {locationId: 33, viewType: 'line'} )) }}
```

This example renders the Content item with Location ID 33 using the line view. To do this, the function applies the `ez_content:viewAction` controller. This is the default controller for rendering content, but can be substituted here with any custom controller of your choice.

#### Assets

Asset files such as CSS stylesheets, JS scripts or image files can be defined in the templates and need to be included in the directory structure in the same way as with any other web project. Assets are placed in the `web/` folder in your installation.

Instead of linking to stylesheets or embedding images like usually, you can use the [`asset`](http://symfony.com/doc/current/book/templating.html#linking-to-assets) function.

#### Controller

While it is possible to template a whole website using only Twig, a custom PHP controller gives many more options of customizing the behavior of the pages.

See [Custom controllers](controllers.md#custom-controllers) for more information.

## Rendering Content items

### Content item Fields

A view template receives the requested Content item, holding all Fields.
In order to display the Fields' value the way you want, you can either manipulate the Field Value object itself, or use a custom template.

#### Getting raw Field value

As you have access to the Content item in the template, you can use [its public methods](https://github.com/ezsystems/ezpublish-kernel/blob/master/eZ/Publish/Core/Repository/Values/Content/Content.php) to access all the information you need. You can also use the `ez_field_value` helper to get the [Field's value only](twig_functions_reference.md#ez_field_value). It will return the correct language if there are several, based on language priorities.

``` html
{# With the following, myFieldValue will be in the Content item's main language #}
{# It will also takes languages you provided to API on retrieval into account #}
{% set myFieldValue = content.getFieldValue( 'some_field_identifier' ) %}

{# Here myTranslatedFieldValue will be in the current language if a translation is available (read from SiteAccess configuration). If not, the Content item's main language will be used #}
{% set myTranslatedFieldValue = ez_field_value( content, 'some_field_identifier' ) %}
```

#### Using the Field Type's template block

All built-in Field Types come with [their own Twig template](https://github.com/ezsystems/ezpublish-kernel/blob/master/eZ/Bundle/EzPublishCoreBundle/Resources/views/content_fields.html.twig). You can render any Field using this default template using the `ez_render_field()` helper.

``` html
{{ ez_render_field( content, 'some_field_identifier' ) }}
```

Refer to [`ez_render_field`](twig_functions_reference.md#ez_render_field) for further information.

!!! tip

    As this makes use of reusable templates, **using `ez_render_field()` is the recommended way and is to be considered the best practice**.

### Content name

The **name** of a Content item is its generic "title", generated by the repository based on the Content Type's naming pattern. It often takes the form of a normalized value of the first field, but might be a concatenation of several fields. There are 2 different ways to access this special property:

- Through the name property of ContentInfo (not translated).
- Through VersionInfo with the TranslationHelper (translated).

#### Translated name

The *translated name* is held in a `VersionInfo` object, in the `names` property which consists of a hash indexed by locale. You can easily retrieve it in the right language via the `TranslationHelper` service.

``` html
{# Languages provided to API will be taken into account so you can do this: #}
<h2>Translated Content name: {{ content.name }}</h2>

{# In earlier versions the same is available using Twig translation helper ez_content_name() #}
<h2>Translated Content name: {{ ez_content_name( content ) }}</h2>
<h3>Also works from ContentInfo: {{ ez_content_name( content.contentInfo ) }}</h3>
```

The helper will by default follow the prioritized languages order. If there is no translation for your prioritized languages, the helper will always return the name in the main language.

You can also **force a locale** in a second argument:

``` html
{# Force fre-FR locale. #}
<h2>{{ ez_content_name( content, 'fre-FR' ) }}</h2>
```

!!! note "Name property in ContentInfo"

    This property is the actual Content name, but **in the main language only** (so it is not translated).

    ``` html
    <h2>Content name: {{ content.contentInfo.name }}</h2>
    ```

    In PHP that would be:

    ``` php
    $contentName = $content->getContentInfo->getName();
    ```

    So make sure to use `$content->getName() or $versionInfo->getName()`, which takes translations into account.

#### Exposing additional variables

It is possible to expose additional variables in a content view template. See [parameters injection in content views](../cookbook/injecting_parameters_in_content_views.md).

### Embedding images

The Rich Text Field allows you to embed other Content items within the Field.

Content items that are identified as images will be rendered in the Rich Text Field using a dedicated template.

You can determine which Content Types will be treated as images and rendered using this template in the `ezplatform.content_view.image_embed_content_types_identifiers` parameter. By default it is set to cover the Image Content Type, but you can add other types that you want to be treated as images, for example:

``` yaml
parameters:
    ezplatform.content_view.image_embed_content_types_identifiers: ['image', 'photo', 'banner']
```

The template that is used when rendering embedded images can be set in the `ezplatform.default_view_templates.content.embed_image` container parameter:

``` yaml
parameters:
    ezplatform.default_view_templates.content.embed_image: 'content/view/embed/image.html.twig'
```

### Adding Links

#### Links to other Locations

Linking to other Locations is done with a [native `path()` Twig helper](http://symfony.com/doc/2.3/book/templating.html#linking-to-pages) (or `url()` if you want to generate absolute URLs). When you pass it the Location object, `path()` will generate the URLAlias.

``` html
{# Assuming "location" variable is a valid eZ\Publish\API\Repository\Values\Content\Location object #}
<a href="{{ path( location ) }}">Some link to a Location</a>
```

If you don't have the Location object, but only its ID, you can generate the URLAlias the following way:

``` html
<a href="{{ path( "ez_urlalias", {"locationId": 123} ) }}">Some link to a Location, with its ID only</a>
```

You can also use the Content ID. In that case the generated link will point to the Content item's main Location.

``` html
<a href="{{ path( "ez_urlalias", {"contentId": 456} ) }}">Some link from a contentId</a>
```

!!! note "Under the hood"

    In the back end, `path()` uses the Router to generate links.

    This makes it also easy to generate links from PHP, via the `router` service.

See also: [Cross-SiteAccess links](siteaccess.md#cross-siteaccess-links)

### Embedding Content items

To render an embedded Content from a Twig template you need to **do a subrequest with the `ez_content` controller**.

#### Using the `ez_content` controller

This controller is exactly the same as [the ViewController presented above](content_rendering.md#the-viewcontroller). It has one main `viewAction` that renders a Content item.

You can use this controller from templates with the following syntax:

``` html
{{ render(controller("ez_content:viewAction", {"contentId": 123, "viewType": "line"})) }}
```

The example above renders the Content item whose ID is **123** with the view type **line**.

Referencing the `ez_content` controller follows the syntax of *controllers as a service*, [as explained in Symfony documentation](http://symfony.com/doc/current/cookbook/controller/service.html).

##### Available arguments

As with any controller, you can pass arguments to `ez_content:viewAction` to fit your needs.
You must provide `contentId` (and, optionally, `locationId`) for the action to work.

|Name|Description|Type|Default value|
|---|---|---|---|
|`contentId`|ID of the Content item you want to render. Can be used together with `locationId`, if the Location belongs to that Content item.|integer|Location's Content item, if defined|
|`locationId`|ID of the Location you want to render. Can be used together with `contentId`, if the Location belongs to that Content item.|integer|Content item's main location, if defined|
|`viewType`|The view type you want to render your Content item/Location in. Will be used by the ViewManager to select a corresponding template, according to defined rules. </br>Example: full, line, my_custom_view, etc.|string|full|
|`layout`|Indicates if the sub-view needs to use the main layout (see [available variables in a view template](content_rendering.md#available-variables))|boolean|false|
|`params`|Hash of variables you want to inject to sub-template, key being the exposed variable name.|hash|empty hash|

For example:

``` html
{{ render(
      controller(
          "ez_content:viewAction",
          {
              "contentId": 123,
              "viewType": "line",
              "params": { "some_variable": "some_value" }
          }
      )
) }}
```

#### Rendering and cache

##### ESI

Just like for regular Symfony controllers, you can take advantage of [ESI](https://symfony.com/doc/current/http_cache/esi.html) and use different cache levels:

``` html
{{ render_esi(controller("ez_content:viewAction", {"contentId": 123, "viewType": "line"})) }}
```

Only scalar variables (not objects) can be sent via `render_esi`.

##### Asynchronous rendering using hinclude

Symfony also supports asynchronous content rendering with the help of the [hinclude.js](http://mnot.github.com/hinclude/) library.

``` html
<!--Asynchronous rendering-->
{{ render_hinclude(controller("ez_content:viewAction", {"contentId": 123, "viewType": "line"})) }}
```

Only scalar variables (not objects) can be sent via `render_hinclude`.

##### Display a default text

If you want to display a default text while a controller is loaded asynchronously, you have to pass a second parameter to your `render_hinclude` Twig function.

``` html
<!--Display a default text during asynchronous loading of a controller-->
{{ render_hinclude(controller('EzCorporateDesignBundle:Header:userLinks'), {'default': "<div style='color:red'>loading</div>"}) }}
```

See also: [Custom controllers](controllers.md#custom-controllers).

[hinclude.js](http://mnot.github.com/hinclude/) needs to be properly included in your layout to work.

[Refer to Symfony documentation](http://symfony.com/doc/current/book/templating.html#asynchronous-content-with-hinclude-js) for all available options.

### Rendering in preview

When previewing content in the back office, the draft view is rendered using the [PreviewController](https://github.com/ezsystems/ezpublish-kernel/blob/master/eZ/Publish/Core/MVC/Symfony/Controller/Content/PreviewController.php).

The first draft of a yet unpublished Content item does not have a Location, because Locations are only assigned when content is published.
To enable rendering in such cases, the PreviewController [creates a temporary virtual Location](https://github.com/ezsystems/ezpublish-kernel/blob/master/eZ/Publish/Core/Helper/PreviewLocationProvider.php#L65).
This Location has some of the properties of the future Location, such as the parent Location ID.
However, it does not fully replace a normal Location.

If the rendering template refers directly to the Location ID of the content, an error will occur.
To avoid such situations, you can check if the Location is virtual using the `location.isDraft` flag in Twig templates, for example:

``` jinja
{% if not location.isDraft %}
    <a href="{{ path(location) }}">{{ ez_content_name(content) }}</a>
{% endif %}
```
