VSCODE-TODO-HIGHLIGHT
===

[![License: MIT](https://img.shields.io/badge/License-MIT-brightgreen.svg)](https://opensource.org/licenses/MIT) [![Build Status](https://travis-ci.org/wayou/vscode-todo-highlight.svg?branch=master)](https://travis-ci.org/wayou/vscode-todo-highlight) [![Version](http://vsmarketplacebadge.apphb.com/version-short/wayou.vscode-todo-highlight.svg)](https://marketplace.visualstudio.com/items?itemName=wayou.vscode-todo-highlight) [![Installs](http://vsmarketplacebadge.apphb.com/installs-short/wayou.vscode-todo-highlight.svg)](https://marketplace.visualstudio.com/items?itemName=wayou.vscode-todo-highlight) [![Ratings](http://vsmarketplacebadge.apphb.com/rating-short/wayou.vscode-todo-highlight.svg)](https://marketplace.visualstudio.com/items?itemName=wayou.vscode-todo-highlight)

Highlight `TODO`,`FIXME` or any other annotations within your code.

Sometimes you will forget to review the TODOs added while coding till publish the code to production.
So I've been long for an extension to highlight them and remind me know there're notes or things not done.

Hope this extension helps you as well.

### Preview

- with `material night` color theme:
![](https://github.com/wayou/vscode-todo-highlight/raw/master/assets/material-night.png)

- with `material night eighties` color theme:
![](https://github.com/wayou/vscode-todo-highlight/raw/master/assets/material-night-eighties.png)

### Config

`TODO:`,`FIXME:` are built in keywords. You can override the look by customizing the setting.

To custom the keywords and other stuff, <kbd>command</kbd> + <kbd>,</kbd> (Windows / Linux: File -> Preferences -> User Settings) open vscode `settings.json` file.

following is an example of configuration:

```js
{
    "todohighlight.isEnable": true, //toggle the highlight, default is true
    "todohighlight.isCaseSensitive": true, //whether the keywords are case sensitive or not
    "todohighlight.highlightWholeLine": false, //highlight whole line instead of keyword only
    "todohighlight.keywords": [
        "BUG:", // adding custom keywords without specifying the look, default color will be applied
        "REVIEW:", //another custom keyword
        {  
            "text": "NOTE:", // custom text to be highlighted
            "color": "#ff0000", // the text color, any css color identifier is valid
            "backgroundColor": "yellow", // the text background color
            "overviewRulerColor": "grey" //the color of the ruler mark on the scroll bar. use rgba() and define transparent colors to play well with other decorations.
        },
        {
            "text": "HACK:",
            "color": "#000"
        },
        {//this block will override the built-in keyword `TODO:` and give it new style
            "text": "TODO:",
            "color": "red",
            "backgroundColor": "rgba(0,0,0,.2)"    
        }
        ...
    ],
    "todohighlight.defaultStyle": { //specify the default style for custom keywords, if not specified, build in default style will be applied
        "color": "#0000ff",
        "backgroundColor": "yellow",
        "overviewRulerColor": "grey"
    },
    "todohighlight.include": "{**/*.js,**/*.html,**/*.php,**/*.css}", //A glob pattern that defines the files to search for. Only include files you need, DO NOT USE `{**/*.*}` for both permormance and avoiding binary files reason
    "todohighlight.exclude": "{**/node_modules/**,**/bower_components/**,**/dist/**,**/build/**,**/.vscode/**,**/_output/**,**/*.min.*,**/*.map}",//A glob pattern that defines files and folders to exclude while listing annotations
    "todohighlight.changeFilePattern": false,//due to an issue of vscode, set this to true if the file path within the output channel not clickable. this will change the file path from `<path>#<line>` to `<path>:<line>:<column>`

}
```

**All settings are optional**

### Commands

This extension contributes the following commands to the Command palette.

- `Toggle highlight` : turn on/off the highlight
![](https://github.com/wayou/vscode-todo-highlight/raw/master/assets/toggle-highlight.gif)
- `List hilighted annotations` : list annotations and reveal from corresponding file
![](https://github.com/wayou/vscode-todo-highlight/raw/master/assets/list-annotations.gif)


### Known issue

If you find files witin the output channel not clickable, set `todohighlight.changeFilePattern` to `true`, this will toggle the file path from `<path>#<line>` to `<path>:<line>:<column>`. This is because the file path differs from platform for vscode to make it clickable (see this [issue](https://github.com/Microsoft/vscode/issues/586) ), but there's no corresponding api that extensions can tell what OS your are running.

