# Assetylene

Assetylene is a plugin for the Movable Type (MT) content management system. It provides a "Caption" field when inserting an asset into a post or page, and the ability to customize the HTML markup produced when inserting Movable Type (MT) assets.

Note that Assetylene 2.0.0 is very different from 1.x, to work with Movable Type 6.2.2 and later. **If upgrading, your Asset Insertion Template Module will need
to be updated to work with Assetylene.**


# Prerequisites

* Movable Type 6.2 or later
* Movable Type 4.2 or later, 5.x, 6.0.x, and 6.1.x are supported with
  [version 1.1.1](https://github.com/endevver/mt-plugin-assetylene/releases) of
  Assetylene.

# Installation

To install this plugin follow the instructions found here:

http://tinyurl.com/easy-plugin-install

# Configuration

In order for Assetylene to generate HTML that displays a caption beneath assets inserted into posts and pages, you must create a Template Module named "Asset Insertion".

The tags provided by Assetylene (and the differences between the Assetylene 2.x and 1.x tags) are discussed in "Template Tags".

In "Structure of the Asset Insertion Template Module", an example "Asset Insertion" template module is provided, and the block tags that must be used in that template module are discussed.

In "Updating an Existing Asset Insertion Template Module When Upgrading from Assetylene 1.x to 2.x", some suggestions for modernizing the Asset Insertion template module are offered.

# Usage

This plugin adds a "Caption" checkbox and field to the asset Insert Options
dialog. The caption field can of course be edited, but is pre-populated with the
value of the asset's Description field. Note that selecting the "Caption"
checkbox enabled/disabled display of the caption; the text doesn't need to be
deleted from the caption field if you don't want it displayed.

After creating the Asset Insertion Template Module and customizing it as
necessary, no further interaction from the author is necessary to use the new
template during the asset insert process.

## Template Tags

Assetylene adds a number of template tags that can be used in the Asset
Insertion Template Module. These tags reflect options that are set on the asset
Insert Options screen.

* `mt:AssetyleneAlign`: The value of the "Alignment" field, either `none`,
  `left`, `center`, or `right`. (In Assetylene 1.x, this was the `align` tag.)
* `mt:AssetyleneCaption`: The value of the caption field, if the "Insert a
  caption?" checkbox is selected. (In Assetylene 1.x, this was the `caption` tag.)
* `mt:AssetyleneEnclose`: This value is used to track whether the asset inserter
  is being used with an Asset Custom Field. If a Custom Field is being used then
  this value is true, otherwise false. (In Assetylene 1.x, this was the `enclose` tag.)
* `mt:AssetyleneInclude`: This value is true if the "Display Image in
  entry/page" checkbox is selected; false otherwise. (In Assetylene 1.x, this was the `include` tag.)
* `mt:AssetyleneNewEntry`: This value is true if the asset is being inserted
  into a new and unsaved Entry or Page, otherwise false.
* `mt:AssetylenePopup`: This value is true if the "Link image to full-size
  version in a popup window" checkbox is selected; false otherwise. (In Assetylene 1.x, this was the `popup` tag.)
* `mt:AssetyleneThumb`: This value is true if the "Use thumbnail" checkbox is
  selected; false otherwise. (In Assetylene 1.x, this was the `thumb` tag.)
* `mt:AssetyleneThumbWidth`: This is the "width: [ ] pixels" value for the
  thumbnail.
* `mt:AssetyleneWrapText`: This value is always true.

Assetylene provides one more tag: `mt:AssetyleneDefaultHTML`. This tag uses the
above tag values to build the default HTML created by Movable Type. (In Assetylene 1.x, this was the `upload_html` tag.)

## Asset Insertion Template Module Structure

The Asset Insertion Template Module should use the Assets container tagset to enter the asset context so Movable Type iterates through the assets selected for inserting. (See [Template Tags in Movable Type](https://movabletype.org/documentation/designer/template-tags.html) for further explanation of the container tags within Movable Type templates.)

This example Asset Insertion template module illustrates this concept:

    <div class="assets">
    <mt:Assets><mt:Section strip_linefeeds="1" replace="    ","">
        <mt:If tag="AssetyleneCaption">
            <div class="caption align-<mt:AssetyleneAlign>">
            <mt:If tag="AssetyleneThumb">
                <mt:AssetyleneThumbWidth setvar="thumb_width">
                <img src="<mt:AssetThumbnailURL width="$thumb_width">" alt="<mt:AssetLabel>" />
            <mt:Else>
                <img src="<mt:AssetURL>" alt="<mt:AssetLabel>" />
            </mt:If>
                <div><mt:AssetyleneCaption></div>
            </div>
        <mt:Else>
            <mt:AssetyleneDefaultHTML>
        </mt:If>
    </mt:Section>
    </mt:Assets></div>

Note the use of the `Section` tag and arguments, and the different spacing of
the `Assets`, `Section`, and closing `div.assets` tags. All of this is to
format the inserted HTML, minimizing space used but still somewhat maintaining
readability.

## Updating an Existing Asset Insertion Template Module When Upgrading from Assetylene 1.x to 2.x

If you are upgrading a Movable Type-based website from a version of Movable Type that is compatible with Assetylene 1.x to a version that requires Assetylene 2.x, the content and structure of the old Asset Insertion template module may be quite different from what will be required going forward.

The easiest way to upgrade to Assetylene 2.x may be to:
* look at previously-generated captions for inserted assets, taking note of things like the tags and CSS that were produced by Assetylene 1.x,
* begin with the Asset Insertion template module listed above,
* add the tags and CSS that were produced by Assetylene 1.x into the tag structure in the example.

The Assetylene 1.x tag corresponding to many Assetylene 2.x tags is listed in "Template and Template Tags" section of this README document to aid in this upgrade process.

# Support

Although After6 Services LLC has contributed to the development of this plugin, After6 only provides support for it as part of a Movable Type support agreement that references this plugin by name.

# License

This plugin has been released under the terms of the GNU Public License, version 2.0. See LICENSE.md for the exact license.

# Authorship

Brad Choate originally created this plugin for Six Apart in December 2008 (version 1.0). Byrne Reese made some updates in May 2009 (version 1.01 and 1.02). Since being imported to Github in 2010, Endevver has maintained this plugin with commits from Dan Wolfgang. Since 2019, After6 Services has maintained this plugin with commits from Dave Aiello.

# Copyright

Copyright &copy; 2008, Six Apart Ltd. All Rights Reserved.
Copyright &copy; 2010-2019, Endevver, LLC. All Rights Reserved.
Copryright &copy; 2019-2020, After6 Services LLC. All Rights Reserved.

Movable Type is a trademark of Six Apart Ltd.

Trademarks, product names, company names, or logos used in connection with this repository are the property of their respective owners and references do not imply any endorsement, sponsorship, or affiliation with After6 Services LLC unless otherwise specified.