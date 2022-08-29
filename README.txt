Entity Embed - Extras
-----------------------------------------------
For blocks placed in a node layout or via the block region system. You should
be able to target it perfectly fine. But for embedded entities.. no such luck.

Extension Custom Module for Entity Embed.
Extends the template suggestions for entities when embedded as a content
element. Review the module file to add or subtract suggestion details.

Example
<!-- FILE NAME SUGGESTIONS:
   * entity-embed-container--type-block-content--entity-type-highlight-block--uuid-8a2fe71b-c23d-4430-b138-7cebb55fb643.html.twig
   * entity-embed-container--type-block-content--entity-type-highlight-block--id-35.html.twig
   * entity-embed-container--type-block-content--entity-type-highlight-block--display-view-mode-block-content-full.html.twig
   * entity-embed-container--type-block-content--entity-type-highlight-block.html.twig
   * entity-embed-container--embed-button-block--embed-display-view-mode-block-content-full.html.twig
   x entity-embed-container--embed-display-view-mode-block-content-full.html.twig
   * entity-embed-container--embed-button-block.html.twig
   * entity-embed-container.html.twig
-->

When registering your hook_theme make sure to properly define the embed values.

function MODULE_THEME_NAME_theme() {
    return [
        'entity_embed_container__embed_display_view_mode_block_content_full' => [
            'template' => 'entity-embed-container--embed-display-view-mode-block-content-full.html',
            'base hook' => 'entity_embed_container',
        ],
    ];
}

within the template I couldn't get the more detailed suggestions to work. 
It appears to only detect up to the main entity type, in this case "block content"
and the display "full".. which is frustrating for sure. I'd like it to detect
the custom block "type" as well.

To get around this I made sure all fields in each block content type are unique.
So detecting if a particular field exists when rendering the template, otherwise 
use the default rendering. Like so:

---- entity-embed-container--embed-display-view-mode-block-content-full.html.twig ---

{% set background_img = element['entity']['field_hl_bk_bg_img']['#markup'] %}
{% if background_img is not empty %}

custom layout and variables here.

{% else %}
<div{{ attributes }}>{{ children }}</div>
{% endif %}

Create a template file inside of a custom module for each block_content type to 
maintain the config and code. Or wrap it all into a single module or theme.