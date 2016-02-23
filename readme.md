#babel-plugin-transform-modules-commonjs-immutable

transform immutable es6 module to commonjs module

##transform
ES6

	import { log , warn } from './a';
	log('init');
	log('now is:'+Date.now());
	warn('a warning');

when transformed, the imported variables will be convert to property access of the imported object. Normally, we don't mangle property name which is a bad case if we know the propety is immutable.

Instead of transform like 

	var _a=require('./a');
	_a.log('init');
	_a.log('now is:'+Date.now());
	_a.warn('a warning');
	
we can refer the imported varibles as local variables if they are immutable. Just like

	var _a=require('./a');
	var _a$log=_a.log;
	_a$log('init');
	_a$log('now is:'+Date.now());
	_a.warn('a warning');
	
When the code is mangled,the local variable names will be shortened.For the once-used imported variables, keep it as a property.

## Usage
Install

    npm install babel-plugin-transform-modules-commonjs-immutable --save-dev

In code

    babel.transform(code,{
      plugins:[
        "babel-plugin-transform-modules-commonjs-immutable"
      ]
    });

This plugin may cause conflict with "babel-plugin-transform-es2015-modules-commonjs"