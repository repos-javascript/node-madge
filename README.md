# MaDGe - Module Dependency Graph

[![Build Status](https://secure.travis-ci.org/pahen/node-madge.png)](http://travis-ci.org/pahen/node-madge)

Create graphs from your [CommonJS](http://nodejs.org/api/modules.html) or [AMD](https://github.com/amdjs/amdjs-api/wiki/AMD) module dependencies. Could also be useful for finding circular dependencies in your code. Tested on [Node.js](http://nodejs.org/) and [RequireJS](http://requirejs.org/) projects. Dependencies are calculated using static code analysis. CommonJS dependencies are found using James Halliday's [detective](https://github.com/substack/node-detective) and for AMD I'm using some parts copied from James Burke's [RequireJS](https://github.com/jrburke/requirejs) (both are using [UglifyJS](https://github.com/mishoo/UglifyJS)).

## Examples
Here's a very simple example of a generated image.

![](https://github.com/pahen/node-madge/raw/master/examples/small.png)

 - blue = has dependencies
 - green = has no dependencies
 - red = has circular dependencies

Here's an example generated from the [Express](https://github.com/visionmedia/express) project.

![](https://github.com/pahen/node-madge/raw/master/examples/express.png)

# Installation

To install as a library:

	$ npm install madge

To install the command-line tool:

	$ sudo npm -g install madge

## Graphviz (optional)

Only required if you want to generate the visual graphs using [Graphviz](http://www.graphviz.org/).

### Mac OS X

	$ sudo port install graphviz

### Ubuntu

	$ sudo apt-get install graphviz

# API

Coming soon ..

# CLI

	Usage: madge [options] <file|dir ...>

	Options:
	  -h, --help              output usage information
	  -V, --version           output the version number
	  -f, --format <name>     format to parse (amd/cjs)
	  -o, --output <type>     output format (plain/json)
	  -s, --summary           show summary of all dependencies
	  -c, --circular          show circular dependencies
	  -d, --depends <id>      show modules that depends on the given id
	  -x, --exclude <regex>   a regular expression for excluding modules
	  -t, --dot               output graph in the DOT language
	  -i, --image <filename>  write graph to file as a PNG image
	  -l, --layout <name>     layout engine to use for image graph (dot/neato/fdp/sfdp/twopi/circo)
	  -b, --break-on-error    break on parse errors & missing modules
	  -n, --no-colors         skip colors in output and images
	  -r, --read              skip scanning folders and read JSON from stdin
	  -C, --config <filename> provide a config file


## Examples:

### List all module dependencies (CommonJS)

	$ madge /path/src

### List all module dependencies (AMD)

	$ madge --format amd /path/src

### Finding circular dependencies

	$ madge --circular /path/src

### Show modules that depends on a given module

	$ madge --depends 'wheels' /path/src

### Excluding modules

	$ madge --exclude '^foo$|^bar$|^tests' /path/src

### Save graph as a PNG image (graphviz required)

	$ madge --image graph.png /path/src

### Save graph as a [DOT](http://en.wikipedia.org/wiki/DOT_language) file for further processing (graphviz required)

	$ madge --dot /path/src > graph.gv

### Pipe predefined results (the example image was produced with the following command)

	$ cat << EOF | madge --read --image example.png
	{
		"a": ["b", "c", "d"],
		"b": ["c"],
		"c": [],
		"d": ["a"]
	}
	EOF

## Config (use with --config)

	{
	    "format": "amd",
	    "image": "dependencyMap.png",
	    "fontFace": "Arial",
	    "fontSize": "14px",
	    "imageColors": {
	        "noDependencies" : "#0000ff",
	        "dependencies" : "#00ff00",
	        "circular" : "#bada55",
	        "edge" : "#666666",
	        "bgcolor": "#ffffff"
	    }
	}

# Running tests

	$ npm test

# License

(The MIT License)

Copyright (c) 2012 Patrik Henningsson &lt;patrik.henningsson@gmail.com&gt;

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
'Software'), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY
CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,
TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE
SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.