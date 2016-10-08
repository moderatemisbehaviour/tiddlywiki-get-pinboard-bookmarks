# TW5-get-pinboard-bookmarks
Enrich your tiddlers with bookmarks from your [Pinboard](https://pinboard.in/) account.

#### _Disclaimer_
This plugin is a work in progress, it is not yet `1.0`.

This plugin only works with the Node.js version of TiddlyWiki5.

# Getting Started
#### If you don't already have a clone of the TiddlyWiki5 repository.
`git clone https://github.com/Jermolene/TiddlyWiki5.git`
#### Clone this repo inside the plugins directory of the TiddlyWiki5 repository.
`cd TiddlyWiki5/plugins`
`git clone https://github.com/moderatemisbehaviour/TW5-get-pinboard-bookmarks.git`
#### Add your Pinboard API key to the plugin's `config.tid`.
1. Go to [the password section of your Pinboard's account setting page](https://pinboard.in/settings/password).
2. Copy the full API token including the username.
3. Paste it into `plugins/TW5-get-pinboard-bookmarks/config.tid` like so:
```
title: $:/config/get-pinboard-bookmarks

API_TOKEN_GOES_HERE
```
#### If you don't already have a wiki created then create one.
1. Navigate back to the root directory of the TiddlyWiki5 repository.
2. `node tiddlywiki your-wiki --init server`

#### Add this plugin to your wiki's `tiddlywiki.info` file.
```
{
    ...,
    "plugins": [
        ...,
        "TW5-get-pinboard-bookmarks"
    ],
    ...,
}
```

#### Open your wiki.
1. From the root of the TiddlyWiki5 repository run:
`node tiddlywiki your-wiki --server`
2. Open your browser and go to `http://localhost:8080`.

#### Call the `get-pinboard-bookmarks` macro in tiddlers that you would like enriching with Pinboard bookmarks.
Add `<<get-pinboard-bookmarks>>` to the body of a tiddler that has tags which also appear on your Pinboard bookmarks.

# How It Works
On startup the plugin retrieves all your bookmarks from the Pinboard API using
the `posts/all` method. It asynchronously processes the JSON response and writes a new tiddler for each bookmark.
These 'bookmark tiddlers' have the following characteristics:
* They are saved in a `.tid` file with the naming convention `pinboard_Bookmark_Title` (the intention was that they be saved in `tiddlers/pinboard` but that is not possible until [this pull request](https://github.com/Jermolene/TiddlyWiki5/pull/2541) is merged on the TiddlyWiki5 repository).
* They are tagged with `$:/tags/Pinboard`.
* They have a *url* field that contains the URL of the original bookmark.
* They have a *type* field set to `text/x-markdown` which means their content is parsed as Markdown.

# Roadmap
* Normalise Pinboard tags by replacing spaces with hyphens and capitalising words, allowing 'tag tiddlers' to have well formed titles.
* Make Markdown parsing and tag normalisation optional via configuration.
* Create **Get Started** instructions as well as **readme** and **usage** information in plugin section of **Control Panel**.
