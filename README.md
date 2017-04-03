# api documentation for  [easyimage (v2.1.0)](https://github.com/hacksparrow/node-easyimage)  [![npm package](https://img.shields.io/npm/v/npmdoc-easyimage.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-easyimage) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-easyimage.svg)](https://travis-ci.org/npmdoc/node-npmdoc-easyimage)
#### A promise-based, user-friendly module for processing images in Node.js

[![NPM](https://nodei.co/npm/easyimage.png?downloads=true)](https://www.npmjs.com/package/easyimage)

[![apidoc](https://npmdoc.github.io/node-npmdoc-easyimage/build/screenCapture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-easyimage_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-easyimage/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-easyimage/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-easyimage/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Hage Yaapa",
        "email": "captain@hacksparrow.com"
    },
    "bugs": {
        "url": "https://github.com/hacksparrow/node-easyimage/issues"
    },
    "dependencies": {
        "colors": "^1.0.3",
        "mkdirp": "^0.5.0",
        "q": "^1.0.1"
    },
    "description": "A promise-based, user-friendly module for processing images in Node.js",
    "devDependencies": {
        "chai": "^1.9.1",
        "chai-as-promised": "^4.1.1",
        "mocha": "^1.21.4",
        "rimraf": "^2.2.8"
    },
    "directories": {},
    "dist": {
        "shasum": "4c3a06f7287a20da62c18201ec82fb928fabe348",
        "tarball": "https://registry.npmjs.org/easyimage/-/easyimage-2.1.0.tgz"
    },
    "gitHead": "ab17d54dc39a2ca51a1e9411721f0971c8ae2b7a",
    "homepage": "https://github.com/hacksparrow/node-easyimage",
    "keywords": [
        "imagemagick",
        "image",
        "graphics",
        "process",
        "convert",
        "resize",
        "crop",
        "thumbnail",
        "promise"
    ],
    "license": "MIT",
    "main": "easyimage.js",
    "maintainers": [
        {
            "name": "hacksparrow",
            "email": "captain@hacksparrow.com"
        }
    ],
    "name": "easyimage",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git+ssh://git@github.com/hacksparrow/node-easyimage.git"
    },
    "scripts": {
        "test": "cd test && mocha"
    },
    "version": "2.1.0"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module easyimage](#apidoc.module.easyimage)
1.  [function <span class="apidocSignatureSpan">easyimage.</span>convert (options)](#apidoc.element.easyimage.convert)
1.  [function <span class="apidocSignatureSpan">easyimage.</span>crop (options)](#apidoc.element.easyimage.crop)
1.  [function <span class="apidocSignatureSpan">easyimage.</span>exec (cmd)](#apidoc.element.easyimage.exec)
1.  [function <span class="apidocSignatureSpan">easyimage.</span>info (file)](#apidoc.element.easyimage.info)
1.  [function <span class="apidocSignatureSpan">easyimage.</span>rescrop (options)](#apidoc.element.easyimage.rescrop)
1.  [function <span class="apidocSignatureSpan">easyimage.</span>resize (options)](#apidoc.element.easyimage.resize)
1.  [function <span class="apidocSignatureSpan">easyimage.</span>rotate (options)](#apidoc.element.easyimage.rotate)
1.  [function <span class="apidocSignatureSpan">easyimage.</span>thumbnail (options)](#apidoc.element.easyimage.thumbnail)



# <a name="apidoc.module.easyimage"></a>[module easyimage](#apidoc.module.easyimage)

#### <a name="apidoc.element.easyimage.convert"></a>[function <span class="apidocSignatureSpan">easyimage.</span>convert (options)](#apidoc.element.easyimage.convert)
- description and source-code
```javascript
convert = function (options) {

	var deferred = Q.defer();

	function imgConvert() {

		if (options.src === undefined || options.dst === undefined) return deferred.reject(error_messages['path']);

		var args = [options.src]
		if (options.quality) {
			args.push('-quality')
			args.push(options.quality)
		}

		if (options.flatten) {
			args.push('-flatten')
			if (options.background) {
				args.push('-background')
				args.push(options.background)
			}	
		}
		else {
			if (options.background) {
				args.push('-background')
				args.push(options.background)
				args.push('-flatten')
			}	
		}

		args.push(options.dst)

		child = exec('convert', args, function(err, stdout, stderr) {

			if (err) deferred.reject(err);
			else deferred.resolve(info(options.dst));
		});

	}

	directoryCheck(options, imgConvert)

	return deferred.promise;
}
```
- example usage
```shell
...
var easyimg = require('easyimage');
'''

EasyImage offers these promise methods:

'''
easyimg.info(<image_path>) - to retrieve information about an image. Will return an object with the following properties - type,
depth, width, height, size, density, name, and path.
easyimg.convert(<options>) - to convert an image from one format to another.
easyimg.resize(<options>) - to resize an image.
easyimg.crop(<options>) - to crop an image.
easyimg.thumbnail(<options>) - to create square thumbnails.
easyimg.rescrop(<options>) - to resize and crop and image in one go, useful for creating customzied thumbnails.
easyimg.rotate(<options>) - to rotate an image.
easyimg.exec(<command>) - when you want to call a custom command to ImageMagick, you will need to take care of escaping special
characters etc.
'''
...
```

#### <a name="apidoc.element.easyimage.crop"></a>[function <span class="apidocSignatureSpan">easyimage.</span>crop (options)](#apidoc.element.easyimage.crop)
- description and source-code
```javascript
crop = function (options) {

	var deferred = Q.defer();

	function imgCrop() {
		if (options.src === undefined || options.dst === undefined) return deferred.reject(error_messages['path']);
		if (options.cropwidth === undefined) return deferred.reject(error_messages['dim']);

		options.cropheight = options.cropheight || options.cropwidth;
		options.gravity = options.gravity || 'Center';
		options.x = options.x || 0;
		options.y = options.y || 0;

    var args = [options.src]

		if (options.flatten) {
			args.push('-flatten')
			if (options.background) {
				args.push('-background')
				args.push(options.background)
			}	
		}
		else {
			if (options.background) {
				args.push('-background')
				args.push(options.background)
				args.push('-flatten')
			}	
		}

    args.push('-auto-orient')
    args.push('-gravity')
    args.push(options.gravity)
    args.push('-crop')
    args.push(options.cropwidth + 'x'+ options.cropheight + '+' + options.x + '+' + options.y)
    if (options.quality) {
    	args.push('-quality')
    	args.push(options.quality)
    }
 		if (options.background) {
			args.push('-background')
			args.push(options.background)
		}
    args.push(options.dst)

		child = exec('convert', args, function(err, stdout, stderr) {
			if (err) deferred.reject(err);
			deferred.resolve(info(options.dst));
		});
	}

	directoryCheck(options, imgCrop)
	return deferred.promise;
}
```
- example usage
```shell
...

EasyImage offers these promise methods:

'''
easyimg.info(<image_path>) - to retrieve information about an image. Will return an object with the following properties - type,
depth, width, height, size, density, name, and path.
easyimg.convert(<options>) - to convert an image from one format to another.
easyimg.resize(<options>) - to resize an image.
easyimg.crop(<options>) - to crop an image.
easyimg.thumbnail(<options>) - to create square thumbnails.
easyimg.rescrop(<options>) - to resize and crop and image in one go, useful for creating customzied thumbnails.
easyimg.rotate(<options>) - to rotate an image.
easyimg.exec(<command>) - when you want to call a custom command to ImageMagick, you will need to take care of escaping special
characters etc.
'''
**NOTE**: 'easyimg.exec()' spawns a subshell.
...
```

#### <a name="apidoc.element.easyimage.exec"></a>[function <span class="apidocSignatureSpan">easyimage.</span>exec (cmd)](#apidoc.element.easyimage.exec)
- description and source-code
```javascript
exec = function (cmd) {

	var deferred = Q.defer();

	process.nextTick(function () {

		child = command(cmd, function(err, stdout, stderr) {
			if (err) return deferred.reject(err);
			deferred.resolve(stdout);
		});

	})

	return deferred.promise;
}
```
- example usage
```shell
...
easyimg.info(<image_path>) - to retrieve information about an image. Will return an object with the following properties - type,
depth, width, height, size, density, name, and path.
easyimg.convert(<options>) - to convert an image from one format to another.
easyimg.resize(<options>) - to resize an image.
easyimg.crop(<options>) - to crop an image.
easyimg.thumbnail(<options>) - to create square thumbnails.
easyimg.rescrop(<options>) - to resize and crop and image in one go, useful for creating customzied thumbnails.
easyimg.rotate(<options>) - to rotate an image.
easyimg.exec(<command>) - when you want to call a custom command to ImageMagick, you will need to take care of escaping special
characters etc.
'''
**NOTE**: 'easyimg.exec()' spawns a subshell.

The EasyImage options object can have these properties depending on the method. Unrelated options are ignored.

'''
src - path to source image.
...
```

#### <a name="apidoc.element.easyimage.info"></a>[function <span class="apidocSignatureSpan">easyimage.</span>info (file)](#apidoc.element.easyimage.info)
- description and source-code
```javascript
info = function (file) {
	return info(file);
}
```
- example usage
```shell
...
'''
var easyimg = require('easyimage');
'''

EasyImage offers these promise methods:

'''
easyimg.info(<image_path>) - to retrieve information about an image. Will return an object with the following properties - type,
depth, width, height, size, density, name, and path.
easyimg.convert(<options>) - to convert an image from one format to another.
easyimg.resize(<options>) - to resize an image.
easyimg.crop(<options>) - to crop an image.
easyimg.thumbnail(<options>) - to create square thumbnails.
easyimg.rescrop(<options>) - to resize and crop and image in one go, useful for creating customzied thumbnails.
easyimg.rotate(<options>) - to rotate an image.
easyimg.exec(<command>) - when you want to call a custom command to ImageMagick, you will need to take care of escaping special
characters etc.
...
```

#### <a name="apidoc.element.easyimage.rescrop"></a>[function <span class="apidocSignatureSpan">easyimage.</span>rescrop (options)](#apidoc.element.easyimage.rescrop)
- description and source-code
```javascript
rescrop = function (options) {

	var deferred = Q.defer();

	function imgResCrop() {

		if (options.src === undefined || options.dst === undefined) return deferred.reject(error_messages['path']);
		if (options.width === undefined) return deferred.reject(error_messages['dim']);

		options.height = options.height || options.width;

		options.cropwidth = options.cropwidth || options.width;
		options.cropheight = options.cropheight || options.height;

		options.gravity = options.gravity || 'Center';
		options.x = options.x || 0;
		options.y = options.y || 0;
		options.fill = options.fill ? '^' : '';

    var args = [options.src]

		if (options.flatten) {
			args.push('-flatten')
			if (options.background) {
				args.push('-background')
				args.push(options.background)
			}	
		}
		else {
			if (options.background) {
				args.push('-background')
				args.push(options.background)
				args.push('-flatten')
			}	
		}

    args.push('-auto-orient')
    args.push('-gravity')
    args.push(options.gravity)
    args.push('-resize')
    args.push(options.width + 'x' + options.height + options.fill)
    args.push('-crop')
    args.push(options.cropwidth + 'x'+ options.cropheight + '+' + options.x + '+' + options.y)
    if (options.quality) {
    	args.push('-quality')
    	args.push(options.quality)
    }
 		if (options.background) {
			args.push('-background')
			args.push(options.background)
		}
    args.push(options.dst)

		child = exec('convert', args, function(err, stdout, stderr) {
			if (err) deferred.reject(err);
			deferred.resolve(info(options.dst));
		});

	}

	directoryCheck(options, imgResCrop)
	return deferred.promise;
}
```
- example usage
```shell
...

'''
easyimg.info(<image_path>) - to retrieve information about an image. Will return an object with the following properties - type,
depth, width, height, size, density, name, and path.
easyimg.convert(<options>) - to convert an image from one format to another.
easyimg.resize(<options>) - to resize an image.
easyimg.crop(<options>) - to crop an image.
easyimg.thumbnail(<options>) - to create square thumbnails.
easyimg.rescrop(<options>) - to resize and crop and image in one go, useful for creating customzied thumbnails.
easyimg.rotate(<options>) - to rotate an image.
easyimg.exec(<command>) - when you want to call a custom command to ImageMagick, you will need to take care of escaping special
characters etc.
'''
**NOTE**: 'easyimg.exec()' spawns a subshell.

The EasyImage options object can have these properties depending on the method. Unrelated options are ignored.
...
```

#### <a name="apidoc.element.easyimage.resize"></a>[function <span class="apidocSignatureSpan">easyimage.</span>resize (options)](#apidoc.element.easyimage.resize)
- description and source-code
```javascript
resize = function (options) {

	var deferred = Q.defer();

	function imgResize() {

		if (options.src === undefined || options.dst === undefined) return deferred.reject(error_messages['path']);
		if (options.width === undefined) return deferred.reject(error_messages['dim']);

		options.height = options.height || options.width;

    var args = [options.src]

		if (options.flatten) {
			args.push('-flatten')
			if (options.background) {
				args.push('-background')
				args.push(options.background)
			}	
		}
		else {
			if (options.background) {
				args.push('-background')
				args.push(options.background)
				args.push('-flatten')
			}	
		}

    args.push('-auto-orient')
    args.push('-resize')
    args.push(options.width + 'x' + options.height)
    if (options.ignoreAspectRatio) {
      args[args.length-1] += '!';
    }
    if (options.quality) {
    	args.push('-quality')
    	args.push(options.quality)
    }
 		if (options.background) {
			args.push('-background')
			args.push(options.background)
		}
    args.push(options.dst)

		child = exec('convert', args, function(err, stdout, stderr) {
			if (err) deferred.reject(err);
			deferred.resolve(info(options.dst));
		});

	}

	directoryCheck(options, imgResize)
	return deferred.promise;
}
```
- example usage
```shell
...
'''

EasyImage offers these promise methods:

'''
easyimg.info(<image_path>) - to retrieve information about an image. Will return an object with the following properties - type,
depth, width, height, size, density, name, and path.
easyimg.convert(<options>) - to convert an image from one format to another.
easyimg.resize(<options>) - to resize an image.
easyimg.crop(<options>) - to crop an image.
easyimg.thumbnail(<options>) - to create square thumbnails.
easyimg.rescrop(<options>) - to resize and crop and image in one go, useful for creating customzied thumbnails.
easyimg.rotate(<options>) - to rotate an image.
easyimg.exec(<command>) - when you want to call a custom command to ImageMagick, you will need to take care of escaping special
characters etc.
'''
**NOTE**: 'easyimg.exec()' spawns a subshell.
...
```

#### <a name="apidoc.element.easyimage.rotate"></a>[function <span class="apidocSignatureSpan">easyimage.</span>rotate (options)](#apidoc.element.easyimage.rotate)
- description and source-code
```javascript
rotate = function (options) {

	var deferred = Q.defer();

	function imgRotate() {

		if (options.src === undefined || options.dst === undefined || options.degree === undefined) return deferred.reject(error_messages
['path']);

		var args = [options.src]

		if (options.flatten) {
			args.push('-flatten')
			if (options.background) {
				args.push('-background')
				args.push(options.background)
			}	
		}
		else {
			if (options.background) {
				args.push('-background')
				args.push(options.background)
				args.push('-flatten')
			}	
		}

		args.push('-rotate')
		args.push(options.degree)
 		if (options.background) {
			args.push('-background')
			args.push(options.background)
		}
		args.push(options.dst)

		child = exec('convert', args, function(err, stdout, stderr) {
			if (err) deferred.reject(err);
			else deferred.resolve(info(options.dst));
		});

	}

	directoryCheck(options, imgRotate)

	return deferred.promise;
}
```
- example usage
```shell
...
'''
easyimg.info(<image_path>) - to retrieve information about an image. Will return an object with the following properties - type,
depth, width, height, size, density, name, and path.
easyimg.convert(<options>) - to convert an image from one format to another.
easyimg.resize(<options>) - to resize an image.
easyimg.crop(<options>) - to crop an image.
easyimg.thumbnail(<options>) - to create square thumbnails.
easyimg.rescrop(<options>) - to resize and crop and image in one go, useful for creating customzied thumbnails.
easyimg.rotate(<options>) - to rotate an image.
easyimg.exec(<command>) - when you want to call a custom command to ImageMagick, you will need to take care of escaping special
characters etc.
'''
**NOTE**: 'easyimg.exec()' spawns a subshell.

The EasyImage options object can have these properties depending on the method. Unrelated options are ignored.

'''
...
```

#### <a name="apidoc.element.easyimage.thumbnail"></a>[function <span class="apidocSignatureSpan">easyimage.</span>thumbnail (options)](#apidoc.element.easyimage.thumbnail)
- description and source-code
```javascript
thumbnail = function (options) {

	var deferred = Q.defer();

	function imgThumbnail() {

		if (options.src === undefined || options.dst === undefined) return deferred.reject(error_messages['path']);
		if (options.width === undefined) return deferred.reject(error_messages['dim']);

		options.height = options.height || options.width;
		options.gravity = options.gravity || 'Center';
		options.x = options.x || 0;
		options.y = options.y || 0;

		info(options.src).then(function(original) {

			// dimensions come as strings, convert them to number
			original.width = +original.width;
			original.height = +original.height;

			var resizewidth = options.width;
			var resizeheight = options.height;

			if (original.width > original.height) { resizewidth = ''; }
			else if (original.height > original.width) { resizeheight = ''; }

	    var args = [options.src]

			if (options.flatten) {
				args.push('-flatten')
				if (options.background) {
					args.push('-background')
					args.push(options.background)
				}	
			}
			else {
				if (options.background) {
					args.push('-background')
					args.push(options.background)
					args.push('-flatten')
				}	
			}

	    args.push('-auto-orient')
	    args.push('-gravity')
	    args.push(options.gravity)
	    args.push('-interpolate')
	    args.push('bicubic')
	    args.push('-strip')
	    args.push('-thumbnail')
	    args.push(resizewidth + 'x' + resizeheight)
	    args.push('-crop')
	    args.push(options.width + 'x'+ options.height + '+' + options.x + '+' + options.y)
	    if (options.quality) {
	    	args.push('-quality')
	    	args.push(options.quality)
	    }
			if (options.background) {
				args.push('-background')
				args.push(options.background)
			}
	    args.push(options.dst)

			child = exec('convert', args, function(err, stdout, stderr) {
				if (err) return deferred.reject(err);
				deferred.resolve(info(options.dst));
			});

		}, function (err) { deferred.reject(err); });

	}

	directoryCheck(options, imgThumbnail)
	return deferred.promise;
}
```
- example usage
```shell
...
EasyImage offers these promise methods:

'''
easyimg.info(<image_path>) - to retrieve information about an image. Will return an object with the following properties - type,
depth, width, height, size, density, name, and path.
easyimg.convert(<options>) - to convert an image from one format to another.
easyimg.resize(<options>) - to resize an image.
easyimg.crop(<options>) - to crop an image.
easyimg.thumbnail(<options>) - to create square thumbnails.
easyimg.rescrop(<options>) - to resize and crop and image in one go, useful for creating customzied thumbnails.
easyimg.rotate(<options>) - to rotate an image.
easyimg.exec(<command>) - when you want to call a custom command to ImageMagick, you will need to take care of escaping special
characters etc.
'''
**NOTE**: 'easyimg.exec()' spawns a subshell.

The EasyImage options object can have these properties depending on the method. Unrelated options are ignored.
...
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
